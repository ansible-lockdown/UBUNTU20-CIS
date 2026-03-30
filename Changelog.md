# Change log for Ubuntu 2004

## v3.0.0 based on CIS v3.0.0

## Major version upgrade from CIS Benchmark v2.0.1 to v3.0.0

### Structural Changes

- Restructured from 6 sections to 7 sections to align with CIS v3.0.0
- Section 3.4 (Firewalls) moved to new Section 4 (Host Based Firewall)
- Section 4 (Access/Auth) moved to Section 5 (Access Control)
- Section 5 (Logging/Auditing) moved to Section 6 (Logging and Auditing)
- Section 6 (System Maintenance) moved to Section 7 (System Maintenance)
- AIDE controls moved from Section 1.2 to Section 6.1
- Cron/At controls moved from Section 4.1 to Section 2.4
- Automounting moved from Section 1.1.9 to Section 2.1.1

### New Controls (30)

- 1.1.1.6 (overlay kernel module), 1.1.1.10 (unused filesystem modules)
- 2.1.12 (rpcbind), 2.1.16 (tftp), 2.1.19 (xinetd), 2.4.1.7 (cron.yearly)
- 4.1.1 (single firewall utility), 4.2.2 (nftables not with ufw)
- 5.1.9 (SSH GSSAPIAuthentication)
- 5.3.1.1-5.3.1.3 (PAM packages), 5.3.2.1, 5.3.2.4 (PAM modules)
- 5.3.3.1.3, 5.3.3.2.3, 5.3.3.2.5, 5.3.3.2.7, 5.3.3.2.8 (PAM quality/faillock)
- 5.3.3.3.2, 5.3.3.3.3 (PAM pwhistory), 5.3.3.4.1, 5.3.3.4.2, 5.3.3.4.4 (PAM unix)
- 5.4.2.2-5.4.2.4, 5.4.2.8 (root/system accounts)
- 6.2.3.8 (logrotate), 6.3.2.4 (audit log space warning)

### Removed Controls (7)

- 1.4.3 (single user mode auth - removed from benchmark)
- 2.1.4.1-2.1.4.4 (NTP controls - deprecated, chrony/systemd-timesyncd only)
- 4.2.12 (SSH X11 forwarding - absorbed into DisableForwarding)
- 4.5.3 (root default group - absorbed into 5.4.2.x)

### Code Quality

- Fixed ~85 ansible-lint issues: key-order, command-instead-of-shell, yaml comment indentation, jinja spacing, name casing, risky-file-permissions
- Fixed yamllint 2-space indentation throughout the playbook
- Capitalized all handler names and notify references for ansible-lint `name[casing]` compliance
- Converted all single-item `when:` lists to inline format across 27 task files (204 occurrences)
- Converted all single-item `tags:` lists to inline format across 4 task files (23 occurrences)
- Task key order normalized: `name → when → tags → block/module`

### Audit Template Fixes

- Fixed duplicate keys in `ansible_vars_goss.yml.j2` that caused goss "unable to determine format" error (Go YAML parser rejects duplicates)
  - Removed duplicate `ubtu20cis_grub_user`, `ubtu20cis_nis_server`, `ubtu20cis_samba_server`, `ubtu20cis_snmp_server`
- Renamed `ubtu20cis_time_service` to `ubtu20cis_time_sync_tool` in template to match goss test variable references
- Added missing audit variables to template and `defaults/main.yml`:
  - `ubtu20cis_bluetooth_service`, `ubtu20cis_bluetooth_mask` (goss test 3.1.3)
  - `ubtu20cis_ftp_client` (goss test 2.2.6)
  - `ubtu20cis_ipv6_disable` (goss test 3.1.1)
  - `ubtu20cis_remote_log_server` (goss tests 6.2.3.6/6.2.3.7)
- Added `---` YAML document marker to template
- Quoted string values containing YAML special characters

### Variable Naming Standardization

- Standardized all `register:` variable prefixes to follow Lockdown conventions:
  - `prelim_` prefix for all preliminary/discovery variables in `tasks/prelim.yml` (17 variables renamed)
  - `discovered_` prefix for all section task registered variables (63 variables renamed)
- Renamed prelim `set_fact` variables: `mount_names` → `prelim_mount_names`, `min_int_uid` → `prelim_min_int_uid`, `max_int_uid` → `prelim_max_int_uid`, etc.
- Removed inconsistent prefixes (`ubtu20cis_`, `avahi_`, `snap_`, bare names) from registered variables
- Updated all cross-file references in defaults, templates, and section tasks

### Warn Count Consistency

- Added missing Warn Count blocks (`import_tasks: warning_facts.yml` + `vars: warn_control_id`) to 34 manual remediation tasks across 11 files
- Fixed `vars: warn_control_id` placement from block-level to task-level (same indentation as `ansible.builtin.import_tasks:`) in 20+ tasks

### Benchmark Title and Logic Alignment

- Validated all 313 task titles against CIS v3.0.0 benchmark JSON — fixed 150+ stale v2 titles
- Fixed 8 critical logic bugs where tasks implemented the wrong control:
  - 2.2.6: Changed from RPC removal (rpcbind) to FTP client removal (ftp) per v3.0.0
  - 7.1.10: Fixed file paths from /etc/opasswd to /etc/security/opasswd (4 references)
  - 7.2.6: Changed from duplicate username check to duplicate GID check per v3.0.0
  - 1.1.2.1.3/1.1.2.1.4: Fixed nosuid/noexec swap in both task logic and systemd template
  - 5.3.3.2.7/5.3.3.2.8: Fixed swapped PAM quality titles
  - 5.4.2.6: Fixed title to "Ensure root user umask is configured"
  - 5.4.2.8: Replaced manual stub with actual logic to find and lock accounts without valid login shells
  - 3.1.1: Changed from active IPv6 disable to audit-first approach per v3.0.0

### Cross-Repo Alignment (Remediation + Audit)

- Fixed remediation 2.4.1.7: replaced manual stub with proper file permission task for /etc/cron.yearly
- Fixed bridge template (`ansible_vars_goss.yml.j2`): `ubtu20cis_telnet_server` and `ubtu20cis_telnet_mask` were both mapped from `ubtu20cis_telnet_required` instead of their actual defaults variables
- Fixed bridge template: `ubtu20_varlog_location` renamed to `ubtu20cis_varlog_location` to match audit `vars/CIS.yml`
- Added missing `ubtu20cis_remote_log_host`, `ubtu20cis_remote_log_port`, `ubtu20cis_remote_log_protocol` to defaults/main.yml and bridge template (goss test 6.2.3.6 references these)
- Added missing `ubtu20cis_ipv4_required` to bridge template (was in defaults but not passed to audit)

### Bug Fixes

- Added missing "Update dconf" handler (14 task references)
- Fixed "Restart timeservice" handler case mismatch
- Added missing when: clause on journald file permissions rule
- Fixed wrong task ID 5.2.3.10 → 5.2.3.20 (audit immutable config)
- Added no_log: true to password task
- Added changed_when to 5 shell/command tasks
- Fixed meta description typo "benmarks" → "benchmarks"
- Removed unused handlers (reload gdm3, reload gdm, persistent ip6tables)
- Created 6 missing dconf templates
- Removed 2 orphaned templates (chrony.conf.j2, ntp.conf.j2)
- Added *.vault, *.pem, *.key to .gitignore

### Defaults

- Complete rewrite of defaults/main.yml with v3.0.0 variable names
- All 313 control toggle variables renamed to v3.0.0 numbering
- Added ubtu20cis_section7_patch toggle
- benchmark_version updated to v3.0.0

### Tags

- Replaced all scored/not_scored tags with automated/manual
- Updated all rule_X.Y.Z tags to v3.0.0 IDs
- Updated level tags for controls that changed profile

## v2.0.1 based on CIS v2.0.1

- issue 148 thanks to @karlg100
- workflow updates for new pipeline
- audit
  - updated files and variables
  - updated vars/audit.yml
  - improved when using local copies or archived

## v2.0.1 based upon CIS 2.0.1

- ability to run goss audit only audit_only variable
  - audit vars mainly moved to var/audit.yml
- several control updates
- goss version update to 0.4.4

## V2.0 based upon CIS 2.0.1

- v2.0.1 - refer to change history from official CIS pdf.
  - ReWrite of many rules
  - Ordering and numbering of rules
  - many title updates
- timesync options increased
  - default systemd-timesyncd
  - chrony options updated
- idempotency improvements
- new discoveries
  - interactive users
  - uid min value
  - is_container discovery and default var
- pre-commit added to setup
- README new layout

- Added test for rule 4.3.4 check user is using sudo has password set before NOPASSWD removed from sudoers
- grub password check update thanks to @Acenl12 on discord

## V1.0.1 - based upon CIS 1.1.0

thanks to ikthomas
[#84](https://github.com/ansible-lockdown/UBUNTU20-CIS/issues/84)

## v1.0.0

- update galaxy lint requirements
- license file
- ansible version

## April 2023 Updates
- Addressed Bugs
  - [#73](https://github.com/ansible-lockdown/UBUNTU20-CIS/issues/73) - Thanks @fnschroeder (Fix Taken From @uk-bolly issue_73 branch)
  - [#80](https://github.com/ansible-lockdown/UBUNTU20-CIS/issues/80) - Thanks @kdebisschop
- Added Fixes For Outstanding PR's
  - [#81](https://github.com/ansible-lockdown/UBUNTU20-CIS/pull/81) - Thanks @kdebisschop
  - Fixed Linting Errors For Yamllint & Ansible-Lint
  - Adjusted Builtin to Posix For sysctl module.

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
