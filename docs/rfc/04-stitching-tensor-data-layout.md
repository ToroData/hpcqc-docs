# RFC-04: Tensor Stitching and GPU Data Layout

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#11 Tensor Contraction Stitching](../adr/0011-tensor-contraction-stitching-cublas-and-cutensornet.md)  
[#12 Storage and Checkpointing](../adr/0012-storage-and-checkpointing-hdf5-with-mpi-io.md)  
[#17 NCCL Multi-GPU](../adr/0017-nccl-for-multi-gpu-intra-node.md)

## Motivation

Efficient stitching after circuit cuts depends on tensor layout, GPU memory management, and distributed reductions. We must maximize throughput and numerical stability.

## Scope

Covers data layout, GPU parallelism, checkpointing and recovery. Excludes quantum-algorithm logic.

## Data Layout Policy

- Row-major storage with stride order following qubit index.
- Batched contractions fused when index overlap > 50 %.
- Use half-precision (FP16) when fidelity impact < 1 e-3.
- Pin buffers in unified memory for async GPU transfers.

## GPU Parallelism

- cuTensorNet for contraction planning and execution.
- cuBLAS for small dense blocks.
- NCCL AllReduce for intra-node aggregation.
- MPI Iallreduce for inter-node fusion of boundary tensors.

## Checkpointing

- HDF5 datasets with chunk size = 128 MB; compression gzip 4.
- Metadata group per wave: time, fidelity_est, alpha_beta_gamma.
- Checkpoints restartable and replayable for regression testing.

## Rationale

Explicit data-layout control reduces GPU $\rightarrow$ CPU traffic
and guarantees reproducibility across architectures.

## Risks

- Half-precision accumulation may affect observables > target $\Delta_F$.
- Large tensor graphs may exceed GPU memory; requires slicing.

## Acceptance Criteria

- Stitching throughput $\geq 85 %$ of cuTensorNet theoretical.
- Reconstructed fidelity $F \geq 0.95$ vs monolithic simulation.
- Restart from checkpoint restores state bit-exact within tolerance $1e-6$.
