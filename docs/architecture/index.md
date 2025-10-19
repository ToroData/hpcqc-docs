# Architecture Views Index

This section presents the C4 model architecture views of the hybrid HPCQC stack. Each level refines the system from high-level context to detailed components, deployment topology, and execution scenarios. These diagrams correspond to the software stack layer of the research project —the runtime and middleware that enable practical realization of space–time circuit knitting.

## C4 Model Overview

| Level | View | Description |
|--------|------|--------------|
| **L1** | [System Context](01-system-context.md) | Defines the system boundaries, users, and external services (RMS, QPU cloud). |
| **L2** | [Container View](02-container.md) | Shows the main software containers: frontends, middleware, runtime, backends, observability. |
| **L3-A** | [Component View: Middleware](03-components-middleware.md) | Detailed view of IR manager, partitioner, models, and scheduler. |
| **L3-B** | [Component View: Runtime](04-components-runtime.md) | Internal structure of the hybrid runtime and tensor data plane. |
| **L2′** | [Deployment View](05-deployment.md) | Typical deployment on HPC clusters (CPU/GPU nodes, RMS, QPU cloud). |
| **Scenario** | [N₂ Job Sequence](06-sequence-n2-job.md) | Sequence diagram of an end-to-end N₂ quantum-chemistry job. |
