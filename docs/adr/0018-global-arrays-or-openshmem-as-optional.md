# 18. Global Arrays or OpenSHMEM as optional

Date: 2025-10-13

## Status

Proposed

## Context

One-to-many access bottlenecks may occur in the tensor plane during distributed stitching.

## Decision

Mark Global Arrays or OpenSHMEM as optional features, enabled only if profiling shows performance benefits over MPI RMA.

## Consequences

- Avoids unnecessary complexity by default.
- Provides a clear path for advanced optimization.
