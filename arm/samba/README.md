# Configuration
```console
$ cat /var/docker/samba/smb.conf
```

```conf
[private]
path = /home/private/
writable = yes
```

# Run
```console
$ docker run \
  -d \
  -v /var/docker/samba/smb.conf:/etc/samba/smb.conf \
  -v /home/private/:/home/private/ \
  -p 445:445 \
  --name samba \
  inspir3/samba
```

# Authentification
Create an user with same name/uid than your Window user
```console
$ docker exec -it samba adduser -D -G users -u $UID -s /bin/sh $USER
$ docker exec -it samba smbpasswd -a $USER
```

Update your image to save your configuration
```console
$ docker commit samba inspir3/samba
```

# Compose
```console
$ cat compose-samba.yml
```

```yml
version: '3.7'
services:
  samba:
    image: inspir3/samba
    container_name: samba
    restart: unless-stopped
    volumes:
      - /var/docker/samba/smb.conf:/etc/samba/smb.conf
      - /home/private/:/home/private/
    ports:
      - '445:445'
    network_mode: bridge
```

```console
$ docker-compose -f compose-samba.yml up -d
```
