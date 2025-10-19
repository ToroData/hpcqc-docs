# 11. Tensor contraction stitching: cuBLAS and cuTensorNet

Date: 2025-10-13

## Status

Proposed

## Context

Post-cut reconstruction requires efficient GPU tensor contractions and distributed aggregation.

## Decision

Use cuTensorNet for tensor contraction and cuBLAS for dense algebra. Use NVIDIA Collective Communication Library (NCCL) for intra-node all-reduce and MPI Iallreduce for inter-node reductions.

## Consequences

- High GPU performance.
- Explicit CUDA and NCCL dependency.
