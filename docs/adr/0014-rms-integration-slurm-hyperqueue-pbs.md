# 14. RMS integration: Slurm, HyperQueue, PBS

Date: 2025-10-13

## Status

Proposed

## Context

Execution at BSC-CNS and similar environments requires integration with resource managers.

## Decision

Implement an RMS adapter for Slurm first, with extensions for HyperQueue and PBS. Support heterogeneous reservations and srun/sbatch launchers.

## Consequences

- Standard deployment in HPC environments.
- Center-specific adaptation layer.
