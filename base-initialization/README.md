base-initialization
=========

- Устанавливает необходимый минимум пакетов


Role Variables
--------------

`base_initialization_upgrade_system: false`

Если присвоить значение `true`, то перед установкой пакетов будут выполнены обновления apt-кэша и всего дистрибутива.

<br>

`base_initialization_timezone: ""`

Если не указывать значение, то переменная будет проигнорированна.
Если задать значение типа `Europe/Samara` или `Europe/Moscow`, то эта временная зона будет выставлена на хосте.

<br>

```yml
base_initialization_install_list:
  - aptitude
  - apt-transport-https
  - bash-completion
  - ca-certificates
  - curl
  - ffmpeg
  - htop
  - net-tools
  - nmon
  - ntp
  - proftpd-basic
  - python-pip
  - python3-pip
  - screen
  - software-properties-common
  - tcpdump
  - zip
```

Список базовых пакетов

```yml
base_initialization_pip_install_list:
  - docker
  - docker-compose
```
Список pip-пакетов


<br>

Example Playbook
----------------
В примере ниже список `base_initialization_install_list` задаётся пустым.
```yml
- hosts: servers
    roles:
      - role: base-initialization
        base_initialization_upgrade_system: false
        base_initialization_timezone: "Europe/Samara"
        base_initialization_install_list:
```



