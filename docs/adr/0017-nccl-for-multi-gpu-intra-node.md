# 17. NCCL for multi-GPU intra-node

Date: 2025-10-13

## Status

Proposed

## Context

Contractions and partial reductions require efficient collectives between GPUs in the same node.

## Decision

Use NCCL for intra-node all-reduce and broadcast, coordinated with MPI for inter-node communication.

## Consequences

- Better utilization of NVLink and GPU topologies.
- Dual MPI–NCCL management complexity.
