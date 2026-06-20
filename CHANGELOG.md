# Changelog

All notable changes to the `n2solutions.homelab` Ansible collection are documented in this file.

## 1.1.0

### Added

- New `k3s_worker_reboot` role: rolling reboot of k3s worker nodes to recover from
  accumulated containerd / kubelet runtime state. Per-worker: cordon → drain (with
  force-delete fallback for stuck-Terminating pods) → reboot → wait Ready → uncordon
  → verify no unhealthy daemonset pods.
- New `playbooks/reboot_k3s_workers.yml`: `serial: 1` orchestration over the
  `k3s_workers` inventory group.

### Changed

- `galaxy.yml`: added `infrastructure`, `linux`, `tools` to satisfy ansible-lint's
  `galaxy[tags]` rule (one of these is required for collection certification).
- Renamed registered variables in molecule verify playbooks to use the role prefix
  (`patch_pihole_bin`, `patch_proxmox_apt_cache`, `patch_ubuntu_apt_cache`) so
  they comply with ansible-lint's `var-naming[no-role-prefix]` rule.
- Cosmetic: capitalize "MacOS" in the `patch_macos` placeholder task name to
  satisfy ansible-lint's `name[casing]` rule.

## 1.0.0

Initial release: `patch_ubuntu`, `patch_proxmox`, `patch_pihole`, `patch_unifi`,
`patch_macos` (stub) roles and `patch_all.yml` orchestrator playbook.
