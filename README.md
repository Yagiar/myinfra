# MyInfra

Этот репозиторий содержит инфра сервисы.

## Требования

* Docker 20.10+
* Docker Compose v2
* **macOS / Linux / WSL2** — любое окружение, где доступен Docker-Daemon.

## Быстрый старт

```bash
# 1. Клонируйте репозиторий
 git clone https://github.com/Yagiar/myinfra.git
 cd myinfra
```
# 2. Сгенерируйте (или используйте свои) сертификаты для localhost
[Инструкция по генерации сертификатов](nginx/README.md)
# 3. Запустите стэк в фоне
 ```bash
 docker compose up -d
```
# 4. Откройте браузер

`https://localhost:8999`
```

При первом запуске OpenProject попросит вас создать учётную запись администратора.

## Структура проекта

```
myinfra/
├─ docker-compose.yml        # Определяет сервисы
└─ nginx/
   ├─ conf.d/openproject.conf # Конфиг виртуального хоста
   ├─ certs/                  # TLS-сертификаты (git-ignore)
   └─ README.md               # Детали по работе Nginx
```

## Изменение доменного имени / порта

1. В файле `docker-compose.yml` поменяйте `OPENPROJECT_HOST__NAME` на свой домен.
2. Обновите переменную `OPENPROJECT_HTTPS` (оставьте `"true"`).
3. В `nginx/conf.d/openproject.conf` измените `server_name`, а при необходимости и секцию `listen`.
4. Пересоздайте сертификат (или получите от Let’s Encrypt).

## Резервное копирование данных

* `openproject_pgdata` — PostgreSQL данные OpenProject.
* `openproject_data`  — загруженные пользователями файлы и ассеты.

Для бэкапа достаточно архивировать эти docker-тома (например, через `docker run --rm … tar`).

## Сценарии

В каталоге `scripts/` могут появляться вспомогательные скрипты.

## Обновление

```bash
# Остановить стэк
 docker compose down

# Получить свежий образ OpenProject
 docker pull openproject/openproject:latest

# Поднять заново
 docker compose up -d
```

Nginx обновляется аналогично (`docker pull nginx:alpine`).

---

Happy coding! 🎉
