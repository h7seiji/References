# Docker

## Access shell inside container

```bash
docker exec -ti CONTAINER_NAME bash
```

## Compose

```bash
docker compose build api
```

```bash
docker compose up
```

```bash
docker compose -f compose.tests.yml up --exit-code-from api_tests
```

## Commands

```bash
docker system prune -a
```
