# C4 Level 3 — Component View: Runtime

Breakdown of the execution runtime and its data plane.

## Relevant ADRs

[3. Base language and toolchain: C++17 + MPI + CUDA](../adr/0003-base-language-and-toolchain-c-23-mpi-cuda.md)  
[10. QPU transport and backends: REST gRPC](../adr/0010-qpu-transport-and-backends-rest-grpc.md)  
[11. Tensor contraction stitching: cuBLAS and cuTensorNet](../adr/0011-tensor-contraction-stitching-cublas-and-cutensornet.md)  
[12. Storage and checkpointing: HDF5 with MPI-IO](../adr/0012-storage-and-checkpointing-hdf5-with-mpi-io.md)  
[17. NCCL for multi-GPU intra-node](../adr/0017-nccl-for-multi-gpu-intra-node.md)

```mermaid
%%{init: {'layout': 'elk', 'theme': 'neutral', 'flowchart': {'useMaxWidth': true}}}%%
flowchart TB
  subgraph RT[Runtime]
    API[API C++ submit collect]
    QUEUE[Task DAG Queue]
    TX[QPU Transport REST gRPC]
    DMA[Data Plane buffers pinned]
    CKPT[Checkpoint HDF5]
  end

  subgraph HPC[HPC Exec]
    MPIC[MPI World and Teams]
    OMP[OpenMP OmpSs 2]
    CUDA[CUDA Kernels]
    CUBLAS[cuBLAS]
    CUTN[cuTensorNet]
    NCCL[NCCL Collectives]
  end

  subgraph QExec[Quantum Exec]
    QPU[QPU Cloud]
    SIM[Simulators cuQuantum Aer]
  end

  API --> QUEUE
  QUEUE --> TX
  QUEUE --> MPIC
  DMA --> CUDA
  CUDA --> CUBLAS
  CUDA --> CUTN
  CUTN --> NCCL
  MPIC --> CUTN
  CUTN --> CKPT
  TX --> QPU
  API --> SIM
  SIM --> DMA
  QPU --> DMA
  CKPT --> API
```

## Responsibilities

- API exposes submit and collect.
- Task DAG Queue maintains dependencies.
- Data Plane manages shots and tensors with pinned buffers.
- cuTensorNet performs stitching and uses NCCL for collectives.
