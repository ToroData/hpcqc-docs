# 16. No Chapel, Charm++, or UPC in core

Date: 2025-10-13

## Status

Proposed

## Context

Alternative models offer productivity and dynamic load balancing but add runtime dependencies and heterogeneity.

## Decision

Do not use Chapel, Charm++, or UPC in the core. They remain optional for comparative prototypes or publications. The core stays in C++, MPI, OpenMP, OmpSs-2.

## Consequences

- Reduced portability complexity.
- Comparative results documented when relevant.
