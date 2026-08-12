---
name: plan-weekly-stock-out-restock-child
description: Child execution skill for Plan weekly stock-out restock. 12 steps, mode: browserless.
type: child_skill
---

# Plan weekly stock-out restock — Child Skill

## Purpose
Execute the "Plan weekly stock-out restock" automation workflow.

## Operator Details
- **Mode:** browserless
- **Steps:** 12
- **Groups:** 0

## Step Summary

| # | Action | Intent |
|---|--------|--------|
| 1 | navigate | Workflow Start |
| 2 | mcp_tool | Scan Shopify Inventory |
| 3 | mcp_tool | Scan Shopify Inventory (copy) |
| 4 | confirmation | Approve Inventory Scan & Transition |
| 5 | mcp_tool | Pipeline Transition - inventory_ready |
| 6 | mcp_tool | Calculate Sales Forecast Reorder Quantities |
| 7 | confirmation | Approve Sales Forecast & Transition |
| 8 | mcp_tool | Pipeline Transition - forecast_ready |
| 9 | mcp_tool | Create Supplier Email Drafts in Gmail |
| 10 | confirmation | Approve Supplier Drafts & Transition |
| 11 | mcp_tool | Pipeline Transition - drafts_ready |
| 12 | api_output | Export Final Restock Plan & Draft Information |

## Execution Notes
- Steps execute sequentially by step_number
- Template variables ({{stepId.var}}) resolve from prior step exports
- Browser steps use selectorPrompts as vision AI fallback if selectors fail
