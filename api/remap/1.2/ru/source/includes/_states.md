<!-- include(metadata.apib) -->

# Статусы документов

Статусы можно добавлять, изменять и удалять через api

## Статусы [/entity/{entityType}/metadata/states]
### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о Статусе `Только для чтения`
+ **id** - ID в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **name** - Наименование Статуса `Необходимое`
+ **color** - Цвет Статуса `Необходимое`
+ **stateType** - Тип Статуса `Необходимое`

Возможные значения: [`Regular`(обычный), `Successful`(Финальный положительный), `Unsuccessful`(Финальный отрицательный)].
Значение по умолчанию - `Regular`

+ **entityType** - Тип сущности, к которой относится Статус (ключевое слово в рамках JSON API) `Только для чтения`

Поле **color** передаётся в АПИ как целое число состоящее из 4х байт.
Т.к. цвет передаётся в цветовом пространстве ARGB, каждый байт отвечает за свой
цвет соответственно: 1 - за прозрачность, 2 - за красный цвет, 3 - за зелёный,
4 - за синий. Каждый байт принимает значения от 0 до 255 как и цвет в каждом из
каналов цветового пространства. Получившееся в итоге из 4 записанных последовательно байт
число, переведённое в 10-чную систему счисления и является представлением цвета статуса в JSON API.

Пример: цвету `rgb(162, 198, 23)` будет соответствовать следующее значение поля `"color": 10667543`.

Посмотреть списки существующих статусов можно в контексте метаданных
документа, например сделав GET запрос по URL http://online.moysklad.ru/api/remap/1.2/entity/demand/metadata
Список статусов для документа `demand`(Отгрузка) будет выведен в коллекции states.

### Получить метаданные [GET /entity/{entityType}/metadata]
Получить метаданные и в том числе статусы
+ Parameters
  + entityType: `counterparty` (required, string) - тип сущности
+ Response 200 (application/json)
  + Body
        <!-- include(body/states/get.json) -->

### Создать статус [POST /entity/{entityType}/metadata/states]
Создать новый статус.
### Описание
Статус создаётся на основе переданного объекта JSON,
который содержит представление нового Статуса.
Результат - JSON представление созданного Статуса. Для создания нового Статуса,
необходимо и достаточно указать в переданном объекте не пустые поля `name`, `color`, `stateType`.

+ Parameters
  + entityType: `counterparty` (required, string) - тип сущности

+ Request Пример (application/json)
Создание одного статуса.
  + Body
        <!-- include(body/states/post_one_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Статуса.
  + Body
        <!-- include(body/states/post_one_response.json) -->


### Обновить статус [PUT /entity/{entityType}/metadata/states/{id}]
Обновить существующий статус.
### Описание
Статус обновляется на основе переданного объекта JSON.
Результат - JSON представление обновленного или созданного Статуса.
Для обновления Статуса, необходимо  указать в переданном объекте
одно или несколько полей с новыми значениями: `name`, `color`, `stateType`.

+ Parameters
  + entityType: `counterparty` (required, string) - тип сущности
  + id: `4dcb3f23-60c4-11e7-6adb-ede500000019` (required, string) - id Статуса

+ Request Пример (application/json)
Обновление статуса.
  + Body
        <!-- include(body/states/put_update_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Статуса.
  + Body
        <!-- include(body/states/put_update_response.json) -->

### Массовое создание и обновление Статусов [POST]
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) Статусов.
В теле запроса нужно передать массив, содержащий JSON представления Статусов, которые вы хотите создать или обновить.
Обновляемые Статусы должны содержать идентификатор в виде метаданных.

+ Request Пример (application/json)
Пример создания и обновления нескольких Статусов
  + Body
        <!-- include(body/states/post_some_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Статусов.
  + Body
        <!-- include(body/states/post_some_response.json) -->

### Удалить Статус [DELETE /entity/{entityType}/metadata/states/{id}]
Запрос на удаление Статуса с указанным id.
+ Parameters
  + entityType: `counterparty` (required, string) - тип сущности
  + id: `4dcb3f23-60c4-11e7-6adb-ede500000019` (required, string) - id Статуса

+ Response 200 (application/json)
Успешное удаление Статуса.
