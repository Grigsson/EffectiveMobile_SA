# Пример REST API запроса и JSON-ответа

## REST API

GET /api/v1/partner-stores?cityId=1
Host: api.petrushka-green.ru
Accept: application/json
Authorization: Bearer <access_token>

## Описание полей

*1. Общие поля*
**Поле Тип Описание**
ScreenTitle string Заголовок экрана
data array Список партнерских магазинов

*2. Поля магазина*
**Поле Тип Описание**
id string Уникальный идентификатор магазина
type string Тип магазина
name string Название магазина
logoUrl string URL логотипа
delivery object Информация о доставке
externalUrl string Ссылка для перехода на внешний ресурс

*3. Поле type*
- external_partner - Партнерский магазин, переход на внешний сайт
- internal_store - Внутренний магазин, открывается внутри приложения
- aggregator - Магазин агрегатор, может открывать список подкаталогов

*4. Поле delivery*
**|Поле| |Тип| |Описание|**
|type| |string| |Тип доставки|
|label| |string| |Заголовок блока|
|displayText| |string| |Готовый текст для изображения|

*5. Типы доставки*
- scheduled - Интервальная доставка
- fast - Быстрая доставка

*6. Дополнительные поля*
- Для scheduled - dataText, timeFrom, timeTo
- Для fast - timefromMinutes, timeToMinutes

## Примеры возможных ответов

