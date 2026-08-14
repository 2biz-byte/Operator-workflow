---
name: plan-weekly-stock-out-restock-runner
description: Run the "Plan weekly stock-out restock" action through the automation API and poll run status.

---

# Plan weekly stock-out restock Runner

## Goal
Run an existing action and return the `runId` so the caller can track progress.

## Authentication
- Use an API token in `Authorization: Bearer <token>`.
- Recommended scope: `api:access` (legacy: `automation:run` + `automation:read`).

## Required Input Keys
This action has no required runtime inputs.

## Start Run
- Endpoint: `POST https://gabrieloperator.com/api/automation/run/70e08a92-ef90-492a-bc7b-2f3b881af062/6a7c642624720ba67d5a1182`
- JSON body:

```json
{
  "parameters": {},
  "runContext": {},
  "dynamicLoopItems": [],
  "selectedLoopGroupId": null,
  "connectorOverrides": [],
  "variableOverrides": {},
  "liveBrowserMode": false,
  "liveBrowserProviderId": "auto",
  "name": "API Run"
}
```

## Poll Status
- Endpoint: `GET https://gabrieloperator.com/api/automation/status/{runId}`
- Continue polling until status is terminal (`COMPLETED`, `FAILED`, or `CANCELLED`).

## Expected Response Format

When this connector completes, write your primary output using a `set_api_output` step
so it appears in the status response as `data.output`.

The calling supervisor reads `data.output` from `GET https://gabrieloperator.com/api/automation/status/{runId}` once the run
reaches a terminal status (`COMPLETED`, `FAILED`, or `CANCELLED`).

### set_api_output contract
The output must be a JSON object. Recommended structure:

```json
{
  "result": "<primary answer or extracted data>",
  "summary": "<one-sentence human-readable summary>",
  "metadata": {}
}
```

### Take-control behaviour
If a step requires human interaction, the run transitions to `paused` status.
The status endpoint returns:

```json
{
  "status": "paused",
  "pauseContext": {
    "message": "Human input required",
    "url": "https://...",
    "stepNumber": 5
  },
  "liveDebugUrl": "https://..."
}
```

Resume the run with:
```
POST https://gabrieloperator.com/api/automation/resume/{runId}
{ "agentId": "70e08a92-ef90-492a-bc7b-2f3b881af062", "actionId": "6a7c642624720ba67d5a1182" }
```

## Key Learnings
- The workflow consistently completes 11 steps; recent durations show optimization (3.2s to 5.0s).
- MCP tool execution failures ("Could not resolve MCP server URL" or "MCP server URL or ID is required") remain non-blocking, though they appear in almost every step log.
- Interactive checkpoints (Inventory Scan, Sales Forecast, Supplier Drafts) are consistently reliable despite underlying MCP configuration warnings.
- Browser cleanup (close) failures continue to appear in logs; these are non-fatal and do not prevent successful workflow termination.
- Ongoing MCP configuration instability does not currently impede successful automation completion or API output delivery.

## Run History
- Run: 3769b4b0 Date: 2026-08-14 Status: completed
  Steps: 11 passed, 0 failed Duration: 5.0s
- Run: 33c3b703 Date: 2026-08-14 Status: completed
  Steps: 11 passed, 0 failed Duration: 3.2s