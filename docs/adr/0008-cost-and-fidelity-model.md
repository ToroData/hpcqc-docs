# 8. Cost and fidelity model

Date: 2025-10-13

## Status

Proposed

### Cost Model (M1)

The M1 model estimates the total time cost of executing a hybrid subcircuit (quantum + classical). For each node of the IR graph, three components are assigned:

- $T_q$: estimated quantum execution time, obtained from the QPU backend or simulator (gate time, queue time, and dispatch latency).
- $T_c$: estimated classical computation time, obtained by benchmarking CUDA kernels, tensor contraction, or GPU reduction.
- $\text{Comm}$: communication time or cost between nodes or devices (MPI, NCCL, or CPU-GPU transfer).

The total cost is modeled as a weighted linear combination:

$C(v)=\alpha T_q(v) + \beta T_c(v) + \gamma \text{Comm}(v)$

where the coefficients $\alpha$, $\beta$, and $\gamma$ reflect the relative importance of each component depending on the context and are empirically calibrated through profiling.

The planner's objective is to minimize the overall makespan by considering this composite cost, dynamically adjusting the weights based on telemetry (O2 and O3,see ADR #13).

### Fidelity Model (M2)

The M2 model estimates the fidelity loss induced by each spatial or temporal slice.
Each partition introduces a bias $\Delta F$ that depends on:

- The number of 2Q gates crossing the slice (a proxy for correlation between subcircuits).
- The bipartition entropy estimated from the IR (a measure of entanglement).
- The local depth and backend noise (expected accumulated error).

The model associates an upper bound $\Delta F_{\max}$ with each cut, and the scheduler penalizes solutions where the total estimated fidelity exceeds a threshold.

Both models are used together: M1 reports the time cost, and M2 imposes an accuracy constraint.

The final scheduling seeks to minimize the total time without degrading fidelity beyond the allowed value.

## Consequences

- Subcircuits can be quantitatively prioritized based on cost and fidelity.
- The HEFT scheduler has consistent information for making multi-objective decisions.
- Precise instrumentation and profiling are required to update the parameters α, β, γ, and $\Delta F$.
