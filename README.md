# Kubernetes Cluster with Ansible and kubeadm

## Status

This repository provisions a Kubernetes cluster with Ansible and kubeadm. The tested initial topology has one control-plane node and two workers, using containerd and Calico.

## Protect Environment-Specific Data

The tracked inventory at `ansible/inventory/production/hosts.yml` is a sanitized example and uses non-routable `.invalid` hostnames. Do not put real hostnames, IP addresses, usernames, private-key paths, or credentials in tracked files.

Keep the real inventory in `ansible/inventory/production/hosts.local.yml`. This local file is ignored by Git. Keep SSH private keys outside the repository; `.ssh/` and common key file extensions are also ignored.

## Run the Playbook

From the `ansible` directory, use the local inventory:

```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook \
	-i inventory/production/hosts.local.yml \
	playbooks/site.yml
```

The local inventory should define the actual control-plane and worker hosts, SSH user, and private-key path for your environment. Never use the sanitized tracked inventory to provision hosts.

## Project Layout

- `ansible/`: inventory, playbooks, and provisioning roles
- `kubernetes/kubeadm/`: kubeadm configuration examples
- `docs/`: architecture, prerequisites, and design decisions

Review [the infrastructure requirements](docs/infrastructure.md), [the prerequisites](docs/prerequisites.md), and the decisions under `docs/decisions/` before adapting the project to another environment.
