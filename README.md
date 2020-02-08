RHEL 7 DISA STIG
================
**This role is purely for demonstration purposes only**


This role as configured will execute the DISA STIG against a RHEL 7 system to be compliant with most Cat II findings.  These will be audited and remediated automatically.  While all content for all Cat II and Cat I findings do exist they are intentionally skipped if you utilize the recommended tag skipping.

Skipped Tags
------------

The below tags are skipped due to specific configuration requirements of the environment and assume that the system as not been registered to RHN.  If using Ansible Tower they will need to also be configured.  

cat1
RHEL-07-040180
RHEL-07-040320
RHEL-07-041004
RHEL-07-041010
RHEL-07-010090
RHEL-07-040300
RHEL-07-040520
RHEL-07-040730

This role is based on RHEL 7 DISA STIG: http://iase.disa.mil/stigs/os/unix-linux/Pages/index.aspx


Requirements
------------

RHEL 7. Other versions are not supported.

Role Variables
--------------

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `rhel7stig_cat1_audit` | `no` | Audit for CAT I findings       |
| `rhel7stig_cat2_audit` | `yes`| Audit for CAT II findings      |
| `rhel7stig_cat3_audit` | `no` | Audit for CAT III findings     |
| `rhel7stig_cat1_patch` | `no` | Correct CAT I findings         |
| `rhel7stig_cat2_patch` | `yes`| Correct CAT II findings        |
| `rhel7stig_cat3_patch` | `no` | Correct CAT III findings       |
| `rhel7stig_gui`        | `no` | Whether or not to run tasks related to auditing/patching the desktop environment |
| `rhel7stig_av_package` | `no` | Anti-virus package(s) to install and service to start and enable. |
| `rhel7stig_lftpd_required` | `no` | If set to `no`, remove `lftpd`. |
| `rhel7stig_tftp_required` | `no` | If set to `no`, remove `tftp` client and server packages. |
| `rhel7stig_snmp_community` | `Endgam3Ladyb0g` | SNMP community string that will replace `public` and `private` in `snmpd.conf`. |
| `rhel7stig_bootloader_password` | `Boot1tUp!` | GRUB2 bootloader password. This should be stored in an Ansible Vault. |

Ansible Tower Extra Vars
------------------------

The below extra variables should be configured in Ansible Tower if using this role within an Ansible Tower Environment.  This will allow future use of the playbook to fully configure systems to be STIG compliant.

rhel7stig_cat1_patch: false
rhel7stig_cat2_patch: true
rhel7stig_cat3_patch: false

Dependencies
------------

None

Example Playbook
----------------

The included example playbook (rhel7stig.yml) can be used to run this role from within Ansible Tower or your Default configurations.  Below is what it looks like.

    - hosts: all
      become: true
      roles:
        - rhel7.stig

Example Command-Line Usage
--------------------------

ansible-playbook rhel7stig.yml -u cloud-user --private-key=~/.ssh/ccoe --skip-tags="cat1,RHEL-07-040180,RHEL-07-040320,RHEL-07-041004,RHEL-07-041010,RHEL-07-010090,RHEL-07-040300,RHEL-07-040520,RHEL-07-040730" -e rhel7stig_cat2_patch=true


License
-------

MIT
