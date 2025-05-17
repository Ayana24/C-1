# 🏔️ FSTR API — Перевалы

Этот проект реализует REST API для отправки и модерации информации о горных перевалах. Используется Django + Django REST Framework + PostgreSQL.

---

## 📦 Установка и запуск (Docker)

```bash
docker-compose up --build
```

Проект будет доступен по адресу:  
[http://localhost:8000](http://localhost:8000)

---

## 📌 Описание API

### 📤 POST `/submitData/`

Добавить информацию о перевале.

**Пример запроса:**

```json
{
  "user": {
    "email": "ivan@example.com",
    "fam": "Иванов",
    "name": "Иван",
    "otc": "Иванович",
    "phone": "89991112233"
  },
  "coords": {
    "latitude": 45.123,
    "longitude": 37.456,
    "height": 1200
  },
  "beauty_title": "пер.",
  "title": "Ай-Юлю",
  "other_titles": "Аюлю",
  "connect": "",
  "level_winter": "1A",
  "level_summer": "1B",
  "level_autumn": "1A",
  "level_spring": "1A",
  "images": [
    {"title": "Вид на перевал", "data": "<base64 изображение>"},
    {"title": "Фото со спуска", "data": "<base64 изображение>"}
  ]
}
```

**Пример ответа:**

```json
{
  "status": 200,
  "message": "Перевал успешно добавлен",
  "id": 42
}
```

---

### 📥 GET `/submitData/<id>/`

Получить информацию о перевале по ID.

**Пример ответа:**

```json
{
  "id": 42,
  "status": "new",
  "user": { ... },
  "coords": { ... },
  "title": "Ай-Юлю",
  ...
}
```

---

### ✏️ PATCH `/submitData/<id>/`

Изменить информацию о перевале (если статус — `new`).  
**FIO, email и телефон редактировать нельзя.**

**Пример запроса:**

```json
{
  "title": "Ай-Юлю обновлён",
  "level_summer": "1A+"
}
```

**Ответ:**

```json
{
  "state": 1,
  "message": "Запись успешно обновлена"
}
```

---

### 📧 GET `/submitData/?user__email=ivan@example.com`

Получить список всех перевалов, добавленных пользователем по email.

---

## 🔐 Переменные окружения

Создайте `.env` в корне:

```
FSTR_DB_HOST=localhost
FSTR_DB_PORT=5432
FSTR_DB_LOGIN=postgres
FSTR_DB_PASS=yourpassword
DJANGO_SECRET_KEY=секретный_ключ
```

---

## 🧪 Тесты

```bash
python manage.py test
```
