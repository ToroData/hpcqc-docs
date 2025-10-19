# RFC-01: IR Specification and Serialization Contract

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#4 OpenQASM 3](../adr/0004-quantum-exchange-format-openqasm-3.md)  
[#5 QASM3 Parser](../adr/0005-qasm3-parser-with-antlr4-in-c.md)  
[#6 Internal IR](../adr/0006-internal-ir-space-time-dag-with-annotations.md)  

## Motivation

Middleware between HPC and QC requires an intermediate representation that expresses quantum-classical dependencies, spatiotemporal structure, and cost metadata. OpenQASM 3 provides the syntax and is nearly standard across many technologies, but does not provide operational semantics. This RFC defines a stable, versioned IR (Intermediate Representation), used internally for partitioning, scheduling, and reproducibility.

## Scope

- Logical and data model of the IR
- Serialization and versioning policy
- Validation and compatibility rules
- Excludes backend-specific transpilation

## Design Overview

Each circuit is parsed into a **space-time DAG**:

- **Node**: represents a quantum or classical operation  
  `id, type, qubits, cvars, time_index, deps, cost, fidelity_est, metadata`
- **Edge**: dependency (temporal or data)
- **Annotations**:  
  `space` labels identify qubit partitions  
  `time` labels identify temporal slices or trotterized steps  
- **Metadata**: `depth`, `2Qcount`, `layout`, `error_rate`

### Invariants

- DAG is acyclic
- `time_index` is non-decreasing along edges
- Space labels form a full partition of qubits
- All nodes carry cost fields compatible with M1 model

### Serialization

Primary format: JSON Schema
Each file includes a `ir_version` field (semver).
Example:

```json
{
  "ir_version":"1.0.0",
  "nodes":[
    {"id":1,"type":"cx","qubits":[0,1],"space":"s0","time":0,
     "cost":{"Tq":0.15,"Tc":0,"Comm":0},"deps":[]}
  ]
}
```

### Versioning Policy

Minor versions add optional fields with defaults.  
Breaking changes increment the major version.  
Migration scripts provided under `tools/ir_migrate`.

## Rationale

A custom IR avoids dependence on LLVM/MLIR while capturing hybrid semantics relevant to space–time circuit knitting.

## Risks

- Divergence from QIR standard if community evolves quickly.
- Parser upgrades must preserve compatibility.

## Acceptance Criteria

- IR validates under schema and round-trips from and to QASM3 without loss.
- Partitioning and scheduling operate solely on IR data.
