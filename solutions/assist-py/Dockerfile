# Базовый образ Python
FROM python:3.11-slim

# Автор и версия образа
LABEL maintainer="annin@lab.local"
LABEL version="1.0"

# Рабочая директория приложения
WORKDIR /app

# Персональный порт приложения
ENV PORT=5448

# Сначала копируем зависимости для отдельного слоя
COPY requirements.txt ./
RUN pip install -r requirements.txt

# Копируем исходный код приложения
COPY app/ ./app/

# Документируем порт приложения
EXPOSE ${PORT}

# Запускаем FastAPI через Uvicorn
CMD uvicorn app.main:app --host 0.0.0.0 --port ${PORT}
