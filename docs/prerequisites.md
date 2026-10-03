# Prerequisites and Discovery Requirements

## Infrastructure discovery required before implementation

The project must establish the following facts before the first OS or Kubernetes change:

- the exact VM inventory
- public and private network details
- Linux distribution and kernel version
- resource sizing and disk layout
- network restrictions and firewall rules
- DNS and service exposure constraints
- the existence of any load-balancing or VIP features

## Operating system constraints

The OS choice must be compatible with the current stable kubeadm-supported Kubernetes release and containerd. The selected distribution will be validated before being adopted.

## Kubernetes compatibility gate

Before installation, the following must be checked:

- kubeadm version compatibility
- kubelet and kubectl version pinning
- containerd compatibility
- CNI support and NetworkPolicy capabilities
- Linux kernel support
- required sysctl and module settings

## Security gate

No service or network exposure should be enabled before validating the actual network model. The project must keep the attack surface limited to the exact ports needed for administration, Kubernetes control-plane traffic, pod traffic, and intentionally public application traffic.

## Implementation gate

The project may proceed to Phase 2 only after:

1. infrastructure inventory is collected
2. design is reviewed
3. required risks are documented
4. architecture remains approved
5. no server changes are made without explicit approval

## Current status

This project is intentionally paused at the discovery and design stage. It is not yet approved for machine-level changes.
