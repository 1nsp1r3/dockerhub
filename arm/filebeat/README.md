# Configuration
```console
# mkdir -p /var/docker/elk/etc/filebeat/ && \
  mkdir -p /var/docker/elk/filebeat/     && \
  mkdir -p /var/docker/elk/log
```

```console
# cat > /var/docker/elk/etc/filebeat/filebeat.yml << EOF
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/docker/elk/log/*.log

output.logstash:
  hosts: ["elk:5044"]
  ssl.certificate_authorities: ["/var/docker/elk/etc/logstash-beats.crt"]
EOF
```

```console
# echo "51.38.49.219    elk2" >> /etc/hosts
```

# Run
```console
$ docker run                                                                             \
  --detach                                                                               \
  --volume /var/docker/elk/etc/filebeat/:/etc/filebeat/                                  \
  --volume /var/docker/elk/filebeat/:/var/lib/filebeat/                                  \
  --volume /var/docker/elk/log/:/var/docker/elk/log/                                     \
  --volume /var/docker/elk/etc/logstash-beats.crt:/var/docker/elk/etc/logstash-beats.crt \
  --network host                                                                         \
  --name filebeat                                                                        \
  inspir3/arm-filebeat
```

# Run with docker-compose
```console
$ cat > compose-filebeat.yml << EOF
version: '3.7'
services:
  filebeat:
    image: inspir3/arm-filebeat
    container_name: filebeat
    restart: "no"
    volumes:
      - /var/docker/elk/etc/filebeat/:/etc/filebeat/
      - /var/docker/elk/filebeat/:/var/lib/filebeat/
      - /var/docker/elk/log/:/var/docker/elk/log/
      - /var/docker/elk/etc/logstash-beats.crt:/var/docker/elk/etc/logstash-beats.crt
    network_mode: host
EOF
```

```console
$ docker-compose -f compose-filebeat.yml up -d
```

# Info
```console
alpine:latest (3.74 Mb)
 |
 |__ inspir3/arm-filebeat:latest (139 Mb)

Total size: 143 Mb
```
