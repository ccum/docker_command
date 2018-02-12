
Construcción de Imágenes
========================

Dockerfile
----------
```
FROM ubuntu:latest
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev
WORKDIR /app
ENV DEBUG=True
EXPOSE 80
VOLUME /data
COPY . /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
```

1. FROM image : para definir la imagen base de nuestro contenedor.
2. RUN comando : para ejecutar un comando en el contexto de la imagen.
3. ENTRYPOINT comando : para definir el entrypoint que ejecuta el container al arrancar.
4. CMD comando : para definir el comando que ejecuta el container al arrancar.
5. WORKDIR path : para definir el directorio de trabajo en el contenedor.
6. ENV var=value : para definir variables de entorno.
7. EXPOSE puerto : para definir puertos donde el contenedor acepta conexiones.
8. VOLUME path : para definir volúmenes en el contenedor.
9. COPY origen destino : para copiar ficheros dentro de la imagen. También se usa para multi-stage builds.

Docker Build
------------
```
docker build -t prueba .
```

![config](https://image.prntscr.com/image/4_ajbm6zTMaqyjdK5taakw.png)

Push to Docker HUB
-------------------

1. Hacemos el build en mi con mi perfil (cecum)
```
docker build -t cecum/prueba .
```

2. Hacemos push de la imagen generada

```
docker push cecum/prueba
``` 
Login on Dockerhub
-------------------

```
docker login
```

Docker pull
-----------

```
docker pull
```

listar Imagenes Locales
-----------

```
docker images ls
```

Inspect de Imagenes Locales
-----------
```
docker inspect <ID_IMAGEN>
```

Borrado de Imagenes Locales
-----------
```
docker image rm <IMAGE ID>
```

Buenas prácticas
----------------

1. Usa .dockerignore
2. Reduce el tamaño de tus imágenes al mínimo
3. Ejecuta sólo un proceso por contenedor
4. Minimiza el número de capas de tu imagen

```
RUN apt-get update
RUN apt-get install -y bzr
RUN apt-get install -y cvs
RUN apt-get install -y git
RUN apt-get install -y mercurial
```

Por

```
RUN apt-get update && apt-get install -y \
    bzr \ 
    cvs \ 
    git \ 
    mercurial \ 
    apt-get clean
```
5. Optimiza el uso de la cache .
>Optimiza el uso de la cache añadiendo al principio de tu Dockerfile las instrucciones que menos cambian (como la instalación de librerías), y dejando para el final las que más cambian (como el copiado del código fuente). 

6. Parametriza tus Dockerfiles usando argumentos
7. Utiliza multi-stage builds

Desarrollo con Contenedores
===========================

Docker Compose y docker-compose.yml
