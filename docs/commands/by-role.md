---
title: Commands by Role
---

# Commands by Role

Find commands relevant to your role.

[:octicons-list-unordered-24: All Commands](index.md){ .md-button }
[:octicons-zap-24: Quick Reference](quick-reference.md){ .md-button }

---

## Product Manager

**Daily:**
- [`/create-story`](product/create-story.md) - Create user stories from ideas

**Weekly:**
- [`/create-epic`](product/create-epic.md) - Define major initiatives

[View role guide →](../roles/product-manager.md)

---

## Software Engineer (IC)

**Daily:**
- [`/start-task`](development/start-task.md) - Begin implementation
- [`/complete-task`](development/complete-task.md) - Create PR

**Weekly:**
- [`/create-task-plan`](development/create-task-plan.md) - Design before coding
- [`/create-unit-tests`](quality/create-unit-tests.md) - Add test coverage

**Occasional:**
- [`/verify-task`](development/verify-task.md) - Pre-completion check
- [`/sync-task`](development/sync-task.md) - Update after merge
- [`/create-integration-tests`](quality/create-integration-tests.md) - Integration coverage

[View role guide →](../roles/engineer.md#ic-engineer)

---

## Senior Engineer

**All IC commands, plus:**

**Daily:**
- [`/review-code`](quality/review-code.md) - Review PRs with AI assistance

**Weekly:**
- [`/create-integration-tests`](quality/create-integration-tests.md) - System integration

**Occasional:**
- [`/create-e2e-tests`](quality/create-e2e-tests.md) - Critical path testing

[View role guide →](../roles/engineer.md#senior-engineer)

---

## Staff / Principal Engineer

**All Senior commands, plus:**

**Weekly:**
- [`/create-epic`](product/create-epic.md) - Technical initiatives
- [`/create-task-plan`](development/create-task-plan.md) - System design

**Occasional:**
- Cross-team coordination using most commands
- Architecture and standards work

[View role guide →](../roles/engineer.md#staff-engineer)

---

## QA Engineer

**Daily:**
- [`/create-e2e-tests`](quality/create-e2e-tests.md) - User journey testing

**Weekly:**
- [`/create-integration-tests`](quality/create-integration-tests.md) - Integration coverage
- [`/create-unit-tests`](quality/create-unit-tests.md) - Component testing

**Occasional:**
- [`/start-task`](development/start-task.md) - Test automation work
- [`/complete-task`](development/complete-task.md) - Submit test code

[View role guide →](../roles/qa.md)

---

## Command Matrix

| Command | PM | IC | Senior | Staff+ | QA |
|---------|----|----|--------|--------|----|
| `/create-story` | ●●● | ○ | ○ | ○ | - |
| `/create-epic` | ●●● | - | - | ●● | - |
| `/create-task-plan` | - | ●●● | ●●● | ●●● | - |
| `/start-task` | - | ●●● | ●●● | ●●● | ●● |
| `/verify-task` | - | ●● | ●● | ●● | ●● |
| `/complete-task` | - | ●●● | ●●● | ●●● | ●● |
| `/sync-task` | - | ●● | ●● | ●● | ○ |
| `/create-unit-tests` | - | ●●● | ●●● | ●● | ●● |
| `/create-integration-tests` | - | ●● | ●●● | ●● | ●●● |
| `/create-e2e-tests` | - | ○ | ●● | ●● | ●●● |
| `/review-code` | - | - | ●●● | ●●● | - |

**Legend:** ●●● Daily | ●● Weekly | ○ Occasional | - Not typical

---

[:octicons-arrow-left-24: Back to Commands](index.md)
