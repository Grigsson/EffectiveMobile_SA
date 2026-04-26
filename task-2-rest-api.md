# Пример REST API запроса и JSON-ответа

## REST API

```http
GET /api/v1/partner-stores?cityId=1 HTTP/1.1
Host: api.petrushka-green.ru
Accept: application/json
Authorization: Bearer <access_token>
```

## Описание полей

### 1. Общие поля

| Поле | Тип | Описание |
|------|-----|----------|
| screenTitle | string | Заголовок экрана |
| data | array | Список партнерских магазинов |


### 2. Поля магазина

| Поле | Тип | Описание |
|------|-----|----------|
| id | string | Уникальный идентификатор магазина |
| type | string | Тип магазина |
| name | string | Название магазина |
| logoUrl | string | URL логотипа |
| delivery | object | Информация о доставке |
| externalUrl | string | Ссылка для перехода на внешний ресурс |


### 3. Поле `type`

| Значение | Описание |
|----------|----------|
| external_partner | Партнерский магазин, переход на внешний сайт |
| internal_store | Внутренний магазин, открывается внутри приложения |
| aggregator | Магазин-агрегатор, может открывать список подкаталогов |


### 4. Поле `delivery`

| Поле | Тип | Описание |
|------|-----|----------|
| type | string | Тип доставки |
| label | string | Заголовок блока |
| displayText | string | Готовый текст для отображения |


### 5. Типы доставки

| Тип | Описание |
|-----|----------|
| scheduled | Интервальная доставка |
| fast | Быстрая доставка |


## 6. Дополнительные поля

### Для `scheduled`

| Поле | Тип | Описание |
|------|-----|----------|
| dateText | string | Текст даты (например "сегодня") |
| timeFrom | string | Время начала доставки |
| timeTo | string | Время окончания доставки |

### Для `fast`

| Поле | Тип | Описание |
|------|-----|----------|
| timeFromMinutes | integer | Минимальное время доставки (в минутах) |
| timeToMinutes | integer | Максимальное время доставки (в минутах) |


## Примеры возможных ответов

## Возможные ответы API

| Статус | Тип контента | Описание | Пример ответа |
|-------|-------------|----------|---------------|
| 200 OK | application/json | Успешное получение списка магазинов | `{<br>"screenTitle": "Выберите магазин",<br>"data": [<br>{<br>"id": "metro",<br>"type": "external_partner",<br>"name": "METRO",<br>"logoUrl": "https://cdn.petrushka-green.ru/partners/metro.png",<br>"delivery": {<br>"type": "scheduled",<br>"label": "Ближайшая доставка",<br>"displayText": "сегодня 21:00–23:00"<br>},<br>"externalUrl": "https://online.metro-cc.ru"<br>}<br>]<br>}` |
| 400 Bad Request | application/json | Некорректные параметры запроса | `{<br>"error": {<br>"code": "INVALID_REQUEST",<br>"message": "Некорректные параметры запроса"<br>}<br>}` |
| 401 Unauthorized | application/json | Пользователь не авторизован | `{<br>"error": {<br>"code": "UNAUTHORIZED",<br>"message": "Требуется авторизация"<br>}<br>}` |
| 403 Forbidden | application/json | Доступ запрещен | `{<br>"error": {<br>"code": "FORBIDDEN",<br>"message": "Доступ запрещен"<br>}<br>}` |
| 404 Not Found | application/json | Магазины не найдены | `{<br>"error": {<br>"code": "NOT_FOUND",<br>"message": "Магазины не найдены"<br>}<br>}` |
| 500 Internal Server Error | application/json | Внутренняя ошибка сервера | `{<br>"error": {<br>"code": "INTERNAL_ERROR",<br>"message": "Внутренняя ошибка сервера"<br>}<br>}` |
