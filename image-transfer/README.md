Ansible role: image-transfer
=========

Выполняет загрузку docker images на удалённые хосты

Requirements
------------

Требуется Docker на целевых хостах и хосте запуска

Role Variables
--------------

Список docker images для передачи на удалённый хост:

    image_transfer_list: []

Директория на локальном хосте для выгрузки docker images в файлы:

    image_transfer_local_path: "/var/tmp/image-transfer-local"

Директория на удалённом хосте, в которую копируются файлы docker images:

    image_transfer_remote_path: "/var/tmp/image-transfer-remote"

Если docker images на удалённом хосте есть, он принудительно удаляется и загружается заново:

    image_transfer_force: false

Кэширующий хост для промежуточной загрузки docker images. После docker images передаются с кэширующего хоста на целевые хосты.

    image_transfer_cache_host: ""

Директория на кэширующим хосте, в которую копируются файлы docker images

    image_transfer_cache_path: "/var/tmp/image-transfer-cache"


Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts:
    - host01
    - host02
    - host03
  gather_facts: false
  strategy: linear
  become: yes

  roles:
    - role: image-transfer
      image_transfer_list:
        - postgres:12.4
        - rabbitmq:3.8.19-management
        - nginx:1.19.10
      image_transfer_cache_host: host01
```

License
-------

BSD

Author Information
------------------

This role was created in 2020 by Andrey Vladimirskiy
