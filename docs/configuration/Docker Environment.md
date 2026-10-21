# Docker Environment

This is the example environment file:

```yaml 
# Image version  
EUROKEEP_VERSION=rc

# Host port of the app. HTTP only.
# Not needed if you want to use the traefik drop-in.
EUROKEEP_PORT=8080

# Public address including https://. Required: without it the API refuses every request.
APP_FULL_BASE_URL=https://eurokeep.example.org

# Random value: openssl rand -hex 32
# NEVER change it after the first start.
SECURITY_SALT=

# Never true in production, it exposes stack traces.
DEBUG=false

ENABLE_REGISTRATION=false

# --- Standalone (standalone-*.yml): MariaDB database is created automatically on the first start.
DATABASE_NAME=eurokeep
DATABASE_USER=eurokeep
DATABASE_USER_PW=somesecretpassworddefinetelynotthisone

# --- Integrated (integrated-*.yml): your own database server.
#DATABASE_URL=mysql://eurokeep:<password>@<db-host>:3306/eurokeep?encoding=utf8mb4
# Existing Docker network through which <db-host> is reachable.
#DATABASE_NETWORK=mariadb-internal

# --- Development (*-development.yml): host directory for the nginx logs (access.log, error.log).
# Unset: no log files, nginx logs to stdout/stderr (docker compose logs).
#NGINX_LOG_DIR=/var/log/nginx

# --- Traefik (traefik.yml)
#EUROKEEP_DOMAIN=eurokeep.example.org
#TRAEFIK_NETWORK=docker-internal
#TRAEFIK_ENTRYPOINT=websecure
#TRAEFIK_CERTRESOLVER=letsencrypt
```



## Environment Settings explained

### ENABLE_REGISTRATION
Always, ALWAYS set this to `false` unless you are creating a user or resetting a user's password right now. Never ever keep this set to `true`.
If `true`, the login form shows the `Create account` button. Just specify a new user's username and password, click 'create account` and the new user is good to go.
See [User Creation](/manual/User Management/#creating-a-user)

### DEBUG
By default, set to `false`. When `true`, the EuroKeep application will respond with detailed error details, stacktraces, etc.
If `true`, this could leak sensitive information, so better keep it set to `false`, unless you know, what you are doing.

### DATABASE_NAME
The name of the database, that will be used.

### DATABASE_USER
The username, the EuroKeep API uses to authenticate to the database.

### DATABASE_USER_PW
The password, the EuroKeep API uses to authenticate to the database, combined with DATABASE_USER

### DATABASE_URL
The User URL that lets EuroKeep API authenticate to your own database server.

### DATABASE_NETWORK
If your own DATABASE_URL points to a docker network, you can configure that here.

### NGINX_LOG_DIR
Host directory to put nginx logs (`access` and `error`). If removed, access logs will be put to stdout.

### EUROKEEP_DOMAIN
The FQDN that points to your instance of EuroKeep.

### TRAEFIK_NETWORK
If you use traefik with a virtual docker network, you can configure that here.

### TRAEFIK_ENTRYPOINT
This is the entrypoint EuroKeep will be available on.

### TRAEFIK_CERTRESOLVER
This is the certresolver for Traefik.
