# STIG Compliance Lab

I'm hardening a small Windows domain to DoD standards (DISA STIGs) and documenting it the way a defense sysadmin or ISSO would. I scanned it before making any changes, I'm applying the STIG settings through Group Policy, and then I'll scan again to compare. At the end I'm writing a mock System Security Plan (SSP) and POA&M based on NIST 800-53.

This builds on my [Active Directory homelab](https://github.com/IsaacMaldonado1/active-directory-homelab). Everything here is a lab with fictional accounts, not a real system.

## Lab setup

| Machine | Role | OS |
|---|---|---|
| Server-DC01 | Domain controller + DNS for johnson.local | Windows Server 2025 Standard Evaluation |
| WIN11 | Domain-joined workstation | Windows 11 Enterprise Evaluation (26H2) |
| Kali | Will run Nessus (not part of the assessed system) | Kali Linux 2026.2 |

All three run as VMs on my ThinkPad (Ubuntu, QEMU/KVM, virt-manager).

## Tools

| Tool | Version | What I use it for |
|---|---|---|
| SCAP Compliance Checker (SCC) | 5.15 | Scanning against the STIGs |
| QEMU/KVM + virt-manager | | Running the VMs |
| qemu-img | | Copying, compacting, and checking VM disks |
| Group Policy Management | | Applying STIG settings (in progress) |
| Nessus Essentials | | Vulnerability scanning (planned) |

## Results

| Benchmark | Before | After |
|---|---|---|
| Windows Server 2025 STIG | 41.08% | |
| Server – Defender STIG | 26.87% | |
| Server – Firewall STIG | 15% | |
| Windows 11 STIG | 37.6% | |
| WIN11 – Defender STIG | 26.87% | |
| WIN11 – Firewall STIG | 15% | |

## Write-ups

1. [Lab environment](documentation/01-lab-environment.md)
2. [Baseline scan](documentation/02-baseline-scan.md)
3. [STIG hardening](documentation/03-stig-hardening.md)
4. [Rescan results](documentation/04-rescan-results.md)
5. [Lessons learned](documentation/05-lessons-learned.md)
