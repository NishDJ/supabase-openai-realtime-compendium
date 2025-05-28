build an app which uses the v0 api to build components based on the user's request. Here is the latest v0 api documentation:

# v0 API

The `v0-1.0-md` model is designed for building modern web applications. It supports text and image inputs, provides fast streaming responses, and is compatible with the [OpenAI Chat Completions API](https://platform.openai.com/docs/api-reference/chat) format.

## [Features](#features)

*   Framework aware completions: Evaluated on modern stacks like Next.js and Vercel.
*   Auto-fix: Identifies and corrects common coding issues during generation.
*   Quick edit: Streams inline edits as they’re available.
*   OpenAI compatible: Can be used with any tool or SDK that supports OpenAI's API format.
*   Multimodal: Supports both text and image inputs (base64-encoded image data).

You can experiment with the `v0-1.0-md` model in the  to test prompts and view responses.

## [Getting started](#getting-started)

The v0 API is currently in beta and requires a Premium or Team plan with usage-based billing enabled. For details, visit the .

To start using the `v0-1.0-md` model, create an API key on .

You can then integrate it using the [AI SDK](/docs/ai-sdk), a TypeScript library designed for working with v0 and other OpenAI-compatible models.

```
npm install ai @ai-sdk/vercel
```

### [Example usage](#example-usage)

```
import { generateText } from 'ai';
import { vercel } from '@ai-sdk/vercel';
 
const { text } = await generateText({
  model: vercel('v0-1.0-md'),
  prompt: 'Create a Next.js AI chatbot with authentication',
});
```

## [Models](#models)

### 

The `v0-1.0-md` model is the default model served by the v0 API.

Capabilities:

*   Supports text and image inputs (multimodal)
*   Compatible with OpenAI’s Chat Completions format
*   Supports function/tool calls
*   Streaming responses with low latency
*   Optimized for frontend and full-stack web development

## [API reference](#api-reference)

### [Endpoint](#endpoint)

`POST https://api.v0.dev/v1/chat/completions`

This endpoint generates a model response based on a list of messages.

### [Headers](#headers)

| Header | Required | Description |
| --- | --- | --- |
| Authorization | Yes | Bearer token: `Bearer $V0_API_KEY` |
| Content-Type | Yes | Must be `application/json` |

### [Request body](#request-body)

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `model` | string | Yes | Model name. Use `"v0-1.0-md"`. |
| `messages` | array | Yes | List of message objects forming the conversation. |
| `stream` | boolean | No | If true, the response will be returned as a stream of data chunks. |
| `tools` | array | No | Optional tool definitions (e.g., functions or API calls). |
| `tool_choice` | string or object | No | Specifies which tool to call, if tools are provided. |

Each message object must contain:

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `role` | string | Yes | One of `"user"`, `"assistant"`, or `"system"`. |
| `content` | string or array | Yes | The message content. Can be a string or array of text/image blocks. |

### [Example request](#example-request)

```
curl https://api.v0.dev/v1/chat/completions \
  -H "Authorization: Bearer $V0_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "v0-1.0-md",
    "messages": [
      { "role": "user", "content": "Create a Next.js AI chatbot" }
    ]
  }'
```

### [Example with streaming](#example-with-streaming)

```
curl https://api.v0.dev/v1/chat/completions \
  -H "Authorization: Bearer $V0_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "v0-1.0-md",
    "stream": true,
    "messages": [
      { "role": "user", "content": "Add login to my Next.js app" }
    ]
  }'
```

### [Response](#response)

If `stream` is `false` (default), the response is a JSON object:

```
{
  "id": "v0-123",
  "model": "v0-1.0-md",
  "object": "chat.completion",
  "created": 1715620000,
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Here's how to add login to your Next.js app..."
      },
      "finish_reason": "stop"
    }
  ]
}
```

If `stream` is `true`, the server returns a series of data chunks formatted as [Server-Sent Events (SSE)](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events). Each line begins with `data:` followed by a partial delta:

```
{
  "id": "v0-123",
  "model": "v0-1.0-md",
  "object": "chat.completion.chunk",
  "choices": [
    {
      "delta": {
        "role": "assistant",
        "content": "Here's how"
      },
      "index": 0,
      "finish_reason": null
    }
  ]
}
```

## [Usage limits](#usage-limits)

| Limit | Value |
| --- | --- |
| Max messages per day | 200 |
| Max context window size | 128,000 tokens |
| Max output context size | 32,000 tokens |

To request a higher limit, contact us at .

By using our API, you agree to our [API Terms](https://vercel.com/legal/api-terms).

## [More resources](#more-resources)

*   
*   
*   

Last updated on May 24, 2025