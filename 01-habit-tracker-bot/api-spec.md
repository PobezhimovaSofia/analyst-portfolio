```markdown
# Спецификация API

## Общее
- Base URL: `https://api.habittracker.local/v1`
- Формат: JSON
- Авторизация: Bearer token (VK ID)

## Эндпоинты

### POST /habits — создать привычку
**Запрос:**
```json
{
  "name": "Зарядка",
  "reminder_time": "08:00"
}
```

Ответ 201:

```json
{
  "id": 1,
  "name": "Зарядка",
  "reminder_time": "08:00",
  "is_active": true
}
```

Ошибки: 400 — неверные данные, 401 — не авторизован.

GET /habits — список привычек

Ответ 200:

```json
[
  { "id": 1, "name": "Зарядка", "is_active": true },
  { "id": 2, "name": "Чтение", "is_active": true }
]
```

POST /habits/{id}/checkin — отметить выполнение

Запрос:

```json
{ "date": "2026-10-16" }
```

Ответ 200:

```json
{ "status": "ok", "streak": 5 }
```

Ошибки: 404 — привычка не найдена, 409 — уже отмечено сегодня.

GET /habits/{id}/stats — статистика

Параметры: ?period=7d
Ответ 200:

``json
{
  "habit_id": 1,
  "completed": 5,
  "total_days": 7,
  "completion_rate": 0.71
}
