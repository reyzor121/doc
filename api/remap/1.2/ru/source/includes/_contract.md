<!-- include(metadata.apib) -->

# Договор
## Договоры [/entity/contract]
Средствами JSON API можно создавать и обновлять сведения о Договорах, запрашивать списки Договоров и сведения по отдельным Договорам. Кодом сущности для Договора в составе JSON API является ключевое слово **contract**. Больше о Договорах и работе с ними в основном интерфейсе вы можете прочитать в нашей службе поддержки по [этой ссылке](https://support.moysklad.ru/hc/ru/articles/218121398-%D0%A3%D1%87%D0%B5%D1%82-%D0%B4%D0%BE%D0%B3%D0%BE%D0%B2%D0%BE%D1%80%D0%BE%D0%B2).
По данной сущности можно осуществлять контекстный поиск с помощью специального параметра `search`. Подробнее можно узнать по [ссылке](/api/remap/1.2/doc/index.html#header-контекстный-поиск). Поиск с параметром search отличается от других тем, что поиск не префиксный, без токенизации и идет только по одному полю одновременно. Ищет такие строки, в которые входит значение строки поиска.

Поиск среди объектов Договора на соответствие поисковой строке будет осуществлён по следующим полям:
+ по номеру Договора **name**
+ по комментарию к Договору **description**

### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о Заказе Покупателя
+ **id** - ID в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **owner** - Ссылка на Владельца (Сотрудника) в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **shared** - Общий доступ
+ **group** - Отдел сотрудника в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **updated** - Момент последнего обновления сущности `Только для чтения`
+ **name** - номер Договора
+ **description** - Комментарий к Договору
+ **code** - Код Договора
+ **externalCode** - Внешний код Договора
+ **archived** - Добавлен ли Договор в архив
+ **moment** - Дата Договора,
+ **sum** - Сумма Договора,
+ **contractType** - Тип Договора. Возможные значения: `Договор комиссии`, `Договор купли-продажи`
+ **rewardType** - Тип Вознаграждения. Возможные значения: `Процент от суммы продажи`, `Не рассчитывать`
+ **rewardPercent** - Вознаграждение в процентах (от 0 до 100).
+ **ownAgent** - Ссылка на ваше юрлицо в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **agent** - Ссылка на Контрагента в формате [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные)
+ **state** - Статус договора в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **organizationAccount** - Ссылка на счёт вашего юрлица в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **agentAccount** - Ссылка на счёт контрагента в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **rate** - Ссылка на валюту
+ **attributes** - Коллекция доп. полей в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)

Таблица полей, их значений и их значений в JSON представлении:

| Имя поля     | Возможные Значения      | Соответствующее значение в JSON| Значение по умолчанию |
| :-----------:|:-----------------------:|:------------------------------:|:---------------------:|
|**contractType**  | Договор комиссии        |Commission                      | Договор купли-продажи |
|              | Договор купли-продажи   |Sales                           |                       |
| **rewardType**   | Процент от суммы продажи|PercentOfSales                  |    Не рассчитывать    |
|              | Не рассчитывать         |None                            |                       |

<!-- include(rate.apib) -->

О работе с доп. полями Договоров можно прочитать [здесь](/api/remap/1.2/doc/index.html#header-работа-с-дополнительными-полями)


### Получить список Договоров [GET]
Запрос на получение списка всех договоров на данной учётной записи.
Результат: Объект JSON, включающий в себя поля:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой Договоры.

+ Parameters
  + limit: 1000 (optional, enum[number])
  Максимальное количество сущностей для извлечения.
  <p>
    <code>Допустимые значения 1 - 1000</code>
  </p>
      + Default: `1000`
  + offset: 40 (optional, number)
    Отступ в выдаваемом списке сущностей
      + Default: `0`

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Договоров.
  + Body
        <!-- include(body/contract/get_list.json) -->

### Создать новый Договор [POST]
Запрос на создание нового Договора.
Обязательные для создания Договора поля:
+ **name** - Номер Договора
+ **ownAgent** - Ссылка на ваше юрлицо в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **agent** - Ссылка на Контрагента в формате [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные)


+ Request Пример 1 (application/json)
Пример создания нового Договора, с запросом, Тело которого содержит только обязательные поля.
  + Body
        <!-- include(body/contract/post_short_request.json) -->
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Договора.
  + Body
        <!-- include(body/contract/post_short_response.json) -->

+ Request Пример 2 (application/json)
Пример создания нового Договора с более насыщенным телом запроса.
  + Body
        <!-- include(body/contract/post_long_request.json) -->
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Договора.
  + Body
        <!-- include(body/contract/post_long_response.json) -->

+ Request Пример с доп. полями (application/json)
Пример создания нового Договора, с запросом, Тело которого содержит дополнительные поля.
  + Body
        <!-- include(body/contract/post_with_attributes_request.json) -->
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Договора.
  + Body
        <!-- include(body/contract/post_with_attributes_response.json) -->

### Массовое создание и обновление Договоров [POST]
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) Договоров.
В теле запроса нужно передать массив, содержащий JSON представления Договоров, которые вы хотите создать или обновить.
Обновляемые Договора должны содержать идентификатор в виде метаданных.

+ Request Пример (application/json)
Пример создания и обновления нескольких Договоров
  + Body
        <!-- include(body/contract/post_massive_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Договоров.
  + Body
        <!-- include(body/contract/post_massive_response.json) -->

### Удалить договор [DELETE /entity/contract/{id}]
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id Договора

Запрос на удаление Договора с указанным id.

+ Response 200 (application/json)
Успешное удаление Договора.

## Метаданные Договоров [/entity/contract/metadata]
### Метаданные Договоров [GET]
Запрос на получение метаданных Договоров. Результат - объект JSON, включающий в себя:
+ **meta** - Ссылка на метаданные Договоров
+ **attributes** - Массив объектов доп. полей Договоров в формате [Метаданных](#header-метаданные)
+ **states** - Массив статусов Договоров
+ **createShared** - создавать новые Договора с меткой "Общий"

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](#header-работа-с-дополнительными-полями).

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Договоров.
  + Body
        <!-- include(body/contract/get_metadata.json) -->

## Отдельное доп. поле [/entity/contract/metadata/attributes/{id}]
+ Parameters
  + id: `5290a290-0313-11e6-9464-e4de00000020` (required, string) - id Доп. поля
### Отдельное доп. поле [GET]
Запрос на получение информации по отдельному дополнительному полю.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.
  + Body
        <!-- include(body/contract/metadata_by_id.json) -->

## Договор [/entity/contract/{id}]
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id Договора
### Получить Договор [GET]
Запрос на получение отдельного Договора с указанным id.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление Договора.
  + Body
        <!-- include(body/contract/get_by_id.json) -->

### Изменить Договор [PUT]
Запрос на обновление отдельного Договора с указанным id.
При обновлении полей **organization** и **agent** нужно также обновить поля **organizationAccount** и
**agentAccount** соответственно, иначе произойдёт ошибка.

+ Request Пример (application/json)
Пример запроса на обновление отдельного Договора.
  + Body
        <!-- include(body/contract/put_request.json) -->
+ Response 200 (application/json)
Удачный запрос. Результат - JSON представление обновлённого Договора.
  + Body
        <!-- include(body/contract/put_response.json) -->

+ Request Пример с доп полями(application/json)
Пример запроса на обновление отдельного Договора с телом запроса, содержащим доп. поля.
  + Body
        <!-- include(body/contract/put_with_attributes_request.json) -->
+ Response 200 (application/json)
Удачный запрос. Результат - JSON представление обновлённого Договора.
  + Body
        <!-- include(body/contract/put_with_attributes_response.json) -->
