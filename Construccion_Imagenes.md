
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
------------

1. Hacemos el build en mi con mi perfil (cecum)
```
docker build -t cecum/prueba .
```

2. Hacemos push de la imagen generada

```
docker push cecum/prueba
``` 
