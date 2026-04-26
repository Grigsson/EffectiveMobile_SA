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

| Статус | Тип контента | Описание | Пример |
|-------|-------------|----------|--------|
| 200 OK | application/json | Успешный ответ | см. Example 200 |
| 400 Bad Request | application/json | Некорректный запрос | см. Example 400 |
| 401 Unauthorized | application/json | Нет авторизации | см. Example 401 |
| 403 Forbidden | application/json | Доступ запрещен | см. Example 403 |
| 404 Not Found | application/json | Нет данных | см. Example 404 |
| 500 Internal Server Error | application/json | Ошибка сервера | см. Example 500 |а | 

### Example 200 OK

```json
{
  "status": "success",
  "data": {
    "screenTitle": "Выберите магазин",
    "stores": [
      {
        "id": "metro",
        "type": "external_partner",
        "name": "METRO",
        "logoUrl": "https://cdn.petrushka-green.ru/partners/metro.png",
        "delivery": {
          "type": "scheduled",
          "label": "Ближайшая доставка",
          "displayText": "сегодня 21:00–23:00"
        },
        "externalUrl": "https://online.metro-cc.ru"
      }
    ]
  }
}
```

### Example 400 Bad Request

```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Некорректные параметры запроса"
  }
}
```

### Example 401 Unauthorized

```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Требуется авторизация"
  }
}
```

### Example 403 Forbidden

```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "FORBIDDEN",
    "message": "Доступ запрещен"
  }
}
```

### Example 404 Not Found

```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "NOT_FOUND",
    "message": "Магазины не найдены"
  }
}
```

### Example 500 Internal Server Error

```json
{
  "status": "error",
  "data": null,
  "error": {
    "code": "INTERNAL_ERROR",
    "message": "Внутренняя ошибка сервера"
  }
}
```
