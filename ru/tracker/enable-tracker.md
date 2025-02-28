# Как подключить Yandex Tracker

{% note warning %}

Подключение {{ tracker-name }} доступно только пользователям, у которых есть аккаунт на Яндексе.

{% endnote %}

Чтобы начать работу с {{ tracker-full-name }}:

1. [Подключите {{ tracker-name }}](enable-tracker.md#enable).

1. [Добавьте в {{ tracker-name }} сотрудников вашей компании](#add-users).

1. Чтобы сотрудники могли работать с задачами, [разрешите им полный доступ в {{ tracker-name }}](#access). 
   
   Стоимость использования {{ tracker-name }} [зависит от количества пользователей с полным доступом](pricing.md#sec_price).


## Подключить {{ tracker-name }} {#enable}

1. Войдите в ваш [аккаунт на Яндексе]({{ link-passport }}). Если у вас еще нет аккаунта, [создайте]({{ support-passport-create }}) его.

1. Перейдите на [страницу {{ tracker-name }}]({{ link-tracker-promo }}) и нажмите кнопку **Попробовать бесплатно**. 

1. Если ваш аккаунт добавлен в одну или несколько организаций {{ yandex-cloud }}, выберите организацию, в которой вы хотите подключить {{ tracker-name }}, и нажмите кнопку **Войти**. 

   Если у вас нет организации {{ yandex-cloud }} или вы хотите создать новую, задайте название организации, добавьте описание и нажмите кнопку **Создать**.

{{ tracker-full-name }} будет автоматически подключен для выбранной или созданной вами организации.

Подробнее об управлении организацией читайте в документации [{{ org-full-name }}]({{ link-org-main }}).

## Добавить пользователей {#add-users}

Пригласите в {{ tracker-name }} пользователей, у которых есть аккаунты на Яндексе, создайте новые аккаунты на домене организации или настройте федерацию удостоверений. 

С помощью федерации удостоверений сотрудники смогут использовать для входа в {{ tracker-name }} свои рабочие аккаунты в Active Directory, Google Workspace или других системах управления учетными записями пользователей.

<!--{% note warning %}
В одну организацию можно добавить не более 1000 сотрудников. Если вам не хватает этого количества, [обратитесь в службу поддержки]({{ link-console-support }}).

{% endnote %}-->

#### Пригласить пользователей {#invite_user}

Вы можете пригласить людей присоединиться к вашей организации со своими аккаунтами на Яндексе, например `{{ example-account }}`:

1. Откройте [страницу {{ tracker-name }}]({{ link-tracker }}) и [войдите в аккаунт администратора организации](user/login.md).

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Управление доступом**.

1. Нажмите кнопку **Пригласить пользователей**.

1. Перечислите через запятую почтовые адреса сотрудников на Яндексе (например, `{{ example-account }}`) и нажмите кнопку **Пригласить**. <!--Каждый пользователь получит письмо с предложением вступить в организацию.-->

<!--1. Чтобы создать ссылку-приглашение, включите опцию **Включить доступ по ссылке**. Ссылку может быть удобно отправить в мессенджере или опубликовать на сайте.-->

Чтобы войти в {{ tracker-name }}, приглашенным сотрудникам нужно будет перейти по ссылке [{{ link-tracker }}]({{ link-tracker }}) и [войти в свой аккаунт на Яндексе](user/login.md).

#### Настроить федерацию удостоверений {#federation}

Федерация удостоверений — это технология, которая позволяет реализовать систему единого входа (Single Sign-On, SSO) и использовать для авторизации в {{tracker-full-name}} корпоративные аккаунты в Active Directory, Google Workspace или других SAML-совместимых системах управления учетными записями пользователей.

Чтобы создать федерацию удостоверений:

1. Откройте [страницу {{ tracker-name }}]({{ link-tracker }}) и [войдите в аккаунт администратора организации](user/login.md).

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Управление доступом**.

1. Нажмите кнопку **Подключить федерацию**. Откроется страница сервиса {{ org-full-name }}.

1. Нажмите кнопку **Создать федерацию** и задайте настройки федерации.

Пользователи с корпоративными аккаунтами смогут [войти в {{ tracker-name }}](user/login.md) с помощью кнопки **Войти через SSO**.

Подробнее о создании федерации читайте в документации [{{ org-full-name }}]({{ link-org-add-federation }}).

#### Создать аккаунты пользователей {#create_users}

Чтобы создать новый аккаунты пользователя: 

1. Откройте [страницу {{ tracker-name }}]({{ link-tracker }}) и [войдите в аккаунт администратора организации](user/login.md).

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Управление доступом**.

1. Справа от кнопки **Пригласить пользователей** нажмите значок ![](../_assets/tracker/add_user.png) и выберите **Создать аккаунт пользователя**.

   {% note info %}

   Если к вашей организации не подключен почтовый домен, нажмите кнопку **Подключить домен** и добавьте домен в сервисе [Яндекс.Почта 360 для бизнеса](https://admin.yandex.ru). Подробнее читайте в [Справке сервиса]({{ support-business-domain }}). Затем вернитесь в аккаунт администратора {{ tracker-name }} и нажмите **Создать аккаунт пользователя**.

   {% endnote %}

1. Заполните форму **Новый аккаунт пользователя** и нажмите **Добавить**.

Чтобы [войти в {{ tracker-name }}](user/login.md), сотруднику с аккаунтом на домене нужно будет ввести полный почтовый адрес (например, `login@example.com`) и пароль.

## Настроить доступ к {{ tracker-name }} {#access}

Все сотрудники организации автоматически получают бесплатный доступ к {{ tracker-name }} в режиме [<q>Только чтение</q>](#readonly). Чтобы сотрудники могли работать с задачами без ограничений, разрешите им полный доступ к {{ tracker-name }}.

{% note info %}

Организации, которые подключили {{ tracker-name }} с 1 до 31 марта 2021 года, смогут бесплатно использовать сервис в течение первого месяца в режиме **Пробный период**.
Затем сотрудники, которым администратор не назначит режим **Полный доступ**, автоматически получат доступ **Только чтение**.

{% endnote %}

Стоимость использования {{ tracker-name }} зависит от количества пользователей с полным доступом. Команды, в которых не более 5 сотрудников, могут работать с {{ tracker-name }} бесплатно. 

Выдавать и отзывать полный доступ к {{ tracker-name }} можно в любое время — стоимость автоматически пересчитывается с учетом того, как меняется количество пользователей с полным доступом. Подробнее читайте в разделе [Расчет стоимости](pricing.md#sec_calculate).


#### Настроить доступ

<!--1. Если вы настраиваете доступ к {{ tracker-name }} впервые, [укажите ваши данные для создания платежного аккаунта](pricing.md#payment_data).

    {% note info %}

    Платежные данные понадобятся для оплаты услуг, если вы будете использовать [платные тарифы {{ tracker-name }}](pricing.md#sec_price).

    {% endnote %}-->

1. Откройте [страницу {{ tracker-name }}]({{ link-tracker }}) и [войдите в аккаунт администратора организации](user/login.md).

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Управление доступом**.

1. В разделе **Все пользователи** для сотрудников, которые будут работать с задачами в {{ tracker-name }}, в столбце **Доступ** выберите **Полный доступ**. 


После настройки доступа в левом нижнем углу страницы отобразится количество сотрудников с полным доступом к {{ tracker-name }} и сумма ежемесячного платежа. Подробнее читайте в разделе [Правила тарификации](pricing.md).

#### Режим <q>Только чтение</q> {#readonly}

В режиме <q>Только чтение</q> пользователи не могут:

- создавать задачи с помощью интерфейса {{ tracker-name }};

- изменять параметры задач, их статусы и резолюции;

- комментировать задачи;

- подписываться на изменения задач.

При этом пользователям доступны все возможности {{ tracker-name }}, связанные с просмотром задач:

- просматривать задачи, [дашборды](user/dashboard.md) и [доски задач](manager/agile.md#sec_boards);

- искать задачи с помощью [конструктора фильтров](user/create-filter.md) и [языка запросов](user/query-filter.md);

- просматривать [страницы очередей](manager/quick-filters.md), [статистику](manager/statistics.md) и так далее.

## Тарифы {{ tracker-name }} {#sec_price}

<!--Первые 30 дней {{ tracker-name }} доступен всем сотрудникам бесплатно и без ограничений. После окончания пробного периода у сотрудников сохранится возможность бесплатно работать с {{ tracker-name }} в режиме [<q>Только чтение</q>](#readonly). Чтобы использовать все возможности {{ tracker-name }}, разрешите сотрудникам [полный доступ](#access).-->

Информацию о тарифах и пример расчета ежемесячной платы за использование {{ tracker-name }} вы найдете в разделе [Правила тарификации](pricing.md).

