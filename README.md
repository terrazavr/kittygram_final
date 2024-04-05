# MyCats 
- социальная сеть для владельцев и любителей сильных и незывисимых животных - КОШЕК и КОТОВ. Не имеет значения, домашнее или дикое животное, если вы счастливый обладатель тигрицы или пантеры - не стесняйтесь, делитесь с миром их фотографиями и достижениями!

### Это вариант проекта mycats собранного на контейнерах Docker и CI/CD с помощью GitHub Actions

## Как развернуть
1. Скачайте репозиторий
2. Создайте файл с переменными окружения .env (в репозитории есть файл пример .env.example)
```
POSTGRES_DB=<БазаДанных>
POSTGRES_USER=<имя пользователя>
POSTGRES_PASSWORD=<пароль>
DB_NAME=<имя БазыДанных>
```
3. Далее устанавите к Docker утилиту Docker Compose:
```
sudo apt update
sudo apt-get install docker-compose-plugin 
```
4. Запустите Dockercompose
```
sudo docker compose -f docker-compose.yml pull
sudo docker compose -f docker-compose.yml down
sudo docker compose -f docker-compose.yml up -d
```
5. Сделайте миграции и соберите статику
```
sudo docker compose -f docker-compose.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.yml exec backend cp -r /app/collected_static/. /backend_static/static/ 
```

## CI/CD c Git Hub Action
Добавьте следующие перменные в Secrets GitHub Actions
```
DOCKER_PASSWORD - пароль от Docker Hub
DOCKER_USERNAME - имя пользователя Docker Hub
HOST - ip сервера
SSH_KEY - ключ ssh для доступа к удаленному серверу
SSH_PASSPHRASE - пароль ssh
TELEGRAM_TO - id пользователя TELEGRAM
TELEGRAM_TOKEN - TELEGRAM токен
USER - имя пользователя сервера
```

Workflow в проекте уже описан, осталось запушить его в репозиторий и смотреть на как все автоматизировалось
