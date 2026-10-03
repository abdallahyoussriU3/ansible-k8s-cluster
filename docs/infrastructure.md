# Infrastructure Discovery Checklist

This document defines the required data that must be collected from the Namecheap VMs before any cluster bootstrap begins.

## Required inventory

| Category      | Required information                  | Why it matters                                       |
| ------------- | ------------------------------------- | ---------------------------------------------------- |
| VM count      | Number of nodes and roles             | Determines bootstrap topology                        |
| OS            | Linux distribution and version        | Affects package repos and kubeadm compatibility      |
| CPU           | Core count and model                  | Affects workload density and control-plane sizing    |
| Memory        | Per-node RAM                          | Determines whether HA and observability are feasible |
| Disk          | Root disk size and layout             | Affects etcd, containerd, and local storage planning |
| Network       | Public IPs, private IPs, subnets      | Needed for firewall and networking design            |
| Routing       | Default gateway and routes            | Required for correct control-plane and pod traffic   |
| Firewall      | Host firewall policy and capabilities | Determines allowed ports and trust boundaries        |
| DNS           | Internal/external DNS configuration   | Needed for node naming and future ingress            |
| Load balancer | VIP or managed LB availability        | Affects multi-control-plane design                   |
| Storage       | Available block devices or partitions | Needed for local PVs, etcd, or future CSI            |
| Access        | User accounts and SSH policy          | Required for secure provisioning                     |

## Minimum validation commands to run on each host

```bash
uname -a
cat /etc/os-release
lsblk
free -h
ip addr
ip route
ss -tulpn
systemctl list-unit-files --type=service | grep -E 'firewalld|ufw|sshd'
```

## Specific questions to answer before approval

1. Are the VMs public-facing or behind additional network controls?
2. Can nodes communicate directly over private IPs?
3. Is there any existing internal subnet or VPN overlap with common Kubernetes CIDRs?
4. Are we allowed to expose only the Kubernetes API and ingress traffic intentionally?
5. Do we have a stable VIP or must we rely on direct node addresses initially?
6. Is the cluster intended for learning only or for future operational workloads?

## Assumptions to document explicitly

- no AWS-like managed networking should be assumed
- no floating IP or load balancer should be assumed unless confirmed
- no private-network topology should be assumed unless tested
- no production-like HA should be implemented unless capacity and networking justify it

## Risk register

- unexpected network restrictions may change the chosen CNI and firewall approach
- insufficient memory may force a more minimal bootstrap and delayed observability stack
- insufficient disk may make local storage or etcd expansion more complex
- a single control plane remains the safest initial choice unless infrastructure supports HA

## Outcome of this phase

The project continues only when the actual infrastructure inventory is captured and reviewed. Until that is complete, the design remains provisional.
