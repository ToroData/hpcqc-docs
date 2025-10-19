# 9. Malleable HEFT scheduler

Date: 2025-10-13

## Status

Proposed

## Context

Subcircuits have heterogeneous costs and QPU windows. Overlapping classical and quantum computation is required.

## Decision

Implement a malleable scheduler based on a modified HEFT algorithm, using dynamic MPI teams via `MPI_Comm_split`, critical-path priorities, and cost-weighted and energy-aware policies.

- Priorities by critical path and topological level,
- Dynamic MPI devices using MPI_Comm_split to adjust concurrency,
- Cost-weighted policy using $w = \alpha T_q + \beta T_c + \gamma \text{Comm}$,
- Energy-aware policy to limit power consumption during peaks,
- Telemetry feedback for online reordering and device resizing.

The alternative could be Charm++ Overdecomposition. Good task object migration, but complicates integration with existing Slurm and MPI.

## Consequences

- Overlaps QPU–HPC workloads and reduces idle time.
- Increases runtime team management complexity.
