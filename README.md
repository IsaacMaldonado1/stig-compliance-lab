# STIG Compliance Lab

Hello! This is my STIG Compliance Lab. I'm doing this to learn the tools and processes the DoD uses to lock down Windows systems. For the lab I'm hardening a small Windows domain to DISA STIGs, the DoD's security configuration standards. First I ran a baseline scan on everything with SCAP Compliance Checker (SCC), then rescanned after applying DISA's GPOs. Currently, I'm fixing the issues the compliance checker flagged to get the systems up to DoD standards. My final objective is to scan with Nessus and then use Kali to test whether I hardened the machines correctly. This lab builds on my [Active Directory homelab](https://github.com/IsaacMaldonado1/active-directory-homelab).

## Setup

Three VMs on my ThinkPad (Ubuntu, QEMU/KVM): a Windows Server 2025 domain
controller, a Windows 11 workstation, and Kali for scanning.

## Results

| Benchmark | Before | After |
|---|---|---|
| Windows 11 STIG | 37.6% | 92.98% |
| Defender (both machines) | 26.87% | 95.52% |
| Firewall (both machines) | 15% | 100% |
| Windows Server 2025 STIG | 41.08% | not rescanned yet |

## Write-ups

1. [Lab environment](documentation/01-lab-environment.md)
2. [Baseline scan](documentation/02-baseline-scan.md)
3. [STIG hardening](documentation/03-stig-hardening.md)
4. [Rescan results](documentation/04-rescan-results.md)
5. [Lessons learned](documentation/05-lessons-learned.md)
