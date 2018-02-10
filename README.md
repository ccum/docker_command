Comandos Docker
==============

Básicos
-------------
```
docker info
```
```
docker version
```
```
docker help
```
```
docker container run --help
```

Correr una imagen
```
docker run -d -p 80:80 nginx
```
Listar contenerdores que se tiene en el host
```
docker ps
```
Obtener mas insformacion de un contenedor
```docker inspect <CONTAINER ID>
```