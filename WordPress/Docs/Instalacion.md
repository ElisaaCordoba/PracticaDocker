Estos son los comandos necesarios para montar el entorno de Wordpress sobre dos contenedores conectados a la red, red_wp.
docker network create red_wp 
docker run -d --name servidor_mysql \
             --network red_wp \
             -v /opt/mysql_wp:/var/lib/mysql \
             -e MYSQL_DATABASE=bdd_wp \
             -e MYSQL_USER=elisa_wp \
             -e MYSQL_PASSWORD=elisa\
             -e MYSQL_ROOT_PASSWORD=elisa \
             mariadb
            
docker run -d --name servidor_wp \
             --network red_wp \
             -v /opt/wordpress:/var/www/html/wp-content \
             -e WORDPRESS_DB_HOST=servidor_mysql \
             -e WORDPRESS_DB_USER=user_wp \
             -e WORDPRESS_DB_PASSWORD=asdasd \
             -e WORDPRESS_DB_NAME=bd_wp \
             -p 80:80  
             wordpress
             
[Comandos principales](Imagenes/RedContenedor.png)
Elementos importantes:

El contenedor servidor_mysql ejecuta un script docker-entrypoint.sh que es el encargado de configurar la base de datos y termina ejecutando el servidor mariadb.
Al crear la imagen mariadb tiene que permitir la conexión desde otra máquina, por lo que en la configuración tenemos comentado el parámetro bind-address.
[Bind-address](Imagenes/Bindadress.png)

Del contenedor servidor_wp ejecuta un script docker-entrypoint.sh, a partir de las variables de entorno, ha creado el fichero wp-config.php de wordpress.

Para visualizar el contenido del fichero `wp-config.php`:
$docker exec -it servidor_wp bash 
$cat wp-config.php



