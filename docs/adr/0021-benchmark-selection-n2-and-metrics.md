# 21. Benchmark selection: N2 and metrics

Date: 2025-10-13

## Status

Proposed

## Context

A representative and measurable case is needed to validate the runtime.

## Decision

Use $N_2$ molecule as the main study case, with dissociation curves in manageable bases for 10 minutes of QPU monthly runtime and HPC simulation. Metrics: fidelity $F$, effective depth $D_eff$, speedup $S$, $p$, efficiency $E_p$, complementary occupancy $\chi$, and approximate energy cost.

## Consequences

- Comparability with recent literature.
- Solid baseline for evaluation and publication.
