<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v3.

## Considered Options

- FastAPI 0.115
- Static S3 hosting only
- Nginx

## Decision Outcome

Chosen option: FastAPI 0.115, because Serves the built SPA assets and a health endpoint. No calculation or data logic runs server-side, matching the client-only design (US-013).

## Consequences

A dedicated app server is more than a pure static bundle strictly needs, but it satisfies the approved server layer with negligible cost and a near-empty footprint.
<!-- sdlc:auto:end adr -->