<!-- include(metadata.apib) -->

# Документ Счет-фактура выданный
## Счета-фактуры выданные  [/entity/factureout]
Средствами JSON API можно создавать и изменять Счет-фактуры выданные, запрашивать списки выданных Счетов-фактур, сведения по отдельным Счетам-фактурам и удалять Счета-фактуры. Счет-фактура может быть создана только на основании отгрузки, возврата поставщику или входящего платежа, без документа-основания счет-фактуру создать нельзя. Кодом сущности для выданного Счета-фактуры в составе JSON API является ключевое слово **factureout**.

### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выданном Счете-фактуре
+ **id** - ID в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **syncId** - ID синхронизации. После заполнения недоступен для изменения.
+ **updated** - Момент последнего обновления сущности `Только для чтения`
+ **deleted** - Момент последнего удаления сущности `Только для чтения`
+ **name** - номер выданного Счета-фактуры
+ **description** - Комментарий выданного Счета-фактуры
+ **externalCode** - Внешний код выданного Счета-фактуры
+ **moment** - Дата выданного Счета-фактуры
+ **applicable** - Отметка о проведении
+ **sum** - Сумма выданного Счета-фактуры в установленной валюте `Только для чтения`
+ **rate** - Валюта
+ **owner** - Ссылка на Владельца (Сотрудника) в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **shared** - Общий доступ
+ **group** - Отдел сотрудника в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные) `Только для чтения`
+ **agent** - Ссылка на контрагента в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные) `Только для чтения`
+ **contract** - Ссылка на договор в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **state** - Статус выданного Счета-фактуры в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **attributes** - Коллекция доп. полей в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
<br>Поля при expand'е:</br>
  - **name** - номер документа
  - **moment** - дата печати
  - **href** - ссылка на файл печатной формы
  - **fileName** - название файла печатной формы
  - **updated** - дата последнего изменения
+ **created** - Дата создания `Только для чтения`
+ **stateContractId** - Идентификатор государственного контракта, договора (соглашения)

### Связи с другими документами
+ **demands** - Массив ссылок на связанные отгрузки в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
  - **meta** - Ссылка на отгрузку, к которой привязан этот Счет-фактура в формате метаданных
+ **payments** - Массив ссылок на связанные входящие платежи в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
  - **meta** - Ссылка на входящий платеж, к которой привязан этот Счет-фактура в формате метаданных
+ **returns** - Массив ссылок на связанные возвраты поставщикам в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
  - **meta** - Ссылка на возврат поставщику, к которой привязан этот Счет-фактура в формате метаданных

###  Другие поля 
+ **consignee** - Грузополучатель
+ **paymentNumber** - Название платежного документа
+ **paymentDate** - Дата платежного документа

<!-- include(rate.apib) -->

О работе с доп. полями Счет-фактур можно прочитать [здесь](/api/remap/1.2/doc/index.html#header-работа-с-дополнительными-полями)


### Получить выданные Счета-фактуры [GET]
Запрос всех выданных Счетов-фактур на данной учётной записи.
Результат: Объект JSON, включающий в себя поля:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой выданные Счета-фактуры.
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

  + search: `0001` (optional, string)
    URL Параметр для поиска по имени документа.
    Фильтр документов по указанной поисковой строке. Фильтрация происходит по
    полю name.

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка выданных Счетов-фактур.
  + Body
        <!-- include(body/facture_out/get_list.json) -->

### Создать Счет-фактуру [POST]
Запрос на создание Счета-фактуры на основании отгрузки, входящего платежа или возврата поставщику.
Документ-основание должен быть указан в единственном экземпляре.</br>
Для установки **paymentNumber**, **paymentDate** значения должны быть переданы в теле Json, так как перечисленные поля не заполняются из документа-основания.
+ Request Пример (application/json)
Пример создания нового Счета-фактуры, содержащим только необходимые поля.
  + Body
        <!-- include(body/facture_out/post_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Счета-фактуры.
  + Body
        <!-- include(body/facture_out/post_response.json) -->

### Массовое создание и обновление выданных Счетов-фактур [POST]
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) выданных Счетов-фактур.
В теле запроса нужно передать массив, содержащий JSON представления выданных Счетов-фактур, которые вы хотите создать или обновить.
Обновляемые выданные Счета-фактуры должны содержать идентификатор в виде метаданных.

+ Request Пример (application/json)
Пример создания и обновления нескольких выданных Счетов-фактур
  + Body
        <!-- include(body/facture_out/post_massive_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных выданных Счетов-фактур.
  + Body
        <!-- include(body/facture_out/post_massive_response.json) -->

## Метаданные выданных Счетов-фактур [/entity/factureout/metadata]
### Метаданные Счетов-фактур [GET]
Запрос на получение метаданных выданных Счетов-фактур. Результат - объект JSON, включающий в себя:
+ **meta** - Ссылка на метаданные выданных Счетов-фактур
+ **attributes** - Массив объектов доп. полей выданных Счетов-фактур в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **states** - Массив статусов выданных Счетов-фактур
+ **createShared** - создавать новые выданные Счета-фактуры с меткой "Общий"

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](/api/remap/1.2/doc/index.html#header-работа-с-дополнительными-полями).

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей выданных Счетов-фактур.
  + Body
        <!-- include(body/facture_out/metadata.json) -->

## Отдельное доп. поле [/entity/factureout/metadata/attributes/{id}]
+ Parameters
  + id: `8b0b6c1d-aa6f-11e6-8a84-bc520000008a` (required, string) - id Доп. поля
### Отдельное доп. поле [GET]
Запрос на получение информации по отдельному дополнительному полю.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.
  + Body
        <!-- include(body/facture_out/metadata_by_id.json) -->

## Шаблон выданного Счета-фактуры [/entity/factureout/new]
### Шаблон выданного Счета-фактуры на основе [PUT]
Запрос на получение предзаполненного шаблона выданного Счета-фактуры на основе отгрузки, возврата поставщику или входящего платежа.
В ответ на запрос вернётся предзаполненный шаблон выданного Счета-фактуры, который
затем можно будет использовать для создания нового Счета-фактуры с помощью POST запроса.

+ Request На основе отгрузки (application/json)
Пример запроса на создание шаблона выданного Счета-фактуры на основе отгрузки.
  + Body
        <!-- include(body/facture_out/new_from_demand_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного выданного Счета-фактуры.
  + Body
        <!-- include(body/facture_out/new_from_demand_response.json) -->

+ Request На основе возврата поставщику (application/json)
Пример запроса на создание шаблона выданного Счета-фактуры на основе возврата поставщику.
  + Body
        <!-- include(body/facture_out/new_from_purchasereturn_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного выданного Счета-фактуры.
  + Body
        <!-- include(body/facture_out/new_from_purchasereturn_response.json) -->

+ Request На основе входящего платежа (application/json)
Пример запроса на создание шаблона выданного Счета-фактуры на основе входящего платежа.
  + Body
        <!-- include(body/facture_out/new_from_paymentin_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного выданного Счета-фактуры.
  + Body
        <!-- include(body/facture_out/new_from_paymentin_response.json) -->

## Счет-фактура выданный [/entity/factureout/{id}]
+ Parameters
  + id: `99d41b01-aa8a-11e6-8af5-581e0000007e` (required, string) - id Счет-фактуры

### Получить выданный Счет-фактуру [GET]
Запрос на получение отдельного выданного Счета-фактуры с указанным id.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление выданного Счета-фактуры.
  + Body
        <!-- include(body/facture_out/get_by_id.json) -->

### Изменить выданный Счет-фактуру [PUT]
Запрос на обновление Счета-фактуры с указанным id.
+ Request Пример (application/json)
Пример запроса на обновление Счет-фактуры.
  + Body
        <!-- include(body/facture_out/put_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённого Счета-фактуры.
  + Body
        <!-- include(body/facture_out/put_response.json) -->

### Удалить выданный Счет-фактуру [DELETE /entity/factureout/{id}]
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b20` (required, string) - id выданного Счета-фактуры

Запрос на удаление выданного Счета-фактуры с указанным id.

+ Response 200 (application/json)
Успешное удаление выданного Счета-фактуры.