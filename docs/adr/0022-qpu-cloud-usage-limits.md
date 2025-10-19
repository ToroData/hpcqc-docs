# 22. QPU cloud usage limits

Date: 2025-10-13

## Status

Proposed

## Context

We have limited execution windows on IBM Torino, around 10 minutes per month.

## Decision

Reserve the QPU for critical subcircuits with higher fidelity impact and validate representative points. Simulate the remaining circuits on HPC using cuQuantum and Aer.

## Consequences

- Efficient use of quantum time.
- Limited statistical results from real hardware.
