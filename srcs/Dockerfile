FROM			alpine:3.21 AS builder

RUN				apk add go

WORKDIR			/build

COPY			go.sum /build/go.sum
COPY			go.mod /build/go.mod
COPY			cmd /build/cmd
COPY			internal /build/internal

RUN				cd /build \
				&& go build git.keyzox.me/42_adjoly/inception/cmd/borg-backup/entrypoint \
				&& go build git.keyzox.me/42_adjoly/inception/cmd/borg-backup/getpassphrase

FROM			alpine:3.21

LABEL			version="0.1"
LABEL			maintainer="KeyZox"

RUN				mkdir -p /backup \
				&& mkdir -p /source \
				&& mkdir /docker-entrypoint.d \
				&& mkdir /docker-backup.d

RUN				apk add --no-cache borgbackup tzdata \
				&& rm -rf /var/cache/apk/*

COPY			--from=builder /build/entrypoint /docker-entrypoint
COPY			--from=builder /build/getpassphrase /bin/getpassphrase
COPY			default-bak.sh /docker-backup.d/default-bak.sh

ENTRYPOINT		[ "/docker-entrypoint" ]
WORKDIR			/

STOPSIGNAL		SIGQUIT

CMD				[ "crond", "-l", "8", "-f" ]
