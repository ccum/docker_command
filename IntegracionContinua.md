Optimización de Docker Build
----------------------------

Por suerte Docker tiene una solución a este problema. Cuando ejecutamos un docker build podemos indicar que utilice la caché de una imagen ya creada. Dicho de otra manera, si estoy construyendo la imagen openwebinars/docker-for-devs:latest , puedo reusar la cache de la última versión de openwebinars/docker-for-devs:latest ejecutando estos commandos:

```
docker pull openwebinars/docker-for-devs:latest
docker build -t openwebinars/docker-for-devs:latest --cache-from=openwebinars/docker-for-devs:latest .

```