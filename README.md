# Ansible Role: SSH chroot jail config

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-security.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-ssh-chroot-jail)

Configures a chroot jail specifically for the purpose of limiting a set of SSH users to the jail. Useful if you have a server where you need to allow very limited access to a very limited amount of functionality.

## Requirements

Requires OpenSSH server. Doesn't require `geerlingguy.security`, but that role (or one like it) is highly recommended to help lock down your server as much as possible.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    TODO

## Dependencies

None.

## Example Playbook

    - hosts: servers
      roles:
        - geerlingguy.security
        - geerlingguy.ssh-chroot-jail

*Inside `vars/main.yml`*:

    TODO.

## License

MIT (Expat) / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

Special thanks to [Acquia](https://www.acquia.com) for sponsoring the initial development of this role.
