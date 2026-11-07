# 03 – STIG Hardening

How the STIG settings were applied and what broke along the way.

## Approach

I used DISA's STIG GPO package (July 2026). I downloaded it from DISA's public download server and checked the SHA-256 hash against the one listed on NIST's National Checklist Program. It matched.

## Changes applied

| Stage | GPO | Linked to | Result |
|---|---|---|---|
| 1 | DOD Defender AV STIG v2r9 | Domain Controllers, Workstations | Defender 26.87% → 95.52% (both machines) |
| 1 | DOD Windows Firewall STIG v2r2 | Domain Controllers, Workstations | Firewall 15% → 100% (both machines) |
| 2 | DOD Windows 11 STIG Computer v2r8 | Workstations | Windows 11 37.6% → 92.98% |
| 2 | DOD Windows 11 STIG User v2r8 | Johnsoncompany → Users | Applies to domain users (James Smith) |

## Issues encountered and fixes

| Issue | Cause | Fix |
|---|---|---|
|V-253491–253495, admins should not be able to log into workstations | DISA left them empty because every domain’s group names are different | Added the Domain Admins and Enterprise Admins groups to the five “Deny log on” settings |
| V-253273, password expiration (on WIN11) | Was set to never expire | [Unchecked](../screenshots/03-stig-hardening/password-expire.png) "Passwords Never Expire" from all accounts listed on Win11 |

## How I Fixed "deny login rights"

To fix this I navigated back to the server’s Group Policy Management tab → DOD Windows 11 STIG computer v2r8 GPO → edit → computer configuration → policies → windows settings → Security Settings → local policies → user rights assignment. From there I added the Domain Admins and Enterprise Admins groups to the five “Deny log on” settings. According to DISA’s Windows 11 STIG (V-253494), DISA leaves these blank because every domain’s group names are different. This leaves an extra layer of protection from a compromised PC getting access to an admin account. 


## Settings intentionally not applied

These are rules I couldn’t fix in the lab. They’ll go on my POA&M (the list of known issues and how I’d fix them).

| STIG ID | Rule | Reason not applied | Risk |
|---|---|---|---|
| V-253470 | Multifactor authentication | Needs smart cards (CAC), for which I don't have | Accounts rely on passwords only which can be an issue |
| V-253254 | Must be Windows 11 Enterprise | Lab uses Enterprise Evaluation | None |

## Screenshots

