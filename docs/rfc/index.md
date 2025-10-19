# RFC Index

This section contains all Request for Comments (RFC) documents that complement and extend the subsystems and protocols of the software stack. Each RFC complements the ADRs by defining how each architectural decision (for example, algorithms or interfaces) is implemented or technically specified.

## Core Specifications

- [RFC-01: IR Specification and Serialization Contract](01-ir-spec.md)
- [RFC-02: Runtime API and YAML Contracts](02-runtime-api.md)

## Execution and Scheduling

- [RFC-03: Malleable HEFT Scheduler and Resizing Rules](03-scheduler-heft-malleability.md)
- [RFC-04: Tensor Stitching and GPU Data Layout](04-stitching-tensor-data-layout.md)

## Observability and Feedback

- [RFC-05: Observability and M₁–M₂ Feedback Loop](05-observability-feedback.md)

## Security and Compliance

- [RFC-06: QPU Credential Security and Threat Model](06-security-credentials.md)

## Deployment and Operations

- [RFC-07: Deployment and Operations on HPC–QC Systems](07-deployment-operations.md)

## Validation and Benchmarking

- [RFC-08: Scientific Validation and Benchmarking ($N_2$ Case)](08-validation-n2-benchmark.md)

## Notes

- RFCs are living documents subject to revision until the prototype phase.
- Each RFC is versioned and cross-referenced to its related ADRs.
- Once implementation begins, additional RFCs will cover:
  - SBOM and dependency traceability
  - CI/CD and testing strategy
  - RACI matrices for engineering governance
