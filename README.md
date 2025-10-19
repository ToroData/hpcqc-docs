# HPC–QC Hybrid Stack Documentation

[![Docs Build (Release)](https://github.com/ToroData/hpcqc-docs/actions/workflows/deploy-version.yml/badge.svg)](https://github.com/ToroData/hpcqc-docs/actions/workflows/deploy-version.yml) [![Docs](https://img.shields.io/badge/docs-online-blue)](https://torodata.github.io/hpcqc-docs/stable/) [![License](https://img.shields.io/github/license/ToroData/hpcqc-docs?color=blue)](LICENSE)

This repository provides the architectural and design documentation for the Hybrid High-Performance Computing and Quantum Computing (HPCQC) Stack, currently under development as part of a research proposal. Covers the software architecture and runtime design. The documentation defines the conceptual, logical, and technical foundations of a hybrid runtime that integrates classical HPC resources with quantum backends under a unified software stack. It focuses on design rationale, interoperability between ecosystems, and formal reproducibility of hybrid workflows.

Currently, this documentation is in the proposal and design phase —no production implementation yet.

## Website

The documentation is published and versioned using [mike](https://github.com/jimporter/mike) and the site is available at:  
[https://torodata.github.io/hpcqc-docs/stable/](https://torodata.github.io/hpcqc-docs/stable/)  

The version selector in the top right allows navigation among published versions.

## Key Documentation Sections  

- C4 Architecture Views: Multi-level diagrams from system context down to deployment and scenario views.  
- Architecture Decision Records (ADRs): Formalized decisions, each with context, decision, consequences.  
- RFCs: In-depth technical specifications complementing ADRs (e.g., IR format, transport, scheduler).  

## What This Documentation Includes

- Conceptual architecture: high-level vision of the hybrid HPC–QC system and its interfaces.  
- Technical architecture: internal models such as the IR (Intermediate Representation), cost and fidelity models, partitioning heuristics, and runtime orchestration.  
- Operational view: scheduling policies, deployment workflows, monitoring and observability design.  
- Scientific validation: benchmark design for the molecular nitrogen ($N_2$) case study.

## Future Additions

As the project transitions to implementation, this documentation will expand to include:

- SBOM and dependency transparency for all toolchains (C++, MPI, CUDA, pybind11, etc.).  
- RACI matrices defining engineering, QA, and research responsibilities.  
- Testing and CI/CD guides for reproducible deployment on BSC clusters.  
- Release documentation aligned with semantic versioning once artifacts exist.

## Additional Information

- Created by: Ricard Santiago Raigada García
- Advised by: Dr. Sergio Iserte Agut
- Reviewed by: Dr. Sergio Iserte Agut
- Lifecycle: Research design baseline
- Versioning: This documentation is versioned using Mike

> Status: *Research design phase — pre-alpha*
>
> This documentation evolves alongside the research. All diagrams, ADRs, and RFCs are living documents and may change as prototypes and experiments mature.
