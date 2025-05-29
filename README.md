# Проектная работа дисциплины «Docker-контейнеризация и хранение данных»
Настроить контейнеризацию существующего приложения с использованием Docker и Docker Compose, а также обеспечить безопасность образов и контейнеров. 

* backend — бэкенд приложения (Go).
* frontend — фронтенд приложения (Vue.js).

### Запуск

В корневой директории проекта выполнить:
* для dev окружения - выполняется сборка: `docker compose up`
* для prod - будет запущен последний образ из dockerhub с повышенной безопасностью:  `docker compose -f docker-compose.prod.yml up -d`

Сервис будет доступен на 80 порту указанного NGINX_SERVER_NAME (например http://localhost)

### Описание
* backend собран на основе легковесного образа alpine:3.21 с использованием multi-stage, дополнительно установлен curl для healthcheck (размер 28.69 MB) 

* frontend собран на основе легковесного non-root образа nginxinc/nginx-unprivileged:1.27-alpine с использованием multi-stage (размер 51.43 MB)

В Docker Compose настроены:
* изолированные сети
* перезапуск контейнеров
* healthchecks
* запуск frontend после backend (для prod окружения)
* убраны лишние capabilities (для prod окружения)
* лимиты ресурсов (для prod окружения)

### Параметры

* `NGINX_SERVER_NAME` - указать имя хоста для работы nginx (по умолчанию localhost)
* `NGINX_BACKEND_ADDRESS` - указать адрес api бэкенда (по умолчанию http://backend:8081/)

