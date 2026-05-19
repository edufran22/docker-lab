# docker-lab
Repo para la realización del laboratorio de Docker del curso INTRODUCCIÓN A DEVOPS. SEGUNDA EDICIÓN. (262922GE160)

## Ejercicio 1 - Creando imágenes
### Paso 1
1. Lo primero que hago es abrir "Docker Desktop" y en el apartado "Docker Hub" busco la imagen "ubuntu" para poder crearme un contenedor en base a esa imagen. Elijo la imagen mas descargada, la primera que me sale. En la parte inferior derecha de "Docker Desktop" pincho en el apartado "terminal". 
2. Ejecuto el comando:
   docker run -it ubuntu /bin/bash
   captura 1
   
4. Instalo "cURL" dentro del contenedor (ya que la imagen base no lo trae), ejecutando el comando:
   apt-get update && apt-get install -y curl
   captura 2
6. Y finalmente compruebo que se ha instalado correctamente ejecutando el comando:
   curl --version
   captura 3

#### Pregunta
¿Con qué comando podrías guardar los cambios del contenedor como una nueva imagen?
Para guardar los cambios de este contenedor como una nueva imagen, tengo que salir del contenedor escribiendo exit y ejecutar el siguiente comando en la terminal (fuera del contenedor):
docker commit 1ac289513036 ubuntu-con-curl
en la que el código que hay después de la palabra "commit" sería el ID del contenedor y a continuaciñón iriía el nombre de la nueva imagen.

### Paso 2
1. Abro "Visual Studio Code" y dentro del directorio de trabajo me creo un "Dockerfile".
2. Creo la nueva imagen con el comando:
  docker build -t mi-ubuntu-curl .
  captura 4
4. Compruebo que funciona:
   captura 5

#### Pregunta
¿Qué comando permite ver las capas de una imagen Docker?  
El comando para ver las capas de una imagen en Docker y es docker history, en mi caso sería:
captura 6

## Ejercicio 3 - Volúmenes persistentes

### Paso 1 - Crear el volumen y ejecutar el contenedor
1. Primero, crearemos un volumen llamado mi_volumen_ejercicio3 y arrancaremos el contenedor:
   docker volume create mi_volumen_ejercicio3

   captura 7

2. Ejecutamos el contenedor basado en postgres:17 haciedno uso de "--detach" (en segundo plano) y añadiendo una contraseña con el flag "-e" (lo exige la imagen oficial de postgres).
   docker run --name mi_postgres_ejercicio3 -e POSTGRES_PASSWORD=mi_clave -v mi_volumen_ejercicio3:/var/lib/postgresql/data --detach postgres:17

   captura 8

3. Nos conectamos a la BBDD y creamos la tabla, para entrar a la terminal de PostgreSQL (psql) dentro del contenedor que está corriendo, uso docker exec:
   captura 9
   
4. Una vez dentro de la consola de Postgres (se ve el prompt postgres=#). Ejecuto los comandos SQL del ejercicio:

   captura 10

5. Ahora detenemos y destruimos el contenedor:
   captura 11

6. Vamos a crear un contenedor completamente nuevo (le llamaremos mi_nuevo_postgres), pero le conectaremos el volumen mi_volumen_ejercicio3 que guardó los datos del contenedor anterior:      
   captura 12
7. Ahora vamos a comprobar que los datos siguen existiendo, me conecto al nuevo contenedor usando psql para verificar si la tabla y el registro sobrevivieron:
   captura 13

## Ejercicio 4 - Bind mounts 
1. Creo el archivo ".html" en mi máquina con el contenido: <h1>Hola Docker</h1>
2. Ejecuto el contenedor de Nginx con el Bind Mount abriendo la terminal dentro de la misma carpeta donde guardé mi index.html y ejecutando el siguiente comando:
   captura 14
   Con la opción "-v" estoy reemplazando el archivo por defecto de Nginx por mi index.html local.
3. Abro mi navegador web e ingreso la dirección http://localhost:8080 y veo una pantalla blanca con el título "Hola Docker".
   captura 15

#### Pregunta
¿Qué ocurre si modificas el archivo index.html en tu máquina?     
Los cambios se reflejan de forma inmediata y en tiempo real dentro del contenedor porque con los bind mounts, Docker no hace una copia del archivo; crea un "enlace directo" (un acceso directo real). El contenedor está leyendo el archivo directamente desde el disco duro de tu propia máquina
   
