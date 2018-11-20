# Валюта

Средствами JSON API можно запрашивать списки валют и сведения по отдельным валютам, а также создавать новые и обновлять сведения по уже существующим валютам. Кодом сущности для валют в составе JSON API является ключевое слово **currency**. Больше о валютах и работе с ними в основном интерфейсе вы можете прочитать в нашей службе поддержки по
[этой ссылке](https://support.moysklad.ru/hc/ru/articles/203294033-%D0%92%D0%B0%D0%BB%D1%8E%D1%82%D1%8B).

## Получить Валюты
Запрос на получение списка всех валют на данной учётной записи.
Результат успешного запроса - JSON представление списка валют с перечисленными полями:

+ **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
+ **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
+ **rows** - Массив JSON объектов, представляющих собой [валюты](#валюта-валюты).

```shell
curl -X GET 
  "https://online.moysklad.ru/api/remap/1.2/entity/currency"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Валют.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
    "type": "currency",
    "mediaType": "application/json",
    "size": 2,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=6314188d-2c7f-11e6-8a84-bae500000055"
      },
      "id": "6314188d-2c7f-11e6-8a84-bae500000055",
      "system": false,
      "name": "руб",
      "fullName": "Рубль",
      "rate": 1.0,
      "multiplicity": 1,
      "indirect": false,
      "rateUpdateType": "manual",
      "code": "643",
      "isoCode": "RUB",
      "majorUnit": {
        "gender": "masculine",
        "s1": "рубль",
        "s2": "рубля",
        "s5": "рублей"
      },
      "minorUnit": {
        "gender": "feminine",
        "s1": "копейка",
        "s2": "копейки",
        "s5": "копеек"
      },
      "archived": false,
      "default": true
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=dc5f76ae-2c89-11e6-8a84-bae50000003f"
      },
      "id": "dc5f76ae-2c89-11e6-8a84-bae50000003f",
      "system": true,
      "name": "доллар",
      "fullName": "Доллар США",
      "rate": 63.0,
      "multiplicity": 1,
      "indirect": false,
      "rateUpdateType": "manual",
      "code": "840",
      "isoCode": "USD",
      "majorUnit": {
        "gender": "masculine",
        "s1": "доллар",
        "s2": "доллара",
        "s5": "долларов"
      },
      "minorUnit": {
        "gender": "masculine",
        "s1": "цент",
        "s2": "цента",
        "s5": "центов"
      },
      "archived": false,
      "default": false
    }
  ]
}
```

### HTTP запрос

`GET https://online.moysklad.ru/api/remap/1.2/entity/currency`

### Параметры запроса
Параметр | Значение по умолчанию | Описание
-------- | --------------------- | --------
limit | 1000 | Максимальное количество сущностей для извлечения
offset | 0 | Отступ в выдаваемом списке сущностей

По данной сущности можно осуществлять контекстный поиск с помощью специального параметра `search`. Подробнее можно узнать по [ссылке](/api/remap/1.2/doc/index.html#header-контекстный-поиск). Поиск с параметром search отличается от других тем, что поиск не префиксный, без токенизации и идет только по одному полю одновременно. Ищет такие строки, в которые входит значение строки поиска.

Поиск среди объектов валют на соответствие поисковой строке будет осуществлён по следующим полям:
+ по краткому наименованию Валюты **name**

### Атрибуты Сущности
Атрибут | Описание
------- | --------
**meta** | [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) объекта
**id** | ID в формате UUID `Только для чтения`
**name** | Краткое наименование Валюты `Необходимое`
**fullName** | Полное наименование Валюты
**code** | Цифровой код Валюты `Необходимое`
**isoCode** | Буквенный код Валюты `Необходимое`
**rate** | Курс Валюты
**multiplicity** | Кратность курса Валюты
**indirect** | Признак обратного курса Валюты
**rateUpdateType** | Способ обновления курса Валюты `Только для чтения`
**majorUnit** | Формы единиц целой части Валюты
**minorUnit** | Формы единиц дробной части Валюты
**archived** | Добавлена ли Валюта в архив
**system** | Основана ли валюта на валюте из системного справочника `Только для чтения`
**default** | Является ли валюта валютой учета `Только для чтения`

### Формы единиц
Поля **majorUnit** и **minorUnit** содержат в себе следующие атрибуты:

+ **gender** - Грамматический род единицы валюты (допустимые значения `masculine` - мужской, `feminine` - женский)
+ **s1** - Форма единицы, используемая при числительном 1
+ **s2** - Форма единицы, используемая при числительном 2
+ **s5** - Форма единицы, используемая при числительном 5

В JSON API валюты в основном представлены в составе сущностей в формате [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные). Для того, чтобы раскрыть их в составе другого объекта нужно воспользоваться [параметром expand](#общие-сведения-замена-ссылок-объектами-с-помощью-expand)


## Создать новую Валюту
Запрос на создание новой валюты. Обязательные поля для создание валюты - **name**, **code** и **isoCode**.
В теле запроса нельзя указать курс валюты (**rate**) равным нулю.

```shell
curl -X POST \
  https://online.moysklad.ru/api/remap/1.2/entity/currency \
  -H "Authorization: Basic <Access-Token>"
  -H 'Content-Type: application/json' \
  -d '{
  "name": "доллар",
  "rate": 63,
  "code" : "840",
  "isoCode": "USD"
}
'
```
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной Валюты.

```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=dc5f76ae-2c89-11e6-8a84-bae50000003f"
    },
    "id": "dc5f76ae-2c89-11e6-8a84-bae50000003f",
    "system": false,
    "name": "доллар",
    "rate": 63.0,
    "multiplicity": 1,
    "indirect": false,
    "rateUpdateType": "manual",
    "code": "840",
    "isoCode": "USD",
    "majorUnit": {
        "gender": "masculine"
    },
    "minorUnit": {
        "gender": "masculine"
    },
    "archived": false,
    "default": false
}
```

## Массовое создание и обновление Валют
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) Валют.
В теле запроса нужно передать массив, содержащий JSON представления Валют, которые вы хотите создать или обновить.
Обновляемые Валюты должны содержать идентификатор в виде метаданных.

```shell
curl -X POST \
  https://online.moysklad.ru/api/remap/1.2/entity/currency \
  -H "Authorization: Basic <Access-Token>"
  -H 'Content-Type: application/json' \
  -d '[
  {
    "name": "доллар",
    "rate": 63,
    "code" : "840",
    "isoCode": "USD"
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
      "type": "currency",
      "mediaType": "application/json"
    },
    "name": "долл",
    "rate": 66,
    "code" : "dollarusd",
    "isoCode": "USD"
  }
]
'
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Валют.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
      "type": "currency",
      "mediaType": "application/json",
      "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=dc5f76ae-2c89-11e6-8a84-bae50000003f"
    },
    "id": "dc5f76ae-2c89-11e6-8a84-bae50000003f",
    "system": false,
    "name": "доллар",
    "rate": 63.0,
    "multiplicity": 1,
    "indirect": false,
    "rateUpdateType": "manual",
    "code": "840",
    "isoCode": "USD",
    "majorUnit": {
      "gender": "masculine"
    },
    "minorUnit": {
      "gender": "masculine"
    },
    "archived": false,
    "default": false
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
      "type": "currency",
      "mediaType": "application/json",
      "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=dc5f76ae-2c89-11e6-8a84-bae50000003f"
    },
    "id": "dc5f76ae-2c89-11e6-8a84-bae50000003f",
    "system": false,
    "name": "долл",
    "rate": 66.0,
    "multiplicity": 1,
    "indirect": false,
    "rateUpdateType": "manual",
    "code": "dollarusd",
    "isoCode": "USD",
    "majorUnit": {
      "gender": "masculine"
    },
    "minorUnit": {
      "gender": "masculine"
    },
    "archived": false,
    "default": false
  }
]
```

## Удалить Валюту
Запрос на удаление Валюты с указанным id. Валюту учета удалить нельзя.

### HTTP запрос

`DELETE https://online.moysklad.ru/api/remap/1.2/entity/currency/<ID>`

### Параметры запроса
Параметр | Описание
-------- | --------
ID | id Валюты

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/currency/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешное удаление Валюты.

## Получить Валюту
Работа с Валютой с указанным id.

### HTTP запрос

`GET https://online.moysklad.ru/api/remap/1.2/entity/currency/<ID>`

### Параметры запроса
Параметр | Описание
-------- | --------
ID | id Валюты

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление запрошенной Валюты.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
    "type": "currency",
    "mediaType": "application/json",
    "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=6314188d-2c7f-11e6-8a84-bae500000055"
  },
  "id": "6314188d-2c7f-11e6-8a84-bae500000055",
  "system": false,
  "name": "руб",
  "fullName": "Рубль",
  "rate": 1.0,
  "multiplicity": 1,
  "indirect": false,
  "rateUpdateType": "manual",
  "code": "643",
  "isoCode": "RUB",
  "majorUnit": {
    "gender": "masculine",
    "s1": "рубль",
    "s2": "рубля",
    "s5": "рублей"
  },
  "minorUnit": {
    "gender": "feminine",
    "s1": "копейка",
    "s2": "копейки",
    "s5": "копеек"
  },
  "archived": false,
  "default": true
}
```

## Изменить Валюту
Запрос на обновление существующей валюты.
В теле запроса нельзя указать курс валюты (**rate**) равным нулю,
 а также пустые поля **name**, **code**, **isoCode**.
Нельзя изменять значения полей **name**, **fullName**, **code**, **isoCode**, **majorUnit**, **minorUnit**
для валют, основанных на системном справочнике валют. Нельзя изменять курс валюты учета. Нельзя изменить курс валюты с автоматическим обновлением.

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055"
  -H "Authorization: Basic <Access-Token>"
  -d '{
  "name": "долл",
  "rate": 66,
  "code" : "dollarusd",
  "isoCode": "USD"
}'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённой Валюты.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/dc5f76ae-2c89-11e6-8a84-bae50000003f",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
    "type": "currency",
    "mediaType": "application/json",
    "uuidHref": "http://online.moysklad.ru/app/#currency/edit?id=dc5f76ae-2c89-11e6-8a84-bae50000003f"
  },
  "id": "dc5f76ae-2c89-11e6-8a84-bae50000003f",
  "system": false,
  "name": "долл",
  "rate": 66.0,
  "multiplicity": 1,
  "indirect": false,
  "rateUpdateType": "manual",
  "code": "dollarusd",
  "isoCode": "USD",
  "majorUnit": {
    "gender": "masculine"
  },
  "minorUnit": {
    "gender": "masculine"
  },
  "archived": false,
  "default": false
}
```
