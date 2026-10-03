# ADR 001: Kubernetes Version Selection

- Status: Proposed
- Date: 2026-10-03

## Context

The cluster will be built using kubeadm on external Linux VMs. The Kubernetes release must be stable, supportable, and compatible with containerd and the selected Linux distribution.

## Decision

Use a stable, currently supported Kubernetes release pinned to an explicit version. Do not use `latest` or a release that is not validated against the host environment.

## Alternatives considered

- latest upstream release
- unpinned short-term release
- a pre-release or unsupported version

## Reason

Version pinning reduces drift, avoids breaking changes, and keeps the build reproducible. The decision must be validated against the host OS and containerd/CRI compatibility before bootstrap.

## Consequences

- additional compatibility review is required before installation
- upgrades must follow a structured process
- future control-plane and worker node upgrades must remain version-aware

## Open question

The definitive version will be chosen only after confirming the actual Linux distribution, containerd package source, and supported Kubernetes release matrix for the target VMs.
