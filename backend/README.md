## Как запустить проект

### 1. Клонировать репозиторий и перейти в директорию проекта

git clone https://github.com/yandex-praktikum/kittygram_backend.git
cd kittygram_backend

---

### 2. Запуск локально без Docker

1. Создайте и активируйте виртуальное окружение:

- Linux/macOS:

python3 -m venv env
source env/bin/activate


- Windows (PowerShell):

python -m venv env
.\env\Scripts\Activate.ps1


2. Обновите pip и установите зависимости:

python3 -m pip install --upgrade pip
pip install -r requirements.txt


3. Создайте файл `.env` в корне проекта и добавьте в него переменные окружения:

POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_HOST=localhost
DB_PORT=5432
SECRET_KEY='ваш_секретный_ключ'
DEBUG=1
ALLOWED_HOSTS=localhost,127.0.0.1


> Если у вас нет локального PostgreSQL, оставьте переменные `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD` пустыми или не задавайте — проект автоматически переключится на SQLite.

4. Выполните миграции:

python3 manage.py migrate


5. Запустите сервер разработки:

python3 manage.py runserver


---

### 3. Запуск с помощью Docker

1. Убедитесь, что у вас установлены Docker и Docker Compose.

2. Создайте `.env` файл в корне проекта с такими переменными:

POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_HOST=db
DB_PORT=5432
SECRET_KEY='ваш_секретный_ключ'
DEBUG=0
ALLOWED_HOSTS=localhost,127.0.0.1,backend,kittygramkosmo.sytes.net


3. Запустите контейнеры:

docker-compose up -d --build


4. Выполните миграции внутри контейнера backend:

docker-compose exec backend python manage.py migrate


5. При необходимости создайте суперпользователя:

docker-compose exec backend python manage.py createsuperuser


6. Откройте в браузере:

http://localhost:8000


---

## Структура проекта

- `backend/` — исходники Django backend
- `requirements.txt` — зависимости Python
- `Dockerfile` — образ для backend
- `docker-compose.yml` или `docker-compose.production.yml` — конфигурация Docker Compose
- `.env` — переменные окружения (не храните в репозитории!)

---

## Особенности

- В `settings.py` реализована универсальная логика подключения к базе данных:  
  - Если заданы переменные окружения для PostgreSQL — используется PostgreSQL  
  - Иначе — SQLite для удобства локальной разработки

- В Docker Compose сервис базы данных называется `db`, поэтому в Docker окружении `DB_HOST=db`.

- Для локального запуска вне Docker используйте `DB_HOST=localhost` или пустые переменные для переключения на SQLite.

---

## Полезные команды

- Запуск тестов:

python manage.py test


- Создание миграций:

python manage.py makemigrations


- Создание суперпользователя:

python manage.py createsuperuser