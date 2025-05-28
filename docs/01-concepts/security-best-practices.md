# Security & Best Practices

This guide covers essential security considerations and best practices for OpenAI + Supabase Realtime applications.

## Authentication & Authorization

### API Key Management

**Never expose API keys in client-side code:**

```typescript
// ❌ BAD: API key exposed in browser
const client = new RealtimeClient({
  apiKey: 'sk-proj-...' // NEVER DO THIS
})

// ✅ GOOD: Use server-side proxy
const response = await fetch('/api/openai-proxy', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ message })
})
```

### Server-Side Proxy Implementation

```typescript
// app/api/openai-proxy/route.ts
import { RealtimeClient } from '@openai/realtime-api-beta'
import { auth } from '@/lib/auth'

export async function POST(request: Request) {
  // Verify user authentication
  const session = await auth()
  if (!session) {
    return new Response('Unauthorized', { status: 401 })
  }

  // Initialize client with server-side API key
  const client = new RealtimeClient({
    apiKey: process.env.OPENAI_API_KEY!
  })

  // Proxy the request
  // ... handle realtime connection
}
```

### Supabase Row Level Security (RLS)

Always enable RLS on sensitive tables:

```sql
-- Enable RLS
ALTER TABLE conversations ENABLE ROW LEVEL SECURITY;

-- Policy: Users can only see their own conversations
CREATE POLICY "Users own conversations" ON conversations
  FOR ALL USING (auth.uid() = user_id);

-- Policy: Users can insert their own conversations
CREATE POLICY "Users insert own conversations" ON conversations
  FOR INSERT WITH CHECK (auth.uid() = user_id);

-- Policy: Prevent updates to user_id
CREATE POLICY "Prevent user_id changes" ON conversations
  FOR UPDATE USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id AND user_id = OLD.user_id);
```

### Private Realtime Channels

Implement authorization for private channels:

```typescript
// Server-side channel authorization
export async function authorizeChannel(userId: string, channelName: string) {
  // Check if user has access to channel
  const { data, error } = await supabase
    .from('channel_members')
    .select('id')
    .eq('user_id', userId)
    .eq('channel_name', channelName)
    .single()

  return !!data && !error
}

// Client-side subscription with auth
const channel = supabase
  .channel('private-room', {
    config: {
      private: true,
      presence: { key: user.id }
    }
  })
  .on('presence', { event: 'sync' }, handlePresence)
  .subscribe((status) => {
    if (status === 'SUBSCRIBED') {
      console.log('Authorized and subscribed')
    }
  })
```

## Data Protection

### Input Validation

Always validate and sanitize user inputs:

```typescript
import { z } from 'zod'

const MessageSchema = z.object({
  content: z.string().min(1).max(1000),
  type: z.enum(['text', 'audio']),
  metadata: z.object({
    timestamp: z.string().datetime(),
    userId: z.string().uuid()
  }).optional()
})

export async function handleMessage(input: unknown) {
  try {
    const validated = MessageSchema.parse(input)
    // Process validated input
  } catch (error) {
    // Handle validation error
    return { error: 'Invalid input' }
  }
}
```

### Content Moderation

Implement content filtering for user-generated content:

```typescript
async function moderateContent(content: string) {
  const response = await openai.moderations.create({
    input: content
  })

  const results = response.results[0]
  if (results.flagged) {
    // Handle inappropriate content
    throw new Error('Content violates usage policies')
  }

  return content
}
```

### Data Encryption

Encrypt sensitive data at rest:

```sql
-- Use Supabase Vault for secrets
INSERT INTO vault.secrets (name, secret)
VALUES ('openai_api_key', 'sk-proj-...')
RETURNING id;

-- Access secrets securely
CREATE FUNCTION get_openai_key()
RETURNS text
LANGUAGE plpgsql
SECURITY DEFINER
AS $$
DECLARE
  secret_value text;
BEGIN
  SELECT decrypted_secret INTO secret_value
  FROM vault.decrypted_secrets
  WHERE name = 'openai_api_key';
  
  RETURN secret_value;
END;
$$;
```

## Performance & Rate Limiting

### Client-Side Rate Limiting

```typescript
class RateLimiter {
  private requests: number[] = []
  private readonly maxRequests: number
  private readonly windowMs: number

  constructor(maxRequests: number, windowMs: number) {
    this.maxRequests = maxRequests
    this.windowMs = windowMs
  }

  canMakeRequest(): boolean {
    const now = Date.now()
    this.requests = this.requests.filter(time => now - time < this.windowMs)
    
    if (this.requests.length < this.maxRequests) {
      this.requests.push(now)
      return true
    }
    
    return false
  }
}

// Usage
const limiter = new RateLimiter(10, 60000) // 10 requests per minute

if (limiter.canMakeRequest()) {
  // Make API call
} else {
  // Show rate limit error
}
```

### Server-Side Rate Limiting

Using Upstash Redis for distributed rate limiting:

```typescript
import { Ratelimit } from '@upstash/ratelimit'
import { Redis } from '@upstash/redis'

const ratelimit = new Ratelimit({
  redis: Redis.fromEnv(),
  limiter: Ratelimit.slidingWindow(10, '1 m'),
  analytics: true
})

export async function middleware(request: Request) {
  const ip = request.headers.get('x-forwarded-for') ?? 'anonymous'
  const { success, limit, reset, remaining } = await ratelimit.limit(ip)

  if (!success) {
    return new Response('Too Many Requests', {
      status: 429,
      headers: {
        'X-RateLimit-Limit': limit.toString(),
        'X-RateLimit-Remaining': remaining.toString(),
        'X-RateLimit-Reset': new Date(reset).toISOString()
      }
    })
  }

  return NextResponse.next()
}
```

## Error Handling

### Graceful Degradation

```typescript
class RealtimeConnection {
  private reconnectAttempts = 0
  private maxReconnectAttempts = 5
  private reconnectDelay = 1000

  async connect() {
    try {
      await this.client.connect()
      this.reconnectAttempts = 0
    } catch (error) {
      if (this.reconnectAttempts < this.maxReconnectAttempts) {
        this.reconnectAttempts++
        const delay = this.reconnectDelay * Math.pow(2, this.reconnectAttempts - 1)
        
        console.log(`Reconnecting in ${delay}ms...`)
        setTimeout(() => this.connect(), delay)
      } else {
        // Fall back to non-realtime mode
        this.enableFallbackMode()
      }
    }
  }

  private enableFallbackMode() {
    // Implement polling or other fallback mechanism
    console.log('Switching to fallback mode')
  }
}
```

### Error Boundaries

```typescript
import { Component, ErrorInfo, ReactNode } from 'react'

interface Props {
  children: ReactNode
  fallback?: ReactNode
}

interface State {
  hasError: boolean
  error?: Error
}

export class ErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props)
    this.state = { hasError: false }
  }

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error }
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    // Log to error reporting service
    console.error('Error caught by boundary:', error, errorInfo)
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || <div>Something went wrong</div>
    }

    return this.props.children
  }
}
```

## Monitoring & Logging

### Structured Logging

```typescript
import pino from 'pino'

const logger = pino({
  level: process.env.LOG_LEVEL || 'info',
  transport: {
    target: 'pino-pretty',
    options: {
      colorize: true
    }
  }
})

// Log security events
logger.info({
  event: 'auth.success',
  userId: user.id,
  ip: request.ip,
  timestamp: new Date().toISOString()
})

// Log errors with context
logger.error({
  event: 'api.error',
  error: error.message,
  stack: error.stack,
  userId: user?.id,
  requestId: request.id
})
```

### Security Headers

```typescript
// middleware.ts
export function middleware(request: Request) {
  const response = NextResponse.next()

  // Security headers
  response.headers.set('X-Frame-Options', 'DENY')
  response.headers.set('X-Content-Type-Options', 'nosniff')
  response.headers.set('X-XSS-Protection', '1; mode=block')
  response.headers.set('Referrer-Policy', 'strict-origin-when-cross-origin')
  response.headers.set(
    'Content-Security-Policy',
    "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline';"
  )
  response.headers.set(
    'Permissions-Policy',
    'camera=(), microphone=(self), geolocation=()'
  )

  return response
}
```

## Compliance Considerations

1. **Data Retention**: Implement policies for data deletion
2. **User Consent**: Obtain explicit consent for voice recording
3. **Privacy Policy**: Clearly state data usage
4. **GDPR Compliance**: Implement right to deletion, data export
5. **Audit Logging**: Track all data access and modifications

## Security Checklist

- [ ] API keys stored securely (environment variables)
- [ ] Server-side proxy for OpenAI API calls
- [ ] Row Level Security enabled on all tables
- [ ] Input validation on all user inputs
- [ ] Rate limiting implemented (client & server)
- [ ] Error boundaries in React components
- [ ] Security headers configured
- [ ] Monitoring and logging in place
- [ ] Regular security audits scheduled
- [ ] Incident response plan documented

## Next Steps

- Review [Integration Architecture](./integration-architecture.md)
- Explore the [Tech Stack](./tech-stack.md)
- See practical [Use Cases](./use-cases.md) 