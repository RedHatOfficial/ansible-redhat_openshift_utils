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


