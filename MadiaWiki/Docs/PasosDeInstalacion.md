Vamos a crear distintos contenedores usando etiquetas distintas al indicar el nombre de la imagen, 
posteriormente accedermos a la aplicación y podremos ver la versión instalada:

Las intrucciones cargan las imagenes de mediawiki en la version latest que es la ultima.

En primer lugar vamos a instalar la última versión:
docker run -d -p 8080:80 --name mediawiki1 mediawiki

Si accedemos a la ip de nuestro ordenador, al puerto 8080, podemos observar que versión hemos instalado.
A continuación vamos a instalar otra versión de la mediawiki, la 1.36.3, creamos otro contenedor con otro nombre y mapeamos 
otro puerto:
docker run -d -p 8081:80 --name mediawiki2 mediawiki:1.36.3

Si accedemos a la ip de nuestro ordenador, al puerto 8081, podemos observar que hemos instalado la versión 1.36.3:
Y finalmente vamos a instalar otra versión en otro contenedor:
docker run -d -p 8082:80 --name mediawiki3 mediawiki:1.35.5

Si accedemos a la ip de nuestro ordenador, al puerto 8082, podemos observar que hemos instalado la versión 1.31.12:

Ya se ha generado el contenedor mediawiki1,2,3 en la puerta 8080:80 una pantalla con la version de la mediawiki
