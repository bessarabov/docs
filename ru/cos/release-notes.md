# Релизы COI

## Версия 2.0.3 {#latest-release}

* Включен строгий режим параметра ядра `net.ipv4.conf.all.rp_filter`.
* Исправлена конфигурация утилиты `logrotate`.
* Удален конфигурационный файл Docker `daemon.json`, ошибочно отключающий доступ из Docker-контейнера в интернет.

## Предыдущие релизы {#previous-releases} 

### Версия 2.0.2 {#version2.0.2}

* Закрытие уязвимости CVE-2021-3156.

### Версия 2.0.1 {#version2.0.1}

* Обновлена версия Docker.

### Версия 2.0.0 {#version2.0.0}

* Осуществлен переход на Ubuntu 20.04.

### Версия 1.3.1 {#version1.3.1}

* Исправлено циклическое пересоздание Docker-контейнеров при ошибках доступа к сервису метаданных.

### Версия 1.3.0 {#version1.3.0}

* Добавлена поддержка дисков в COI и Docker Compose спецификациях.

### Версия 1.2.1 {#version1.2.1}

* Улучшена работа с `docker volumes`.

### Версия 1.2.0 {#version1.2.0}

* Добавлена возможность использования службы OS Login, пользователи OS Login автоматически добавляются в группу `docker`.
* Улучшено обновление проектов Docker Compose (добавлен флаг `--delete-orphans` для удаления старой версии проекта).

### Версия 1.1.2 {#version1.1.2}

* Исправления в автоматическом запуске Docker-контейнеров.

### Версия 1.1.1 {#version1.1.1}

* Исправления в автоматическом запуске Docker-контейнеров.

### Версия 1.1.0 {#version1.1.0}

* Добавлена поддержка Docker Compose.

### Версия 1.0.3 {#version1.0.3}

Исправления в автоматическом запуске Docker-контейнеров:
* При перезапуске ВМ и обновлении метаданных устаревший Docker-контейнер теперь не запускается.
* Уменьшено количество логов в `yc-container-daemon`.
* Добавлены повторные попытки обновить контейнер при ошибке обновления Docker-контейнера.

### Версия 1.0.2 {#version1.0.2}

Исправление в автоматическом запуске Docker-контейнеров:
* Добавлено подробное сообщение об ошибке при использовании `docker login` для домена с настроенным Docker Credential Helper.

### Версия 1.0.1 {#version1.0.1}

Исправление в автоматическом запуске Docker-контейнеров:
* Теперь Docker-контейнеры с символом `-` в названии не удаляются.

### Версия 1.0 {#version1.0}

* Первая версия COI на Ubuntu 16.04.

