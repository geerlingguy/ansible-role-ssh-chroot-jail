# Ansible Role: SSH chroot jail config

[![CI](https://github.com/geerlingguy/ansible-role-ssh-chroot-jail/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-ssh-chroot-jail/actions?query=workflow%3ACI)

Configures a chroot jail specifically for the purpose of limiting a set of SSH users to the jail. Useful if you have a server where you need to allow very limited access to a very limited amount of functionality.

## Requirements

Requires OpenSSH server. Doesn't require `geerlingguy.security`, but that role (or one like it) is highly recommended to help lock down your server as much as possible.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ssh_chroot_jail_path: /var/jail

The path to the root of the chroot jail.

    ssh_chroot_jail_group_name: ssh_jailed

The group into which jailed users should be added.

    ssh_chroot_jail_users:
      - name: foo
        home: /home/foo
        shell: /bin/bash

A list of users who should be in the chroot jail. Leave set to the default (`[]`) if you would like to manage users on your own.

    ssh_chroot_jail_dirs:
      - bin
      - dev
      - etc
      - lib
      - lib64
      - usr/bin
      - usr/lib
      - usr/lib64
      - home

Base directories that should exist in the jail.

    ssh_chroot_jail_devs:
      - { dev: 'null', major: '1', minor: '3' }
      - { dev: 'random', major: '5', minor: '0' }
      - { dev: 'urandom', major: '1', minor: '5' }
      - { dev: 'zero', major: '1', minor: '8' }

Devices that should exist in the jail.

    ssh_chroot_bins:
      - /bin/cp
      - /bin/sh
      - /bin/bash
      - /bin/ls
      ...
      - /usr/bin/tail
      - /usr/bin/head
      - /usr/bin/awk
      - /usr/bin/wc
      ...
      - bin: /usr/bin/which
        l2chroot: false

A list of binaries which should be copied over to the jail. Each binary will also have its library dependencies copied into the jail using the `l2chroot` script included with this role; you can skip that task by setting the `bin` key explicitly and setting `l2chroot: false` as in the last example above.

    ssh_chroot_l2chroot_template: l2chroot.j2
    ssh_chroot_l2chroot_path: /usr/local/bin/l2chroot

The download URL and path into which `l2chroot` should be installed.

    ssh_chroot_copy_extra_items:
      - /etc/hosts
      - /etc/passwd
      - /etc/group
      - /etc/ld.so.cache
      - /etc/ld.so.conf
      - /etc/nsswitch.conf

Extra items which should be copied into the jail.

    ssh_chroot_sshd_chroot_jail_config: |
      Match group {{ ssh_chroot_jail_group_name }}
          ChrootDirectory {{ ssh_chroot_jail_path }}
          X11Forwarding no
          AllowTcpForwarding no

Configuration to add to the server's `sshd_config` controlling how users in the chroot jail group are handled.

    ssh_chroot_jail_dirs_recurse: true

When adding jail directories, whether the directory addition should be done recursively or not. If you have many directories with thousands of files, and/or have the directories on a slow filesystem, this should be set to `false`.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      become: yes
      roles:
        - geerlingguy.security
        - geerlingguy.ssh-chroot-jail

*Inside `vars/main.yml`*:

    ssh_chroot_jail_users:
      - name: janedoe
        home: /home/janedoe
        shell: /bin/bash

## License

MIT (Expat) / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

Special thanks to [Acquia](https://www.acquia.com) for sponsoring the initial development of this role.
