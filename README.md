Kopia
==========

This role was used to install and configure kopia with scaleway s3 bucket

tags :
- ```kopia``` for install and connect repo
- ```kopia_ui``` to add service for ui
- ```kopia_create``` for init the repo (just run once)
- ```kopia_connect``` just for connect to the repo
- ```kopia_cron``` just for add crontab
- ```kopia_script``` for add scriptt
- ```kopia_exclude``` for add exclude
- ```kopia_readonly``` for make repo readonly
- ```kopia_global_retention``` for change global retention

# First run

If your backend is not initialysed, you need to add this extra var on the first run : ```kopia_create_repo_enable=true```
```bash
ansible-playbook playbooks/my_server.yml -t kopia -e kopia_create_repo_enable=true -DC
```

Bucket variables example on scaleway FR
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
kopia_metadata_cache_size_mb: 5000
kopia_upload_max: 20000000
kopia_repo_readonly: false
```

UI variables example
--------------
```yml
kopia_ui_install: true
kopia_ui_service_enable: true
kopia_ui_service_start: true
kopia_ui_systemd_user: root
kopia_ui_systemd_group: root
kopia_ui_username: admin
kopia_ui_password: super_password
kopia_ui_address: "127.0.0.1:51515"
kopia_ui_log_dir: /var/log/kopia
kopia_ui_insecure: true
kopia_ui_disable_csrf_token_checks: true

```

Cron variables example
--------------
```yml
kopia_cron_enable: true

kopia_cron_directory:
  - name: var_www
    path: /var/www
    cron:
      hour: 3
      minute: 0
      day: '*'
      month: '*'
      weekday: '*'
      user: root
```

Script variables example
--------------
```yml
kopia_script_enable: true
```

Exclude variables example
--------------
will create list of exclude in a file .kopiaignore on declared path
for more information, go on kopia doc : https://kopia.io/docs/advanced/kopiaignore/#kopiaignore-files
```yml
kopia_exclude_list:
  - path: /
    exclude:
      - /var/lib/bareos
      - /dev
      - /media
      - /mnt
      - /proc
      - /run/docker
      - /sys
      - /tmp
      - /var/cache
      - /var/tmp
      - /var/lib/mongodb
      - /var/lib/mysql
      - /var/lib/postgresql
      - /var/lib/redis
      - /var/lib/solr
      - /var/lib/elasticsearch
      - /var/spool/postfix
      - /VMs
      - /.journal
      - /.fsck
      - /zpve
```

Retention variables example
--------------

```yml
kopia_global_retention:
  keep_latest: 10
  keep_hourly: 48
  keep_daily: 7
  keep_weekly: 4
  keep_monthly: 24
  keep_annual: 3
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
| kopia_metadata_cache_size_mb                 | integer | | | 2000 |
| kopia_cron_directory                         | integer | | | 2000 |
| kopia_script_enable                          | bool | true/false | false |  |
| kopia_repo_readonly                          | bool | true/false | false |  |
| kopia_ui_insecure                            | bool | true/false | true |  |
| kopia_ui_disable_csrf_token_checks           | bool | true/false | true |  |
| kopia_ui_systemd_user | string  |  | root | |
| kopia_ui_systemd_group | string  |  | root | |
| kopia_ui_config_file | string | |  |  /root/.config/kopia/repository.config |

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

TODO
----------------
- ajouter de la compression
```
kopia policy set --global --compression=zstd
```

License
-------

GPLv3

Author Information
------------------

Written by Jean-Yves Fournier
