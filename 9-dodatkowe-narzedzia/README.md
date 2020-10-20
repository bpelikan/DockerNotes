# 9. Dodatkowe narzędzia

### 9.1 Narzędzie z graficznym interfejsem 1

* [Portainer](https://www.portainer.io/)

```bash
docker container run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v P:\Docker\Portainer:/data portainer/portainer
docker container run -d nginx
```