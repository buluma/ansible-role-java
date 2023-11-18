# [Ansible role java](#java)

Install and configure java on your system.

|GitHub|GitLab|Downloads|Version|Issues|Pull Requests|
|------|------|-------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-java/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-java/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-java/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-java)|[![downloads](https://img.shields.io/ansible/role/d/4740)](https://galaxy.ansible.com/buluma/java)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-java.svg)](https://github.com/buluma/ansible-role-java/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-java.svg)](https://github.com/buluma/ansible-role-java/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-java.svg)](https://github.com/buluma/ansible-role-java/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-java/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  # We want to test some non-default version of java, to ensure we can install a specific version.
  vars:
    _desired_java_version:
      default: 8
      Debian: 11
      Debian-bookworm: 17
    desired_java_version: "{{ _desired_java_version[ansible_distribution ~ '-' ~ ansible_distribution_release] | default(_desired_java_version[ansible_distribution] | default(_desired_java_version['default'])) }}"

  roles:
    - role: buluma.java
      java_version: "{{ desired_java_version }}"
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-java/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.bootstrap
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-java/blob/master/defaults/main.yml):

```yaml
---
# defaults file for java

# Set the vendor of java, valid values are "openjdk" and "oracle".
java_vendor: openjdk

# Set the variable to install the type, valid values are "jre" and "jdk".
java_type: jre

# Set the version of java, valid values are 6, 7, 8, 9, 10, 11, 12 or 13.
# By default, a distribution default is used, mapped in `vars/main.yml`.
# By setting java_version, you overwrite this default to your selected
# version.
java_version: "{{ java_default_version }}"

# Set the format of the installation source, valid values are "targz" and
# "rpm". This is only valid with "java_vendor == oracle"
java_format: targz

# Where do the RPMs come from when installing Oracle RPMs?
# Either "local" or "repository".
# Valid for "java_vendor == oracle" and "java_format" == "rpm"
java_rpm_source: local

# Choose if you can JCE installed. Only applicable for (both):
# - java_vendor == "oracle"
# - java_version == "8"
java_jce: yes

# In case of "java_vendor == oracle" and "java_format == targz", a directory
# as to be set where to install.
java_install_directory: /opt
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-java/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-java/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Alpine](https://hub.docker.com/repository/docker/buluma/alpine/general)|all|
|[Amazon](https://hub.docker.com/repository/docker/buluma/amazonlinux/general)|Candidate|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|8|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[opensuse](https://hub.docker.com/repository/docker/buluma/opensuse/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-java/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-java/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-java/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

Please consider [sponsoring me](https://github.com/sponsors/buluma).

### [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
