<!-- include(metadata.apib) -->

# Настройки компании
На данный момент можно только получить информацию о текущих настройках компании и типах цен товаров. Создавать новые настройки или изменять существующие пока невозможно.
## Настройки компании [/context/companysettings]
### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о Настройках компании
+ **currency** - Ссылка на стандартную валюту в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **priceTypes** - коллекция всех существующих типов цен.
+ **discountStrategy** - Cовместное применение скидок. Может принимать значения `[bySum, byPriority]` означающие "Сумма скидок" и "Приоритетная" соответственно. `Необходимое`
  - *"Сумма скидок"* `[bySum]` означает, что должна действовать сумма скидок
  - *"Приоритетная"* `[byPriority]` должна действовать одна, наиболее выгодная для покупателя скидка

#### Тип цены:
Структура отдельного объекта, представляющего тип цены:
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о Типе цены `Только для чтения`
+ **id** - ID в формате UUID `Только для чтения`
+ **name** - Наименование Типа цены `Необходимое`
+ **externalCode** - Внешний код Типа цены

### Метаданные настроек
В метаданных Настроек компании, в поле **customEntities** показан список пользовательских справочников.
Каждый пользовательский справочник содержит поля:
+ **meta** - Ссылка на представление пользовательского справочника
+ **entityMeta** - Ссылка на список сущностей данного пользовательского справочника
+ **name** - Наименование справочника

### Получить Настройки компании [GET]
Запрос на получение Настроек компании.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление Настроек компании.
  + Body
        <!-- include(body/companysettings/get.json) -->

## Метаданные настроек компании [/context/companysettings/metadata]
### Получить метаданные настроек компании [GET]
Запрос на получение метаданных Настроек компании.
+ Response 200 (application/json)
Успешный запрос. Результат - JSON представление метаданных настроек компании.
  + Body
        <!-- include(body/companysettings/metadata.json) -->