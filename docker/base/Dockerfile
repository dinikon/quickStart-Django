# Используем официальный образ Python как базовый
FROM python:3.12-slim
LABEL authors="inikon"

# Устанавливаем рабочую директорию в контейнере
WORKDIR /django-app

# Копируем зависимости
COPY ./app/requirements.txt /django-app/requirements.txt

# Устанавливаем зависимости
RUN pip install --no-cache-dir -r /django-app/requirements.txt

# Копируем остальные файлы проекта
COPY ./app /django-app/

# Указываем порт, который будет слушать контейнер
EXPOSE 8000

# Записываем статические файлы
CMD ["python", "manage.py", "collectstatic", "--noinput"]

# Запускаем Django-приложение
CMD ["python", "-m", "gunicorn", "app.asgi:application", "-k", "uvicorn.workers.UvicornWorker", "--bind", "0.0.0.0:8000"]