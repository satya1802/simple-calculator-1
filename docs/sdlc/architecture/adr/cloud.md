<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v3.

## Considered Options

- AWS
- Vercel
- Netlify
- Cloudflare Pages

## Decision Outcome

Chosen option: AWS, because Delivers a responsive public page worldwide at low cost and scales to any number of anonymous visitors without managed machines (US-011, US-012). CloudFront caching keeps latency low globally.

## Consequences

AWS has more moving parts than a single-purpose static host, but it is the approved platform default and comfortably covers a free utility page's modest traffic.
<!-- sdlc:auto:end adr -->