# RFC-07: Deployment and Operations on HPCQC Systems

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#20 Containers and Reproducibility](../adr/0020-containers-and-reproducibility-with-apptainer.md)  
[#14 RMS Integration](../adr/0014-rms-integration-slurm-hyperqueue-pbs.md)

---

## Motivation

To ensure reproducibility and operability within the HPC cluster, deployment, and operational processes must be standardized.

## Deployment Architecture

- Containerized runtime built with Apptainer SIF images.
- Modules managed through LMod.
- Continuous integration via GitLab Runner on a staging node.
- RMS backends: Slurm primary, HyperQueue/PBS optional.

## Build Pipeline

1. Compile with `CMake` and `NVCC 12`.
2. Run unit tests under `ctest`.
3. Package SIF image with checksum and signature.
4. Publish to internal registry `hpc-registry.local/quantum/`.

## Job Submission Example

```bash
srun --mpi=pmix -N4 -G4 apptainer exec qc_runtime.sif ./hybrid_job.yaml
```

## Monitoring & Alerts

- Logs streamed to `Elastic` via JSONL collector.
- Node energy metrics integrated with HPC telemetry bus.
- Alert thresholds: job stall > 5 min, QPU latency $> 2 \, \times$ median.

## Acceptance Criteria

- Build reproducible from commit hash.
- End-to-end deployment < 30 min.
- All jobs traceable by unique wave ID.
