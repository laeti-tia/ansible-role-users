The users role
==============

This ansible role takes care of adding user accounts to machines.  Users are defined by:
    - a username
    - some groups
    - some ssh options
    - some additional packages they want to have installed
    - some dotfiles files/repo they want to have in their home directory

It is advised to store the user account passwords in a crypted ansible-vault file.

Requirements
------------

This should work with CentOS 7, Debian 9 and Ubuntu 18 hosts at least.

Role Variables
--------------

In default/main.yml:
    - users_accounts: a list of all users to be managed by the role
    - users_group_names: a list of all groups to be managed by the role
    - users_additional_packages: a list of additional packages to be installed

The `users_accounts` list can contain the following elements defining a user (as per [ansible user module][ansible_user]):
    - name: the username
    - group: the main group
    - groups: all the groups the user belongs to
    - password: the password to be set for the user, must be in a format as recognised by the shadow file, this will then always be set for the user account
    - shell: the shell to be used by the user
    - state: absent|present

A user in the `users_accounts` list can also contain these additional elements:
    - a list defining a "dotfiles" repository that will be installed for the user, this list can contain:
        - dotfiles_repo: a git repository from where to clone the "dotfiles"
        - dotfiles_dest: the destination where to copy the "dotfiles" repository, defaults to '~/.config/dotfiles'
        - dotfiles_command: the command to use to deploy the "dotfiles" repository (used only if defined)

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: smallnodes
      roles:
         - role: users

License
-------

Apache 2.0

Author Information
------------------

Antoine Delvaux - https://github.com/tonin/

This role takes some inspiration from [debops.users][debops_users].


[ansible_user]: https://docs.ansible.com/ansible/latest/modules/user_module.html
[debops_users]: https://docs.debops.org/en/latest/ansible/roles/debops.users/index.html

