# 12. Storage and checkpointing: HDF5 with MPI-IO

Date: 2025-10-13

## Status

Proposed

## Context

We need to persist shots, tensors, intermediate states, and reproducible checkpoints.

## Decision

Use HDF5 with MPI-IO for parallel writes, versioning artifacts and execution metadata.

## Consequences

- Enables reproducibility and fault-tolerant restart.
- Requires specialized I/O layer and dataset schemas.
