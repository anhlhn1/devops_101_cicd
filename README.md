# 1. Setup full Jenkins, SonarQube, Nexus
```bash
# Initial setup
docker compose down --remove-orphans && docker network prune && docker compose up

# Restart all services
docker compose up
```