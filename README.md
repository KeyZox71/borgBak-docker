# [borgBak-docker](https://hub.docker.com/r/keyzox/borg-backup)
💾 A borg backup docker image with cron automation


## Supported tags and respective Dockerfile links
- [latest](https://github.com/KeyZox71/borgBak-docker/commit/c4603fc858d38c9b36782428884c731e8a82011a)

## Compose example

```yml
services:
  backup:
    image: keyzox/borg-backup:latest
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

## License
This project is licensed under the MIT license - see the [LICENSE]()
