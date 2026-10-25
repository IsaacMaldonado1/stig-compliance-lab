# STIG Compliance Lab

A small "mini DoD network" built in a homelab to practice the day-to-day work of a defense system administrator / ISSO: hardening Windows systems to **DISA STIGs**, measuring compliance before and after with DoD-style scanning tools, and documenting the results in a mock **NIST 800-53** compliance package (System Security Plan + POA&M).

This lab hardens the Active Directory environment built in [active-directory-homelab](https://github.com/IsaacMaldonado1/active-directory-homelab).

> **Mock / lab use only.** This is an isolated learning environment with fictional accounts. It is not an accredited system, and the compliance package is a training exercise.

---

## Objectives

- Establish a **baseline** STIG compliance score for a Windows domain controller and a Windows client
- Apply DISA STIG settings through **Group Policy** and resolve anything the hardening breaks
- **Rescan** and document the before/after results
- Write a mock **System Security Plan (SSP)** and **Plan of Action & Milestones (POA&M)** mapped to NIST 800-53 controls

## System Boundary

| System | Role | OS |
|---|---|---|
| Server-DC01 | Domain controller, DNS (`johnson.local`) | Windows Server 2025 Evaluation |
| WIN11 | Domain-joined client workstation | Windows 11 Enterprise Evaluation (26H2) |
| Kali | Scanner host (outside the assessed boundary) | Kali Linux |

Network diagram: *TBD*

## Tools

| Tool | Purpose |
|---|---|
| QEMU/KVM + virt-manager | Virtualization on an Ubuntu host |
| DISA STIGs + STIG Viewer | Security requirements and checklists |
| DISA SCAP Compliance Checker (SCC) | Automated STIG compliance scoring |
| Nessus Essentials | Credentialed vulnerability scanning (the DoD's ACAS is built on Nessus) |
| Group Policy Management | Applying STIG settings across the domain |

## Results

| Metric | Before | After |
|---|---|---|
| Server-DC01 SCC score | TBD | TBD |
| WIN11 SCC score | TBD | TBD |
| CAT I findings | TBD | TBD |
| CAT II findings | TBD | TBD |
| CAT III findings | TBD | TBD |
| Nessus critical/high vulnerabilities | TBD | TBD |

## Documentation

1. [Lab environment](documentation/01-lab-environment.md)
2. [Baseline scan](documentation/02-baseline-scan.md)
3. [STIG hardening](documentation/03-stig-hardening.md)
4. [Rescan results](documentation/04-rescan-results.md)
5. [Lessons learned](documentation/05-lessons-learned.md)

## Compliance Package

See [compliance-package](compliance-package/) for the mock SSP and POA&M.

## Repository Layout

```
stig-compliance-lab/
├── README.md
├── documentation/         step-by-step write-ups
├── compliance-package/    SSP and POA&M
├── scan-results/          sanitized SCC and Nessus summaries
└── screenshots/           evidence for each step
```
