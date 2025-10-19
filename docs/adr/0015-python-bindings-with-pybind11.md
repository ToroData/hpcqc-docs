# 15. Python bindings with pybind11

Date: 2025-10-13

## Status

Proposed

## Context

Researchers and users need a fast scripting and notebook interface.

## Decision

Expose bindings with pybind11 over the C++ runtime API, limiting Python usage to the edge and avoiding hot data paths.

## Consequences

- Easy adoption without penalizing data-plane performance.
- Requires maintaining wrapper layers.
