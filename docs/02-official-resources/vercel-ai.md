# Vercel AI SDK Official Resources

This page provides curated links to official Vercel AI SDK documentation and resources for building AI-powered applications.

## 🔗 Quick Links

- [AI SDK Documentation](https://sdk.vercel.ai/docs)
- [AI SDK Examples](https://sdk.vercel.ai/examples)
- [AI SDK Playground](https://sdk.vercel.ai/playground)
- [GitHub Repository](https://github.com/vercel/ai)

## 📚 Documentation

### Getting Started
- [Introduction](https://sdk.vercel.ai/docs/introduction) - Overview of the AI SDK
- [Quick Start](https://sdk.vercel.ai/docs/getting-started) - Get up and running quickly
- [Core Concepts](https://sdk.vercel.ai/docs/concepts/streaming) - Understanding key concepts

### AI SDK Core
- [Generating Text](https://sdk.vercel.ai/docs/ai-sdk-core/generating-text) - Text generation
- [Streaming Text](https://sdk.vercel.ai/docs/ai-sdk-core/streaming-text) - Streaming responses
- [Generating Objects](https://sdk.vercel.ai/docs/ai-sdk-core/generating-structured-data) - Structured data
- [Tool Calling](https://sdk.vercel.ai/docs/ai-sdk-core/tools-and-tool-calling) - Function calling

### AI SDK UI
- [Chatbot](https://sdk.vercel.ai/docs/ai-sdk-ui/chatbot) - Building chatbots
- [Completion](https://sdk.vercel.ai/docs/ai-sdk-ui/completion) - Text completion UI
- [Assistant](https://sdk.vercel.ai/docs/ai-sdk-ui/assistant) - AI assistants

### AI SDK RSC
- [Streaming React Components](https://sdk.vercel.ai/docs/ai-sdk-rsc/streaming-react-components) - Server components
- [Generative UI](https://sdk.vercel.ai/docs/ai-sdk-rsc/generative-ui) - Dynamic UI generation

## 🛠️ Installation & Setup

### Package Installation
```bash
# Core package
npm install ai

# Provider packages
npm install @ai-sdk/openai
npm install @ai-sdk/anthropic
npm install @ai-sdk/google
npm install @ai-sdk/mistral
```

### Basic Setup
```typescript
import { openai } from '@ai-sdk/openai';
import { streamText } from 'ai';

const result = await streamText({
  model: openai('gpt-4-turbo'),
  prompt: 'Write a poem about recursion in programming.',
});
```

## 🤖 Supported Providers

### Official Providers
- [OpenAI](https://sdk.vercel.ai/providers/ai-sdk-providers/openai) - GPT models
- [Anthropic](https://sdk.vercel.ai/providers/ai-sdk-providers/anthropic) - Claude models
- [Google](https://sdk.vercel.ai/providers/ai-sdk-providers/google-generative-ai) - Gemini models
- [Mistral](https://sdk.vercel.ai/providers/ai-sdk-providers/mistral) - Mistral models
- [AWS Bedrock](https://sdk.vercel.ai/providers/ai-sdk-providers/amazon-bedrock) - Multiple models
- [Azure](https://sdk.vercel.ai/providers/ai-sdk-providers/azure) - Azure OpenAI

### Community Providers
- [Cohere](https://sdk.vercel.ai/providers/ai-sdk-providers/cohere)
- [Fireworks](https://sdk.vercel.ai/providers/ai-sdk-providers/fireworks)
- [Groq](https://sdk.vercel.ai/providers/ai-sdk-providers/groq)
- [Perplexity](https://sdk.vercel.ai/providers/ai-sdk-providers/perplexity)
- [Together AI](https://sdk.vercel.ai/providers/ai-sdk-providers/togetherai)

## 🎓 Examples & Templates

### Official Examples
- [Next.js Chatbot](https://github.com/vercel/ai-chatbot) - Full-featured chatbot
- [AI SDK Examples](https://github.com/vercel/ai/tree/main/examples) - Various examples
- [Playground](https://sdk.vercel.ai/playground) - Interactive playground

### Framework Examples
- [Next.js App Router](https://sdk.vercel.ai/examples/next-app)
- [Next.js Pages Router](https://sdk.vercel.ai/examples/next-pages)
- [Nuxt](https://sdk.vercel.ai/examples/nuxt)
- [SvelteKit](https://sdk.vercel.ai/examples/sveltekit)
- [Express](https://sdk.vercel.ai/examples/express)

## 🔧 Advanced Features

### Streaming
- [Text Streaming](https://sdk.vercel.ai/docs/concepts/streaming) - Real-time responses
- [Object Streaming](https://sdk.vercel.ai/docs/concepts/object-generation) - Structured data
- [Stream Helpers](https://sdk.vercel.ai/docs/reference/stream-helpers) - Utility functions

### Tools & Functions
- [Tool Definition](https://sdk.vercel.ai/docs/ai-sdk-core/tools-and-tool-calling) - Define tools
- [Tool Execution](https://sdk.vercel.ai/docs/ai-sdk-core/tools-and-tool-calling#tool-execution) - Execute tools
- [Parallel Tools](https://sdk.vercel.ai/docs/ai-sdk-core/tools-and-tool-calling#parallel-tool-calls) - Multiple tools

### Error Handling
- [Error Types](https://sdk.vercel.ai/docs/reference/errors) - Understanding errors
- [Retry Logic](https://sdk.vercel.ai/docs/ai-sdk-core/settings#retry) - Automatic retries
- [Error Recovery](https://sdk.vercel.ai/docs/troubleshooting/common-issues) - Best practices

## 📊 Observability & Monitoring

### Built-in Telemetry
- [Telemetry](https://sdk.vercel.ai/docs/ai-sdk-core/telemetry) - Monitoring setup
- [Custom Metadata](https://sdk.vercel.ai/docs/ai-sdk-core/telemetry#custom-metadata) - Add context
- [Tracing](https://sdk.vercel.ai/docs/ai-sdk-core/telemetry#tracing) - Request tracing

### Integrations
- [Vercel AI SDK Telemetry](https://sdk.vercel.ai/docs/ai-sdk-core/telemetry)
- [LangSmith](https://sdk.vercel.ai/providers/observability/langsmith)
- [Helicone](https://sdk.vercel.ai/providers/observability/helicone)

## 🚀 Best Practices

### Performance
- Use streaming for better UX
- Implement proper error boundaries
- Cache responses when appropriate
- Use edge runtime for lower latency

### Security
- Never expose API keys in client code
- Implement rate limiting
- Validate and sanitize inputs
- Use server-side API calls

### Cost Optimization
- Monitor token usage
- Implement caching strategies
- Use appropriate models for tasks
- Set max token limits

## 📰 Community & Support

### Official Channels
- [GitHub Discussions](https://github.com/vercel/ai/discussions) - Q&A forum
- [Discord](https://vercel.com/discord) - Community chat
- [Twitter](https://twitter.com/vercel) - Updates

### Resources
- [Blog Posts](https://vercel.com/blog/category/ai) - AI articles
- [Changelog](https://github.com/vercel/ai/releases) - Latest updates
- [Contributing](https://github.com/vercel/ai/blob/main/CONTRIBUTING.md) - Contribution guide

## 🚀 Quick Start Checklist

1. [ ] Install the AI SDK: `npm install ai`
2. [ ] Choose and install a provider
3. [ ] Set up environment variables
4. [ ] Create your first AI route
5. [ ] Implement streaming UI
6. [ ] Add error handling
7. [ ] Set up monitoring
8. [ ] Deploy to Vercel

## 💡 Code Snippets

### Next.js App Router Example
```typescript
// app/api/chat/route.ts
import { openai } from '@ai-sdk/openai';
import { streamText } from 'ai';

export async function POST(req: Request) {
  const { messages } = await req.json();

  const result = await streamText({
    model: openai('gpt-4-turbo'),
    messages,
  });

  return result.toDataStreamResponse();
}
```

### React Hook Usage
```typescript
// app/chat/page.tsx
'use client';

import { useChat } from 'ai/react';

export default function Chat() {
  const { messages, input, handleInputChange, handleSubmit } = useChat();

  return (
    <div>
      {messages.map(m => (
        <div key={m.id}>
          {m.role}: {m.content}
        </div>
      ))}
      <form onSubmit={handleSubmit}>
        <input value={input} onChange={handleInputChange} />
        <button type="submit">Send</button>
      </form>
    </div>
  );
}
```

---

*Last updated: Check the official Vercel AI SDK documentation for the most current information.* 