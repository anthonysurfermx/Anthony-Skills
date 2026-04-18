# Anthony Skills

Multi-LLM workflows, skills, subagents y templates para día a día de trabajo AI-asistido.

## Structure

```
skills/                                 # Skills activables por Claude Code
├── security-and-hardening/SKILL.md     # ← addyosmani/agent-skills (MIT)
└── spec-driven-development/SKILL.md    # ← addyosmani/agent-skills (MIT)

agents/                                 # Subagents invocables con Task tool
├── ceo.md                              # Perspectiva estratégica
├── engmgr.md                           # Plan de ejecución
├── qa.md                               # Edge cases / red team
└── designer.md                         # UX / microcopy

templates/                              # Briefs para delegación multi-LLM
├── codex-brief.md                      # Backend / devil's advocate
├── gemini-brief.md                     # UX / user advocate
├── stitch-brief.md                     # Design system generation
└── synthesis.md                        # Combinar respuestas

guides/
└── opus-4.7-best-practices.md          # Effort levels + adaptive thinking

workflows/
└── multi-llm-head-of-product.md        # Claude como Head of Product

SKILL.md                                # Skill principal: anthony-daily-ai
```

## Installation

### Como skills y agents en Claude Code

Copia los directorios a la ubicación correspondiente:

```bash
# Skills globales
cp -r skills/* ~/.claude/skills/

# Agents globales (Task tool los encuentra por frontmatter `name:`)
cp -r agents/* ~/.claude/agents/
```

O clona y symlinkea:

```bash
git clone https://github.com/anthonysurfermx/Anthony-Skills ~/anthony-skills
ln -s ~/anthony-skills/skills/* ~/.claude/skills/
ln -s ~/anthony-skills/agents/* ~/.claude/agents/
```

### Como templates en un proyecto

```bash
cp -r templates/ .ai/templates/
```

## Skills incluidas

| Skill | Origen | Uso |
|---|---|---|
| `security-and-hardening` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | Review de secrets, API keys, DB passwords, trust boundaries antes de merge |
| `spec-driven-development` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | Escribir spec antes de código cuando la tarea no es trivial |
| `anthony-daily-ai` (SKILL.md raíz) | Propio | Multi-LLM orchestration + Opus 4.7 tuning |

## Agents / Subagents

Invocables con el Task tool de Claude Code. Cada uno carga un system prompt especializado:

- **`ceo`** (🎩) — trade-offs estratégicos, quarterly horizon, opportunity cost.
- **`engmgr`** (🛠️) — plan numerado, tiempos, blockers, rollback.
- **`qa`** (🔴) — cómo se va a romper, edge cases, silent failures.
- **`designer`** (🎨) — copy exacto, tono Chief of Staff, mobile-first.

Los mismos personas están en [anthony30x/skills/personas](https://github.com/anthonysurfermx/anthony30x/tree/main/skills/personas) y se invocan por Telegram con `claude haz @ceo ...`.

## Multi-LLM Workflow (resumen)

Core idea: en vez de usar un solo modelo, delegar a especialistas y sintetizar.

- **Claude Code** = Head of Product (analyze, decide, delegate, synthesize)
- **Codex/o1** = Backend Architect / Devil's Advocate
- **Gemini** = UX Designer / User Advocate
- **Stitch** = Design System Generator

Ver [workflows/multi-llm-head-of-product.md](workflows/multi-llm-head-of-product.md).

## Guides

### Opus 4.7 Best Practices
Referencia operativa: effort levels (`xhigh` default), adaptive thinking, subagent rules, session optimization, migración desde Opus 4.6. [guides/opus-4.7-best-practices.md](guides/opus-4.7-best-practices.md).

## Attribution

Ver [ATTRIBUTION.md](ATTRIBUTION.md) y [LICENSE.addyosmani](LICENSE.addyosmani) para las skills derivadas de `addyosmani/agent-skills`.

## License

Trabajo propio: MIT.
Partes derivadas de `addyosmani/agent-skills`: MIT, copyright (c) 2025 Addy Osmani.
