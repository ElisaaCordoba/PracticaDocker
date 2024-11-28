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

Del mismo modo el contenedor servidor_wp ejecuta un script docker-entrypoint.sh, que entre otras cosas, a partir de las variables de entorno, ha creado el fichero wp-config.php de wordpress, por lo que durante la instalación no te ha pedido las credenciales de la base de datos.
Si te das cuenta la variable de entorno WORDPRESS_DB_HOST la hemos inicializado al nombre del servidor de base de datos. Como están conectada a la misma red definida por el usuario, el contenedor wordpress al intentar acceder al nombre servidor_mysql estará accediendo al contenedor de la base de datos.
Al servicio al que vamos a acceder desde el exterior es al servidor web, es por lo que hemos mapeado los puertos con la opción -p. Sin embargo, en el contenedor de la base de datos no es necesario mapear los puertos porque no vamos a acceder a ella desde el exterior. Sin embargo, el contenedor servidor_wp puede acceder al puerto 3306 del servidor_mysql sin problemas ya que están conectados a la misma red.

