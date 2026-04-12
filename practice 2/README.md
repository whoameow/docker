<<<<<<< HEAD
# Задание 2: Использование Yandex Mirror Registry

## Цель

Научиться использовать альтернативные Docker-репозитории (зеркала) вместо Docker Hub.

---

## Yandex Mirror

**URL**: `cr.yandex/mirror/`

Формат образа:
```dockerfile
FROM cr.yandex/mirror/<образ>:<тег>
```

**Примеры:**
- `cr.yandex/mirror/python:3.11-slim`
- `cr.yandex/mirror/node:18-alpine`
- `cr.yandex/mirror/nginx:alpine`
- `cr.yandex/mirror/ubuntu:22.04`

---

## Задание

Написать Dockerfile, который:
1. Использует базовый образ **из Yandex Mirror**: `cr.yandex/mirror/python:3.11-slim`
2. Устанавливает рабочую директорию `/app`
3. Устанавливает переменную окружения `REGISTRY="Yandex Mirror"`
4. Копирует `app.py`
5. Работает от пользователя `1001`
6. Открывает порт `8080`


## Выполнение

### Шаг 1: Собрать образ

### Шаг 2: Запустить контейнер 

### Шаг 3: Проверить

```bash
# Проверить логи
docker logs yandex-app

# Проверить в браузере
# http://localhost:8080

# Проверить переменную
docker exec yandex-app env | grep REGISTRY
```

---
=======
# Задание 10: Контейнеры крашатся - найди все проблемы

## Проблема
6 контейнеров, все с проблемами. Ничего не работает.

## Запуск
```bash
cd d10
docker-compose up
# Смотри на ошибки
```

## Диагностика
```bash
# Статус контейнеров
docker-compose ps

# Логи
docker-compose logs app1
docker-compose logs app6

# Exit codes
docker inspect app4 --format='{{.State.ExitCode}}'
docker inspect app5 --format='{{.State.ExitCode}}'

# Проверка портов
docker ps -a | grep 8080
```

## 6 проблем:

**1. app1 - нет конфига**
```
Error: ./config/app1.conf not found
Fix: cp config/app1.conf.example config/app1.conf
```

**2. app2 - конфликт портов**
```
Error: port 8080 already in use
Fix: Изменить порт на 8081:80
```

**3. app3 - read-only volume**
```
Error: Read-only file system
Fix: Убрать :ro или создать ./data директорию с правами
```

**4. app4 - exit 0 при ошибке**
```
Fix: Убрать "|| exit 0", использовать set -e
```

**5. app5 - restart loop**
```
Fix: Изменить restart: always на restart: "no"
```

**6. app6 - нет обязательной env**
```
Error: POSTGRES_PASSWORD not set
Fix: Добавить environment: POSTGRES_PASSWORD: secret
```
>>>>>>> c11f7f4527513c11863c5445b5da891bf51fdc7f
