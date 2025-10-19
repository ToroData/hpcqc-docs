# RFC-05: Observability and M1–M2 Feedback Loop

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#8 Cost and Fidelity Model](../adr/0008-cost-and-fidelity-model.md)  
[#13 Observability Logging Metrics and Profiling](../adr/0013-observability-logging-metrics-and-profiling.md)

## Motivation

To validate and recalibrate models M1 (cost) and M2 (fidelity), the runtime requires continuous telemetry from modules O2 and O3. Observability enables evidence-based adaptation of scheduling and fidelity bounds.

## Scope

Defines metrics, telemetry collection, feedback integration, and update rules for $\alpha,\, \beta,\,\gamma,\,\Delta F$.

## Components

- O2 Metrics Aggregator — computes $S,\, p,\, E_p,\, \chi,\, F$ from logs.  
- O3 Profilers — Nsight Systems, mpiP, Scalasca produce traces
  for GPU utilization, Comm costs, synchronization imbalance.  
- Telemetry Bus — JSONL streams merged into HDF5 datasets.  
- Feedback Engine — adjusts M1/M2 parameters each $N$ waves.

## Feedback Algorithm

1. Collect mean $T_q$, $T_c$, and $\mathrm{Comm}$ from O3 traces.
2. Compute $\chi$ and $p$ from O2.
3. Update weights:
   - $\alpha \leftarrow \alpha \times \bigl(1 + \frac{\Delta T_q}{T_{q,\mathrm{ref}}}\bigr)$
   - $\beta \leftarrow \beta \times \bigl(1 + \frac{\Delta T_c}{T_{c,\mathrm{ref}}}\bigr)$
   - $\gamma \leftarrow \gamma \times \bigl(1 + \frac{\Delta \mathrm{Comm}}{\mathrm{Comm}_{\mathrm{ref}}}\bigr)$
4. If observed $\Delta F > \Delta F_{\mathrm{bound}}$ → tighten $\Delta F$ by factor $0.9$.
5. Notify scheduler for next wave plan.

## Data Retention

- Logs kept 90 days.
- Metrics aggregated hourly.
- Sensitive data anonymized before export.

## Risks

- Over-frequent recalibration may destabilize scheduling.  
- Profiling overhead if Nsight sampling > 10 %.  

## Acceptance Criteria

- Telemetry overhead < 3 % runtime.  
- M1 prediction error < 10 % of measured times.  
- $\Delta F$ prediction error < 0.01 absolute.
