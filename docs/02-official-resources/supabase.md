# Supabase Official Resources

This page provides curated links to official Supabase documentation, SDKs, and resources for building real-time applications.

## 🔗 Quick Links

- [Supabase Dashboard](https://supabase.com/dashboard)
- [Supabase Documentation](https://supabase.com/docs)
- [Supabase Status](https://status.supabase.com/)
- [Pricing](https://supabase.com/pricing)

## 📚 Documentation

### Realtime
- [Realtime Overview](https://supabase.com/docs/guides/realtime) - Introduction to Supabase Realtime
- [Realtime Quickstart](https://supabase.com/docs/guides/realtime/quickstart) - Get started with Realtime
- [Postgres Changes](https://supabase.com/docs/guides/realtime/postgres-changes) - Listen to database changes
- [Broadcast](https://supabase.com/docs/guides/realtime/broadcast) - Send messages between clients
- [Presence](https://supabase.com/docs/guides/realtime/presence) - Track user presence
- [Authorization](https://supabase.com/docs/guides/realtime/authorization) - Secure your channels

### Core Features
- [Database](https://supabase.com/docs/guides/database) - PostgreSQL database
- [Auth](https://supabase.com/docs/guides/auth) - Authentication and authorization
- [Storage](https://supabase.com/docs/guides/storage) - File storage
- [Edge Functions](https://supabase.com/docs/guides/functions) - Serverless functions
- [Vector/AI](https://supabase.com/docs/guides/ai) - AI and embeddings

## 🛠️ Official SDKs

### JavaScript/TypeScript
- **Repository**: [supabase/supabase-js](https://github.com/supabase/supabase-js)
- **NPM**: [@supabase/supabase-js](https://www.npmjs.com/package/@supabase/supabase-js)
- **Installation**: `npm install @supabase/supabase-js`

Key libraries:
- `@supabase/supabase-js` - Main client library
- `@supabase/ssr` - Server-side rendering helpers
- `@supabase/auth-helpers-nextjs` - Next.js integration
- `@supabase/realtime-js` - Standalone realtime client

### Python
- **Repository**: [supabase/supabase-py](https://github.com/supabase/supabase-py)
- **PyPI**: [supabase](https://pypi.org/project/supabase/)
- **Installation**: `pip install supabase`

### Other Official SDKs
- [Flutter/Dart](https://github.com/supabase/supabase-flutter)
- [Swift](https://github.com/supabase/supabase-swift)
- [Kotlin](https://github.com/supabase/supabase-kt)
- [C#/.NET](https://github.com/supabase/supabase-csharp)

## 🎓 Learning Resources

### Tutorials & Guides
- [Supabase Tutorials](https://supabase.com/docs/guides) - Official tutorials
- [Video Tutorials](https://www.youtube.com/@Supabase) - YouTube channel
- [Blog](https://supabase.com/blog) - Technical articles and updates

### Example Applications
- [Example Projects](https://github.com/supabase/supabase/tree/master/examples) - Official examples
- [Auth Examples](https://github.com/supabase/auth-helpers/tree/main/examples) - Authentication patterns
- [Realtime Examples](https://github.com/supabase/realtime/tree/main/examples) - Realtime patterns

### Templates
- [Next.js Starter](https://github.com/supabase/supabase/tree/master/examples/auth/nextjs)
- [React Native Starter](https://github.com/supabase/supabase/tree/master/examples/react-native)
- [Flutter Starter](https://github.com/supabase/supabase/tree/master/examples/flutter)

## 🔐 Security & Best Practices

### Security
- [Row Level Security](https://supabase.com/docs/guides/auth/row-level-security) - Database security
- [Auth Deep Dive](https://supabase.com/docs/learn/auth-deep-dive) - Authentication details
- [Security Advisories](https://github.com/supabase/supabase/security/advisories)

### Performance
- [Performance Tuning](https://supabase.com/docs/guides/platform/performance)
- [Database Optimization](https://supabase.com/docs/guides/database/performance)
- [Realtime Performance](https://supabase.com/docs/guides/realtime/performance)

## 🧪 Development Tools

### CLI & Local Development
- [Supabase CLI](https://supabase.com/docs/guides/cli) - Command line tools
- [Local Development](https://supabase.com/docs/guides/cli/local-development) - Run Supabase locally
- **Installation**: `npm install -g supabase`

### Database Tools
- [Table Editor](https://supabase.com/docs/guides/database/tables) - Visual table management
- [SQL Editor](https://supabase.com/docs/guides/database/sql-editor) - Run SQL queries
- [Database Migrations](https://supabase.com/docs/guides/database/migrations) - Version control

### Monitoring
- [Logs Explorer](https://supabase.com/docs/guides/platform/logs) - Application logs
- [Metrics](https://supabase.com/docs/guides/platform/metrics) - Performance metrics
- [Query Performance](https://supabase.com/docs/guides/database/query-performance) - Analyze queries

## 📰 Community & Support

### Community
- [Discord](https://discord.supabase.com/) - Community chat
- [GitHub Discussions](https://github.com/supabase/supabase/discussions) - Q&A forum
- [Twitter](https://twitter.com/supabase) - Updates and news
- [Reddit](https://reddit.com/r/supabase) - Community discussions

### Support
- [Support Portal](https://supabase.com/support) - Official support
- [Documentation](https://supabase.com/docs) - Comprehensive docs
- [System Status](https://status.supabase.com/) - Service status

## 🚀 Getting Started Checklist

1. [ ] Create a [Supabase account](https://supabase.com/dashboard)
2. [ ] Create a new project
3. [ ] Get your project URL and anon key
4. [ ] Install Supabase CLI: `npm install -g supabase`
5. [ ] Install client library for your framework
6. [ ] Enable Realtime in your project settings
7. [ ] Set up Row Level Security policies
8. [ ] Try a [quickstart guide](https://supabase.com/docs/guides/getting-started)

## 💡 Pro Tips

### Realtime Specific
- Enable Realtime on tables via Dashboard or SQL
- Use Row Level Security for channel authorization
- Implement presence for user tracking
- Use broadcast for ephemeral messages
- Monitor Realtime quotas in project settings

### General Best Practices
- Always use environment variables for keys
- Enable RLS on all public tables
- Use connection pooling for better performance
- Set up proper indexes for queries
- Regular backups are automatic but can be configured

## 🔧 Useful SQL Snippets

### Enable Realtime on a table
```sql
ALTER TABLE your_table REPLICA IDENTITY FULL;

-- Via Dashboard: Database > Replication > Toggle tables
```

### Create a Realtime-ready table
```sql
CREATE TABLE messages (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id),
  content TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Enable RLS
ALTER TABLE messages ENABLE ROW LEVEL SECURITY;

-- Add policy
CREATE POLICY "Users can see all messages" ON messages
  FOR SELECT USING (true);

-- Enable Realtime
ALTER TABLE messages REPLICA IDENTITY FULL;
```

---

*Last updated: Check the official Supabase documentation for the most current information.* 