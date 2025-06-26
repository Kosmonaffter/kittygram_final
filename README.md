# Kittygram Final Project

## Как запустить проект

### 1. Клонировать репозиторий и перейти в директорию проекта

git clone https://github.com/Kosmonaffter/kittygram_final.git
cd kittygram_final

### 2. Создать и запустить контейнеры, выполнить миграции и собрать статику

Все эти шаги автоматизированы и выполняются через GitHub Actions при пуше в ветку `main`.

### 3. Запушить изменения в ветку `main`

git add .
git commit -m "Deploy Kittygram"
git push origin main


После пуша:

- Запустится автоматическое тестирование backend и frontend
- Соберутся и опубликуются Docker-образы на Docker Hub
- На удалённом сервере обновятся контейнеры с новыми образами
- Выполнятся миграции и сбор статики
- Вы получите уведомление в Telegram о статусе деплоя

---

## Важные моменты

- Для корректной работы CI/CD настройте секреты в GitHub (Docker Hub, SSH, Telegram и др.)
- Убедитесь, что на сервере настроен Docker Compose и доступен SSH по ключу
- Вся инфраструктура и деплой автоматизированы — ручные действия не требуются

---

## Дополнительные инструкции

Если хотите запустить проект локально без GitHub Actions, используйте:

docker-compose up -d --build
docker-compose exec backend python manage.py migrate
docker-compose exec backend python manage.py collectstatic --noinput

---

*Теперь вы готовы к работе с Kittygram! Просто пушьте в main — и проект автоматически развернётся.*
