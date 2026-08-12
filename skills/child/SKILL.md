---
name: plan-weekly-stock-out-restock-child
description: Child execution skill for Plan weekly stock-out restock. 1 steps, mode: browserless.
type: child_skill
---

# Plan weekly stock-out restock — Child Skill

## Purpose
Execute the "Plan weekly stock-out restock" automation workflow.

## Operator Details
- **Mode:** browserless
- **Steps:** 1
- **Groups:** 0

## Step Summary

| # | Action | Intent |
|---|--------|--------|
| 1 | navigate | Workflow Start |

## Execution Notes
- Steps execute sequentially by step_number
- Template variables ({{stepId.var}}) resolve from prior step exports
- Browser steps use selectorPrompts as vision AI fallback if selectors fail
