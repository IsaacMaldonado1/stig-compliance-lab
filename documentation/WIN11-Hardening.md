# Overview
This page entails the issues that needed to be fixed within the windows machine. 

## What I scanned
The following was scanned using SCC

[Microsoft_Windows_11_STIG](../screenshots/03-stig-hardening/selected2.png)

[Microsoft MS_Defender_Antivirus](../screenshots/03-stig-hardening/selected2.png)

[Windows_Firewall_with_Advanced_Security](../screenshots/03-stig-hardening/selected1.png)

## WIN11 Score after applying DISA's GPOs

| STIG | Score | Pass | Fail | Error | N/A | Not checked | Total |
|---|---|---|---|---|---|---|---|
| Windows 11 | 92.98% | 225 | 17 | 0 | 5 | 10 | 257 |
| Defender Antivirus | 95.52% | 64 | 0 | 3 | 0 | 0 | 67 |
| Windows Firewall | 100% | 20 | 0 | 0 | 0 | 1 | 21 |

## Fixing Microsoft_Windows_11_STIG score
My goal is to get the scanned score from 92.98% to 100%.

## What needed fixing

- Domain admin accounts could still log on to WIN11 (5 rules)
- Local accounts had passwords set to never expire (1 rule)
- DoD and ECA root certificates weren't installed, and cross-certificates weren't blocked (4 rules)
- Virtualization-based code integrity (HVCI) wasn't on (1 rule)
- The drive wasn't encrypted with BitLocker (1 rule, CAT I)
- App suggestions, lock screen notifications, and attachment zone info weren't set for the scanning account (3 rules)
- No multifactor authentication (1 rule)
- Not running licensed Windows 11 Enterprise (1 rule)

## The Fixes

I fixed each issue line by line according the "What needs fixing" column.

### Fixing "Domain admin accounts could still log on to WIN11" (V-253491 – V-253495)
To fix this I navigated back to the server’s Group Policy Management tab and edited DOD Windows 11 STIG computer v2r8 GPO [user rights assignment](../screenshots/03-stig-hardening/admin-login.png). From there I added the Domain Admins and Enterprise Admins groups to the [five](../screenshots/03-stig-hardening/logins.png) “Deny log on” settings. Below are the rules that required manual fixes alongside their solutions. 

The five rules can be found here - [Rules](../screenshots/03-stig-hardening/logins.png)

The fixes

[V-253491](../screenshots/03-stig-hardening/deny-login-from-network-fix.png) = Deny access to this computer from the network

[V-253492](../screenshots/03-stig-hardening/Deny-login-as-batch-job-fix.png) = Deny log on as a batch job

[V-253493](../screenshots/03-stig-hardening/Deny-login-as-service-fix.png) = Deny log on as a service

[V-253494](../screenshots/03-stig-hardening/Logon-locally-fix.png) = Deny log on locally

[V-253495](../screenshots/03-stig-hardening/Deny-login-remote-fix.png) = Deny log on through Remote Desktop Services


### Fixing "Local accounts had passwords set to never expire" (V-253273)

V-253273, password expiration (on WIN11) Was set to never expire [Unchecked](../screenshots/03-stig-hardening/password-expire.png) "Passwords Never Expire" from all accounts listed on Win11.


Score after these two fixes: 95.87% (10 fails left).


### Fixing DoD and ECA root certificates weren't installed, and cross-certificates weren't blocked"

This has to deal with certificates and my windows machine not set up to trust DoD certificates. To do this I navigated to cybermill and downloaded the latest version of Installroot. InstallRoot adds the DoD’s (and ECA’s) root certificates to Windows’ trusted list, and blocks a few cross-certificates that could create back-door trust paths.

I installed the following version: InstallRoot 5.6 NIPR 64-bit Windows Installer

Score after: 97.52% (6 fails left).

### Fixing "Virtualization-based code integrity (HVCI) wasn't on"V-253371)
Virtualization-based code integrity wasn't on. I didn't change anything; it passed after a restart.

### BitLocker (V-253259, CAT I)
The drive wasn't encrypted. Turning on BitLocker with a startup PIN. 

Turned on Bitlocker and will re-scan after finished. After the scan Bitlocker passed. 

Score after: 97.93%


### User settings (V-253425, V-253477, V-253478)
App suggestions, lock screen notifications, and attachment zone info. These are user settings, and SCC checks them for whoever runs the scan. I ran it as Labadmin, a local account the domain User GPO doesn't apply to, so these still fail even though the GPO covers domain users like James Smith.

### Can't fix in the lab (V-253470, V-253254)
- MFA needs smart cards (CAC), which I don't have.
- The lab runs Windows 11 Enterprise Evaluation instead of licensed Enterprise.

Both go on the POA&M.
