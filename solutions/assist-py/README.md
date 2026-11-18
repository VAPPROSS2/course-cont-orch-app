# Personal Assistant

Персональный ассистент на FastAPI. Проект используется в лабораторных работах по Docker и контейнерной оркестрации.

**Автор:** Аннин Макар Дмитриевич  
**Персональный префикс:** `annin`  
**Персональный порт:** `5448`

## Сборка и запуск

```bash
docker build -t annin-assistant:v1 .
docker run -d \
  --name annin-assistant-1 \
  -p 5448:5448 \
  -e APP_OWNER=annin \
  -e APP_SECRET="$APP_SECRET" \
  annin-assistant:v1
```

Перед запуском задайте секрет в переменной окружения текущего терминала:

```bash
export APP_SECRET='secret18annin'
```

Не сохраняйте секрет в репозитории и не добавляйте файл `.env` в Git.

## Переменные окружения

| Переменная | Назначение | Значение |
| --- | --- | --- |
| `APP_OWNER` | Имя владельца, отображается в ответах API | `annin` |
| `APP_SECRET` | Секрет для эндпоинта `/secret/{key}` | задаётся при запуске |
| `PORT` | Порт Uvicorn внутри контейнера | `5448` |

## Проверка

```bash
curl http://localhost:5448/
curl http://localhost:5448/me
curl -X POST http://localhost:5448/notes \
  -H "Content-Type: application/json" \
  -d '{"text":"ЛР2: сборка образа"}'
curl http://localhost:5448/notes
curl http://localhost:5448/secret/secret18annin
```

Проверка готовности приложения:

```bash
curl http://localhost:5448/health
```

## Эндпоинты

- `GET /` — приветствие и информация о сервисе.
- `GET /me` — персональные параметры владельца.
- `GET /health` — состояние приложения.
- `GET /notes` — список заметок.
- `POST /notes` — создание заметки.
- `GET /secret/{key}` — проверка секретного ключа.
- `GET /weather/{city}` — погода через Open-Meteo.
