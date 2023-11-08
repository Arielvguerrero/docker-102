# Laboratorio Docker Compose

Este laboratorio se basa en el mismo ejercicio que corrimos en Replit con Python y Flask.

## Preparación

Haz un fork de este repo.

Clona el fork en tu pc.

## Paso 1

Ejecuta `docker init`.

Selecciona Python como el `application platform`.

Cuando aparezca la pregunta `What is the command to run your app?`, escribe `python main.py`.

Abre el archivo `compose.yaml`, en la línea 16, debajo de la sección `ports` agrega estas líneas:

```
    enviroment:
      - PORT
      - HOST
      - DB
      - DB_USERNAME
      - DB_PASSWORD
```

Asegurate que `ports` y `enviroment` estén alineados en la misma columna.

Revisa el archivo `.env`, configura las variables con los valores que usaste en el ejercicio en Replit (es decir, usa las credenciales de ElephantSQL).

Levanta la aplicación con el siguiente comando:

```
docker compose up --build
```

Revisa que todo está bien navegando a la dirección `localhost:8000`.

### Preguntas

¿Qué pasa si cambias el valor de la variable PORT?
  Si cambiamos el puerto, no podemos acceder a la pagina, sin embargo, el servidor sigue funcionando.
¿Qué cambios debes hacer para cambier el port a 8080?
  Se debe cambiar en primera en el archivo .env y en el docker compose.yalm. ademas se debe hacer nuevamente el build para que la aplicacion ejecute los cambios.


## Paso 2

Deten `docker compose` presionando `control-c`.

Elimina los comentarios a partir de la línea 28.

Asegurate de crear un archivo en la carpeta `db` llamado `password.txt`, coloca en este una clave cualquiera.

Modifica el archivo `.env` para que se pueda conectar al servicio `db`.

Tips: 
  - El valor para `HOST` es `db`
  - los valores que necesitan están declarados en la definición del servicio, debes hacer el "match" de las variables allí definidas con las que necesitas.

Esta vez ejecuta el comando `docker compose` de este modo:

```
docker compose up -d --build 
```

La opción `-d` permite dejar ejecutando los servicios y libera la consola.

### Actividades

Ejecuta `docker ps`. 

¿Qué obtienes?.
Obtenemos informacion de los diferentes servicios que tenemos en nuestro contenedor.

```
CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS                          PORTS                      NAMES
ba20db67805f   postgres                "docker-entrypoint.s…"   4 minutes ago   Restarting (1) 37 seconds ago                              docker-102-db-1
c64f201ceb93   mongo                   "docker-entrypoint.s…"   31 hours ago    Up 27 hours                     0.0.0.0:27017->27017/tcp   kastor-operation-db-1
54c75369cb30   kastor-development_pg   "docker-entrypoint.s…"   4 months ago    Up 27 hours                     0.0.0.0:5432->5432/tcp     kastordb
```


Ejecuta `docker images`. 

¿Cuál es el tamaño de la imagen del servidor flask?
  170 MB
¿Cuál es el tamaño de la imagen postgres?
  348 MB
¿Cuándo fueron creadas cada una de las imágenes?
  ambas fueron creadas hace 31 minutos
Ahora ejecuta `docker compose logs -f`, esto te permite revisar el log de los contenedores.

Si navegas hacia la aplicación (http://localhost:8000/) se produce un error, revisa el log.

¿Cuál es la causa del error?
  relation "books" does not exist at character 15. el cual se refiere a que no existe la tabla books

Cierra el log presionando `control-c`, luego detén la aplicación con este comando:

```
docker compose down
```

