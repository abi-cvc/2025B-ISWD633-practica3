# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
docker run -d --name nginx-bind -p 8080:80 -v "C:\Users\carol\nginx\html":/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Se muestra una página en blanco o un error 403, ya que la carpeta html está vacía y el contenedor no tiene ningún archivo index.html propio (ha sido reemplazada por el directorio vacío del host).

### ¿Qué pasa con el archivo index.html del contenedor?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El archivo index.html original del contenedor queda oculto o reemplazado, porque el bind mount monta la carpeta del host encima de esa ruta, ocultando su contenido original.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El servidor Nginx muestra el template descargado. Los archivos HTML, CSS y JS que se colocaron en la carpeta del host se sirven directamente desde el contenedor gracias al bind mount.

### Eliminar el contenedor
# COMPLETAR CON EL COMANDO
docker rm -f nginx-bind

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El nuevo contenedor muestra el mismo contenido (el template) sin necesidad de volver a copiar los archivos, ya que los archivos están almacenados en el host, no dentro del contenedor.

