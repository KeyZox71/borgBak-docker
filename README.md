# borgBak-docker
💾 A borg backup docker image with cron automation

```yml
build:
  context: .
  dockerfile: docker/bonus/borg-backup/Dockerfile
container_name: inception-backup
networks:
- inception
environment:
  - CRON_INTERVAL=0 2 * * *
  - BORG_PASSPHRASE_FILE=/run/secrets/borg-passphrase
  - BORG_PRUNE_KEEP_DAILY=3
  - BORG_PRUNE_KEEP_WEEKLY=2
  - BORG_PRUNE_KEEP_MONTHLY=1
  - BORG_LOG_LEVEL=info
  - BORG_CHECK_LAST=3
  - BORG_CHECK_DATA=1
depends_on:
  nginx:
    condition: service_healthy
volumes:
  - wp-db:/source/db
  - wp-site:/source/wordpress
  - backup:/backup
secrets:
  - borg-passphrase
restart: unless-stopped
```
