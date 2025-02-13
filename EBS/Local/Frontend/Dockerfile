# Etapa de construcción: usar Node.js para construir la aplicación AngularJS
FROM node:18 AS build

# Establecer directorio de trabajo
WORKDIR /app

# Copiar los archivos de configuración y el código fuente del frontend
COPY ./frontend/package*.json ./

# Instalar dependencias de AngularJS
RUN npm install

# Copiar todo el código fuente al contenedor
COPY ./frontend .

# Construir la aplicación AngularJS para producción
RUN npm run build --prod

# Etapa de servicio: usar Apache para servir los archivos estáticos
FROM php:8.3-apache

# Habilitar el módulo rewrite de Apache
RUN a2enmod rewrite

# Copiar los archivos estáticos generados por Angular al directorio de Apache
COPY --from=build /app/dist/ /var/www/html/

# Exponer el puerto 80
EXPOSE 80

# Ejecutar Apache en primer plano
CMD ["apache2-foreground"]
