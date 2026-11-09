# 01 – Lab Environment

This section covers the hardware, virtualization setup, and storage changes made before any scanning or hardening began.

## Host

| Item | Detail |
|---|---|
| Laptop | Lenovo ThinkPad T14 Gen 1 (AMD) |
| CPU | AMD Ryzen 5 PRO 4650U (6 cores / 12 threads) |
| RAM | 22 GB |
| Host OS | Ubuntu Linux |
| Hypervisor | QEMU/KVM, managed with virt-manager and `virsh` |

## Lab Storage

The VMs originally ran off an old 1 TB HDD over USB, but it was too slow to use with both running. I cleaned up space and moved all VMs back to the host's internal drive. The HDD is now just for backups.

| Item | Detail |
|---|---|
| Drive | 1 TB HDD (Toshiba MQ01ABD100) via USB-to-SATA adapter |
| Filesystem | ext4, label `vmlab` |
| Mount point | `/mnt/vmlab` (mounted by UUID in `/etc/fstab`) |
| Mount options | `defaults,nofail,x-systemd.device-timeout=10s` so the host boots normally when the drive is unplugged |
| Layout | `/mnt/vmlab/images` (VM disks), `/mnt/vmlab/iso` (installers) |

### Migration steps

1. Shut down both Windows VMs cleanly (the DC was in a saved state and was resumed and shut down from inside Windows first).
2. Deleted two old internal snapshots on Server-DC01. They stored the old disk path and would have broken after the move.
3. Copied the disks with `qemu-img convert`, which also compacted them (52 GB to 44 GB), and verified each copy with `qemu-img check`.
4. Pointed each VM at its new disk with `virt-xml` and detached the installer ISOs.
5. Fixed a "Permission denied" error on first boot: the copied disks were owned by `root`, so they were changed to `libvirt-qemu:kvm` with mode `600`.
6. Test-booted Server-DC01 from the new drive, then removed the old copies from the host (host free space went from 15 GB to 71 GB).

## Virtual Machines

### Server-DC01

| Item | Detail |
|---|---|
| OS | Windows Server 2025 Evaluation |
| Role | Domain controller and DNS for `johnson.local` |
| Firmware | BIOS (Q35 chipset) |

### WIN11

| Item | Detail |
|---|---|
| OS | Windows 11 Enterprise Evaluation, version 26H2 |
| Role | Domain-joined client workstation |
| Firmware | UEFI with Secure Boot |
| TPM | Emulated TPM 2.0 (`tpm-crb`) |
| RAM | 8 GB |

### Kali (scanner)

Kali stays on the host's internal drive and will run the scanning tools. 

## Network

| Item | Detail |
|---|---|
| Domain | `johnson.local` |
