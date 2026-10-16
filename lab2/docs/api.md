# API documentation for lab2

Все эндпоинты доступны на `http://localhost:1880`.
Формат ответа — JSON (кроме `/api/text`, где plain text).

---

## GET /api/text

Возвращает простое текстовое приветствие.

**Запрос:**
```
GET http://localhost:1880/api/text
```

**Ответ (200 OK):**
```
Привет от Node-RED! Студент: Данилиk
```

---

## GET /api/info

Возвращает информацию о сервисе в формате JSON.

**Запрос:**
```
GET http://localhost:1880/api/info
```

**Ответ (200 OK):**
```json
{
  "service": "Node-RED lab2",
  "author": "Данилиk",
  "version": "1.0.0"
}
```

---

## GET /api/items/:id

Возвращает информацию о «предмете» по его id.
Поддерживает query-параметр `limit`.

**Path params:**
- `id` (обязательный) — целое число от 1 до 100

**Query params:**
- `limit` (опциональный) — число, по умолчанию 10

### Успешный запрос

```
GET http://localhost:1880/api/items/5
```

**Ответ (200 OK):**
```json
{
  "id": 5,
  "name": "item-5",
  "limit": 10,
  "status": "ok"
}
```

### Успешный запрос с query-параметром

```
GET http://localhost:1880/api/items/5?limit=20
```

**Ответ (200 OK):**
```json
{
  "id": 5,
  "name": "item-5",
  "limit": 20,
  "status": "ok"
}
```

### Ошибка 400 — id не является числом

```
GET http://localhost:1880/api/items/abc
```

**Ответ (400 Bad Request):**
```json
{
  "error": "Bad Request",
  "message": "id must be a number"
}
```

### Ошибка 404 — элемент не найден

```
GET http://localhost:1880/api/items/999
```

**Ответ (404 Not Found):**
```json
{
  "error": "Not Found",
  "message": "item with id 999 not found"
}
```

---

## Сводная таблица

| Метод | URL | Код | Описание |
|---|---|---|---|
| GET | /api/text | 200 | Простой текст |
| GET | /api/info | 200 | JSON с полями сервиса |
| GET | /api/items/:id | 200 | Элемент найден |
| GET | /api/items/:id | 400 | id не число |
| GET | /api/items/:id | 404 | id > 100 (не найден) |