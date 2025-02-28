# Как начать работать с {{ mmg-short-name }}

Чтобы начать работу с сервисом:

1. [Создайте кластер](#cluster-create).
1. [Подключитесь к БД](#connect).


## Перед началом работы {#before-you-begin}

1. Перейдите в [консоль управления]({{ link-console-main }}), затем войдите в {{ yandex-cloud }} или зарегистрируйтесь, если вы еще не зарегистрированы.
1. Если у вас еще нет каталога, создайте его:

    {% include [create-folder](../_includes/create-folder.md) %}

1. Подключаться к кластерам БД можно как изнутри, так и извне {{ yandex-cloud }}:
   - Чтобы подключиться изнутри {{ yandex-cloud }}, создайте виртуальную машину на основе [Linux](../compute/quickstart/quick-create-linux.md) или [Windows](../compute/quickstart/quick-create-windows.md) в той же сети, что и кластер БД.
   - Чтобы подключиться к кластеру из интернета, запросите публичный доступ к хостам при создании кластера.

   {% note info %}

   Следующий шаг предполагает, что подключение к кластеру производится с ВМ на основе [Linux](../compute/quickstart/quick-create-linux.md).

   {% endnote %}

1. [Подключитесь](../compute/operations/vm-connect/ssh.md) к виртуальной машине по SSH.
1. Установите MongoDB Shell:

   ```bash
   cd ~/ && \
   wget https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/4.4/multiverse/binary-amd64/mongodb-org-shell_4.4.1_amd64.deb && \
   sudo dpkg -i mongodb-org-shell_4.4.1_amd64.deb
   ```

## Создайте кластер {#cluster-create}

1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором нужно создать кластер БД.
1. Выберите сервис **{{ mmg-name }}**.
1. Нажмите кнопку **Создать кластер**.
1. Задайте параметры кластера и нажмите кнопку **Создать кластер**. Процесс подробно рассмотрен в разделе [{#T}](operations/cluster-create.md).
1. Когда кластер будет готов к работе, его статус сменится на **Running**, а состояние - на **Alive**. Это может занять некоторое время.

## Подключитесь к БД {#connect}

1. Получите SSL-сертификат:

    
    1. Создайте каталог:

        ```bash
        $ mkdir ~/.mongodb
        ```

    1. Получите сертификат:

        ```bash
        $ wget "https://{{ s3-storage-host }}{{ pem-path }}" -O ~/.mongodb/root.crt
        ```

    1. Настройте права доступа к сертификату:

        ```bash
        $ chmod 0600 ~/.mongodb/root.crt
        ```
 
1. Подключитесь к кластеру с помощью {{ MG }} CLI:

    
    ```bash
    $ mongo --norc \
            --ssl \
            --sslCAFile ~/.mongodb/root.crt \
            --host 'rs01/<адрес хоста 1>:27018,<адрес хоста 2>:27018,<адрес хоста N>:27018' \
            -u <имя пользователя> \
            -p <пароль пользователя> \
            <имя БД>
    ```

## Что дальше

- Изучите [концепции сервиса](concepts/index.md).
- Узнайте подробнее о [создании кластера](operations/cluster-create.md) и [подключении к БД](operations/connect.md).
- Ознакомьтесь с [вопросами и ответами](qa/general.md).
