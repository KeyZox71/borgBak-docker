# [borgBak-docker](https://hub.docker.com/r/keyzox/borg-backup)
💾 A borg backup docker image with cron automation


```yml
services:
  backup:
    image: keyzox/borg-backup
    environment:
      - CRON_INTERVAL=0 2 * * *
      - BORG_PASSPHRASE_FILE=/run/secrets/borg-passphrase
      - BORG_PRUNE_KEEP_DAILY=3
      - BORG_PRUNE_KEEP_WEEKLY=2
      - BORG_PRUNE_KEEP_MONTHLY=1
      - BORG_LOG_LEVEL=info
      - BORG_CHECK_LAST=3
      - BORG_CHECK_DATA=1
    volumes:
      - src:/source
      - backup:/backup
    secrets:
      - borg-passphrase
    restart: unless-stopped

volumes:
  src:
  backup:

secrets:
  borg-passphrase:
    file: ./borg-passphrase.txt
```
