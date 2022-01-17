# [repository_epel](#repository_epel)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-repository_epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-repository_epel/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-repository_epel/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-repository_epel)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/repository_epel)|

Add the epel Repository to the System

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
repository_epel_url: "https://dl.fedoraproject.org/pub/epel/epel-release-latest-{{ repository_epel_version }}.noarch.rpm"
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


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
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

The machine needs to be prepared in CI this is done using `molecule/default/prepare.yml`:
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





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [centos7](https://hub.docker.com/r/mullholland/docker-molecule-centos7)
-   [centos-stream8](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream8)
-   [centos-stream9](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream9)
-   [ubi8](https://hub.docker.com/r/mullholland/docker-molecule-ubi8)
-   [amazonlinux](https://hub.docker.com/r/mullholland/docker-molecule-amazonlinux)
-   [rockylinux8](https://hub.docker.com/r/mullholland/docker-molecule-rockylinux8)
-   [almalinux8](https://hub.docker.com/r/mullholland/docker-molecule-almalinux8)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The last 2 versions.
-   The current version.



## [Exceptions](#exceptions)

Some variations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Ubuntu* | repo only supports RedHat/CentOS Server |
| Debian* | repo only supports RedHat/CentOS Server |
| Fedora* | repo only supports RedHat/CentOS Server |


If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-repository_epel/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
