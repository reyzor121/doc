<!-- include(metadata.apib) -->

# Единица измерения
## Единицы измерения [/entity/uom]
По данной сущности можно осуществлять контекстный поиск с помощью специального параметра `search`. Подробнее можно узнать по [ссылке](/api/remap/1.2/doc/index.html#header-контекстный-поиск). Поиск с параметром search отличается от других тем, что поиск не префиксный, без токенизации и идет только по одному полю одновременно. Ищет такие строки, в которые входит значение строки поиска.

Поиск среди объектов единиц измерения на соответствие поисковой строке будет осуществлён по следующим полям:
+ по наименованию Единицы измерения **name**
+ по описанию Единицы измерения **description**

### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о единице измерения
+ **id** - ID в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **updated** - Момент последнего обновления сущности `Только для чтения`
+ **shared** - Флаг Общий доступ `Только для пользовательских единиц измерений`
+ **owner** - Сотрудник-владелец `Только для пользовательских единиц измерений`
+ **group** - Отдел-владелец `Только для пользовательских единиц измерений`
+ **name** - Наименование единицы измерения `Необходимое`
+ **description** - Описание единицы измерения
+ **code** - Код единицы измерения
+ **externalCode** - Внешний код единицы измерения


### Получить Единицы измерения [GET]
Запрос на получения списка всех единиц измерения для данной учётной записи.
Результат: Объект JSON, включающий в себя поля:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой Единицы измерения.

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
Успешный запрос. Результат - JSON представление списка единиц измерения.
  + Body
        <!-- include(body/uom/get_list.json) -->

### Создать Единицу измерения [POST]
Запрос на создание новой единицы измерения на данной учётной записи.
Единственное поле, которое обязательно должно присутствовать в теле запроса
на создание Единицы измерения - поле **name**.

+ Request Пример (application/json)
Пример запроса на создание новой единицы измерения.
  + Body
        <!-- include(body/uom/post_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной единицы измерения.
  + Body
        <!-- include(body/uom/post_response.json) -->

### Массовое создание и обновление единиц измерения [POST]
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) единиц измерения.
В теле запроса нужно передать массив, содержащий JSON представления единиц измерения, которые вы хотите создать или обновить.
Обновляемые единицы измерения должны содержать идентификатор в виде метаданных.

+ Request Пример (application/json)
Пример создания и обновления нескольких единиц измерения
  + Body
        <!-- include(body/uom/post_massive_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных единиц измерения.
  + Body
        <!-- include(body/uom/post_massive_response.json) -->

### Удалить Единицу измерения [DELETE /entity/uom/{id}]
Запрос на удаление единицы измерения. Невозможно удаление предустановленных единиц измерения (единиц измерений имеющихся на учётной записи по умолчанию).
Удалить можно только единицы измерения, созданные через основной интерфейс или через метод POST.
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id Единицы измерения

+ Response 200 (application/json)
Успешное удаление Розничной продажи.
+ Body

## Единица измерения [/entity/uom/{id}]
+ Parameters
  + id: `7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id Единицы измерения
## Получить Единицу измерения [GET]
Запрос на получение единицы измерения с указанным id.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление Единицы измерения с указанным id.
  + Body
        <!-- include(body/uom/get_by_id.json) -->

## Изменить Единицу измерения [PUT]
Запрос на изменение объекта, представляющего собой единицу измерения. Невозможно изменение предустановленных единиц измерения
 (единиц измерения имеющихся на учётной записи по умолчанию).
Изменить можно только единицы измерения, созданные через основной интерфейс или через метод POST.

+ Request Пример (application/json)
Пример запроса на обновление новой единицы измерения.
  + Body
        <!-- include(body/uom/put_request.json) -->

+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённой Единицы измерения.
  + Body
        <!-- include(body/uom/put_response.json) -->
