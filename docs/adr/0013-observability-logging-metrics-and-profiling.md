# 13. Observability: logging, metrics, and profiling

Date: 2025-10-13

## Status

Proposed

## Context

Cut tuning and scheduling require detailed operational data.

## Decision

- JSONL logging by wave and subcircuit  
Each log entry captures timestamps, subcircuit ID, space-time labels, node allocation, and outcome hashes. This enables deterministic reconstruction of executions and facilitates regression analysis.

- Metrics: $S$ (speed), $p$ (parallel efficiency), $E_p$ (energy performance), $\chi$ (complementary occupancy), $F$ (fidelity)
- Profiling: Nsight, mpiP, Scalasca  
  - *Nsight Systems/Compute:* GPU kernel occupancy, CUDA stream overlap, tensor contraction bottlenecks.
  - *mpiP:* inter-node MPI traffic patterns, communication cost (Comm) correlation with M1 model.
  - *Scalasca:* call-path tracing and synchronization imbalance for identifying malleability limits.
  Profiling is integrated into continuous integration for automatic sampling on representative runs.

- YAML config for reproducibility

### O2 & O3 Telemetry and Feedback Loop

The observability subsystem consists of two complementary components, O2 and O3, that together provide continuous performance insight and model feedback for the hybrid HPCQC runtime.

- O2 collects high-level operational metrics — such as speedup ($S$), parallel efficiency ($p$) or energy performance ($E_p$). Offering a global view of how efficiently resources are used and how well the system balances quantum and classical workloads.

- O3 performs low-level profiling through tools like Nsight, mpiP, and Scalasca, capturing detailed traces of GPU kernels, MPI communication patterns, synchronization delays, and power consumption.

This enables adaptive scheduling, improved parameter stability, and evidence-driven performance tuning without manual intervention, ensuring that the runtime remains consistent with real hardware behavior under varying load and quantum-device conditions.

## Consequences

- Evidence-based improvement cycles.
- Controlled telemetry overhead.
