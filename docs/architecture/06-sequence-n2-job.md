# C4 Scenario — $N_2$ Job Sequence

High-level sequence for a simulation job of the $N_2$ molecule from submission to reconstruction.

## Relevant ADRs

[6. Internal IR: space–time DAG with annotations](../adr/0006-internal-ir-space-time-dag-with-annotations.md)  
[7. Partition policy: wire cuts and time cuts](../adr/0007-partition-policy-wire-cuts-and-time-cuts.md)  
[9. Malleable HEFT scheduler](../adr/0009-malleable-heft-scheduler.md)  
[11. Tensor contraction stitching: cuBLAS and cuTensorNet](../adr/0011-tensor-contraction-stitching-cublas-and-cutensornet.md)  
[13. Observability: logging, metrics, and profiling](../adr/0013-observability-logging-metrics-and-profiling.md)

```mermaid
%%{init: {'layout': 'elk', 'theme': 'neutral', 'flowchart': {'useMaxWidth': true}}}%%
sequenceDiagram
  autonumber
  participant User as User
  participant CLI as CLI
  participant Parser as QASM3 Parser
  participant IR as IR Manager
  participant Part as Partitioner
  participant Plan as HEFT Scheduler
  participant RT as Runtime
  participant MPI as MPI Teams
  participant CUTN as cuTensorNet
  participant QPU as QPU Cloud
  participant SIM as Simulator
  participant HDF5 as HDF5 Store
  participant OBS as Observability O2 O3

  User->>CLI: submit $N_2$ job with QASM3 and YAML
  CLI->>Parser: validate and normalize
  Parser->>IR: build space time DAG with metadata
  IR->>Part: low correlation bipartitions and time layers
  Part->>Plan: subcircuits with M1 cost and M2 fidelity bounds
  Plan->>RT: wave plan and team sizes
  RT->>MPI: create dynamic teams
  par classical wave
    RT->>MPI: launch classical subcircuits
    MPI->>CUTN: tensor kernels
    CUTN->>HDF5: partial results and checkpoints
  and quantum wave
    RT->>QPU: send QASM3 fragments
    QPU->>RT: bitstrings and calib data
    RT->>HDF5: persist shots
  end
  RT->>CUTN: stitching contraction
  CUTN->>RT: observables and rho
  RT->>OBS: metrics and traces
  RT->>CLI: final results and artifacts
```

## Results

- Observables and fidelity of $N_2$.
- JSONL traces and O2 O3 profiles.
- Reproducible HDF5 checkpoints.
