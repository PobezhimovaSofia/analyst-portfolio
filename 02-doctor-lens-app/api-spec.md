```markdown
# Спецификация API (MVP мобильного приложения)

## Общее
- Base URL: `https://api.doctor-lens.ru/v1`
- Формат данных: JSON
- Авторизация: Bearer token (JWT)

## Эндпоинты

### GET /doctors — список врачей
**Параметры:** `?clinic_id=1`
**Ответ 200:**
```json
[
  { "id": 10, "name": "Иванова А.А.", "specialization": "Офтальмолог" }
]
```

GET /schedule/{doctor_id} — свободные слоты

Ответ 200:

```json
{
  "doctor_id": 10,
  "available_slots": ["2026-11-01T10:00", "2026-11-01T11:30"]
}
```

POST /appointments — создать запись

Запрос:

```json
{
  "doctor_id": 10,
  "slot": "2026-11-01T10:00",
  "patient_id": 555
}
```

Ответ 201:

```json
{ "appointment_id": 777, "status": "created" }
```

Возможные ошибки:

· 400 Bad Request — неверные данные
· 409 Conflict — слот уже занят

```
