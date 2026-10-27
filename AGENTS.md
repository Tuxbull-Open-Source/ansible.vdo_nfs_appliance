# Repository instructions

This repository provides the reusable `tuxbull.vdo_nfs_appliance` role.

## Safety

The role can create VDO storage and format XFS. Test only against an explicitly
identified, disposable blank data disk. Never use an OS disk, a mounted device,
or a disk with partitions/filesystem signatures. Keep inventories, generated
lab credentials, logs, and real NFS client networks outside this repository.

## Supported platform

The maintained target is RHEL-family 10. Controller collections are declared in
`collections/requirements.yml` and must be installed before validation.

## Validation

Run YAML parsing, a syntax check through a role harness, `git diff --check`, and
an explicitly authorized lab test using a disposable target with a separate
blank backing disk. Verify the VDO mapping, XFS mount, NFS export, firewalld,
service state, and a second no-change converge. Destroy or reset the disposable
lab afterward.

## Publication

`README.md` documents use; `CHANGELOG.md` records release history. GitHub source
is `Tuxbull-Open-Source/ansible.vdo_nfs_appliance`; Galaxy FQN is
`tuxbull.vdo_nfs_appliance`. Do not self-merge. After review/merge, create an
immutable three-component SemVer tag and published GitHub Release, then import
and verify unpinned and version-pinned Galaxy installations.
