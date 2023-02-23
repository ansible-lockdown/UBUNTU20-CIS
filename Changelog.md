# Change log for Ubuntu 2004



## Feb 23 updates

### based upon CIS 1.1.0

Big changes across the board

- lint files updated
- ansible version updated
- Lots of lint and standardisation changes
- fqcn
- Assertions for root and grub passwords
- Import tasks to allow tags to be used
- Warnings made standard

### Remediate portion

### Issues and PRs address

- #1 set bootloader pwd
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

### Audit

- updated goss version used
- aligned new variables with audit
- audit path used now default to /opt from /var/tmp

## Started at devel version 1.1.0 Feb_23
