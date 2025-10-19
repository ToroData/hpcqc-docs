# 3. Base language and toolchain: C++23 + MPI + CUDA

Date: 2025-10-13

## Status

Proposed

## Context

High performance, HPC portability, and GPU acceleration are required. BSC offers mature toolchains for C++, MPI, and CUDA.

## Decision

Use C++23 for the core, MPI for inter-node communication, and CUDA >= 12.x for GPU kernels and libraries. Use OpenMP and OmpSs-2 for intra-node parallelism. Compilation handled with CMake.

## Consequences

- High performance and fine memory control.
- Natural integration with cuBLAS, cuTensorNet, and NCCL.
- More complex than Python for the core, but Python bindings will be provided at the outer layer.
