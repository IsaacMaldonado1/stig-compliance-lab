# 04 – Rescan Results

Before rescanning, I linked DISA’s Defender and Firewall GPOs to the Domain Controllers and Workstations OUs. The difference was night and day in that they took Defender from 26.87% to 95.52% and Firewall from 15% to 100% on both machines. 

## What Was Scanned
I scanned both with the following:
- MS_Defender_Antivirus
- Windows_Firewall_With_Advanced_Security

## Stage 1: Defender and Firewall GPOs (Oct 28, 2026)

| System | STIG | Before | After | Change |
|---|---|---|---|---|
| Server-DC01 | Defender Antivirus | 26.87% | 95.52% | +68.65 |
| Server-DC01 | Windows Firewall | 15% | 100% | +85 |
| WIN11 | Defender Antivirus | 26.87% | 95.52% | +68.65 |
| WIN11 | Windows Firewall | 15% | 100% | +85 |


## Screenshots

*Add to `screenshots/04-rescan-results/`.*
