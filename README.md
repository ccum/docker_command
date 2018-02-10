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
Listar contenedores ejecutandose
```
docker ps
```
Obtener mas información de un contenedor
```
docker inspect <CONTAINER ID>
```
```
docker inspect -f '{{.Name}}' <CONTAINER ID>
```
Stop container
```
docker stop <CONTAINER ID>
```
Listar container parados y ejecutandose
```
docker ps -a
```
Listar solo ID
```
docker ps -q
```
Arrancar container
```
docker start <CONTAINER ID>
```
Parar todos los contenedores
```
docker stop `docker ps -q`
```
Borrar contenedores 
```
docker rm <CONTAINER ID>
```
Borrar contenedores ejecutandose
```
docker rm -f <CONTAINER ID>
```
Copiar ficheros dentro del contenedor y fuera de contedor
```
docker cp <CONTAINER ID>:/.fichero
```
Ejecutar un comando dentro del contenedor
```
docker exec <CONTAINER ID> <COMANDO>
docker exec <CONTAINER ID> ls 
```:white_check_mark: