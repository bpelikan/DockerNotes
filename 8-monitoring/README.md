# 8. Monitoring

### 8.1 Wstęp do monitoringu
```bash
docker stats

#
docker container run -d --name apache1 httpd
docker container run -d --name apache2 httpd
docker container run -d --name redis1 redis
docker container run -d --name redis2 redis
docker container ls
docker container stats
docker container stats --no-stream
```
