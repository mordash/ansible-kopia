Kopia
==========

This role was used to install and configure kopia with scaleway s3 bucket

tags :
- kopia for install and connect repo
- kopia_ui to add service for ui
- kopia_create for init the repo (just run once)
- kopia connect just for connect to the repo

If your backend is not initialysed, you need to add this var on the first run : ```kopia_create_repo_enable: true```, then remove it

If you want install, enable the ui service or start the ui service use :

```yml
kopia_ui_install: true
kopia_ui_service_enable: true
kopia_ui_service_start: true
```

Backend variables example on scaleway FR
--------------
```yml
kopia_bucket_name: my_bucket
kopia_access_key: SCW11111111
kopia_secret_access_key: 111111-11111-1111-1111-111111
kopia_endpoint: s3.fr-par.scw.cloud
kopia_endpoint_password: toto
kopia_log_dir: /var/backup_test/kopia/log
kopia_cache_directory: /var/backup_test/kopia/cache-dir/
kopia_content_cache_size_mb: 5000
kopia_upload_max: 20000000

kopia_directory:
  - name: var_www
    path: /var/www
```

UI variables example
--------------
```yml
kopia_ui_username: admin
kopia_ui_password: super_password
kopia_ui_address: "127.0.0.1:51515"
kopia_ui_log_dir: /var/log/kopia
```

Cron variables example
--------------
```yml
kopia_cron_enable: true
kopia_cron_minute: 0
kopia_cron_hour: 3
kopia_cron_day: '*'
kopia_cron_month: '*'
kopia_cron_num_day: '*'
kopia_cron_user: 'root'
```


Role variables
--------------

TODO : refaire cette liste

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
```yml
---
#
# ansible-galaxy -r install requirements.yml
# or
# ansible-galaxy install -r requirements.yml
#
- src: git+ssh://git@github.com/mordash/ansible-kopia.git
  version: main
  name: ansible-kopia
```

License
-------

GPLv3

Author Information
------------------

Written by Jean-Yves Fournier
