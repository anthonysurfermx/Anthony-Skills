# Anthony Skills

Reusable AI agent skills, multi-LLM workflows, and brief templates by Anthony Chavez.

## Structure

```
skills/              # Autonomous agent skill definitions
└── bobby-trader/    # AI Trading CIO with 3-agent debate system

templates/           # Brief templates for multi-LLM delegation
├── codex-brief.md   # Backend architecture / devil's advocate (Codex/o1/o3)
├── gemini-brief.md  # UX design / user advocate (Gemini)
├── stitch-brief.md  # Design system screen generation (Stitch MCP)
└── synthesis.md     # Combine responses from multiple models

workflows/           # Reusable AI workflows
└── multi-llm-head-of-product.md  # Claude as Head of Product in a multi-LLM team
```

## Skills

### Bobby Agent Trader
AI Trading CIO with a 3-agent internal debate system (Alpha Hunter, Red Team, CIO). 10 real-time data sources, technical analysis, conviction scoring, and on-chain execution on OKX X Layer.

## Multi-LLM Workflow

The core idea: instead of using one AI model for everything, delegate specialized tasks to the right model and synthesize their responses.

- **Claude Code** = Head of Product (analyze, decide, delegate, synthesize)
- **Codex/o1** = Backend Architect / Devil's Advocate
- **Gemini** = UX Designer / User Advocate
- **Stitch** = Design System Generator

See [workflows/multi-llm-head-of-product.md](workflows/multi-llm-head-of-product.md) for the full framework.

## Usage

### Use a skill in your project
Copy the skill markdown into your agent framework (OpenClaw, Hermes, or any system that reads skill files).

### Use the multi-LLM workflow
1. Copy `templates/` into your project's `.ai/templates/`
2. Add the workflow instructions to your `CLAUDE.md`
3. Create `.ai/briefs/`, `.ai/responses/`, `.ai/decisions/` directories

See the workflow doc for details.

## License
MIT
