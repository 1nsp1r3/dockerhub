# Configuration
```console
# mkdir -p /var/docker/samba/
```

```console
# cat > /var/docker/samba/smb.conf << EOF
[private]
path = /home/private/
writable = yes
EOF
```

# Authentification
Create an user with same name/uid than your Window user
```console
$ docker exec -it samba adduser -D -G users -u $UID -s /bin/sh $USER
```

```console
$ docker exec -i samba smbpasswd -a $USER << EOF
secret
secret
EOF
```

Update your image to save your configuration
```console
$ docker commit samba inspir3/arm-samba
```

# Run
```console
$ docker run                                              \
  --detach                                                \
  --volume /var/docker/samba/smb.conf:/etc/samba/smb.conf \
  --volume /home/private/:/home/private/                  \
  --publish 445:445                                       \
  --name samba                                            \
  inspir3/arm-samba
```

# Run with docker-compose
```console
$ cat > ~/compose-samba.yml << EOF
version: '3.7'
services:
  samba:
    image: inspir3/arm-samba
    container_name: samba
    restart: unless-stopped
    volumes:
      - /var/docker/samba/smb.conf:/etc/samba/smb.conf
      - /home/private/:/home/private/
    ports:
      - '445:445'
    network_mode: bridge
EOF
```

```console
$ docker-compose -f ~/compose-samba.yml up -d
```

# Info
```console
alpine:latest (3.74 Mb)
 |
 |__ inspir3/arm-samba:latest (29.4 Mb)

Total size: 33.1 Mb
```