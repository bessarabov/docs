# Создание {{ MY }}-кластера

{{ MY }}-кластер — это один или несколько хостов базы данных, между которыми можно настроить репликацию. Репликация работает по умолчанию в любом кластере из более чем 1 хоста: хост-мастер принимает запросы на запись, синхронно дублирует изменения в основной реплике и асинхронно — во всех остальных.


Количество хостов, которые можно создать вместе с {{ MY }}-кластером, зависит от выбранного варианта хранилища:

- при использовании сетевых дисков доступное количество хостов ограничено текущей [квотой](../concepts/limits.md);
- при использовании SSD-дисков вместе с кластером создаются минимум 3 реплики, чтобы обеспечить отказоустойчивость.

{% note info %}

Если хранилище баз данных заполнится на 95%, кластер перейдет в режим только чтения. Увеличивайте размер хранилища заранее.

{% endnote %}

## Как создать кластер {{ MY }} {#create-cluster}

{% list tabs %}

- Консоль управления

  1. В консоли управления выберите каталог, в котором нужно создать кластер БД.
  1. Выберите сервис **{{ mmy-name }}**.
  1. Нажмите кнопку **Создать кластер**.
  1. Введите имя кластера в поле **Имя кластера**. Имя кластера должно быть уникальным в рамках {{ yandex-cloud }}.
  1. Выберите окружение, в котором нужно создать кластер (после создания кластера окружение изменить невозможно):
      - `PRODUCTION` — для стабильных версий ваших приложений.
      - `PRESTABLE` — для тестирования, в том числе самого сервиса {{ mmy-short-name }}. В Prestable-окружении раньше появляются новая функциональность, улучшения и исправления ошибок. При этом не все обновления обеспечивают обратную совместимость.
  1. Выберите версию СУБД.
  1. Выберите класс хостов — он определяет технические характеристики виртуальных машин, на которых будут развернуты хосты БД. Все доступные варианты перечислены в разделе [{#T}](../concepts/instance-types.md). При изменении класса хостов для кластера меняются характеристики всех уже созданных хостов.
  1. В блоке **Размер хранилища**:
      - Выберите тип хранилища — более гибкое сетевое (**network-hdd** или **network-ssd**) или более быстрое локальное хранилище (**local-ssd**). Размер локального хранилища можно менять только с шагом 100 ГБ.
      - Выберите объем, который будет использоваться для данных и резервных копий. Подробнее о том, как занимают пространство резервные копии, см. раздел [{#T}](../concepts/backup.md).
  1. В блоке **База данных** укажите атрибуты БД:

      - Имя базы данных. Имя БД должно быть уникальным в рамках каталога и содержать только латинские буквы, цифры и подчеркивания.
      - Имя пользователя — владельца БД. Имя пользователя должно содержать только латинские буквы, цифры и подчеркивания.
      - Пароль пользователя, от 8 до 128 символов.

  1. В блоке **Хосты** выберите параметры хостов БД, создаваемых вместе с кластером (помните, что используя SSD-диски при создании {{ MY }}-кластера можно задать не меньше 3 хостов). Открыв блок **Расширенные настройки**, вы можете выбрать конкретные подсети для каждого хоста — по умолчанию каждый хост создается в отдельной подсети.

  1. При необходимости задайте дополнительные настройки кластера:

     {% include [mmy-extra-settings](../../_includes/mdb/mmy-extra-settings-web-console.md) %}

  1. При необходимости задайте настройки СУБД:

     {% include [mmy-dbms-settings](../../_includes/mdb/mmy-dbms-settings.md) %}

  1. Нажмите кнопку **Создать кластер**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы создать кластер:

  1. Проверьте, есть ли в каталоге подсети для хостов кластера:

     ```
     $ yc vpc subnet list
     ```

     Если ни одной подсети в каталоге нет, [создайте нужные подсети](../../vpc/operations/subnet-create.md) в сервисе {{ vpc-short-name }}.

  1. Посмотрите описание команды CLI для создания кластера:

      ```
      $ {{ yc-mdb-my }} cluster create --help
      ```

  1. Укажите параметры кластера в команде создания:

     ```
     $ {{ yc-mdb-my }} cluster create \
        --name=<имя кластера> \
        --environment <окружение, prestable или production> \
        --network-name <имя сети> \
        --host zone-id=<зона доступности>,subnet-id=<идентификатор подсети> \
        --mysql-version <версия MySQL> \
        --resource-preset <класс хоста> \
        --user name=<имя пользователя>,password=<пароль пользователя> \
        --database name=<имя базы данных>
     ```

      Идентификатор подсети `subnet-id` необходимо указывать, если в выбранной зоне доступности создано 2 и больше подсетей.

- Terraform

  {% include [terraform-definition](../../solutions/_solutions_includes/terraform-definition.md) %}

  Если у вас ещё нет Terraform, [установите его и настройте провайдер](../../solutions/infrastructure-management/terraform-quickstart.md#install-terraform).

  Чтобы создать кластер:

  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

     {% include [terraform-create-cluster-step-1](../../_includes/mdb/terraform-create-cluster-step-1.md) %}

     Пример структуры конфигурационного файла:

     ```
     resource "yandex_mdb_mysql_cluster" "<имя кластера>" {
       name        = "<имя кластера>"
       environment = "<окружение, PRESTABLE или PRODUCTION>"
       network_id  = "<идентификатор сети>"
       version     = "<версия MySQL: 5.7 или 8.0>"

       resources {
         resource_preset_id = "<класс хоста>"
         disk_type_id       = "<тип хранилища>"
         disk_size          = "<размер хранилища в гигабайтах>"
       }

       database {
         name = "<имя базы данных>"
       }

       user {
         name     = "<имя пользователя>"
         password = "<пароль пользователя>"
         permission {
           database_name = "<имя базы данных>"
           roles         = ["ALL"]
         }
       }

       host {
         zone      = "<зона доступности>"
         subnet_id = "<идентификатор подсети>"
       }
     }

     resource "yandex_vpc_network" "<имя сети>" { name = "<имя сети>" }

     resource "yandex_vpc_subnet" "<имя подсети>" {
       name           = "<имя подсети>"
       zone           = "<зона доступности>"
       network_id     = "<идентификатор сети>"
       v4_cidr_blocks = ["<диапазон>"]
     }
     ```

     Более подробную информацию о ресурсах, которые вы можете создать с помощью Terraform, см. в [документации провайдера](https://www.terraform.io/docs/providers/yandex/r/mdb_mysql_cluster.html).

  1. Проверьте корректность конфигурационных файлов.

     {% include [terraform-create-cluster-step-2](../../_includes/mdb/terraform-create-cluster-step-2.md) %}

  1. Создайте кластер.

     {% include [terraform-create-cluster-step-3](../../_includes/mdb/terraform-create-cluster-step-3.md) %}

{% endlist %}


## Примеры {#examples}

### Создание кластера с одним хостом {#creating-a-single-host-cluster}

{% list tabs %}

- CLI

  Чтобы создать кластер с одним хостом, следует передать один параметр `--host`.

  Допустим, нужно создать {{ MY }}-кластер со следующими характеристиками:

    
    - С именем `my-mysql`.
    - Версии `8.0`.
    - В окружении `production`.
    - В сети `default`.
    - С одним хостом класса `{{ host-class }}` в подсети `{{ subnet-id }}`, в зоне доступности `{{ zone-id }}`.
    - С быстрым сетевым хранилищем (`{{ disk-type-example }}`) объемом 20 Гб.
    - С одним пользователем (`user1`), с паролем `user1user1`.
    - С одной базой данных `db1`, в которой пользователь `user1` имеет полные права (эквивалент `GRANT ALL PRIVILEGES on db1.*`).

  1. Запустите команду создания кластера:

      
      ```bash
      {{ yc-mdb-my }} cluster create \
         --name="my-mysql" \
         --mysql-version 8.0 \
         --environment=production \
         --network-name=default \
         --host zone-id={{ host-net-example }} \
         --resource-preset {{ host-class }} \
         --disk-type {{ disk-type-example }} \
         --disk-size 20 \
         --user name=user1,password="user1user1" \
         --database name=db1
      ```

  1. Запустите команду изменения привилегий пользователя `user1`.

      ```bash
      {{ yc-mdb-my }} user grant-permission user1 \
         --cluster-name="my-mysql" \
         --database=db1 \
         --permissions ALL
      ```

- Terraform

  Допустим, нужно создать {{ MY }}-кластер и сеть для него со следующими характеристиками:
  - С именем `my-mysql`.
  - Версии `8.0`.
  - В окружении `PRESTABLE`.
  - В облаке с идентификатором `{{ tf-cloud-id }}`.
  - В каталоге `myfolder`.
  - В новой сети `mynet`.
  - С одним хостом класса `{{ host-class }}` в новой подсети `mysubnet`, в зоне доступности `{{ zone-id }}`. Подсеть `mysubnet` будет иметь диапазон `10.5.0.0/24`.
  - С быстрым сетевым хранилищем (`{{ disk-type-example }}`) объемом 20 ГБ.
  - С одним пользователем (`user1`), с паролем `user1user1`.
  - С одной базой данных `db1`, в которой пользователь `user1` имеет полные права (эквивалент `GRANT ALL PRIVILEGES on db1.*`).

  Конфигурационный файл для такого кластера выглядит так:

  ```
  provider "yandex" {
    token     = "<OAuth или статический ключ сервисного аккаунта>"
    cloud_id  = "{{ tf-cloud-id }}"
    folder_id = "${data.yandex_resourcemanager_folder.myfolder.id}"
    zone      = "{{ zone-id }}"
  }

  resource "yandex_mdb_mysql_cluster" "my-mysql" {
    name        = "my-mysql"
    environment = "PRESTABLE"
    network_id  = "${yandex_vpc_network.mynet.id}"
    version     = "8.0"

    resources {
      resource_preset_id = "{{ host-class }}"
      disk_type_id       = "{{ disk-type-example }}"
      disk_size          = 20
    }

    database {
      name = "db1"
    }

    user {
      name     = "user1"
      password = "user1user1"
      permission {
        database_name = "db1"
        roles         = ["ALL"]
      }
    }

    host {
      zone      = "{{ zone-id }}"
      subnet_id = "${yandex_vpc_subnet.mysubnet.id}"
    }
  }

  resource "yandex_vpc_network" "mynet" { name = "mynet" }

  resource "yandex_vpc_subnet" "mysubnet" {
    name           = "mysubnet"
    zone           = "{{ zone-id }}"
    network_id     = "${yandex_vpc_network.mynet.id}"
    v4_cidr_blocks = ["10.5.0.0/24"]
  }
  ```
