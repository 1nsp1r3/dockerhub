FROM alpine:latest

RUN apk update && \
  apk add samba

EXPOSE 445/tcp

ENTRYPOINT ["/usr/sbin/smbd", "-FS", "--no-process-group"]
