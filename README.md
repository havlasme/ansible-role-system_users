system_users
============

[![Ansible Galaxy][galaxy_image]][galaxy_link]
[![Build Status][travis_image]][travis_link]
[![Latest Tag][tag_image]][tag_link]

An [Ansible](https://www.ansible.com/) role to manage system users.

User `root` can't be managed using this role for security reasons.

Requirements
------------

None.

Role Variables
--------------

```yaml
# separate user specification for ansible needs (matches system users specification)
system_users__ansible: []

# list of system users
system_users__list: []
## user name
#  - name: string
## OPTIONAL: should specified groups be appended
#    append: bool
## OPTIONAL: user description (GECOS)
#    comment: string
## OPTIONAL: should be home directory created if it does not exists
#    createhome: bool
## OPTIONAL: user expiration time
#    expires: date
## OPTIONAL: should user removal be forced
#    force: bool
## OPTIONAL: primary user group
#    group: string
## OPTIONAL: list of additional user groups, all groups are removed if empty
#    groups: [ string ]
## OPTIONAL: user home directory
#    home: string
## OPTIONAL: group of user home directory
#    home_group: string
## OPTIONAL: access mode of user home directory
#    home_mode: int
## OPTIONAL: owener of user home directory
#    home_owner: string
## OPTIONAL: should be user home directory moved, if it's location differs
#    move_home: bool
## OPTIONAL: user password
#    password: string
## OPTIONAL: should be user home directory removed, when user is removed
#    remove: bool
## OPTIONAL: user's default shell
#    shell: string
## OPTIONAL: skeleton for home directory creation
#    skeleton: string
## OPTIONAL: system user flag
#    system: bool
## OPTIONAL: user id
#    uid: int
## OPTIONAL: password update behavior
#    update_password: bool
## OPTIONAL: should be SSH key generated, if the isn't one
#    generate_ssh_key: bool
## OPTIONAL: bit lenght of generated SSH key
#    ssh_key_bits: int
## OPTIONAL: comment for generated SSH key
#    ssh_key_comment: string
## OPTIONAL: location of file containing generated SSH key
#    ssh_key_file: string
## OPTIONAL: passphrase used to encrypt generated SSH key
#    ssh_key_passphrase: string
## OPTIONAL: type of generated SSH key
#    ssh_key_type: string
## OPTIONAL: if set to true, user is removed from host
#    disabled: bool

# list of default groups for all users managed by role
# to ignore these for selected user, that must have set option "append" to false in it's specification
system_users__default_groups_list: []

# should be default groups appended to potential existing user's group
system_users__default_groups_append: true
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: "tomashavlas.system_users"
      system_users__ansible:
        - name: "ansible"
          uid: 1500
          system: true

      system_users__list:
        - name: "commonuser"
        - name: "userhomedir"
          createhome: true
          home_owner: "userhomedir"
          home_mode: 0750
          generate_ssh_key: true
          ssh_key_bits: 4096
          ssh_key_comment: "test_ssh_key"
```

For more examples see [test cases](https://github.com/tomashavlas/ansible-role-system_users/tree/master/tests).

License
-------

BSD

Author Information
------------------

Created by [Tomáš Havlas](https://github.com/tomashavlas) in 2016.

[galaxy_image]: https://img.shields.io/badge/galaxy-tomashavlas.system__users-blue.svg?style=flat
[galaxy_link]: https://galaxy.ansible.com/tomashavlas/system_users/
[tag_image]: https://img.shields.io/github/tag/tomashavlas/ansible-role-system_users.svg
[tag_link]: https://github.com/tomashavlas/ansible-role-system_users/tags
[travis_image]: https://travis-ci.org/tomashavlas/ansible-role-system_users.svg?branch=master
[travis_link]: https://travis-ci.org/tomashavlas/ansible-role-system_users/
