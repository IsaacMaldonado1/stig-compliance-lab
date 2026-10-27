# Baseline Scan

## Getting and using SCC
SCC (SCAP Compliance Checker) is a free DoD tool made by NIWC Atlantic. I used it to scan my Windows machines against the DISA STIGs and gave me a compliance score.

Getting the tool was difficult and toook me longer than expected. I first checked NIWC's GitHub, but the releases page was empty. Then I tried DISA's website, and it sent me to a DoD login page that needs a CAC (military ID card). I didn't try to sign in. I was sure that the tool was publicly available as NIWC's SCAP page says it is. I saw that 5.15 is the latest version, but it only had the checksum file, not the installer. I ended up getting the installer from DISA's public download server, which didn't need a login:

https://dl.dod.cyber.mil/wp-content/uploads/stigs/zip/scc-5.15_Windows_bundle.zip

## Checking the installer

## What I scanned against

| Benchmark | Version | Scanned on |
|---|---|---|
| Windows Server 2025 STIG | V1R1 | Server-DC01 |
| Windows 11 STIG | V2R10 | WIN11 |
| Microsoft Defender Antivirus STIG | V2R9 | Both |
| Windows Defender Firewall STIG | V2R3 | Both |

## Results

### Server-DC01 (Oct 26, 2026)

| Benchmark | Score | Pass | Fail | Not checked | Total |
|---|---|---|---|---|---|
| Windows Server 2025 | 41.08% | 99 | 142 | 29 | 291 |
| Defender Antivirus | 26.87% | 18 | 49 | 0 | 67 |
| Windows Firewall | 15% | 3 | 17 | 1 | 21 |

Average: 27.65%

### WIN11 (Oct 26, 2026)

| Benchmark | Score | Pass | Fail | Not checked | Total |
|---|---|---|---|---|---|
| Windows 11 | 37.6% | 91 | 151 | 10 | 257 |
| Defender Antivirus | 26.87% | 18 | 49 | 0 | 67 |
| Windows Firewall | 15% | 3 | 17 | 1 | 21 |

Average: 26.49%

## What I noticed

## Screenshots
