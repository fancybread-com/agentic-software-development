---
title: Skills Reference
---

# Skills Reference

**SDLC workflow skills (Agent Skills format) for AI-assisted development.**

The canonical skill definitions live in **`skills/`** (each skill is `skills/<name>/SKILL.md`). This documentation describes what each skill does. For full instruction content, see the [repository `skills/` folder](https://github.com/fancy-bread/sdlc-workflow-skills/tree/main/skills).

[:octicons-zap-24: Quick Reference](quick-reference.md){ .md-button }

---

## Development

| Command | What It Does |
|---------|--------------|
| **[`/start-task`](start-task.md)** | Begin implementation with branch and context |
| **[`/complete-task`](complete-task.md)** | Commit, push, create PR |

---

## Quality

| Command | What It Does |
|---------|--------------|
| **[`/review-code`](review-code.md)** | AI-assisted code review |

---

## Navigation

- **[Quick Reference](quick-reference.md)** - Copy-paste cheat sheet

---

## How Skills Work

Skills are Agent Skills (markdown with frontmatter) that tell AI agents what to achieve. The AI reads your project structure, issue tracker, implementation plans, and team conventions, then executes contextually—same skill, different projects, intelligent adaptation.

Each skill aligns with specific [ASDLC](https://asdlc.io) patterns and pillars (Factory Architecture, Standardized Parts, Quality Control); see [Agentic SDLC](https://asdlc.io/concepts/agentic-sdlc/) section 5. Strategic Pillars for details.

[See the full product flow →](../index.md#how-it-works)
