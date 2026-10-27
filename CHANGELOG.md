# Changelog

## v1.0.0 - 2026-10-27

### Changed

- Migrate the role to the `tuxbull.vdo_nfs_appliance` Galaxy identity.
- Align implementation with Rocky Linux 10 and fully qualified Ansible modules.
- Replace unsupported legacy package assumptions with the Rocky 10 `vdo` package.
- Add explicit destructive-device validation before VDO or filesystem creation.
- Manage VDO, XFS mounting, NFS exports, firewalld, and optional Cockpit socket.

### Verified

- Live Rocky Linux 10 lab validation using a dedicated blank 100-GB data disk.
