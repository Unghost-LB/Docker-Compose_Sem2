# LABORATORIO 2

Se utilizara Docker Compose para desplegar una BD y un Servidor Web. 

## STACK
Primer Parte:
API

Para este apartado utilizaremos el siguiente repositorio de la Api creado por nmatsui:
https://hub.docker.com/r/nmatsui/hello-world-api

Despues para crear las instancias crearemos el archivo docker-compose.yml

-   API PRIMERA INSTANCIA:
    Retornara mi nombre: Daniela Cristina
-   API SEGUNA INSTANCIA:
    Retornara el mensaje: "Aprendiendo Docker Compose" 
-   API TERCERA INSTANCIA:
    Retornara el mensaje: "Little Mariposas"

Segunda parte:
Postgres 

Para este punto se utillizo la siguiente imagen de postgres:
https://hub.docker.com/_/postgres

Tambien nos guiamos de su repositorio para poder realizar su instalación y de un video en youtube:
https://youtu.be/hVrKX2RtigQ

En esta parte usaremos la parte via docker compose. 
Donde editamos nuestro archivo docker compose.

Agregamos un codigo similar al siguiente en el docker-compose.yml

```
# Use postgres/example user/password credentials

services:

  db:
    image: postgres
    restart: always
    # set shared memory limit when using docker compose
    shm_size: 128mb
    # or set shared memory limit when deploy via swarm stack
    #volumes:
    #  - type: tmpfs
    #    target: /dev/shm
    #    tmpfs:
    #      size: 134217728 # 128*2^20 bytes = 128Mb
    environment:
      POSTGRES_PASSWORD: example

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

```
## COMANDOS
Estos comandos se utilizan dentro de la Terminal de VS con Git Bash

1.- Clonar Api nmatsui/hello-world-api
```
git clone https://github.com/nmatsui/hello-world-api.git
cd hello-world-api
docker build -t nmatsui/hello-world-api .
```

1.- Para levantar todo
```
docker composer up 
```
si es que queda cache y poder limpiar

```
docker composer up --build 
```
2.- Ver contenedores

```
docker compose ps
```
3.- Probar Instancias
```
curl -i http://localhost:3000/
curl -i http://localhost:3001/
curl -i http://localhost:3002/
```
4.- Instalar Postgres
```
docker pull postgres
```

## EVIDENCIAS/CAPTURAS
Link para visualizar documento en Drive donde se sube fotos de las evidencias: 
https://docs.google.com/document/d/1wzvSVX5IuM5kwXisXg-7Aq_ttb8mg2Bu-3oQgOh8XUg/edit?usp=sharing
