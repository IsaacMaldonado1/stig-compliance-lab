# 01 – Lab Environment

Everything runs as VMs on my ThinkPad T14 (Ryzen 5 PRO 4650U, 22 GB RAM, Ubuntu)
using QEMU/KVM and virt-manager.

| Machine | Role | OS |
|---|---|---|
| Server-DC01 | Domain controller + DNS for johnson.local | Windows Server 2025 Evaluation |
| WIN11 | Domain-joined workstation (UEFI, Secure Boot, emulated TPM 2.0, 8 GB RAM) | Windows 11 Enterprise Evaluation 26H2 |
| Kali | Runs the scanning tools, not part of the assessed system | Kali Linux 2026.2 |

## Storage

My internal drive was almost full, so I first moved the VMs onto an old 1 TB HDD
over USB. That was a mistake. With both VMs running it was barely usable, and the
WIN11 baseline scan took over an hour. I cleaned up space on the laptop and moved
everything back to the internal drive. The HDD is just for backups now.
