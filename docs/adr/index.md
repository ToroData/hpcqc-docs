# ADR Index

This section collects all the Architecture Decision Records (ADRs) that define the rationale, trade-offs, and final choices made during the design of the hybrid HPCQC software stack.

Each ADR follows the [Michael Nygard pattern](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions), represents a temporal and transparent record of the specific decisions made. Together, they ensure the long-term traceability and reproducibility of architectural reasoning.

## Core Architecture Decisions

- [1. Record architecture decisions](0001-record-architecture-decisions.md)
- [2. Product: Hybrid HPCQC middleware and runtime](0002-hybrid-hpc-qc-middleware-and-runtime-product.md)
- [3. Base language and toolchain: C++23 + MPI + CUDA](0003-base-language-and-toolchain-c-23-mpi-cuda.md)
- [4. Quantum exchange format: OpenQASM 3](0004-quantum-exchange-format-openqasm-3.md)
- [5. QASM3 parser with ANTLR4 in C++](0005-qasm3-parser-with-antlr4-in-c.md)
- [6. Internal IR: space–time DAG with annotations](0006-internal-ir-space-time-dag-with-annotations.md)
- [7. Partition policy: wire cuts and time cuts](0007-partition-policy-wire-cuts-and-time-cuts.md)

## Modeling and Scheduling

- [8. Cost and fidelity model](0008-cost-and-fidelity-model.md)
- [9. Malleable HEFT scheduler](0009-malleable-heft-scheduler.md)
- [14. RMS integration: Slurm, HyperQueue, PBS](0014-rms-integration-slurm-hyperqueue-pbs.md)

## Runtime and Execution Layer

- [10. QPU transport and backends: REST gRPC](0010-qpu-transport-and-backends-rest-grpc.md)
- [11. Tensor contraction stitching: cuBLAS and cuTensorNet](0011-tensor-contraction-stitching-cublas-and-cutensornet.md)
- [12. Storage and checkpointing: HDF5 with MPI-IO](0012-storage-and-checkpointing-hdf5-with-mpi-io.md)
- [15. Python bindings with pybind11](0015-python-bindings-with-pybind11.md)

## Observability, Data, and Security

- [13. Observability: logging, metrics, and profiling](0013-observability-logging-metrics-and-profiling.md)
- [19. QPU credential security and management](0019-qpu-credential-security-and-management.md)
- [24. Structured JSONL logs and wave IDs](0024-structured-jsonl-logs-and-wave-ids.md)

## Deployment and Portability

- [16. No Chapel, Charm++, or UPC in core](0016-no-chapel-charm-or-upc-in-core.md)
- [17. NCCL for multi-GPU intra-node](0017-nccl-for-multi-gpu-intra-node.md)
- [18. Global Arrays or OpenSHMEM as optional](0018-global-arrays-or-openshmem-as-optional.md)
- [20. Containers and reproducibility with Apptainer](0020-containers-and-reproducibility-with-apptainer.md)

## Validation and Configuration

- [21. Benchmark selection: $N_2$ and metrics](0021-benchmark-selection-n2-and-metrics.md)
- [22. QPU cloud usage limits](0022-qpu-cloud-usage-limits.md)
- [23. Configuration and contracts in YAML](0023-configuration-and-contracts-in-yaml.md)
