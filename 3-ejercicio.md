## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es (COMPLETAR CON LA RUTA) /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Contiene los archivos del sistema de bases de datos MySQL: subcarpetas, tablas, índices y configuraciones internas necesarias para almacenar la información de las bases creadas y sus datos.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
docker run -d --name mysql-wp --network net-wp \
-e MYSQL_ROOT_PASSWORD=rootpass \
-e MYSQL_DATABASE=wordpressdb \
-e MYSQL_USER=wpuser \
-e MYSQL_PASSWORD=wppass \
-v "C:\Users\carol\ejercicio3\db":/var/lib/mysql \
mysql:8


### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Ahora contiene varios archivos y carpetas creados automáticamente por MySQL, que corresponden al almacenamiento físico de la base de datos wordpressdb, además de los metadatos y configuraciones del servidor MySQL.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es (COMPLETAR CON LA RUTA) /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
docker run -d --name wordpress-wp --network net-wp \
-e WORDPRESS_DB_HOST=mysql-wp:3306 \
-e WORDPRESS_DB_USER=wpuser \
-e WORDPRESS_DB_PASSWORD=wppass \
-e WORDPRESS_DB_NAME=wordpressdb \
-p 9500:80 \
-v "C:\Users\carol\ejercicio3\www":/var/www/html \
wordpress

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
El sitio web conserva la personalización, los temas instalados y las entradas creadas. Esto ocurre porque los datos del sitio y la base de datos se almacenan en las carpetas del host (db y www), las cuales permanecen intactas incluso al eliminar y recrear los contenedores.

