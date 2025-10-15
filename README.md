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
      PS_FOLDER_ADMIN: admin4577
      PS_FOLDER_INSTALL: install4577
      ADMIN_MAIL: ${ADMIN_MAIL}
      ADMIN_PASSWD: ${ADMIN_PASSWD}
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
      PMA_HOST: ${DB_SERVER}
      PMA_ARBITRARY: ${PMA_ARBITRARY}
      PMA_USER: ${DB_USER}
      PMA_PASSWORD: ${DB_PASSWD}
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
PS_LANGUAGE=es
PS_COUNTRY=es
DB_NAME=prestashop
ADMIN_MAIL=admin@prestashop.local
ADMIN_PASSWD=admin123
```
# Instalacion 
<img width="1375" height="295" alt="imagen" src="https://github.com/user-attachments/assets/40dcf4b0-47c2-4a02-a833-f94a260d7656" />
Al poner mi ip con el puerto en especifico ``127.0.0.1:8080`` aparece esta pagina
Que por lo que se debe ser la pagina de prestashop una vez instalado con la instalacion automatica, cosa que se porque la ip que aparece en la barra de busqueda es la del contenedor
<img width="2730" height="1641" alt="imagen" src="https://github.com/user-attachments/assets/34c87854-0a0b-43e5-930a-0a4e22d49da6" />

Accedo al contenedor de nombre ``prestashop`` y compruebo

<img width="1416" height="820" alt="imagen" src="https://github.com/user-attachments/assets/73ddea15-1b3e-44a2-bf85-e49388ffa048" />

De esta manera se que la ip del contendor es `172.18.0.4` ya que luego en el panel administrativo aparece eso, ya que redirecciona a la IP del contenedor

Luego accedo al panel administrativo

<img width="2773" height="1801" alt="imagen" src="https://github.com/user-attachments/assets/23b72206-ddc5-412c-9eb7-23f438a5b801" />

Meto mis credenciales

<img width="2790" height="1801" alt="imagen" src="https://github.com/user-attachments/assets/a85eb01d-dcc7-47d7-9b7f-38cdd32e8c1c" />

Y aparece esto: 

<img width="2779" height="1801" alt="imagen" src="https://github.com/user-attachments/assets/76b2ab9c-8fba-4c93-b152-43416f69e8f4" />

Luego accedo al endpoint con el nombre puesto en la carpeta ``$PS_ADMIN_FOLDER`` que es ``admin4577``


Ahora entro en php my admin y me aparece esta pantalla, donde podemos ver la tabla de prestashop
<img width="2736" height="1652" alt="imagen" src="https://github.com/user-attachments/assets/878dbf86-7146-489b-a9b2-2d0c36f32840" />

<img width="1301" height="1801" alt="imagen" src="https://github.com/user-attachments/assets/c377a282-dabd-4a78-a3ed-113c5f37be03" />



