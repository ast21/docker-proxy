# Get started

## create network
```sh
docker network create front
```

## and start it
```sh
docker-compose up -d
```

### FOR WINDOWS fix environment. Start windows powershell and first run:
```sh
$Env:COMPOSE_CONVERT_WINDOWS_PATHS=1
```
------------------------------------------------------------
### other methods start proxy nginx:
1. with ssl
```sh
docker run -d --name proxy-ssl -p 80:80 -p 443:443 -v D:\projects\proxy-ssl\ssl-certs:/etc/nginx/certs -v /var/run/docker.sock:/tmp/docker.sock:ro --net front --restart always jwilder/nginx-proxy
```

2. not ssl
```sh
docker run -d --name proxy -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro --net front --restart always jwilder/nginx-proxy
```

