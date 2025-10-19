# 23. Configuration and contracts in YAML

Date: 2025-10-13

## Status

Proposed

## Context

Resources, limits, and policies must be parameterized per job reproducibly.

## Decision

Use YAML to describe resources, QPU windows, scheduling policies, fidelity limits, and CPU–GPU affinity. Version YAML files along with IR and results.

## Consequences

- Execution traceability.
- Requires validators and schema definitions.
