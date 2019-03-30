mebooks.ansible-role-docker-datadog
===================================

This role installs the [dockerised datadog agent](https://docs.datadoghq.com/agent/docker/) on an Ubuntu server.

We assume that we've probably run:

* [ansible-role-users](https://github.com/jcdarwin/ansible-role-users)
* [ansible-role-common](https://github.com/jcdarwin/ansible-role-common)


The above all chain as dependencies of our main dependency:

* [ansible-role-docker](https://github.com/jcdarwin/ansible-role-docker)

Requirements
------------

Developed and tested on *Ubuntu Server 16.10 Yakkety*, but should work on other OSes.

It's running on Docker.

Role Variables
--------------

For let's encrypt certificate, and automatic reverse proxy

- `datadog.agent_run_dir`  defaults to */opt/datadog-agent/run*
- `datadog.DD_API_KEY`  defaults to *WHATEVER*
- `datadog.DD_LOGS_ENABLED` defaults to *true*
- `datadog.DD_AC_EXCLUDE`: defaults to *"name:datadog"*
- `datadog.DD_AC_INCLUDE` defaults to *"name:traefik name:gollum ghost tomcat"*

Dependencies
------------

- `mebooks.ansible-role-docker`

Example Playbook
----------------

```yml
- hosts: remote
  remote_user: deploy
  become: true
  become_user: root
  become_method: sudo

  vars:
    datadog:
      agent_run_dir: /opt/datadog-agent/run
      # datadog.DD_API_KEY is defined in the unversioned group_vars/remote
      DD_API_KEY: WHATEVER
      DD_LOGS_ENABLED: true
      DD_AC_EXCLUDE: "name:datadog"
      DD_AC_INCLUDE: "name:traefik name:gollum name:ghost name:tomcat"

  roles:
    # We presume we've already run ansible-role-users and ansible-role-common
    - role: ansible-role-docker-datadog
```

License
-------

GPLv3

Author Information
------------------

Jason Darwin
