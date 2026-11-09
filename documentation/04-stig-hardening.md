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

To fix this I navigated back to the server’s Group Policy Management tab and edited DOD Windows 11 STIG computer v2r8 GPO [user rights assignment](../screenshots/03-stig-hardening/admin-login.png). From there I added the Domain Admins and Enterprise Admins groups to the [five](../screenshots/03-stig-hardening/logins.png) “Deny log on” settings. Below are the rules that required manual fixes alongside their solutions. 

The five rules can be found here - [Rules](../screenshots/03-stig-hardening/logins.png)

The fixes

[V-253491](../screenshots/03-stig-hardening/deny-login-from-network-fix.png) = Deny access to this computer from the network

[V-253492](../screenshots/03-stig-hardening/Deny-login-as-batch-job-fix.png) = Deny log on as a batch job

[V-253493](../screenshots/03-stig-hardening/Deny-login-as-service-fix.png) = Deny log on as a service

[V-253494](../screenshots/03-stig-hardening/Logon-locally-fix.png) = Deny log on locally

[V-253495](../screenshots/03-stig-hardening/Deny-login-remote-fix.png) = Deny log on through Remote Desktop Services


## Settings intentionally not applied

These are rules I couldn’t fix in the lab. They’ll go on my POA&M (the list of known issues and how I’d fix them).

| STIG ID | Rule | Reason not applied | Risk |
|---|---|---|---|
| V-253470 | Multifactor authentication | Needs smart cards (CAC), for which I don't have | Accounts rely on passwords only which can be an issue |
| V-253254 | Must be Windows 11 Enterprise | Lab uses Enterprise Evaluation | None |

## Screenshots

