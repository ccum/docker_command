Desarrollo con Contenedores
===========================

Docker Compose y docker-compose.yml
-----------------------------------

Docker Compose se define un fichero docker-compose.yml 

```
db:
    image: mysql:5.7
    restart: always
    environment:
    MYSQL_ROOT_PASSWORD: password
wordpress:
    image: wordpress:latest
    depends_on:
    - db
    ports:
    - "8000:80"

```

```
app:
image: myapp
build:
    context: ./dir
    dockerfile: Dockerfile
    args:
    - arg1=val1
    - arg2=val2
```
levantar la aplicación es simplemente:

```
docker-compose up -d
```

[Ejemplo](https://github.com/ccum/docker-for-devs/blob/master/auto-build/docker-compose.yml)

Comandos comunes de compose I
-----------------------------

```
docker-compose up
docker-compose pull
docker-compose build
docker-compose push
docker-compose run
docker-compose rm
```

Destacar los siguientes puntos sobre docker-compose:
docker-compose up -d levanta la aplicación en modo demonio, docker-compose up la levanta en primer plano, mostrando los logs de los distintos contenedores. La ejecución sucesiva del comando docker-compose up -d sólo recrea los contenedores que hayan cambiado su imagen o su definición. docker-compose up -d no hace el build cada vez que es invocado de las imágenes locales. Si deseas actualizar tu aplicación en base a los últimos cambios de tu código, tendrás que ejecutar docker-compose up --build -d. Un truco para mejorar este proceso es montar tu código como un volumen en el fichero docker-compose.yml, de tal manera que tu container siempre ve los últimos cambios en tu código fuente. Si quieres levantar solo uno o varios de los servicios en un compose, puedes añadir su nombre, por ejemplo docker-compose up -d redis.

docker-compose pull actualiza las imágenes definidas en el compose con la versión actual que haya en el registro. En otras palabras, si alquien hace un push al registro, actualiza la versión de estas imágenes en nuestra máquina. Con la opción --parallel hace el pull en paralelo. Como todo comando de docker-compose se puede hacer pull de un subconjunto de servicios: docker-compose pull servicioA ServicioB.

docker-compose build reconstruye las imágenes de los servicios que tengan una sección de build definida. Opciones interesantes son: --no-cache para invalidad la caché, --pull para hacer pull de las imágenes base y --build-arg key=val para pasar argumentos. Como todo comando de docker-compose se puede hacer build de un subconjunto de servicios: docker-compose build servicioA ServicioB.

docker-compose push pushea al registro la versión local de las imágenes con una sección de build definida. Como todo comando de docker-compose se puede hacer pull de un subconjunto de servicios: docker-compose push servicioA ServicioB.

docker-compose run ejecuta un contenedor de uno de los servicios definido en el compose. La diferencia principal con docker-compose up es que permite definir el comando a ejecutar, así como otra información de contexto como variables de entorno, el entrypoint, volúmenes, el directorio de trabajo… Es uno de los comandos más útil para el entorno del desarrollador. Por ejemplo, podemos definir un servicio en nuestro docker-compose.yml con todas las dependencias necesarios para ejecutar nuestros comandos de desarrollo. Haciendo uso de docker-compose run podemos ejecutar comandos aleatorios en ese entorno, evitando la necesidad de instalar todas las dependencias del entorno en la máquina actual. El caso más común es tener un servicio para ejecutar tests, como veremos más adelante, pero podríamos tener para cualquier tipo de tarea.

docker-compose rm elimina los contenedores y otros recursos como redes, creados a partir de un compose.

docker-compose permite definir prácticamente todos los flags que soportan tanto el comando docker run como el docker build, pero docker-compose es mucho más fácil de utilizar. Las opciones más comunes son:

build: para indicar que el container se construye desde un Dockerfile local. Puede tener subcampos como context, dockerfile, cache_from o args.
image: para indicar que el container corre un imagen remota. También indica el nombre de la imagen que se crea si hay un campo build.
command: para redefinir el comando que ejecuta el container en lugar del comando definido en la imagen.
environment: para definir variables de entorno en el contenedor. Se pueden pasar haciendo referencia a un fichero usando la propiedad env_file. Si la variable no tiene un valor dado, su valor se cogerá del entorno de shell que ejecuta el docker-compose up, lo que puede ser útil para pasar claves, por ejemplo.
depends_on: para definir relaciones entre contenedores.
ports: para mapear los puertos donde el contenedor acepta conexiones.
