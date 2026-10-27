# simple calculator-1 — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
simple calculator

**Documentation version:** v6
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v4 approved |
| [Architecture](architecture/README.md) | 12 entries |
| [Development](development/README.md) | 2 entries |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 4 decisions |
| [Sprint plan](development/sprint-plan.md) | 2 sprints |
| [Developer guide](development/developer-guide.md) | generated |
| [API reference](development/api-reference.md) | 1 route |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 13 requirements |
| [Changelog](CHANGELOG.md) | 6 versions |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Database and backend are named for policy/platform-default reasons only, not functional need -- confirm with architecture phase that no incidental persistence or API surface gets introduced beyond serving the static page.
- No explicit approval status recorded for the scope document itself (only the technology stack is stated as approved by the product owner).
- No requirement addresses numeric overflow or very long numbers (e.g. display width limits) beyond the divide-by-zero case -- only that one error condition is specified.
- No acceptance criteria cover chained calculations combined with decimals or negative numbers together.
- No specific breakpoints, minimum tap-target size, or device matrix defined for the responsive layout (US-010) -- left to design phase.
- No specification of keyboard behavior for the sign-toggle or decimal keys (only digit/operator/Enter/Escape/Delete keys are specified).
- No requirement states how the approved FastAPI/PostgreSQL layers (named for policy reasons only) will be kept entirely inert from a privacy standpoint -- worth confirming in architecture phase that no telemetry or logging inadvertently captures calculation data.
- NFR-005 only names divide-by-zero as the invalid-input example; no other invalid-input scenarios (e.g. malformed keyboard sequences) are enumerated.
- No explicit performance budget (e.g. max latency in ms) given for 'instantly' in NFR-003 -- qualitative only.

### Architecture

- PostgreSQL 16 RDS node is provisioned but has no schema or current use -- confirm whether it should remain provisioned (cost) or be deferred until a feature needs persistence.
- Rationale references NFR-002 and NFR-003, which are not present in the known requirement-key list provided -- confirm these NFR ids and add traceability once available.
- Rationale references NFR-001, which is not present in the known requirement-key list provided -- confirm this NFR id for traceability.
- Database is provisioned with zero current schema/use; flagged for cost/scope review (see ARCH-DEPLOY-1).

### Development

- No development execution evidence (tickets, commits, build/test status) provided for Sprint 1 — cannot confirm whether any of these items were actually implemented.
- Epics EPIC-007, EPIC-008, EPIC-009 have no assigned role and no point estimate recorded.
- US-005, US-014 referenced in requirement keys are not part of Sprint 1 scope despite being under the same epics as some Sprint 1 items — confirm this split is intentional.
- No development execution evidence (tickets, commits, build/test status) provided for Sprint 2 — cannot confirm whether any of these items were actually implemented.
- 'Confirmation of client-side-only privacy behavior' is stated as a sprint goal but no verification method, test, or result was supplied to confirm US-013 was actually validated.

### Testing

- Testing phase has not started -- no test artifacts exist to document.

### Deployment

- No deployment recorded yet -- nothing to document for this phase.

### Maintenance

- Maintenance phase has not started -- no post-deployment activity exists to document.
<!-- sdlc:auto:end open-gaps -->
