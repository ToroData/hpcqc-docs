# 10. QPU transport and backends: REST gRPC

Date: 2025-10-13

## Status

Proposed

## Context

Interaction with IBM Runtime, Braket, and IonQ requires remote calls and session/credential management.

## Decision

Use REST gRPC as the transport channel from the runtime to providers, with a backend-specific adapter and token management outside the MPI domain. REST gRPC is chosen to reduce latency at the risk of a tightly coupled service.

## Consequences

- Improved security through credential isolation.
- Requires provider-specific adaptation layer.
