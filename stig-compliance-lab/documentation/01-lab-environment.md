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

My internal drive was 95% full (15 GB free), which was not enough room for the VMs, snapshots, and scan tooling. All I had was a HDD that I pulled out of an old computer. Originally I moved both onto the HDD and found out quick just how much of a mistake that was. With both running, it became virtually impossible to use them. Decided to move the server to my host machine and kept windows 11 on the HDD. Also got a HDD enclosure to protect the exposed drive. 

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
| RAM / vCPU | TBD |
| IP address | TBD |
| Evaluation days remaining | TBD (`slmgr /dlv`) |

### WIN11

| Item | Detail |
|---|---|
| OS | Windows 11 Enterprise Evaluation, version 26H2 |
| Role | Domain-joined client workstation |
| Firmware | UEFI with Secure Boot |
| TPM | Emulated TPM 2.0 (`tpm-crb`) |
| RAM | 8 GB |
| IP address | TBD |

### Kali (scanner)

Kali stays on the host's internal drive and will run the scanning tools. 

## Network

| Item | Detail |
|---|---|
| Virtual network | TBD |
| Subnet | TBD |
| Domain | `johnson.local` |

## Session Routine

**Start:** plug in the drive, `sudo mount /mnt/vmlab`, start Server-DC01, wait 3–5 minutes for AD and DNS, then start WIN11.

**Stop:** shut down WIN11, then Server-DC01, confirm both are off with `sudo virsh list --all`, then `sudo umount /mnt/vmlab` before unplugging.

## Screenshots

*Add screenshots to `screenshots/01-lab-environment/` and link them here.*
