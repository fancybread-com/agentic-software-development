# ASDLC Alignment: Skills → Patterns

This document provides explicit traceability from skills to ASDLC patterns and pillars, helping users understand the methodology behind the factory.

## Overview

The skills in this project implement ASDLC patterns and pillars. Each skill serves as a specialized station in a Factory Architecture, uses Standardized Parts (schema-enforced structure), and implements Quality Control (validation gates).

## Command Mapping

| Command | ASDLC Patterns | ASDLC Pillar | Description |
|---------|---------------|--------------|-------------|
| `/start-task` | [The Spec](https://asdlc.io/patterns/the-spec/), [The PBI](https://asdlc.io/patterns/the-pbi/), [Context Gates](https://asdlc.io/patterns/context-gates/) | Factory Architecture, Quality Control | Command station with pre-flight validation gates |
| `/complete-task` | [Constitutional Review](https://asdlc.io/patterns/constitutional-review/), [The Spec](https://asdlc.io/patterns/the-spec/), [The PBI](https://asdlc.io/patterns/the-pbi/), [Context Gates](https://asdlc.io/patterns/context-gates/) | Quality Control, Standardized Parts | Review Gate with dual-contract validation (Spec + Constitution) |
| `/review-code` | [Adversarial Code Review](https://asdlc.io/patterns/adversarial-code-review/), [Constitutional Review](https://asdlc.io/patterns/constitutional-review/), [The Spec](https://asdlc.io/patterns/the-spec/) | Quality Control | Review Gate using Critic Agent for dual-contract validation |

## ASDLC Pillars

The three ASDLC pillars are implemented across the skill set. **On ASDLC.io they are defined in one place:** [Agentic SDLC](https://asdlc.io/concepts/agentic-sdlc/) → **Strategic Pillars** (Factory Architecture, Standardized Parts, Quality Control). There are no separate pillar articles; use that concept page and scroll to section 5.

- **Factory Architecture**: Specialized skill stations that handle specific workflow phases

- **Standardized Parts**: Schema-enforced skills with consistent structure and validation

- **Quality Control**: Automated validation gates that ensure correctness before proceeding


## Pattern Details

### Core Patterns

- **[The Spec](https://asdlc.io/patterns/the-spec/)**: Living documents as permanent source of truth for features
- **[The PBI](https://asdlc.io/patterns/the-pbi/)**: Transient execution units that reference permanent Specs
- **[Context Gates](https://asdlc.io/patterns/context-gates/)**: Architectural checkpoints that filter input context and validate output artifacts

### Review Patterns

- **[Constitutional Review](https://asdlc.io/patterns/constitutional-review/)**: Verification pattern validating against both Spec and Constitution
- **[Adversarial Code Review](https://asdlc.io/patterns/adversarial-code-review/)**: Consensus verification using Critic Agent

### Governance Patterns

- **[Agent Constitution](https://asdlc.io/patterns/agent-constitution/)**: Persistent high-level directives shaping agent behavior

## How Skills Implement ASDLC

The skill mapping table above shows which patterns each skill implements. Key implementation details:

- **Context Gates**: Multiple skills implement validation checkpoints (see skills with Context Gates in the mapping table)
- **The Spec Pattern**: Skills create, read, or validate against Specs (permanent state documents)
- **The PBI Pattern**: Skills create or work with PBIs (transient execution units that reference Specs)
- **Constitutional Review**: Skills validate against both functional requirements (Spec) and architectural values (Constitution)

## Related Documentation

- [Skills Reference](../skills/index.md) - Detailed documentation for each skill
- [Getting Started](../getting-started.md) - Setup and usage guide
- [AGENTS.md](https://github.com/fancy-bread/sdlc-workflow-skills/blob/main/AGENTS.md) - Agent Constitution and operational boundaries

## External Resources

- [ASDLC.io](https://asdlc.io/) - ASDLC methodology and patterns
- [Agentic SDLC → Strategic Pillars](https://asdlc.io/concepts/agentic-sdlc/) - Where Factory Architecture, Standardized Parts, and Quality Control are defined (one concept page, scroll to section 5)
