# [Ansible role repository_epel](#repository_epel)

Add the epel Repository to the System

|GitHub|Downloads|Version|
|------|---------|-------|
|[![github](https://github.com/mullholland/ansible-role-repository_epel/actions/workflows/molecule.yml/badge.svg)](https://github.com/mullholland/ansible-role-repository_epel/actions/workflows/molecule.yml)|[![downloads](https://img.shields.io/ansible/role/d/mullholland/repository_epel)](https://galaxy.ansible.com/mullholland/repository_epel)|[![Version](https://img.shields.io/github/release/mullholland/ansible-role-repository_epel.svg)](https://github.com/mullholland/ansible-role-repository_epel/releases/)|
## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/mullholland/ansible-role-repository_epel/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  # vars:
  #   example_var: "value"
  roles:
    - role: "mullholland.repository_epel"
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/mullholland/ansible-role-repository_epel/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: mullholland.repository_codereadybuilder
      when:
        - (ansible_distribution == "RedHat" and ansible_distribution_major_version == "8") or
          (ansible_distribution == "CentOS" and ansible_distribution_major_version == "9")
    - role: mullholland.repository_powertools
      when:
        - ansible_distribution in [ "CentOS", "Rocky", "AlmaLinux" ]
        - ansible_distribution_major_version == "8"
```



## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/mullholland/ansible-role-repository_epel/blob/master/defaults/main.yml):

```yaml
---
repository_epel_key_url: "https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-{{ repository_epel_version }}"

_repository_epel_version:
  RedHat:
    "7": 7
    "8": 8
  CentOS:
    "7": 7
    "8": 8
    "9": 9
  Rocky:
    "8": 8
  AlmaLinux:
    "8": 8
  Amazon:
    "2": 7

repository_epel_version: "{{ _repository_epel_version[ansible_distribution][ansible_distribution_major_version] }}"

repository_epel_packages:
  RedHat:
    "7":
      - "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm"
    "8":
      - "https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm"
  CentOS:
    "7":
      - "epel-release"
    "8":
      - "epel-release"
      - "epel-next-release"
    "9":
      - "https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm"
      - "https://dl.fedoraproject.org/pub/epel/epel-next-release-latest-9.noarch.rpm"
  Rocky:
    "8":
      - "epel-release"
  AlmaLinux:
    "8":
      - "epel-release"
  Amazon:
    "2":
      - "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/mullholland/ansible-role-repository_epel/blob/master/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://mullholland.net) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/mullholland/ansible-role-repository_epel/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/mullholland/enterpriselinux)|all|
|[Amazon](https://hub.docker.com/r/mullholland/amazonlinux)|Candidate|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-repository_epel/issues).

## [License](#license)

[MIT](https://github.com/mullholland/ansible-role-repository_epel/blob/master/LICENSE).

## [Author Information](#author-information)

[Mullholland](https://mullholland.net)
