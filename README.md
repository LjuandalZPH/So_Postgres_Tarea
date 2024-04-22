<em> # Postgres & contenedores</em>


<h4 align="center">
:hugs: Proyecto terminado :hugs:
</h4>

<p align="centeer">
   <img src="https://user-images.githubusercontent.com/66388384/169884770-c7364478-2430-445f-97e1-b5c19e736c4f.png">
   </p>

## Table of Contents
1. [Descripcion del código]
2. [Paso a paso]
3. [Video]
4. [Integrantes]

<h4 align="center">
1. Descripción del código
</h4>

<h5>
   La idea principal de esta tarea es poder conectarnos a una virtual  machine que contiene una base de datos en postgres y poder utilizarla, usando principal lo aprendido en clase
   usando docker para hacer los contenedores. 
</h5>
<hr>

<h4 align="center">
2. Paso a paso
</h4>

<h5>
   <p>
   Pasos Tarea SO:
Primero lo que tenemos que hacer es crear el volumen al cual vamos a asignarle a pg_server:
      
``docker volume create pg_db``
      
Ahora lo que hacemos es crear la red por la cual van a estar conectados el cliente y el servidor:
``docker network create pg_network``
Por consiguiente lo que vamos a hacer es crear el pg_server:
``docker run --name pg_server --network pg_network -v pg_db:/var/lib/postgresql/data -e POSTGRES_PASSWORD=contrasena -d postgres:15-bookworm``

[!IMPORTANT]
Utilizamos - docker logs pg_server para ver el estado del  servidor

</p>`
<p>
Ahora, creamos la base de datos dentro del pg_server de la siguiente manera:
   
``docker exec -it pg_server bash ``
``psql -U postgres -> Acceder a postgres``
Ahora, una vez dentro hacemos el db y hacemos una tabla en este:
``CREATE DATABASE tarea_db;``
`` \c tarea_db``

``CREATE TABLE pg_tabla(
    id SERIAL PRIMARY KEY,
    mensaje TEXT
); ``
Y nos salimos
``\q
exit ``
</p>
</p>
Ahora creamos el cliente y de tacazo abrimos la terminal del contenedor:

`` docker run - - name pg_client - -network pg_network -it postgres:15-bookworm psql -h pg_server -U postgres ``
Colocamos la clave que le hayamos puesto al server, en este caso “contrasena”
Una vez dentro, debemos poner lo siguiente:
`` \c tarea_db
SELECT*FROM pg_tabla
``  
De ahí solamente hacemos los pasos que nos piden dentro de la validación:

Ingresamos los datos con 
`` INSERT INTO pg_tabla(mensaje) VALUES(‘hola mundo’);``
  
Detener la ejecución del contenedor que corre la versión Postgres 15-bookworm.
``docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)``
Ejecute ahora el cliente y ejecutar dentro de este contenedor lo siguiente:
Borrar los contenedores (pg_server, pg_client), el volumen (pg_db) y la red (pg_network) creados para esta tarea.
para borrar:
``docker network rm pg_network
 docker volume rm pg_db``


</h5>
:trollface:
