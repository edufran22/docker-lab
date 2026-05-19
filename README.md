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

2. Ejecutamos el contenedor basado en postgres:17 haciedno uso de "--detach" (en segundo plano)
   docker run --name mi_postgres_ejercicio3 -e POSTGRES_PASSWORD=mi_clave -v mi_volumen_ejercicio3:/var/lib/postgresql/data --detach postgres:17

   


