# Tarea06_SXE_PrestaShop

# Docker-compose
```yaml
services:
  mysql:
    container_name: prestashop-mysql
    image: mysql:5.7
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
    networks:
      - prestashop_network
    volumes:
      - dbdata:/var/lib/mysql
  prestashop:
    container_name: prestashop
    image: prestashop/prestashop:latest
    restart: unless-stopped
    depends_on:
      - mysql
    ports:
      - 8080:80
    environment:
      PS_LANGUAGE: ${PS_LANGUAGE}
      PS_COUNTRY: ${PS_COUNTRY}
      DB_SERVER: ${DB_SERVER}
      DB_NAME: ${DB_NAME}
      DB_USER: ${DB_USER}
      DB_PASSWD: ${DB_PASSWD}
      PS_INSTALL_AUTO: ${PS_INSTALL_AUTO}
    networks:
      - prestashop_network
    volumes:
      - psdata:/var/www/html
  phpmyadmin:
    image: phpmyadmin
    restart: always
    ports:
      - 8090:80
    environment:
      PMA_HOST: ${PMA_HOST}
      PMA_ARBITRARY: ${PMA_ARBITRARY}
    networks:
      - prestashop_network
networks:
    prestashop_network:
volumes:
    dbdata:
    psdata:

```
Este es el fichero docker compose, aqui añado diversas cosas como la instalacion, automatica el poner las cosas en variables de entorno y algunas cosas por el estilo
## Archivo .env
```sh
MYSQL_ROOT_PASSWORD=admin
MYSQL_DATABASE=prestashop
DB_SERVER=prestashop-mysql
DB_USER=root
DB_PASSWD=admin
PMA_ARBITRARY=1
PS_INSTALL_AUTO=1
PMA_HOST=prestashop-mysql
PS_LANGUAGE=es
PS_COUNTRY=es
DB_NAME=prestashop

```
# Instalacion 
<img width="1375" height="295" alt="imagen" src="https://github.com/user-attachments/assets/40dcf4b0-47c2-4a02-a833-f94a260d7656" />
