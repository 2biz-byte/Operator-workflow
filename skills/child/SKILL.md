---
name: plan-weekly-stock-out-restock-child
description: Child execution skill for Plan weekly stock-out restock. 11 steps, mode: browserless.
type: child_skill
---

# Plan weekly stock-out restock — Child Skill

## Purpose
Execute the "Plan weekly stock-out restock" automation workflow.

## Operator Details
- **Mode:** browserless
- **Steps:** 11
- **Groups:** 0

## Step Summary

| # | Action | Intent |
|---|--------|--------|
| 1 | navigate | Workflow Start |
| 2 | mcp_tool | Scan Shopify Inventory |
| 3 | confirmation | Approve Inventory Scan & Transition |
| 4 | mcp_tool | Pipeline Transition - inventory_ready |
| 5 | mcp_tool | Calculate Sales Forecast Reorder Quantities |
| 6 | confirmation | Approve Sales Forecast & Transition |
| 7 | mcp_tool | Pipeline Transition - forecast_ready |
| 8 | mcp_tool | Create Supplier Email Drafts in Gmail |
| 9 | confirmation | Approve Supplier Drafts & Transition |
| 10 | mcp_tool | Pipeline Transition - drafts_ready |
| 11 | api_output | Export Final Restock Plan & Draft Information |

## Execution Notes
- Steps execute sequentially by step_number
- Template variables ({{stepId.var}}) resolve from prior step exports
- Browser steps use selectorPrompts as vision AI fallback if selectors fail
