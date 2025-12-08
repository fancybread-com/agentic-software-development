---
title: Quick Reference
---

# Command Quick Reference

**Copy-paste ready commands.**

[:octicons-list-unordered-24: All Commands](index.md){ .md-button }
[:octicons-person-24: By Role](by-role.md){ .md-button }

---

## Command Organization

```
agentic-software-development/
├── Product (2)
│   ├── /create-story
│   └── /create-epic
│
├── Development (5)
│   ├── /create-task-plan
│   ├── /start-task
│   ├── /verify-task
│   ├── /complete-task
│   └── /sync-task
│
└── Quality (4)
    ├── /create-unit-tests
    ├── /create-integration-tests
    ├── /create-e2e-tests
    └── /review-code
```

**11 commands total**

---

## Product Management

```bash
# Create user story
/create-story for [feature description]

# Create epic from plan
/create-epic from [plan-file.md]
```

---

## Development

```bash
# Design implementation
/create-task-plan for TASK-123

# Start work
/start-task TASK-123

# Pre-flight check (optional)
/verify-task TASK-123

# Ship it
/complete-task TASK-123

# Update after merge
/sync-task TASK-123
```

---

## Quality

```bash
# Write tests
/create-unit-tests for ClassName
/create-integration-tests for FeatureName
/create-e2e-tests for [user journey]

# Review code
/review-code for PR #42
```

---

## By Role

**Product Manager:**
```bash
/create-story for [feature]
/create-epic from [plan.md]
```

**Engineer (Daily):**
```bash
/create-task-plan for TASK-123
/start-task TASK-123
/complete-task TASK-123
```

**QA:**
```bash
/create-e2e-tests for [user journey]
/create-integration-tests for FeatureName
/create-unit-tests for ClassName
```

---

[:octicons-arrow-left-24: Back to Commands](index.md)
