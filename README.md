# ansible-redhat_openshift_utils
Ansible content supplemental to the openshift-ansible project for doing things that don't ship with that project, such as prerequisites for updates, upgrades, restarts, etc.

## Playbooks
Playbooks provided by this project are currently supported in either OCP 3.9 or OCP 3.11. See details for each playbook to determine OCP compatability.

### ocp-rolling-os-update-and-upgrade.yml (OCP 3.11)
Performs a rolling (one host at a time) operating system (OS) update and/or upgrade to the OCP cluster. This is done as per the instructions at [Operating System Updates and Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/os_upgrades.html).

#### Assumptions
* etcd is deployed to masters
  * pull request welcome to make this work with etcd either on masters or on seperate nodes

#### Required groups
* masters
* infra-nodes
* app-nodes

#### Default Vars (defaults/main.yml)
* ocp_deployment_version: <ocp version>
* ocp_docker_storage: <device to use for docker storage>
* expected_docker_version: <1.13.1 if using OCP 3.11>
* ocp_repositories: <which repos to enable>
* ocp_deployment_packages: <required packages for OCP>

### ocp-rolling-hosts-reboot.yml (OCP 3.11)
Performs a rolling (one host at a time) reboot for each node in the OCP cluster.

### ocp-rolling-services-restart.yml (OCP 3.11)
Performs a rolling (one host at a time) restart of OCP services for each node in the OCP cluster.

### ocp-hosts-reboot.yml (OCP 3.11)
Performs a blanket reboot for all nodes in the OCP cluster

### ocp-install-preparation.yml (OCP 3.9)
Performs some prerequisite steps before [Installing OpenShift](https://docs.openshift.com/container-platform/3.11/install/host_preparation.html)

```
ansible-playbook ocp-install-preparation.yml
```

### ocp-upgrade-preparation.yml (OCP 3.9)
Executes the steps that should be performed before [Performing Automated In-place Cluster Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html). Specifically before running the appropriate upgrade playbook in the [openshift-ansible](https://github.com/openshift/openshift-ansible/) project.

This is essentially an ansible version of [Preparing for an Automated Upgrade](https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html#preparing-for-an-automated-upgrade).

### ocp-upgrade-cleanup.yml (OCP 3.9)
Executes the steps that should be performed after [Performing Automated In-place Cluster Upgrades](https://docs.openshift.com/container-platform/latest/install_config/upgrading/automated_upgrades.html). Specifically after running the appropriate upgrade playbook in the [openshift-ansible](https://github.com/openshift/openshift-ansible/) project.

### ocp-ldap-groups-sync.yml (OCP 3.9)
Performs an ldap group sync.

#### Options
| parameter                            | required | default | choices     | comments
|--------------------------------------|----------|---------|-------------|---------------------------------------------
| ocp\_ldap\_server\_fqdn              | yes      |         |             | FQDN of the LDAP server
| ocp\_ldap\_bind\_dn                  | yes      |         |             | Bind DN to use
| ocp\_ldap\_bind\_password            | yes      |         |             | Bind passwrod assoicated with the `ocp_ldap_bind_dn`
| ocp\_ldap\_groups\_query\_base\_dn   | yes      |         |             | Base DN for looking for LDAP groups
| ocp\_ldap\_users\_query\_base\_dn    | yes      |         |             | Base DN for looking for LDAP users
| ocp\_ldap\_group\_uid\_name\_mapping | yes      |         |             | Hash of LDAP group DNs to OCP group names to map
| ocp\_ldap\_insecure                  | no       | false   | true, false | Whether to use insecure connection to LDAP
| ocp\_ldap\_ca                        | no       |         |             | Path to CA for LDAP server
| ocp\_projects\_group\_roll\_mapping  | no       |         |             | Array of dictionaries mapping a group and role to a projects
