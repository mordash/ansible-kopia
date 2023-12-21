Kopia
==========

This role was used to install and configure kopia with scaleway s3 bucket

Role variables
--------------

| Variable                                     | Type    | Choices                           | Default                 | Example                |
|----------------------------------------------|---------|-----------------------------------|-------------------------|------------------------|
| kopia_ui_install                             | bool    |                                   | false                   |                        |
| kopia_bucket_name                            | string  |                                   |                         | my_bucket              |
| kopia_access_key                             | string  |                                   |                         | SCW1234                |
| kopia_secret_access_key                      | string  |                                   |                         | 111-1111-1111-111-1111 |
| kopia_endpoint                               | string  |                                   | s3.fr-par.scw.cloud     |                        |
| kopia_endpoint_password                      | string  |                                   |                         | secret                 |
| kopia_log_dir                                | string  |                                   | ~/.cache/kopia          |                        |
| kopia_cache_directory                        | string  |                                   | ~/.cache/kopia          |                        |
| kopia_content_cache_size_mb                  | integer |                                   |                         | 5000                   |

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
