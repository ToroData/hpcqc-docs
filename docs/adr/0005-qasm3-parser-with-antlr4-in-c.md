# 5. QASM3 parser with ANTLR4 in C++

Date: 2025-10-13

## Status

Proposed

## Context

The runtime must transform QASM3 into an internal IR for analysis and partitioning.

## Decision

Implement a QASM3 parser in C++ using ANTLR4, generating an abstract syntax tree (AST) and a space–time DAG with annotations.

## Consequences

- Robust and extensible parser.
- Adds ANTLR4 dependency to the toolchain.
