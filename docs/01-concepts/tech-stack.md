# Tech Stack Compatibility

This guide covers the recommended technology stack for building OpenAI + Supabase Realtime applications.

## Core Technologies

### Frontend Frameworks

#### Next.js 15 (Recommended)
- **App Router**: Modern routing with React Server Components
- **Streaming**: Built-in support for streaming responses
- **Edge Runtime**: Deploy functions closer to users
- **TypeScript**: First-class TypeScript support

```json
{
  "dependencies": {
    "next": "^15.0.0",
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  }
}
```

#### Alternative Frameworks
- **Remix**: Full-stack React framework
- **SvelteKit**: Svelte-based full-stack framework
- **Nuxt**: Vue.js framework with SSR support
- **SolidStart**: SolidJS meta-framework

### Styling & UI

#### Tailwind CSS
- Utility-first CSS framework
- Excellent performance with JIT compilation
- Works seamlessly with component libraries

#### Component Libraries
- **shadcn/ui**: Copy-paste component library
- **Radix UI**: Unstyled, accessible components
- **Headless UI**: Unstyled components by Tailwind team
- **Arco Design**: Enterprise-focused component library

#### Animation
- **Framer Motion**: Production-ready animation library
- **Auto-animate**: Zero-config animation utility
- **React Spring**: Spring-physics animations

### Database & Backend

#### Supabase Stack
```typescript
// Supabase client setup
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
)

// Realtime subscription
const channel = supabase
  .channel('room1')
  .on('presence', { event: 'sync' }, () => {
    const state = channel.presenceState()
    console.log('Presence state:', state)
  })
  .subscribe()
```

#### Database Features
- **PostgreSQL**: Powerful relational database
- **Row Level Security**: Fine-grained access control
- **Realtime**: WebSocket-based change notifications
- **Vector Search**: pgvector for AI embeddings

### AI & Real-time

#### OpenAI Realtime API
```typescript
// OpenAI Realtime setup
import { RealtimeClient } from '@openai/realtime-api-beta'

const client = new RealtimeClient({
  apiKey: process.env.OPENAI_API_KEY,
  dangerouslyAllowAPIKeyInBrowser: false // Use server-side proxy
})

// Connect to realtime
await client.connect()

// Handle events
client.on('conversation.item.created', (event) => {
  console.log('New conversation item:', event)
})
```

#### Vercel AI SDK
```typescript
import { openai } from '@ai-sdk/openai'
import { streamText } from 'ai'

const result = await streamText({
  model: openai('gpt-4-turbo'),
  messages: [{ role: 'user', content: 'Hello!' }],
})

// Stream to client
return result.toDataStreamResponse()
```

### Communication Protocols

#### WebSocket
- Native browser support
- Low latency bi-directional communication
- Used by both OpenAI and Supabase Realtime

#### WebRTC
- Peer-to-peer communication
- Audio/video streaming
- Ultra-low latency for voice

### Development Tools

#### Package Managers
- **pnpm**: Fast, disk-space efficient (recommended)
- **npm**: Default Node.js package manager
- **yarn**: Alternative with workspaces support
- **bun**: All-in-one JavaScript runtime

#### Build Tools
- **Vite**: Fast development server
- **Turbopack**: Next.js bundler
- **esbuild**: Fast JavaScript bundler
- **SWC**: Rust-based compiler

#### Testing
- **Playwright**: E2E testing framework
- **Vitest**: Fast unit testing
- **React Testing Library**: Component testing
- **Cypress**: Alternative E2E testing

## Recommended Stack

### For Voice-First Applications
```json
{
  "frontend": "Next.js 15 + TypeScript",
  "ui": "shadcn/ui + Tailwind CSS",
  "realtime": "OpenAI Realtime API + Supabase Realtime",
  "database": "Supabase (PostgreSQL)",
  "auth": "Supabase Auth",
  "deployment": "Vercel",
  "testing": "Playwright + Vitest"
}
```

### For Chat Applications
```json
{
  "frontend": "Next.js 15 + TypeScript",
  "ui": "shadcn/ui + Tailwind CSS",
  "ai": "Vercel AI SDK",
  "database": "Supabase (PostgreSQL)",
  "realtime": "Supabase Realtime",
  "deployment": "Vercel",
  "search": "pgvector"
}
```

### For Collaborative Tools
```json
{
  "frontend": "Next.js 15 + TypeScript",
  "ui": "Radix UI + Tailwind CSS",
  "realtime": "Supabase Realtime (Presence)",
  "database": "Supabase (PostgreSQL)",
  "auth": "Supabase Auth",
  "storage": "Supabase Storage",
  "deployment": "Vercel or Cloudflare"
}
```

## Version Compatibility

### Minimum Requirements
- Node.js: 18.17 or later
- React: 18.2.0 or later (19.0 for latest features)
- Next.js: 14.0 or later (15.0 recommended)
- TypeScript: 5.0 or later

### Package Versions
Always check for the latest stable versions, but here are tested combinations:

```json
{
  "next": "^15.0.0",
  "react": "^19.0.0",
  "react-dom": "^19.0.0",
  "@supabase/supabase-js": "^2.45.0",
  "@supabase/ssr": "^0.5.0",
  "ai": "^3.4.0",
  "@ai-sdk/openai": "^0.0.66",
  "tailwindcss": "^3.4.0",
  "typescript": "^5.6.0"
}
```

## Performance Considerations

1. **Bundle Size**: Use dynamic imports for large dependencies
2. **Connection Pooling**: Reuse WebSocket connections
3. **Edge Deployment**: Deploy close to users
4. **Caching**: Implement proper caching strategies
5. **Optimistic Updates**: Update UI before server confirmation

## Next Steps

- Explore [Integration Architecture](./integration-architecture.md)
- Review [Security Best Practices](./security-best-practices.md)
- See real-world [Use Cases](./use-cases.md) 