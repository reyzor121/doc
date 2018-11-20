<!-- include(metadata.apib) -->

# Отчёт Показатели контрагентов
Средствами JSON API можно запросить отчёт "Показатели контрагентов" по всем или по отдельному контрагенту.
О том, что представляет собой отчёт "Показатели контрагентов" вы можете прочитать по [этой ссылке](https://support.moysklad.ru/hc/ru/articles/206657807-%D0%9E%D1%82%D1%87%D0%B5%D1%82-%D0%BF%D0%BE-%D0%BF%D0%BE%D0%BA%D0%B0%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%BC-%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%B0%D0%B3%D0%B5%D0%BD%D1%82%D0%BE%D0%B2).

## Показатели контрагентов [/report/counterparty]
### Атрибуты показателей
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) отчёта по данному контрагенту
+ **counterparty** - Контрагент
  - **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) контрагента
  - **id** - id контрагента
  - **name** - Имя контрагента
  - **externalCode** - Внешний код контрагента
  - **companyType** - Тип контрагента
+ **firstDemandDate** - Дата первой продажи
+ **lastDemandDate** - Дата последней продажи
+ **demandsCount** - Количество продаж
+ **demandsSum** - Сумма продаж
+ **averageReceipt** - Средний чек
+ **returnsCount** - Количество возвратов
+ **returnsSum** - Сумма возвратов
+ **discountsSum** - Сумма скидок
+ **balance** - Баланс
+ **profit** - Прибыль
+ **lastEventDate** - Дата последнего события
+ **lastEventText** - Текст последнего события
+ **updated** - Момент последнего изменения контрагента

### Атрибуты доступные для фильтрации
+ **id** - id контрагента
+ **counterparty****.name** - Имя контрагента
+ **counterparty.phone** - Номер телефона
+ **counterparty.email** - Адрес электронной почты
+ **counterparty.inn** - Тип контрагента
+ **counterparty.companyType** - Тип контрагента
+ **counterparty.description** - Комментарий к Контрагенту
+ **firstDemandDate** - Дата первой продажи
+ **lastDemandDate** - Дата последней продажи
+ **demandsCount** - Количество продаж
+ **demandsSum** - Сумма продаж
+ **averageReceipt** - Средний чек
+ **returnsCount** - Количество возвратов
+ **returnsSum** - Сумма возвратов
+ **discountsSum** - Сумма скидок
+ **balance** - Баланс
+ **profit** - Прибыль
+ **lastEventDate** - Дата последнего события
+ **lastEventText** - Текст последнего события
+ **updated** - Момент последнего изменения контрагента

### Тарифные ограничения
Если в вашем тарифе не предусмотрена опция CRM вы не сможете получить этот запрос через API.


### Показатели контрагентов [GET]
Запрос на получение отчёта по контрагентам.
Результат успешного запроса - JSON представление списка отчётов по отдельным котрагентам:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) отчёта,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой отчёты по отдельным контрагентам.
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
Успешный запрос. Результат - JSON представление отчёта по контрагентам.
  + Body
        <!-- include(body/report_counterparty/get_list.json) -->

### Выборочные показатели контрагентов [POST]
Запрос на получение отчёта по указанным контрагентам. Необходимо передать массив `counterparties`,
содержащий метаданные контрагентов, по которым требуются отчёты.
Результат успешного запроса - JSON представление списка отчётов по указанным котрагентам:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) отчёта,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой отчёты по отдельным контрагентам.

+ Request Пример (application/json)
Пример запроса отчётов для нескольких контрагентов.
  + Body
        <!-- include(body/report_counterparty/request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление отчёта по контрагентам.
  + Body
        <!-- include(body/report_counterparty/response.json) -->

## Показатели контрагента [/report/counterparty/{id}]
### Показатели контрагента [GET]
Запрос на получение отчёта по контрагенту с указанным id.
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id контрагента
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
Успешный запрос. Результат - JSON представление отчёта по контрагенту.
  + Body
        <!-- include(body/report_counterparty/get_by_id.json) -->
