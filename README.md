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


Tercera Parte:
Volumenes

Para esta parte nos guiaremos del siguiente guia:
https://docs.docker.com/engine/storage/volumes/

En la parte de "Utilice un volumen con Docker Compose" encontraremos el siguiente ejemplo:
```
services:
  frontend:
    image: node:lts
    volumes:
      - myapp:/home/node/app
volumes:
  myapp:
    external: true
```

Para entender un poco más la configuración se visualizo los siguientes videos:
- Docker Compose: https://www.youtube.com/watch?v=y-sMw9937PM
- Bash: https://youtu.be/omEFZHHXVdc 

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
## Tipos de redes y Tipos de volumen que existen en docker

- Tipos de Redes:

Para la creación de aplicaciones modernas se usan varios servicios. La red Docker  sirve para definicir cómo se comunican los contenedores sin perder la separación de muchos servidores que corren de forma aislada.

Para esto utiliza network drivers, que resuelven diferentees problemas:

    - Bridge: Es ideal para desarrollo y pruebas al ser una red privada por defecto en un host los contenedores se pueden comunicar por IP o nombre
    
    - Host: Tiene mejor rendimiento, pero no permite mapear el mismo puerto en varios contenedores. El contenedor usa la IP y puertos del host directamente
    
    - None:Desactiva toda la red del contenedor, solo queda loopback. Es útil cuando no se necesita conectividad ni se requiere tanto aislamiento.
    
    - Overlay: Conecta contenedores en distintos hosts físiscos como si feran una sola red y se es usado comunmente para Clusters de Docker Swarn.
    
    -Macvlan: Muy utilespara apps heredadas con acceso directo a la red. Asigna una Mac propia al contenedor para que actúe como otro dispositivo físico en la LAN
    
    -Ipvlan: Es similar a Macvlan pero da mejor rendimiento en entorno de alta densidad por que enruta en la capa IP en vez de usar MAC.


Fuentes:
https://docs.docker.com/engine/network/drivers/
https://www.datacamp.com/es/tutorial/docker-networking 

- Tipos de Volumenes:

Los contonedores son efimeros, esto significa que si borras uno, lo que se escribio dentro desaparece. Por eso existen los volumenes que te da datos persistentes, intercambio de datos, separación del código de la aplicación de los datos, y copia de seguridad y recuperación:

    - Volumenes nombrados: Se guardan en una ruta interna y se gestionan totalmente por Docker. Recomendad para persistir datos. En este proyecto la hemos usado tambien (ej.data_prueba2)
    
    - Volúmenes anonimos: Igual que el primer tipo (volumenes nombrados) con el unico cambio de que el nombre es aleatorio y asignado por Docker. No tiene un identificador establa asi que es dificil de reutilizar entre despliegues.

Fuentes:
https://semaphore.io/blog/docker-volumes

## EVIDENCIAS/CAPTURAS
Link para visualizar documento en Drive donde se sube fotos de las evidencias: 
https://docs.google.com/document/d/1wzvSVX5IuM5kwXisXg-7Aq_ttb8mg2Bu-3oQgOh8XUg/edit?usp=sharing
