# ADR 002: Container Runtime

- Status: Proposed
- Date: 2026-10-03

## Context

The cluster must use a supported CRI runtime for Kubernetes, and the runtime must be deployed with production-oriented defaults.

## Decision

Use containerd as the runtime for the initial implementation.

## Alternatives considered

- Docker Engine directly
- containerd with minimal configuration
- a non-supported runtime for test or lab use

## Reason

containerd is the Kubernetes-standard runtime and is the best fit for kubeadm-based clusters. It aligns with current best practices and is systemd-friendly when configured properly.

## Consequences

- a validated containerd configuration must be created
- `crictl` validation is required
- the runtime configuration must be version-pinned and documented

## Open question

The exact containerd version and systemd cgroup settings will be confirmed after the target VM kernel and distro review.
