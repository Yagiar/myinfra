# Nginx-прокси для OpenProject

Каталог содержит конфигурацию виртуального хоста и TLS-сертификаты, которые использует сервис `nginx` из `docker-compose.yml`.

## Генерация самоподписанных сертификатов

Выполните команду **один раз**, чтобы создать самоподписанный сертификат для `localhost`:

```bash
mkdir -p certs
openssl req -x509 -nodes -days 365 \
  -newkey rsa:2048 -keyout certs/openproject.key \
  -out certs/openproject.crt \
  -subj "/CN=localhost"
```

Оба файла `openproject.crt` и `openproject.key` должны лежать в каталоге `nginx/certs/`, который монтируется внутрь контейнера.

> 💡 **В проде** лучше использовать сертификаты от доверенного УЦ (например, Let’s Encrypt).
