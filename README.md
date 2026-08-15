# Strapi v4 skeleton

A Strapi 4 application skeleton with SQLite, MariaDB, or PostgreSQL database support.

## Requirements

- Node.js 18.x
- npm 9 or newer
- Docker and Docker Compose (optional, for database services)

## Create a project

Clone this repository or use it as a GitHub template, then install the locked dependencies:

```bash
git clone https://github.com/contributte/strapi-v4-skeleton.git acme
cd acme
cp .env.example .env
npm ci
```

## Local development

The example configuration uses SQLite. Its database is stored in `.tmp/data.db`; no database service is required.

```bash
make dev
```

Open the application at [http://localhost:1337](http://localhost:1337). Create the initial administrator account at [http://localhost:1337/admin](http://localhost:1337/admin).

Use `make strapi-admin` to develop the admin UI, `make strapi-build` to build it, and `make start` to build and start Strapi.

## Docker database services

Docker Compose provides MariaDB, PostgreSQL, and Adminer; it does not run the Strapi application. Start the services with:

```bash
docker compose up -d
```

MariaDB is available on `localhost:3306`, PostgreSQL on `localhost:5432`, and Adminer at [http://localhost:8080](http://localhost:8080). Use `make docker-mariadb` to start only MariaDB.

Run `make dev` separately to start Strapi. The `make docker-dev` target runs an already built application image and requires `DOCKER_IMAGE` to be set.

## Configuration

Copy `.env.example` to `.env` and replace all placeholder secrets before deployment. Strapi reads the host and port from `HOST` and `PORT`; `DOMAIN` is used by plugin configuration.

Set `DATABASE_TYPE` to one of `sqlite`, `mysql`, or `postgres`:

- `sqlite` uses `DATABASE_FILENAME` (default: `.tmp/data.db`) and does not use `DATABASE_URL`.
- `mysql` and `postgres` require `DATABASE_URL` in the matching connection-string format, such as `mysql://strapi:strapi@127.0.0.1:3306/strapi` or `postgres://postgres:strapi@127.0.0.1:5432/strapi`.

The Compose MariaDB service provides the `strapi` database and `strapi`/`strapi` credentials. The PostgreSQL service provides the `strapi` database and the `postgres` user with password `strapi`. Set `DATABASE_SSL=true` only when the database connection requires TLS.

Optional S3, SMTP, and Sentry integrations are controlled by their respective `*_ENABLED` variables in `.env`.
