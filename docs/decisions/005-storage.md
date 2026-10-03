# ADR 005: Storage Architecture

- Status: Proposed
- Date: 2026-10-03

## Context

The cluster must include a storage strategy that is clear, maintainable, and compatible with future stateful workloads.

## Decision

Use the simplest reliable storage design compatible with the environment and document that this is initial infrastructure, not a long-term production storage platform by default.

## Alternatives considered

- local ephemeral storage only
- local persistent volumes without dynamic provisioning
- NFS-based CSI
- Longhorn
- Rook/Ceph
- cloud-backed block storage

## Reason

The actual VM resources and disk topology determine whether local PVs, shared storage, or external storage are feasible. The initial design should avoid overcommitting to a storage platform before the infrastructure is evaluated.

## Consequences

- database and stateful workloads will be constrained by the selected storage model
- the storage layer is likely to evolve in later phases
- backups and DR planning are mandatory for any persistent workload

## Open question

The selected storage approach depends on the actual node disks, volume layout, and desired resilience profile.
