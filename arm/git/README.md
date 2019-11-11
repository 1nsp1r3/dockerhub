# Authentification
Create an user with same name/uid than your Linux user
```console
$ docker run \
  -it \
  --name git \
  inspir3/arm-git \
  adduser -D -G users -u $UID -s /bin/sh $USER
```

Update your image to save your configuration
```console
$ docker commit git inspir3/arm-git
$ docker rm git
```

# Usage
```console
$ cat > ~/bin/git << EOF
#!/bin/sh

docker run \
  --user $USER \
  --volume \$HOME/:\$HOME/ \
  --workdir \$PWD/ \
  -ti --rm \
  inspir3/arm-git /usr/bin/git "\$@"
EOF
$ chmod +x ~/bin/git
$ git --version
```

# Info
```console
alpine:latest (3.74 Mb)
 |
 |__ inspir3/arm-git:latest (17.4 Mb)

Total size: 21.1 Mb
```
