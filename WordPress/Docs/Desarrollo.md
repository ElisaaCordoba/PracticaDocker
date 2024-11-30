En este fichero se incluye la solucion de todos los apartados de la practica y la instalacion utilizando dos contenedores y una red con drupal.

1-Para visualizar el contenido del fichero `wp-config.php`:

docker exec -it servidor_wp bash 

cat wp-config.php
[Comprobacion](Imagenes/Servidor.wp.png)

2-Para realizar un ping sobre el servidor_wp:
2.1- Dentro del contenedor servidor_wp hay que instalar los iputils-ping

apt-get update 

apt-get install -y iputils-ping
[update](Imagenes/update.png)

docker exec -it servidor_wp ping -c 5 servidor_mysql

[5 pings](Imagenes/pings.png)


El resto de las cuestiones de la práctica se encuentran en el Manual de Usuario wordpress de la carpeta Word.

