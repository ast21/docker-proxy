# Get started

## create network
```bash
docker network create --subnet=192.168.200.0/24 front
```

## and start it
```bash
docker-compose up -d
```

## Настройка ssl для домена
для домена `domain.example.com`, переименовать сертификаты по шаблону домена: `domain.example.com.crt`, `domain.example.com.key`. После скопировать сертификаты в папку `certs`.

## Настройка аутентификации на конкретный сервис
`htpasswd` находится внутри пакета `apache2-utils`, установить:
```bash
sudo apt install apache2-utils
```

нужно в папку `htpasswd/` добавить файл конфига `htpasswd` с названием `url`. Чтобы сгенерировать его, нужно воспользоваться следующей командой:
```bash
# example.domain.com - по какому url поставить аутентификацию
# some_user - имя пользователя
htpasswd -c ./htpasswd/example.domain.com some_user
```

------------------------------------------------------------
### other methods start proxy nginx:
1. with ssl
```bash
docker run -d --name nginx-proxy -p 80:80 -p 443:443 -v $CERTS_FOLDER:/etc/nginx/certs -v /var/run/docker.sock:/tmp/docker.sock:ro --net front --restart always jwilder/nginx-proxy
```
2. without ssl
```bash
docker run -d --name nginx-proxy -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro --net front --restart always jwilder/nginx-proxy
```
