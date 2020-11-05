# ubuntu-20
Ubuntu 20 CIS
=========

Configure Ubuntu 20 machine to be [CIS](https://www.cisecurity.org/cis-benchmarks/) compliant. There are some intrusive tasks that have a toggle in defaults main.yml to disable to automated fix

This role **will make changes to the system** that could break things. This is not an auditing tool but rather a remediation tool to be used after an audit has been conducted.

Based on [CIS Ubuntu Linux 20.04 LTS Benchmark ](https://community.cisecurity.org/collab/public/index.php).


Requirements
------------

You should carefully read through the tasks to make sure these changes will not break your systems before running this playbook.
If you want to do a dry run without changing anything, set the below sections (rhel8cis_section1-6) to false. 

Role Variables
--------------

There are many role variables defined in defaults/main.yml. This list shows the most important.

**ubtu20cis_disruption_high**: Run CIS checks that we typically do NOT want to automate due to the high probability of breaking the system (Default: false)

**ubtu20cis_section1_patch**: CIS - Iniitial setup (Section 1) (Default: true)

**ubtu20cis_section2_patch**: CIS - Services settings (Section 2) (Default: true)

**ubtu20cis_section3_patch**: CIS - Network Configuration (Section 3) (Default: true)

**ubtu20cis_section4_patch**: CIS - Logging and Auditing settings (Section 4) (Default: true)

**ubtu20cis_section5_patch**: CIS - Access, Authentication and Authorization settings (Section 5) (Default: true)

**ubtu20cis_section6_patch**: CIS - System Maintenance settings (Section 6) (Default: true) 


##### Service variables:
###### These control whether a server should or should not be allowed to continue to run these services

```
ubtu20cis_allow_autofs: false
ubtu20cis_allow_usb_storage: false
ubtu20cis_avahi_server: false
ubtu20cis_cups_server: false
ubtu20cis_dhcp_server: false
ubtu20cis_ldap_server: false
ubtu20cis_nfs_server: false
ubtu20cis_dns_server: false
ubtu20cis_vsftpd_server: false
ubtu20cis_httpd_server: false
ubtu20cis_dovecot_server: false
ubtu20cis_smb_server: false
ubtu20cis_squid_server: fase
ubtu20cis_snmp_server: false
ubtu20cis_rsync_server: false
ubtu20cis_nis_server: false
ubtu20cis_rpc_required: false
```

##### Client variables:
###### These control whether a client should or should not be allowed to continue to run these services
```
ubtu20cis_nis_required: false
ubtu20cis_rsh_required: false
ubtu20cis_talk_required: false
ubtu20cis_telnet_required: false
ubtu20cis_ldap_clients_required: false
ubtu20cis_is_router: false
```

##### IPv4 required
`ubtu20cis_ipv4_required`

##### IPv6 required
`ubtu20cis_ipv6_required`

##### X-Windows required
`ubtu20cis_xwindows_required`

##### Is system a container
`ubtu20cis_system_is_container:`

Dependencies
------------

Ansible > 2.6.5

Example Playbook
----------------

This sample playbook should be run in a folder that is above the main UBUNTU-18-CIS folder.

```
- hosts: all
  become: true
  vars:
      is_container: false

  roles:

      - role: "{{ playbook_dir }}"
        ubtu20cis_skip_for_travis: false
        ubtu20cis_oscap_scan: yes

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
```

Tags
----
Many tags are available for precise control of what is and is not changed.

Some examples of using tags:

```
    # Audit and patch the site
    ansible-playbook site.yml --tags="patch"
```