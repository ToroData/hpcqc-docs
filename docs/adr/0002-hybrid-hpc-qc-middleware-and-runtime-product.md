# 2. Product: Hybrid HPCQC middleware and runtime

Date: 2025-10-13

## Status

Proposed

## Context

The project must integrate quantum computing on QPUs and classical HPC computing, orchestrating spatiotemporal partitioning and tensor contraction, without modifying QPU firmware.

## Decision

We define the product as hybrid HPCQC middleware + runtime:

- Middleware: partitioning, scheduling, orchestration with RMS, and telemetry.
- Runtime: Execution API, task queues, transport to QPUs, and data plane.

## Consequences

The scope is defined based on middleware/execution layer software, avoiding firmware layers and maximizing portability between vendors and HPC centers.
