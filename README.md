![icon](https://www.borgbackup.org/favicon.ico)


# borgBak-docker
A borg backup docker image with cron automation

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

## Contributing
Feel free to contribute to this project but there is a few rule you need to follow in [CONTRIBUTING.md](https://github.com/KeyZox71/borgBak-docker/blob/main/CONTRIBUTING.md) \
On this repo [KeyZox71/borgBak-docker](https://github.com/KeyZox71/borgBak-docker)

## License
This project is licensed under the MIT license - see the [LICENSE](https://github.com/KeyZox71/borgBak-docker/blob/main/LICENSE)
