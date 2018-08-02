Comandos de gestión de contenedores
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
docker run -d <IMAGEN ID>
docker run -d -p 80:80 nginx
docker run -d mysql
docker run --name myAlpineContainer -it <IMAGEN ID>
docker run --rm --name myAlpineContainer -it <IMAGEN ID>
```
agregamos ´´´--rm´´´ para cuando el contenedor se pare se elimine automaticamente


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
```
docker start -ai <CONTAINER ID>
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
docker exec <CONTAINER ID> sh
docker exec -it <CONTAINER ID> sh bash
```
:white_check_mark:

Log del contenedor

```
docker logs <CONTAINER ID>
```
Listar CPU,memoria,etc
```
docker stat <CONTAINER ID>
```
Borrar la basura de docker (imagenes sin usar, volunenes, redes)
```
docker system prune -a
```
Variables $DOCKER_HOST, es para coneectarnos a otros host donde tengamos un demonio docker instalado
Configuración cluster
```
export DOCKER_HOST="tcp://ucp.dckr.io:443"
export DOCKER_TLS_VERIFY=1
export DOCKER_CERT_PATH="~/ucp/stage"
```

![config](https://image.prntscr.com/image/sQNAL2F1SYKjg704xhOziw.png)

ejecución y listado re deamon remote

![config](https://image.prntscr.com/image/ZnMxI8eIRK6V66b124eDgQ.png)

Docker y microservicios

![config](https://image.prntscr.com/image/NFGbjRnxS0ejJyeN356KFw.png)