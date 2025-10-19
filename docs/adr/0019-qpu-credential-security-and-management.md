# 19. QPU credential security and management

Date: 2025-10-13

## Status

Proposed

## Context

Access to cloud QPU providers requires secure tokens and credentials.

## Decision

Keep credentials outside the MPI domain in an auxiliary process or in the Apptainer container secret store. Use read-only mounts and scheduled rotation.

## Consequences

- Reduced exposure surface.
- Additional bootstrap and renewal logic.
