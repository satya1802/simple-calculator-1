<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v3.

## Considered Options

- PostgreSQL 16
- None needed in this version

## Decision Outcome

Chosen option: PostgreSQL 16, because No data is stored or persisted in this version (NFR-001), so PostgreSQL carries no schema. It is named to satisfy the approved data layer and is the one to adopt if saved history or settings are added later.

## Consequences

Provisioning an unused database adds a small fixed cost; it is retained only to honour the approved stack and ease a future persistence feature.
<!-- sdlc:auto:end adr -->