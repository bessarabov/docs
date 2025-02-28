# О сервисе {{ ml-platform-name }}

{{ ml-platform-full-name }} — среда для ML-разработки, которая сочетает в себе привычный интерфейс Jupyter® Notebook, технологию бессерверных вычислений и возможность бесшовного использования разных конфигураций вычислительных ресурсов. {{ ml-platform-full-name }} помогает значительно сократить стоимость машинного обучения по сравнению с вычислениями на собственном оборудовании или на других облачных платформах.

Если вы ещё не пользовались Jupyter Notebook, то попробуйте: ноутбуки удобны тем, что позволяют вам исполнять код последовательно и сразу визуализировать результаты. Ноутбуки также удобно использовать для подготовки аналитических отчетов и статей: между ячейками кода вы можете добавлять пояснения на языке [Markdown](https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/Working%20With%20Markdown%20Cells.html).

## Преимущества сервиса {#advantages}

### Среда разработки, готовая к использованию {#ready-to-use}

Вам не нужно тратить время на создание и обслуживание виртуальных машин — при создании нового [проекта](project.md), автоматически выделяются вычислительные ресурсы для решения ваших задач.

На виртуальной машине уже установлена среда разработки JupyterLab и пакеты для анализа данных и машинного обучения (TensorFlow, Keras, NumPy и другие) — вы можете сразу начать их использовать. Полный список [предустановленных пакетов](preinstalled-packages.md).

Если какого-то пакета вам не хватает, вы можете [установить его](../operations/projects/install-dependencies.md) прямо из ноутбука.

### Автоматическое обслуживание вычислительных ресурсов {#auto-service}

Сервис автоматически управляет выделением ресурсов. Если вы не будете производить вычисления, сервис не будет выделять ресурсы. Если вы используете функции режима раннего доступа, объемы использования ядер процессора и памяти показываются прямо в интерфейсе ноутбука.

### Сохранение состояния при завершении работы {#save-state}

Если вы закроете вкладку с ноутбуком, состояние интерпретатора, все переменные и результаты вычислений сохранятся. Вы сможете продолжить работу, когда снова откроете проект.

{% include [include](../../_includes/datasphere/saving-variables-warn.md) %}

### Управление вычислительными ресурсами {#control-computing-resources}

Для разных задач нужны разные вычислительные ресурсы. Для одних задач достаточно обычного процессора, а для других нужен графический процессор.

В {{ ml-platform-name }} доступны разные [конфигурации](configurations.md) вычислительных ресурсов. По умолчанию проект запускается с минимальной конфигурацией <q>S</q> (32 ГБ RAM и 2 vCPU).

Вы можете [изменить конфигурацию](../operations/projects/control-compute-resources.md) в любой момент в процессе работы. Состояние интерпретатора сохранится.

### Вы сможете поделиться вашими результатами {#share-results}

Вы можете [экспортировать ноутбук в формат HTML](../operations/projects/publication.md) со всеми результатами расчетов и пояснениями к ячейкам и поделиться ссылкой на отчет в этом формате. Экспорт в других форматах сейчас недоступен.

## Существующие ограничения сервиса {#known-restrictions}

Подробнее об ограничениях сервиса читайте в разделе [{#T}](limits.md).

## Режим раннего доступа {#early-access}

Опробуйте новые функции {{ ml-platform-name }} до их релиза в [режиме раннего доступа](../early-access/index.md) и поделитесь мнением об их работе.

#### См. также {#see-also}

* [{#T}](../operations/index.md)
* [{#T}](limits.md)
* [{#T}](../pricing.md)
