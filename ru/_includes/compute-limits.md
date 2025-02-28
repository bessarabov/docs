#### Квоты {#compute-quotas}

Вид ограничения | Значение
----- | -----
Количество виртуальных машин в одном облаке | 12
Суммарное количество vCPU для всех виртуальных машин в одном облаке | 32
Суммарный объем виртуальной памяти для всех виртуальных машин в одном облаке | 128 ГБ
Суммарное количество дисков в одном облаке | 32
Суммарный объем SSD-дисков в одном облаке | 200 ГБ
Суммарный объем HDD-дисков в одном облаке | 500 ГБ
Суммарное количество нереплицируемых SSD-дисков в одной группе размещения | 5
Суммарное количество снимков дисков в одном облаке | 32
Суммарный объем всех снимков дисков в одном облаке | 400 ГБ
Количество образов в одном облаке | 8
Количество групп виртуальных машин в одном облаке | 10
Суммарное количество GPU для всех виртуальных машин в одном облаке* | 0
Количество одновременно выполняемых [операций](../api-design-guide/concepts/operation.md) в облаке | 15
Максимальное количество ВМ в одной [группе размещения](../compute/concepts/placement-groups.md) | 5
Максимальное количество групп размещения в одном облаке | 2
Количество выделенных хостов в одном облаке* | 0

\* Чтобы создать виртуальную машину с GPU или выделенный хост, обратитесь в [техническую поддержку]({{ link-console-support }}).

#### Лимиты виртуальных машин {#compute-limits-vm}

Вид ограничения | Значение
----- | -----
Максимальное количество vCPU для одной виртуальной машины | 32 и 80 для [платформ](../compute/concepts/vm-platforms.md) Intel Broadwell и Intel Cascade Lake соответственно
Максимальный объем виртуальной памяти для одной виртуальной машины | 256 ГБ и 640 ГБ для [платформ](../compute/concepts/vm-platforms.md) Intel Broadwell и Intel Cascade Lake соответственно
Максимальное количество дисков, подключенных к одной виртуальной машине | 7
Максимальное количество GPU, подключенных к одной виртуальной машине | 4 и 8 для [платформ](../compute/concepts/vm-platforms.md) Intel Broadwell и Intel Cascade Lake соответственно
Максимальное количество vGPU, подключенных к одной виртуальной машине | 1
Максимальное количество vCPU для виртуальных машин с GPU | 32
Максимальное количество RAM для виртуальных машин с GPU | 384
Максимальное количество групп безопасности на один интерфейс | 5

#### Лимиты дисков {#compute-limits-disks}

{% list tabs %}

- Сетевой SSD-диск

    Вид ограничения | Значение
    ----- | -----
    Максимальный размер диска | 4 ТБ
    Максимальный размер снимка диска | 4 ТБ
    Размер [блока размещения](../compute/concepts/disk.md#rw) | 32 ГБ
    Максимальный[*](../compute/concepts/limits.md#max_iops) [IOPS](../compute/concepts/disk.md#rw) на запись, на 1 диск | 40000
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на запись, на блок размещения | 1000
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) [пропускная способность](../compute/concepts/disk.md#rw) на запись, на 1 диск | 450 МБ/с
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на запись, на блок размещения | 15 МБ/с
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на чтение, на 1 диск | 12000
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на чтение, на блок размещения | 400
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на чтение, на 1 диск | 450 МБ/с
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на чтение, на блок размещения | 15 МБ/с

- Cетевой HDD-диск

    Вид ограничения | Значение
    ----- | -----
    Максимальный размер снимка диска | 4 ТБ
    Размер [блока размещения](../compute/concepts/disk.md#rw) | 256 ГБ
    Максимальный[*](../compute/concepts/limits.md#max_iops) [IOPS](../compute/concepts/disk.md#rw) на запись, на 1 диск | 11000
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на запись, на блок размещения | 300
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) [пропускная способность](../compute/concepts/disk.md#rw) на запись, на 1 диск | 240 МБ/с
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на запись, на блок размещения | 30 МБ/с
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на чтение, на 1 диск | 300
    Максимальный[*](../compute/concepts/limits.md#max_iops) IOPS на чтение, на блок размещения | 100
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на чтение, на 1 диск | 240 МБ/с
    Максимальная[**](../compute/concepts/limits.md#max_bandwidth) пропускная способность на чтение, на блок размещения | 30 МБ/с

- Нереплицируемый SSD-диск
  
    Вид ограничения | Значение
    ----- | -----
    Минимальный размер нереплицируемого диска | 93 ГБ

{% endlist %}

Операции чтения и записи потребляют один и тот же дисковый ресурс — чем больше производится операций чтения, тем меньше операций записи, и наоборот. Подробнее читайте в разделе [Диски](../compute/concepts/disk.md#rw).

##### * {#max_iops}

Для получения максимального значения IOPS рекомендуется делать операции чтения и записи, по объему близкие к размеру блока диска (по умолчанию — 4 КБ).

##### ** {#max_bandwidth}

Для получения максимального значения пропускной способности рекомендуется делать чтения и записи размером 4 МБ.
