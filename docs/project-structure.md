# Project Structure

This document provides a detailed explanation of the OpenAI & Supabase Realtime Integration Compendium's organization.

## Overview

The project is organized into four main directories:

- **`docs/`** - All documentation, guides, and research
- **`templates/`** - Curated, production-ready starter templates
- **`scripts/`** - Utility scripts for project management
- **`archive/`** - Historical content and embedded repositories

## Directory Structure

```
supabase-openai-realtime-compendium/
├── docs/                       # Central documentation hub
│   ├── project-structure.md    # This file
│   ├── contributing.md         # Contribution guidelines
│   │
│   ├── 01-concepts/            # Core conceptual information
│   │   ├── integration-architecture.md
│   │   ├── tech-stack.md
│   │   ├── security-best-practices.md
│   │   └── use-cases.md
│   │
│   ├── 02-official-resources/  # Curated links to official docs
│   │   ├── openai.md
│   │   ├── supabase.md
│   │   └── vercel-ai.md
│   │
│   ├── 03-custom-research/     # Original research and analysis
│   │   ├── individual-analysis/
│   │   ├── merged-analysis/
│   │   └── other-notes-and-guides/
│   │
│   ├── 04-developer-experience/
│   │   ├── developer-experience-optimization-plan.md
│   │   └── getting-started-tomorrow.md
│   │
│   └── assets/                 # Images and static assets
│
├── templates/                  # Production-ready starter templates
│   ├── openai/
│   │   ├── realtime-agents/    # Multi-agent voice application
│   │   ├── realtime-console/   # Development console
│   │   ├── realtime-solar-system/ # Educational demo
│   │   ├── cookbook-highlights/ # Curated examples
│   │   └── js-workers-integration/ # Cloudflare Workers
│   │
│   ├── supabase/
│   │   ├── realtime-auth-demo/ # Authorization with RLS
│   │   ├── realtime-presence/  # Presence tracking
│   │   └── ai-vector-search-example/ # AI integration
│   │
│   ├── vercel-ai/
│   │   ├── ai-chatbot/         # Production chat app
│   │   └── next-openai-example/ # Integration example
│   │
│   └── mcp/
│       └── servers/            # MCP server implementations
│
├── scripts/                    # Utility scripts
│
└── archive/                    # Historical/reference content
    ├── embedded-libraries/     # Original SDK repositories
    ├── embedded-supabase-docs/ # Supabase documentation mirror
    └── v0-api-documentation.md
```

## Key Directories Explained

### `/docs/`

The documentation hub is organized with numbered prefixes to guide users through the content:

1. **`01-concepts/`** - Start here to understand the core concepts
2. **`02-official-resources/`** - Links to official documentation and SDKs
3. **`03-custom-research/`** - Original research and analysis
4. **`04-developer-experience/`** - Plans and guides for improving DX

### `/templates/`

Each template category contains production-ready starter projects:

- **`openai/`** - Templates focused on OpenAI Realtime API
- **`supabase/`** - Templates showcasing Supabase Realtime features
- **`vercel-ai/`** - Templates using Vercel AI SDK
- **`mcp/`** - Model Context Protocol implementations

### `/archive/`

Contains the original embedded repositories and documentation that were moved to reduce repository size and improve maintainability. These are kept for reference but are not actively maintained.

## Navigation Tips

1. **New to the project?** Start with `/docs/01-concepts/`
2. **Looking for templates?** Browse `/templates/` by technology
3. **Need official docs?** Check `/docs/02-official-resources/`
4. **Want to see research?** Explore `/docs/03-custom-research/`

## File Naming Conventions

- Documentation files use kebab-case: `integration-architecture.md`
- Directories use lowercase with hyphens: `realtime-auth-demo/`
- Research files maintain original names for traceability 