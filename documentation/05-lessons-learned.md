# 05 – Lessons Learned

## What went well

DISA's GPO packages did most of the work. Windows 11 went from 37.6% to 92.98% and Firewall went from 15% to 100% just from linking them.

## What was harder than expected

Getting SCC. NIWC's GitHub releases were empty and DISA's site wanted a CAC, so I had to find the public download server and verify the installer myself. Running both VMs off an old USB HDD was also a mistake. The WIN11 scan took over an hour.

## What I'd do differently

Sort out storage before building anything.

## How this maps to real ISSO / sysadmin work

Verifying software before installing it, not installing services I don't need, filling in the site-specific settings DISA leaves blank, and tracking what I can't fix, like MFA without a CAC, for the POA&M.
