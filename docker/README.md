# Docker Compose Continuous Deployment


## Useful commands

```bash
docker compose --profile build build

docker compose up -d
docker compose down
docker compose down --remove-orphans # --volumes

docker compose up -d --force-recreate hermes
docker compose down hermes
docker compose exec hermes hermes -p orchestrator
docker compose exec hermes bash

docker compose --profile coding-agent up -d --force-recreate hermes

```
