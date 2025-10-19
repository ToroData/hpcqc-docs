# RFC-03: Malleable HEFT Scheduler and Resizing Rules

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#8 Cost and Fidelity Model](../adr/0008-cost-and-fidelity-model.md)  
[#9 Malleable HEFT Scheduler](../adr/0009-malleable-heft-scheduler.md)  
[#14 RMS Integration](../adr/0014-rms-integration-slurm-hyperqueue-pbs.md)

## Motivation

Hybrid subcircuits differ in cost composition ($T_q,\, T_c,\, \text{Comm}$). The scheduler must minimize total makespan while overlapping HPC and QPU work, adjusting dynamically to resource availability.

## Scope

Defines the modified HEFT algorithm, malleability model, resizing policies, and rescheduling triggers.

## Algorithm Design

Base algorithm: HEFT (Heterogeneous Earliest Finish Time)  
Modifications:

- Composite cost model:  
  $C(v) = \alpha \cdot T_q(v) + \beta \cdot T_c(v) + \gamma \cdot \text{Comm}(v)$
- Window awareness: penalties when QPU slot unavailable
- Dynamic teams: create/destroy MPI communicators (`MPI_Comm_split`)
- Energy-aware policy: global power cap and cost feedback
- Re-scheduling: triggered by deviations reported by O2/O3 modules

### Priority Computation

Each node receives rank u (upward) based on critical path length using M1 costs. Tasks scheduled in descending rank u, earliest start respecting dependencies.

### Malleability Rules

- Teams resized at wave boundaries only.
- Minimum dwell time between resizes $= 2\,\times$ average $T_q$.
- Resizing favored when occupancy $\chi < 0.7$ or GPU idle $> 20 \%$.
- Team creation limited by RMS quotas.

### Pseudocode

```Python
for wave in ready_waves:
  ranks = sort_by_rank_u(wave)
for task in ranks:
  device = select_best_resource(task)
  schedule(task, device)
  update_teams(O2.metrics)
```

## Telemetry Integration

O2 supplies $\chi,\, E_p,\, p$; O3 supplies Comm and GPU utilization.
Weights ($\alpha,\, \beta,\, \gamma$) recalibrated periodically.

## Risks

- Parameter sensitivity may cause oscillations.  
- Re-sizing overhead on large MPI worlds.

## Acceptance Criteria

- Idle HPC time reduced ≥ 30 %.  
- Complementary occupancy χ ≥ 0.8.  
- Scheduler overhead ≤ 2 % of runtime.
