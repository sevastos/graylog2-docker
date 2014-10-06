graylog2-docker
===============

This docker image is a ready-to-run graylog2 server instance.

Configuration
--------------
For now there is only 1 configuration option, the admin password, you can set it using the environment variables with docker using `-e "GRAYLOG2_PASSWORD=adminpass"`

Use
---
Run as a daemon:
```
docker run -d -v /opt/graylogdocker/data:/data -p 9000:9000 -p 12201:12201/udp -p 12201:12201 -p 12900:12900 -e "GRAYLOG2_PASSWORD=adminpass" sevastos/graylog2
```

Bash in:
```
docker run --rm -t -i -v /opt/graylogdocker/data:/data -p 9000:9000 -p 12201:12201/udp -p 12201:12201 -p 12900:12900 -e "GRAYLOG2_PASSWORD=adminpass" sevastos/graylog2 /bin/bash
```

Manual execute (for convenience):
```
nohup /etc/service/elasticsearch/run&
nohup /etc/service/mongod/run&
nohup /etc/service/graylog2-server/run&
nohup /etc/service/graylog2-web-interface/run&
```

Tail logs:
```
tail -f /var/log/elasticsearch.log /var/log/mongodb/mongodb.log /var/log/graylog2-server.log /var/log/graylog2-web-interface.log
```
