# Configuration
```console
# mkdir -p /var/docker/samba/
# cat > /var/docker/samba/smb.conf << EOF
[private]
path = /home/private/
writable = yes
EOF
```

# Run
```console
$ docker run \
  --detach \
  --volume /var/docker/samba/smb.conf:/etc/samba/smb.conf \
  --volume /home/private/:/home/private/ \
  --publish 445:445 \
  --name samba \
  inspir3/x86-samba
```

# Authentification
Create an user with same name/uid than your Window user
```console
$ docker exec -it samba adduser -D -G users -u $UID -s /bin/sh $USER
$ docker exec -i samba smbpasswd -a $USER << EOF
secret
secret
EOF
```

Update your image to save your configuration
```console
$ docker commit samba inspir3/x86-samba
```

# With docker-compose
```console
$ cat > ~/compose-samba.yml << EOF
version: '3.7'
services:
  samba:
    image: inspir3/x86-samba
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
$ cat >> ~/.profile << EOF
alias smb='docker-compose -f ~/compose-samba.yml'
EOF
$ . ~/.profile
$ smb up -d
```

# Info
```console
alpine:latest (5.55 Mb)
 |
 |__ inspir3/x86-samba:latest (40.5 Mb)

Total size: 46 Mb
```