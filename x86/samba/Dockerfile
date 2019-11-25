FROM alpine:latest

RUN apk update && \
  apk add samba

EXPOSE 445/tcp

ENTRYPOINT ["/usr/sbin/smbd", "-FS", "--no-process-group"]

# docker build --network host -t inspir3/x86-samba ./
# docker login && docker push inspir3/x86-samba
