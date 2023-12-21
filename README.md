Kopia
==========

Role variables
--------------

| Variable                                     | Type    | Choices                           | Default                 | Comment         |
|----------------------------------------------|---------|-----------------------------------|-------------------------|-----------------|
| kopia_xyz                                    | string  |                                   | xyz                     |                 |


Example Playbook
----------------
```yml
---
- hosts: localhost
  gather_facts: yes
  ignore_errors: "{{ ansible_check_mode }}" # ignore errors only in check mode !

  roles:
    - { role: ansible-kopia,          tags: ['kopia'] }
```


Requirement file
----------------
#
# ansible-galaxy -r install requirements.yml
# or
# ansible-galaxy install -r requirements.yml
#
- src: git+ssh://git@github.com/mordash/ansible-kopia.git
  version: main
  name: ansible-kopia


License
-------

GPLv3

Author Information
------------------

Written by Jean-Yves Fournier
