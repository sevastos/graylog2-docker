graylog2-docker
===============

This docker image is a ready-to-run graylog2 server instance.

Configuration
--------------
For now there is only 1 configuration option, the admin password, you can set it using the environment variables with docker using `-e "GRAYLOG2_PASSWORD=adminpass"`

Use
---
Run as a daemon:

** Host Volumes Problem (OSX/Boot2Docker) **
Host volumes don't work at the moment with Boot2Docker 1.2, however it will work with on 1.3 using vbox shared folders.
The problem is that MongoDB doesn't work with vbox shared folders, so the only option is to use (Data Volumes)[http://docs.docker.com/userguide/dockervolumes/#data-volumes].
```
docker run -v /data --name yourData busybox true
docker run --name graylogger -d --volumes-from yourData -p 9000:9000 -p 12201:12201/udp -p 12201:12201 -p 12900:12900 -e "GRAYLOG2_PASSWORD=adminpass" sevastos/graylog2
```

From here on depending on your case use:
`--volumes-from yourData` or `/opt/graylogdocker/data:/data`

```
docker run --name graylogger -d -v /opt/graylogdocker/data:/data -p 9000:9000 -p 12201:12201/udp -p 12201:12201 -p 12900:12900 -e "GRAYLOG2_PASSWORD=adminpass" sevastos/graylog2
```


Bash in:
```
docker run --name graylogger --rm -t -i -v /opt/graylogdocker/data:/data -p 9000:9000 -p 12201:12201/udp -p 12201:12201 -p 12900:12900 -e "GRAYLOG2_PASSWORD=adminpass" sevastos/graylog2 /bin/bash
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
