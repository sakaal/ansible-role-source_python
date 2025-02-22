Ansible role: source_python
===========================

forked from upstream: https://github.com/nmusatti/source-python

upstream: ![test](https://github.com/nmusatti/source-python/actions/workflows/test.yml/badge.svg)

An Ansible role to download and install Python from source using standard
filesystem hierarchy (FHS) locations, with separate build and deployment users,
configurable build options, and support for alternate installations. Supported
distributions are the currently maintained releases of the Red Hat family and
derivatives, and Ubuntu LTS. At this time tests are run on Rocky Linux 9, 
CentOS Stream 10, CentOS Stream 9, Fedora 41, Fedora 40, Fedora 39,
Ubuntu 24.04, Ubuntu 22.04 and Ubuntu 20.04.


Requirements
------------

None.

Role Variables
--------------

The variables that control the role behaviour are listed below with their respective defaults:

    python_install_dir: /usr/local

The base directory of the installation

    python_release: 3.13.0

The version of Python to be installed, in x.y.z form.

    python_build_user: "{{ ansible_facts['user_id'] | default(lookup('env', 'USER')) }}"

The owner of the source directory.

    python_build_group: "{{ python_build_user }}"

The source directory group.

    python_user: root

The owner of the installation.

    python_group: root

The installation group.

    python_src_dir: /usr/local/src/python

The directory where the source archive is downloaded, extracted and built.

    python_configure_options: >
      --enable-optimizations
      --enable-loadable-sqlite-extensions
      --with-computed-gotos
      --with-dbmliborder=bdb:gdbm
      --with-ensurepip=install
      --with-lto=full
      --with-system-ffi
      --prefix={{ python_install_dir }}

Lists the options passed to the configure script when building Python

    python_make_install_target: altinstall

Sets the installation target (altinstall allows multiple versions to coexist without overriding the system default).

    python_force: false

When `true` installation is performed even if a bug fix release of the same minor version was already installed.
Useful to repeat installations after something went wrong or to perform upgrades. Note that setting `python_force`
to `true` breaks the role's idempotence.

Dependencies
------------

Supported Linux distribution.

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: source_python
           vars:
             python_release: 3.13.0

Note the underscore in the name.

License
-------

GPLv3

Author Information
------------------

Sakari Maaranen - https://github.com/sakaal
Nicola Musatti - https://github.com/nmusatti
