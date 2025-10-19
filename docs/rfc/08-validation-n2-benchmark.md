# RFC-08: Scientific Validation and Benchmarking (N₂ Case)

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#21 Benchmark Selection N₂](../adr/0021-benchmark-selection-n2-and-metrics.md)

---

## Motivation

Validation must demonstrate that the hybrid system reproduces quantum-chemical observables of molecular nitrogen $\mathrm{N_2}$ within acceptable error bounds compared to reference simulations.

## Benchmark Definition

- Basis set: STO-3G
- Number of orbitals: 6  
- Hamiltonian mapped via Jordan–Wigner
- Expected ground-state energy: $E_0 = -108.988\,\mathrm{Ha}$

## Procedure

1. Generate circuit with Qiskit.
2. Export to QASM3 and ingest into hybrid runtime.  
3. Partition into $k$ spatial and $m$ temporal layers.  
4. Execute classical contractions on HPC nodes; quantum waves on QPU cloud.  
5. Reconstruct density matrix ρ and compute observables.

## Metrics

- Energy deviation $|E - E_0| < 10^{-3}\,\mathrm{Ha}$
- Fidelity $F(ρ,ρ_{\text{ref}}) > 0.95$
- Speedup $S = T_{\text{mono}} / T_{\text{hybrid}} > 1.5$
- Complementary occupancy $\chi > 0.8$

## Acceptance Criteria

- All metrics satisfied in ≥ 3 consecutive runs.  
- Results reproducible with identical IR hash.  
- Benchmark documented and versioned under `/benchmarks/N2`.
