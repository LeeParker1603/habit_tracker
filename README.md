# Трекер полезных привычек (Backend SPA)

Бэкенд-часть SPA-приложения для отслеживания привычек, разработанная на Django REST Framework (DRF) с интеграцией Celery и Telegram-бота для отправки напоминаний.

## Установка и запуск проекта

### 1. Подготовка окружения
Клонируйте репозиторий и перейдите в папку проекта:
```bash
git clone https://github.com
cd habit_tracker
```

Cоздайте виртуальное окружение и активируйте его:
```powershell
# Для Windows (PowerShell)
python -m venv venv
.\venv\Scripts\Activate.ps1
```

Установите необходимые зависимости:
```powershell
pip install -r requirements.txt
```

### 2. Настройка переменных окружения
Создайте файл `.env` на основе шаблона `.env.template` и заполните своими данными (настройки базы данных PostgreSQL, секретный ключ Django, токен Telegram-бота):
```powershell
cp .env.template .env
```

### 3. Миграции и запуск Django
Выполните миграции базы данных и запустите локальный сервер разработки:
```powershell
python manage.py migrate
python manage.py runserver
```

---

## Тестирование и покрытие (Coverage)

Для запуска Unit-тестов и проверки покрытия кода (критерий 80%+) выполните:
```powershell
coverage run --source='.' manage.py test
coverage report
```

---

## Запуск очередей задач (Celery & Telegram)

Для корректной работы периодических рассылок напоминаний в Telegram запустите в отдельных окнах терминала процессы воркера и планировщика (адаптировано под Windows):

1. **Запуск Celery Worker (выполнение задач):**
   ```powershell
   celery -A config worker -l info -P threads
   ```

2. **Запуск Celery Beat (планировщик расписания):**
   ```powershell
   celery -A config beat -l info
   ```