# ansible-redhat_openshift_utils
Ansible content supplemental to the openshift-ansible project for doing things that don't ship with that project, such as prerequisites for updates, upgrades, restarts, etc.

## Playbooks
Playbooks provided by this project.

### ocp-rolling-os-update-and-upgrade.yml
Performs a rolling (one host at a time) operating system (OS) update and/or upgrade to the OCP cluster. This is done as per the instructions at [Operating System Updates and Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/os_upgrades.html).

#### Assumptions
* etcd is deployed to masters
  * pull request welcome to make this work with etcd either on masters or on seperate nodes

#### Required groups
* masters
* infra-nodes
* app-nodes

### ocp-upgrade-preparation.yml
Performs the steps should be preforemd before [Performing Automated In-place Cluster Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html). Specifically before running the appropriate upgrade playbook in the [openshift-ansible](https://github.com/openshift/openshift-ansible/) project.

This is essentially an assible version of [Preparing for an Automated Upgrade] (https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html#preparing-for-an-automated-upgrade).

### ocp-upgrade-cleanup.yml
Performs the steps that should be prefored after [Performing Automated In-place Cluster Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html). Specifically after running the appropriate upgrade playbookin the [openshift-ansible](https://github.com/openshift/openshift-ansible/) project.

### ocp-ldap-groups-sync.yml
Performs an ldap group sync.

#### Options
| parameter                       | required | default | choices | comments
|---------------------------------|----------|---------|---------|---------------------------------------------
| ocp_ldap_server_fqdn            | yes      |         |         | FQDN of the LDAP server
| ocp_ldap_bind_dn                | yes      |         |         | Bind DN to usu
| ocp_ldap_bind_password          | yes      |         |         | Bind passwrod assoicated with the `ocp_ldap_bind_dn`
| ocp_ldap_groups_query_base_dn   | yes      |         |         | Base DN for looking for LDAP groups
| ocp_ldap_users_query_base_dn    | yes      |         |         | Base DN for looking for LDAP users
| ocp_ldap_group_uid_name_mapping | yes      |         |         | Hash of LDAP group DNs to OCP group names to map
