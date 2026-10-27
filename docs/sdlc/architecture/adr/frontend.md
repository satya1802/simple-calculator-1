<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v3.

## Considered Options

- React 19
- Vue
- Svelte
- Vanilla JS

## Decision Outcome

Chosen option: React 19, because React 19 renders the interactive single-page calculator, holds calculation state in a reducer hook, and updates the display instantly on each tap or keypress (NFR-003). Responsive CSS adapts the keypad for desktop and mobile (NFR-002).

## Consequences

React is heavier than vanilla JS for so small an app, but it is the approved platform default and gives a clean component and state model for the keypad, display and keyboard handling.
<!-- sdlc:auto:end adr -->