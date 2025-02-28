# Изменение настроек кластера

После создания кластера вы можете:

* [Изменить класс хостов](#change-resource-preset).

* [Увеличить размер хранилища](#change-disk-size) (доступно только для сетевого хранилища, `network-hdd` и `network-ssd`).

* [Настроить серверы](#change-mysql-config) {{ MY }}.

* [Изменить дополнительные настройки кластера](#change-additional-settings).

{% note warning %}

Вы не можете менять настройки серверов {{ MY }} с помощью команд SQL.

{% endnote %}

## Изменить класс хостов {#change-resource-preset}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmy-name }}**.
  1. Выберите кластер и нажмите кнопку **Изменить кластер** на панели сверху.
  1. Чтобы изменить класс хостов {{ MY }}, в блоке **Класс хоста** выберите нужный класс.
  1. Нажмите кнопку **Сохранить изменения**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы изменить [класс хостов](../concepts/instance-types.md) для кластера:

  1. Посмотрите описание команды CLI для изменения кластера:

      ```
      $ {{ yc-mdb-my }} cluster update --help
      ```

  1. Запросите список доступных классов хостов (в колонке `ZONES` указаны зоны доступности, в которых можно выбрать соответствующий класс):

     
     ```
     $ {{ yc-mdb-my }} resource-preset list

     +-----------+--------------------------------+-------+----------+
     |    ID     |            ZONE IDS            | CORES |  MEMORY  |
     +-----------+--------------------------------+-------+----------+
     | s1.micro  | ru-central1-a, ru-central1-b,  |     2 | 8.0 GB   |
     |           | ru-central1-c                  |       |          |
     | ...                                                           |
     +-----------+--------------------------------+-------+----------+
     ```

  1. Укажите нужный класс в команде изменения кластера:

      ```
      $ {{ yc-mdb-my }} cluster update <имя кластера>
           --resource-preset <ID класса>
      ```

      {{ mmy-short-name }} запустит операцию изменения класса хостов для кластера.

- API

  Изменить [класс хостов](../concepts/instance-types.md) кластера можно с помощью метода API [update](../api-ref/Cluster/update.md): передайте в запросе нужное значение в параметре `configSpec.resources.resourcePresetId`.

  Список поддерживаемых значений запрашивайте методом [list](../api-ref/ResourcePreset/list.md) для ресурсов `ResourcePreset`.

{% endlist %}

## Увеличить размер хранилища {#change-disk-size}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmy-name }}**.
  1. Выберите кластер и нажмите кнопку **Изменить кластер** на панели сверху.
  1. В блоке **Размер хранилища** укажите необходимое значение.
  1. Нажмите кнопку **Сохранить изменения**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы увеличить размер хранилища для кластера:

  1. Посмотрите описание команды CLI для изменения кластера:

      ```
      $ {{ yc-mdb-my }} cluster update --help
      ```

  1. Проверьте, что в облаке хватает квоты на увеличение хранилища: откройте страницу [Квоты]({{ link-console-quotas }}) для вашего облака и проверьте, что в секции {{ mmy-full-name }} не исчерпано место в строке **space**.

  1. Проверьте, что нужный кластер использует именно сетевое хранилище (увеличить размер локального хранилища пока невозможно). Для этого запросите информацию о кластере и найдите поле `disk_type_id` — его значение должно быть `network-hdd` или `network-ssd`:

      ```
      $ {{ yc-mdb-my }} cluster get <имя кластера>

      id: c7qkvr3u78qiopj3u4k2
      folder_id: b1g0ftj57rrjk9thribv
      ...
      config:
        ...
        resources:
          resource_preset_id: s1.micro
          disk_size: "10737418240"
          disk_type_id: network-ssd
      ...
      ```

  1. Укажите нужный объем хранилища в команде изменения кластера (должен быть не меньше, чем значение `disk_size` в свойствах кластера):

      ```
      $ {{ yc-mdb-my }} cluster update <имя кластера>
           --disk-size <размер хранилища в ГБ>
      ```

      Если все условия выполнены, {{ mmy-short-name }} запустит операцию по увеличению объема хранилища.

- API

  Изменить размер хранилища для кластера можно с помощью метода API [update](../api-ref/Cluster/update.md): передайте в запросе нужные значения в параметре `configSpec.resources.diskSize`.

  Проверьте, что в облаке хватает квоты на увеличение хранилища: откройте страницу [Квоты]({{ link-console-quotas }}) для вашего облака и проверьте, что в секции {{ mmy-full-name }} не исчерпано место в строке **space**.

{% endlist %}

## Изменить настройки {{ MY }} {#change-mysql-config}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmy-name }}**.
  1. Выберите кластер и нажмите кнопку **Изменить кластер** на панели сверху.
  1. Измените настройки {{ MY }}, нажав на кнопку **Настроить** в блоке **Настройки СУБД**:

     {% include [mmy-dbms-settings](../../_includes/mdb/mmy-dbms-settings.md) %}

  1. Нажмите кнопку **Сохранить**.
  1. Нажмите кнопку **Сохранить изменения**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы изменить настройки сервера {{ MY }}:

  1. Посмотрите описание команды CLI для изменения конфигурации кластера:

      ```
      $ {{ yc-mdb-my }} cluster update-config --help
      ```

  1. Установите нужные значения параметров.

     Все поддерживаемые параметры перечислены в [формате запроса для метода update](../api-ref/Cluster/update.md), в поле `mysql_config_5_7`. Чтобы указать имя параметра в вызове CLI, преобразуйте его имя из вида <q>lowerCamelCase</q> в <q>snake_case</q>, например, параметр `logMinDurationStatement` из запроса к API преобразуется в `log_min_duration_statement` для команды CLI:

     ```
     $ {{ yc-mdb-my }} cluster update-config <имя кластера>
          --set log_min_duration_statement=100,<имя параметра>=<значение>,...
     ```

     {{ mmy-short-name }} запустит операцию по изменению настроек кластера.

- API

  Изменить настройки СУБД для кластера можно с помощью метода API [update](../api-ref/Cluster/update.md): передайте в запросе нужные значения в параметре `configSpec.mysql_config_5_7`.

{% endlist %}

## Изменить дополнительные настройки кластера {#change-additional-settings}

{% list tabs %}

* Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmy-name }}**.
  1. Выберите кластер и нажмите кнопку **Изменить кластер** на панели сверху.
  1. Измените дополнительные настройки кластера:

     {% include [mmy-extra-settings](../../_includes/mdb/mmy-extra-settings-web-console.md) %}

* CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы изменить дополнительные настройки кластера:

    1. Посмотрите описание команды CLI для изменения кластера:

        ```bash
        {{ yc-mdb-my }} cluster update --help
        ```

    1. Выполните команду, передав список настроек, которые хотите изменить:

        ```bash
        {{ yc-mdb-my }} cluster update <имя кластера> \
            --backup-window-start <время начала резервного копирования> \
            --datalens-access=<true или false> \
            --maintenance-window type=<weekly или anytime> \
            --websql-access=<true или false>
        ```

    Вы можете изменить следующие настройки:

    {% include [backup-window-start](../../_includes/mdb/cli-additional-settings/backup-window-start.md) %}

    * `--datalens-access` — разрешает доступ из DataLens. Значение по умолчанию — `false`. Подробнее о настройке подключения см в разделе [{#T}](datalens-connect.md).

    {% include [maintenance-window](../../_includes/mdb/cli-additional-settings/maintenance-window.md) %}

    * `--websql-access` — разрешает [выполнять SQL запросы](web-sql-query.md) из консоли управления. Значение по умолчанию — `false`.

    Имя кластера можно [получить со списком кластеров в каталоге](cluster-list.md#list-clusters).

* API

  Воспользуйтесь методом API [update](../api-ref/Cluster/update.md): передайте в запросе нужные значения в параметрах `configSpec.access` и `configSpec.backupWindowStart`.

{% endlist %}
