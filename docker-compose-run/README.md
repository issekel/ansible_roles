Ansible role: docker-compose-run
=========

Запускает сервис, описанный в docker-compose.yaml

Requirements
------------

Требуется Docker и docker-compose на целевых хостах

Role Variables
--------------

Список сервисов для запуска. Каждый сервис называется как каталог, в котором находится файл docker-compose.yaml:

    docker_compose_run_services_list: ""


Каталог на локальном хосте, в котором находятся каталоги с сервисами для запуска:

    docker_compose_run_local_services_dir: ""

Каталог на удалённом хосте, в котором находятся каталоги с сервисами для запуска:

    docker_compose_run_remote_services_dir: "/opt/services"

Префикс добавляется в название сервиса на удалённом хосте:

    docker_compose_run_remote_service_prefix: ""


Что с сервисом должна сделать эта роль.

    docker_compose_run_action: present

Возможные значения:

    present - скопировать каталог-сервис, загрузить docker images, запустить сервис в бэкграунде. Выполняется docker-compose up -d

    present-and-wait-until-end - тоже, что и present только сервис запускается не в бэкграунде. Выполняется docker-compose up

    absent - остановить и удалить контейнер. Выполняется docker-compose down

    absent-and-delete - тоже, что и absent плюс удаление каталога с сервисом

    copy - каталог с сервисом только копируется на удалённый хост без запуска

    pull - тоже, что и copy плюс выполняется загрузка docker images


Переменные docker_compose_run_registry_* используются для авторизации в приватном docker registry:

    docker_compose_run_registry_hostname: ""
    docker_compose_run_registry_username: ""
    docker_compose_run_registry_password: ""
    docker_compose_run_registry_login_befor: no
    docker_compose_run_registry_logout_after: no


Пауза в секундах перед выполнением роли:
```
docker_compose_run_timeout_befor:
  seconds: 0
  message: "Wait a few seconds"
```

Пауза в секундах после выполнения роли:
```
docker_compose_run_timeout_after:
  seconds: 0
  message: "Wait a few seconds"
```

Передавать или нет docker images с локального хоста на удалённый. Позволяет отказаться от авторизации в приватном docker registry на удалённом хосте. Используется внешняя роль
image-transfer:

    #docker_compose_run_transfer_images: false
    inventory_transfer_images: yes



Dependencies
------------

Ansible role: image-transfer

Example Playbook
----------------
```yaml
- hosts:
    - host01
  gather_facts: true
  strategy: linear
  become: yes

  roles:
    - role: docker-compose-run
      docker_compose_run_local_common_services_dir: "./services"
      docker_compose_run_action: present
      docker_compose_run_services_list:
        - redis
```

License
-------

BSD
