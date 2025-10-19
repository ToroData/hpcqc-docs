# 7. Partition policy: wire cuts and time cuts

Date: 2025-10-13

## Status

Proposed

## Context

We need to reduce quantum depth and latency while maintaining fidelity.

## Decision

Apply wire cuts on low-correlation bipartitions and time cuts on trotterized sequences or temporal layers. Use heuristics based on crossed 2Q counts and entropy estimators.

## Consequences

- Controlled trade-off between fidelity and cost.
- Requires an explicit evaluation of the expected fidelity loss ($\Delta F$) introduced by each cut, using conservative upper bounds to ensure that the overall circuit accuracy remains within the target error tolerance.
