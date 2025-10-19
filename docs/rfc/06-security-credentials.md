# RFC-06: QPU Credential Security and Threat Model

Date: 2025-10-18  
Status: Proposed  
Owner: Ricard Santiago Raigada García

## ADR Links

[#19 QPU Credential Security](../adr/0019-qpu-credential-security-and-management.md)  
[#20 Containers and Reproducibility](../adr/0020-containers-and-reproducibility-with-apptainer.md)

## Motivation

Access to QPU cloud providers requires authentication tokens. These credentials must remain isolated from MPI processes and logs
while ensuring usability for automated runs.

## Threat Model

| Asset | Threat | Mitigation |
|--------|---------|------------|
| QPU API tokens | Exposure via logs | Redact before persistence |
| Network calls | MITM attack | TLS 1.3, pinned certs |
| Container image | Tampering | Signed Apptainer SIF |
| Host filesystem | Token leakage | Read-only mount, ephemeral store |

## Design

- Secrets mounted in `/run/secrets/qpu/` inside container, mode 0400.
- Each MPI rank uses helper daemon to request token via Unix socket.
- Tokens valid ≤ 15 min; refreshed via short-lived service account.
- No environment variables with secrets.
- Logging subsystem filters `Authorization` headers automatically.

## Risks

- Token refresh failures may abort long runs.
- Need coordination with RMS when re-launching container.

## Acceptance Criteria

- No credentials present in any HDF5 or JSONL artifacts.
- Successful automated refresh in ≥ 99 % of sessions.
- Zero open findings in periodic container scan.
