# Ansible VDO NFS appliance role

Create a guarded VDO-backed XFS volume and export a directory over NFS on
Enterprise Linux 10. The role can optionally install Cockpit storage tooling.

## Destructive-operation warning

The role creates a VDO volume and an XFS filesystem. It requires a dedicated,
blank, unpartitioned, unmounted whole disk. It rejects common OS-disk names and
checks the requested device before making changes. Never point `vdoPhyDev` at a
system disk or a disk containing data.

## Requirements

- Ansible 2.15 or later.
- RHEL-family 10 target.
- A dedicated blank backing disk; at least 50 GB physical capacity is recommended.
- Required collections:

  ```bash
  ansible-galaxy collection install -r collections/requirements.yml
  ```

## Important variables

| Variable | Default | Purpose |
| --- | --- | --- |
| `vdoPhyDev` | `vdb` | Bare name of the dedicated backing disk. |
| `vdoLogicalSize` | `2T` | Logical VDO capacity; thin provisioning applies. |
| `vdoDev` | `store-{{ vdoPhyDev }}` | VDO device name. |
| `vdoMountDir` | `/srv/{{ vdoDev }}` | XFS mount point. |
| `vdoNfsDir` | `{{ vdoMountDir }}/nfs` | Exported NFS directory. |
| `nfsWriteIps` | `127.0.0.1` | Comma-separated writable NFS clients. |
| `nfsReadIps` | `127.0.0.2` | Comma-separated read-only NFS clients. |
| `installCockpit` | `true` | Install and enable `cockpit.socket`. |

Review NFS client addresses and export options before production use. The
default options are intended only as a lab-safe example.

## Example playbook

```yaml
---
- name: Build VDO NFS appliance
  hosts: storage
  become: true
  roles:
    - role: tuxbull.vdo_nfs_appliance
      vars:
        vdoPhyDev: vdb
        vdoLogicalSize: 500G
        nfsWriteIps: 192.0.2.10
        nfsReadIps: 192.0.2.11
```

## Operations and limitations

The role manages VDO, XFS mounting, NFS exports, firewalld NFS access, and
optional Cockpit. It does not configure backup, restore, monitoring, HA, NFSv4
identity mapping, or client mounts. Test backup and recovery independently.

## License

[GPL-3.0-only](https://www.gnu.org/licenses/gpl-3.0.html)
