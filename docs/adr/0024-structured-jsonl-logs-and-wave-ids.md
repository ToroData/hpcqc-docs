# 24. Structured JSONL logs and wave IDs

Date: 2025-10-13

## Status

Proposed

## Context

Post-mortem analysis and auditing require machine-readable traces.

## Decision

Emit JSONL logs with wave and subcircuit IDs, timestamps, latencies, and GPU/MPI counters. Store indexes for fast search.

## Consequences

- Production-level observability.
- Additional disk space for trace data.
