# Docker

## EuroKeep is Available For Docker
EuroKeep is available on docker hub.
Create a directory to put the [Environment file](#environment-file) and the [Compose File](#compose-file).
Then run `docker compose up` and EuroKeep will be downloaded and started.

# Compose File
This file, as of October 21st 2026 is just an example, but it works. It tells docker to deploy two separate services: The EuroKeep application and a designated instance of mariadb.

```yaml
services:
  eurokeep:
    image: eurokeep/eurokeep:${EUROKEEP_VERSION:-rc}
    restart: unless-stopped
    ports:
      - "8080:8080"
    environment:
      DATABASE_URL: mysql://eurokeep:${DATABASE_USER_PW:?}@db:3306/eurokeep?encoding=utf8mb4
      SECURITY_SALT: ${SECURITY_SALT:?}
      APP_FULL_BASE_URL: ${APP_FULL_BASE_URL:?}
      ENABLE_REGISTRATION: ${ENABLE_REGISTRATION:-false}
      DEBUG: ${DEBUG:-false}
    volumes:
      - uploads:/var/www/html/uploads
      - logs:/var/www/html/logs
    depends_on:
      db:
        condition: service_healthy

  db:
    image: mariadb:11.8
    restart: unless-stopped
    environment:
      MARIADB_DATABASE: eurokeep
      MARIADB_USER: eurokeep
      MARIADB_PASSWORD: ${DATABASE_USER_PW:?}
      MARIADB_RANDOM_ROOT_PASSWORD: "1"
    volumes:
      - db:/var/lib/mysql
    healthcheck:
      test: ["CMD", "healthcheck.sh", "--connect", "--innodb_initialized"]
      interval: 10s
      retries: 10
      start_period: 30s

volumes:
  db:
  uploads:
  logs:
```

# Environment File

The environment file `.env` in your docker directory determines the most important settings. This one is much limited but it deploys a working instance of EuroKeep.
For further information, please refer to the [Docker Environment Documentation](/configuration/Docker Environment/)

```yaml
APP_FULL_BASE_URL=https://eurokeep.my.example.domain
SECURITY_SALT=353d9d20b333fa9cd514e2e3cb7768ae9109f5as58e6bc128ecc783ff5c190cc          # openssl rand -hex 32  — never change it after the first start
DATABASE_USER_PW=Another0neBytesTheDu$t!
EUROKEEP_VERSION=rc
ENABLE_REGISTRATION=false
DEBUG=false
```

# Running Commands

Many management commands need to be executed in the EuroKeep container, since they are part of the CakePHP binaries.

Run them with `docker compose exec` from your docker directory. For example, this command creates a new user:

```bash
docker compose exec eurokeep bin/cake user_add
```
