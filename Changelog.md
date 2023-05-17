# Change log for Ubuntu 2004

## V1.0.1 - based upon CIS 1.1.0

thanks to ikthomas
[#84](https://github.com/ansible-lockdown/UBUNTU20-CIS/issues/84) 

## v1.0.0

- update galaxy lint requirements
- license file
- ansible version

## Feb 23 updates - Initial

- lint files updated
- ansible version updated
- Lots of lint and standardisation changes
- fqcn
- Assertions for root and grub passwords
- Import tasks to allow tags to be used
- Warnings made standard
- warn count feature added
- workflow updates
- wireless interface discovery
- idempotency checks and updates

reboot variable changed from ubtu20_skip_reboot to skip_reboot (still default true)

### Remediate portion

### Issues and PRs address

- #1 set bootloader pwd - Allowed unrestricted by default but set new variables
  - Added extra variable options ubtu20cis_set_grub_password and ubtu20cis_set_root_password (defaults true)

- #2 Ensure locks for failed attempts
- #3 root path integrity
- thanks to @vbotka
  - #63 parse_etc_password
- thanks to @makefu
  - #67 UFW incoming firewall ports (optional)
- thanks to @CFoltin
  - #68 logrotate alignment
  - #69 stop rule overwrite UFW
- thanks to @hackery
  - #70 TMOUT stops being repeated

Many improvements on multiple controls
Remediate and audit version now match. When using remediate will pull in latest version of audit for that release.

### Audit

- updated goss version used
- aligned new variables with audit
- audit path used now default to /opt from /var/tmp

## Started at devel version 1.1.0 Feb_23
