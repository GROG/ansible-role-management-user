# Management user

[![Ansible Galaxy](http://img.shields.io/badge/galaxy-GROG.management--user-660198.svg?style=flat)](https://galaxy.ansible.com/GROG/management-user)
[![Build Status](https://travis-ci.org/GROG/ansible-role-management-user.svg?branch=master)](https://travis-ci.org/GROG/ansible-role-management-user)

A role for managing a management user.

## Requirements

- Hosts should be bootstrapped for ansible usage (have python,...)
- Root privileges, eg `become: yes`
- `useradd`, `userdel` and `usermod` should be available on the host
- sudo should be available **(attention: this role will enable sudoers.d if not
  enabled)**

## Role Variables

| Variable | Description | Default value |
|----------|-------------|---------------|
| `management_user_list` | List of management users | `[ management_user_settings ]` |
| `management_user_list_host` | List of management users | `[]` |
| `management_user_list_group` | List of management users | `[]` |
| `management_user_settings` | Settings for the management user **(see details!)** | see details |

`management_user_list`, `_list_host` and `_list_group` are merged when managing the
users. You can use the host and group lists to specify users per host or group
off hosts.

#### `management_user_settings` details

By default a user with following data will be created;

```yaml
management_user_settings:
  name: management
  comment: Ansible
  shell: '/bin/bash'
  authorized_keys:
    - key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
  sudo:
    hosts: ALL
    as: ALL
    commands: ALL
    nopasswd: yes
```

It is however recomended to use your own custom user settings. More
information about the available attributes can be found in the documentation of
the GROG [user](https://galaxy.ansible.com/list#/roles/4730),
[authorized-key](https://galaxy.ansible.com/list#/roles/4737) and
[sudo](https://galaxy.ansible.com/list#/roles/4765) roles.

## Dependencies

- [GROG.user](https://galaxy.ansible.com/list#/roles/4730)
- [GROG.authorized-key](https://galaxy.ansible.com/list#/roles/4737)
- [GROG.sudo](https://galaxy.ansible.com/list#/roles/4765)

## Example Playbook

```yaml
---
- hosts: all
  roles:
  - { role: GROG.management-user, become: yes }
```

## License

LGPLv3

## Contributing

All assistance, changes or ideas [welcome](https://github.com/GROG/ansible-role-management-user/issues)!

## Author Information

By [G. Roggemans](https://github.com/groggemans)
