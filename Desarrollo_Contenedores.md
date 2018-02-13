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