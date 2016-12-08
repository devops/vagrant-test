# Ansible Role: base

RedHat/CentOS system base configure

## Requirements
1. 执行本role前，要先确认系统的repo配置，如果是用系统默认的repo则不用做其他设置，否则请先设置repo。
2. 系统一定要关闭selinux，如果没有关闭，可以在设置repo后设置本role的`base_selinux_disabled`为true，本role会自动禁用selinux.
3. 如果采用本role关闭了selinux，建议执行其他playbooks之前，先重启系统。

## Role Variables

Available variables are listed below.

###  `defaults/main.yml`
*default lower priority variables for this role*

* `host_name: localhost`

* `packages_base:`
    ```
      - wget
      - lsof
      - sysstat
      - dstat
      - openssh-clients
    ```

* `packages_extension: []`

* `base_selinux_disabled: false`

* `base_nameserver_search: []`

* `base_nameserver_servers:`
    ```
      - 114.114.114.114
      - 8.8.8.8
    ```

###  `vars/RedHat.yml`
*The variables for RedHat/CentOS*

* `service_redhat6:`
    ```
      - ip6tables
      - netfs
      - postfix
      - mdmonitor
      - iscsi
      - iscsid
    ```

* `service_redhat7:`
    ```
      - microcode
      - postfix
      - NetworkManager
    ```

## Dependencies

None.

## Example Playbook

    - name: system base configure
      hosts: servers
      vars:
        host_name: example
        packages_extension:
          - gcc
        base_selinux_disabled: true
        base_nameserver_servers:
          - 114.114.114.114
      roles:
        - base

## License

MIT / BSD

## Author Information

z@zstack.net
