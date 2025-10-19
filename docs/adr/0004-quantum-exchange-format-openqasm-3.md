# 4. Quantum exchange format: OpenQASM 3

Date: 2025-10-13

## Status

Proposed

## Context

We need interoperability between Qiskit, Cirq, and Braket, and a standard representation for QPU submission.

## Decision

Adopt OpenQASM 3 as both input and output format toward providers. The internal parser will convert QASM3 to a lightweight proprietary Intermediate Representation (IR).

## Consequences

- Avoids dependency on specific SDKs.
- Preserves optimizations before partitioning.
- Simplifies transport to multiple backends.
