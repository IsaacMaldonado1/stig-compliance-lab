# 03 – STIG Hardening

How the STIG settings were applied and what broke along the way.

## Approach

I used DISA's STIG GPO package (July 2026). I downloaded it from DISA's public download server and checked the SHA-256 hash against the one listed on NIST's National Checklist Program. It matched.

## Version mismatch

Upon downloading the package I found that The GPO versions don't all match the STIG versions SCC scanned with:

| STIG | SCC scanned with | GPO package |
|---|---|---|
| Windows Server 2025 | V1R1 | V1R2 |
| Windows 11 | V2R10 | V2R8 |
| Defender Antivirus | V2R9 | V2R9 |
| Windows Firewall | V2R3 | V2R2 |

Windows 11 is the biggest gap. The GPO is two releases older than what SCC checks for, so some rules will probably still fail after I apply it. Anything left over will need a manual fix or will go on the POA&M.
## Changes applied

| Stage | GPO | Linked to | Date | Result |
|---|---|---|---|---|
| 1 | TBD | TBD | TBD | TBD |

## Issues encountered and fixes

| Issue | Cause | Fix |
|---|---|---|
| TBD | TBD | TBD |

## Settings intentionally not applied

Every deviation needs a written justification. These carry over to the POA&M.

| STIG ID | Rule | Reason not applied | Risk |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

## Screenshots

*Add to `screenshots/03-stig-hardening/`.*
