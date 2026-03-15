# n2solutions.homelab

Ansible collection for homelab patch management and maintenance.

## Roles

| Role | Target | Description |
|------|--------|-------------|
| `patch_ubuntu` | Ubuntu/Debian hosts | APT updates with optional k3s drain/uncordon and conditional reboot |
| `patch_proxmox` | Proxmox VE hosts | APT dist-upgrade with VM safety checks and conditional reboot |
| `patch_pihole` | Pi-hole hosts | Pi-hole software update + gravity refresh, delegates OS patches to `patch_ubuntu` |
| `patch_macos` | macOS hosts | System software updates + Homebrew upgrades (planned) |
| `patch_unifi` | UniFi devices | Controller API firmware upgrades (planned) |

## Installation

```bash
ansible-galaxy collection install n2solutions.homelab
```

Or from source:

```bash
ansible-galaxy collection install git+https://github.com/n2solutionsio/ansible-collection-homelab.git
```

## Usage

```yaml
- hosts: k3s_nodes
  become: true
  roles:
    - role: n2solutions.homelab.patch_ubuntu
      vars:
        patch_ubuntu_reboot: true
        patch_ubuntu_drain_k3s: true
```

## Playbooks

The collection includes a `patch_all.yml` playbook that orchestrates patching across all device types with proper ordering and rolling updates.

```bash
ansible-playbook n2solutions.homelab.patch_all -i inventory.ini
```

## Requirements

- Ansible >= 2.15
- Target hosts accessible via SSH (or local connection for macOS)
- `become: true` for package management operations

## License

MIT
