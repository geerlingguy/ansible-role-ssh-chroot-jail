# Ansible Role: SSH chroot jail config

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-security.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-ssh-chroot-jail)

**First, a major, MAJOR caveat**: the security of your servers is YOUR responsibility.

TODO.

Again: Your servers' security is *your* responsibility.

## Requirements

Requires OpenSSH server.

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
