# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Core arithmetic engine, display, on-screen button input, clear/reset, decimal entry, chained calculations, and free/anonymous access.

Capacity: 20 points · Committed: 17

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Perform addition, subtraction, multiplication and division | 3 | frontend-agent | — |
| US-002 | Story | Chained multi-step calculations | 3 | frontend-agent | US-001 |
| US-003 | Story | Decimal number entry | 2 | frontend-agent | US-001 |
| US-006 | Story | Current entry and result display | 2 | frontend-agent | — |
| US-007 | Story | On-screen button input | 3 | frontend-agent | US-006 |
| US-009 | Story | Clear and all-clear | 2 | frontend-agent | US-006 |
| US-011 | Story | Anonymous use with no login | 1 | frontend-agent | US-006 |
| US-012 | Story | Free to use with no payments | 1 | frontend-agent | — |

## Sprint 2: Sprint 2

Keyboard input, sign toggle, divide-by-zero error handling, responsive layout, and confirmation of client-side-only privacy behavior.

Capacity: 20 points · Committed: 13

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-005 | Story | Divide-by-zero and invalid-input error state | 3 | frontend-agent | US-001 |
| US-008 | Story | Keyboard number and operator input | 3 | frontend-agent | US-006, US-007 |
| US-014 | Story | Sign toggle (positive / negative) | 2 | frontend-agent | US-006 |
| US-010 | Story | Responsive desktop and mobile layout | 3 | frontend-agent | US-007 |
| US-013 | Story | Client-side operation with no stored data | 2 | frontend-agent | US-001 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
