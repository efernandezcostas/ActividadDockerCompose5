# Docker Compose

## Crear la carpeta donde voy a almacenar el archivo .yaml
<code>mkdir compose</code>   
<code>cd compose</code>

## Crear y modificar el archivo .yaml
<code>touch docker-compose.yaml</code>   
<code>nano docker-compose.yaml</code>   

**Incluyendo lo siguiente:**
~~~
name: tarea5

services:
  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: enrique
      MYSQL_PASSWORD: admin
      MYSQL_ROOT_PASSWORD: admin
    volumes:
      - db_data:/var/lib/mysql

  wp:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
    ports:
      - 8000:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: enrique
      WORDPRESS_DB_PASSWORD: admin
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data:
~~~

## Ejecutar el archivo .yaml
<code>docker compose up -d</code>
- -d -> Para que se haga en segundo plano y poder utilizar la consola una vez termine
~~~
enrique@enrique:~/compose$ docker compose up -d
[+] Running 3/3
 ✔ Network tarea5_default  Created                                                                                                                0.3s
 ✔ Container tarea5-db-1   Started                                                                                                                1.0s
 ✔ Container tarea5-wp-1   Started                                                                                                                1.9s
~~~

## Comprobar si funciona

**Comprobar que se crearon los contenedores**
<code>docker ps</code>
~~~
enrique@enrique:~/compose$ docker ps
CONTAINER ID   IMAGE              COMMAND                  CREATED          STATUS          PORTS                                     NAMES
ef11d8a64f6e   wordpress:latest   "docker-entrypoint.s…"   12 minutes ago   Up 12 minutes   0.0.0.0:8000->80/tcp, [::]:8000->80/tcp   tarea5-wp-1
47f083f346e9   mariadb:latest     "docker-entrypoint.s…"   12 minutes ago   Up 12 minutes   3306/tcp                                  tarea5-db-1
~~~

**Comprobar que funciona desde el navegador**

![image](https://github.com/user-attachments/assets/f7c5fb08-54f9-48a8-ad1e-61cbb5d18012)

**Una vez puestos los datos, comprobar la página de wordpress**

![image](https://github.com/user-attachments/assets/d1e2c29c-604d-4841-814a-44638ed83026)

