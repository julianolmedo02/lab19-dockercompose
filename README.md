REPORTE DE PRÁCTICA
Laboratorio 19: Orquestación de una Stack Web Completa con Docker Compose

Objetivo
Desplegar una aplicación web completa (MariaDB + WordPress) utilizando Docker Compose, mediante un archivo YAML que define el estado deseado de múltiples contenedores.

Herramientas Utilizadas

Docker Engine
Docker Compose
Editor de texto (nano/vim)
Navegador web


Procedimiento
1. Creación del directorio y archivo
Bashmkdir lab19
cd lab19
Se creó el archivo docker-compose.yml con la siguiente configuración:
YAMLversion: '3.8'
services:
  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: uagro_password
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - red-academica

  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_PASSWORD: uagro_password
    networks:
      - red-academica

networks:
  red-academica:

volumes:
  db_data:
2. Despliegue de la stack
Bashdocker-compose up -d
3. Verificación
Bashdocker-compose ps
4. Acceso
Se accedió a la aplicación a través del navegador en:
http://[IP_DE_TU_VM]:8080

Resultados

Ambos contenedores (db y wordpress) se ejecutaron correctamente.
Se creó automáticamente la red red-academica y el volumen db_data.
WordPress se cargó correctamente y pudo conectarse a la base de datos MariaDB.

<img width="641" height="484" alt="Captura de pantalla 2026-05-27 213041" src="https://github.com/user-attachments/assets/f53d457e-9bd3-459d-92c3-4c2fb45ba685" />
