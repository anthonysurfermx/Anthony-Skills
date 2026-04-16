# Anthony Skills

Multi-LLM workflows, brief templates, and best practices for day-to-day AI-assisted work by Anthony Chavez.

## Structure

```
templates/           # Brief templates for multi-LLM delegation
├── codex-brief.md   # Backend architecture / devil's advocate (Codex/o1/o3)
├── gemini-brief.md  # UX design / user advocate (Gemini)
├── stitch-brief.md  # Design system screen generation (Stitch MCP)
└── synthesis.md     # Combine responses from multiple models

guides/              # Model-specific best practices and operational references
└── opus-4.7-best-practices.md  # Effort levels, adaptive thinking, session optimization

workflows/           # Reusable AI workflows
└── multi-llm-head-of-product.md  # Claude as Head of Product in a multi-LLM team
```

## Multi-LLM Workflow

The core idea: instead of using one AI model for everything, delegate specialized tasks to the right model and synthesize their responses.

- **Claude Code** = Head of Product (analyze, decide, delegate, synthesize)
- **Codex/o1** = Backend Architect / Devil's Advocate
- **Gemini** = UX Designer / User Advocate
- **Stitch** = Design System Generator

See [workflows/multi-llm-head-of-product.md](workflows/multi-llm-head-of-product.md) for the full framework.

## Guides

### Opus 4.7 Best Practices
Referencia operativa para Claude Opus 4.7 con Claude Code: effort levels (`xhigh` default), adaptive thinking, subagent rules, session optimization, y tabla de migración desde Opus 4.6.

See [guides/opus-4.7-best-practices.md](guides/opus-4.7-best-practices.md).

## Usage

### Use the multi-LLM workflow
1. Copy `templates/` into your project's `.ai/templates/`
2. Add the workflow instructions to your `CLAUDE.md`
3. Create `.ai/briefs/`, `.ai/responses/`, `.ai/decisions/` directories

See the workflow doc for details.

## License
MIT
