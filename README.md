<em> # Postgres & contenedores</em>


<h4 align="center">
 :whale2: Proyecto terminado  :whale2:
</h4>

<p align="center">
   <img src="https://user-images.githubusercontent.com/66388384/169884770-c7364478-2430-445f-97e1-b5c19e736c4f.png">
   </p>

## Table of Contents
1. [<a href="#descripcion-del-codigo">Descripción del código</a>]
2. [<a href="#paso-a-paso">Paso a paso</a>]
3. [<a href="#video">Video</a>]
4. [<a href="#integrantes">Integrantes</a>]
<h4 align="center" id="descripcion-del-codigo">


<hr>
<h3>
 Tecnologia usada:
![alt text](https://www.docker.com/sites/default/files/d8/2019-07/horizontal-logo-monochromatic-white.png "Logo de Docker")

</h3>
 
1. Descripción del código
</h4>

<h5>
   La idea principal de esta tarea es poder conectarnos a una virtual  machine que contiene una base de datos en postgres y poder utilizarla, usando principal lo aprendido en clase
   usando docker para hacer los contenedores. 
</h5>
<hr>

<h4 align="center" id="paso-a-paso">
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


Ahora, creamos la base de datos dentro del pg_server de la siguiente manera y entramos a postgres:
   
``docker exec -it pg_server bash 
psql -U postgres -> Acceder a postgres``

Ahora, una vez dentro hacemos el db y hacemos una tabla en este:
``CREATE DATABASE tarea_db;
 \c tarea_db
 CREATE TABLE pg_tabla(
    id SERIAL PRIMARY KEY,
    mensaje TEXT
); ``

Y nos salimos
``\q
exit ``
</p>
</p>
Ahora creamos el cliente y entramos al shell de este:

`` docker run - - name pg_client - -network pg_network -it postgres:15-bookworm psql -h pg_server -U postgres ``

Colocamos la clave de la base de datos, entramos a la database tarea_db y vemos lo que hay:

`` \c tarea_db
SELECT*FROM pg_tabla
``  

De ahí solamente hacemos los pasos que nos piden dentro de la validación:

Ingresamos los datos con 

`` INSERT INTO pg_tabla(mensaje) VALUES(‘hola mundo’);``
  
Detenemos la ejecución del contenedor que corre la versión Postgres 15-bookworm:

``docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)``

Ya procedemos a borrar todo:

``docker network rm pg_network
 docker volume rm pg_db``

</h5>

<hr>
<h4 align="center" id="video"> 
3. Video
</h4>

<h5 align="center">
   ![YouTube]()

</h5>
<hr>

<h4 align="center" id="integrantes"> 
4. Integrantes
</h4>

</h4>
<div align="center">
   
| Nombre                      | Código  |
|-----------------------------|---------|
| Juan David Pinto Rodríguez | 2240440 |
| Juan Jose Mafla Pacheco     | 2126990 |
| Jose Adrian Marin Ordonez   | 2126988 |
   
</div>

<h2>
<p align="right">
:trollface:
</p>
</h2>
