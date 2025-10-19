# 20. Containers and reproducibility with Apptainer

Date: 2025-10-13

## Status

Proposed

## Context

Reproducibility is required across clusters and lab environments.

## Decision

Distribute binaries and dependencies in Apptainer containers with signed hashes, integrating LMod modules and center toolchains.

## Consequences

- Portability and reproducibility ensured.
- Requires recipes and build pipeline in CI.
