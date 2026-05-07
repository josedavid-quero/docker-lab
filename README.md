# 1. Creando imágenes
## Paso 1
Ejecuta un contenedor basado en la imagen:

**`ubuntu`**

Con el comando

![Captura 1](capturas/captura1.PNG)

Se arranca el contenedor y se accede directamente a la terminal del mismo:

![Captura 2](capturas/captura2.PNG)

Una vez dentro de la terminal, ejecutamos el siguiente comando para actualizar el sistema e instalar **`curl`**:

![Captura 3](capturas/captura3.PNG)

Con el comando **`curl --version`** comprobamos que se ha instalado correctamente:

![Captura 4](capturas/captura4.PNG)

## Pregunta
¿Con qué comando podrías **guardar los cambios del contenedor como una nueva imagen**?

Con el comando **`docker commit`**

Si miramos la ayuda de **docker** obtenemos la siguiente información:

![Captura 5](capturas/captura5.PNG)

Donde:
- **`CONTAINER`** sería el contenedor.
- **`REPOSITORY`** sería el nombre que daríamos a la imagen.
- **`[:TAG]`** sería la versión o etiqueta que asignaríamos a la imagen.

## Paso 2
Crea un **`Dockerfile`** que haga lo mismo automáticamente.

![Captura 6](capturas/captura6.PNG)

Construye la imagen y ejecuta un contenedor.

- Con el comando **`docker build -t ubuntu-paso-2 .`** se construye la imagen:

![Captura 7](capturas/captura7.PNG)

- Con el comando **`docker run -it ubuntu-paso-2`** se ejecuta el contenedor:

![Captura 8](capturas/captura8.PNG)

Y, una vez dentro del contenedor, podemos comprobar si se ha instalado **`curl`** con el comando **`curl --version`**:

![Captura 9](capturas/captura9.PNG)

## Pregunta
¿Qué comando permite ver las **capas de una imagen Docker**?

El comando **`docker history <imagen>`**

Por ejemplo:

![Captura 10](capturas/captura10.PNG)

# 2. Limpiando imágenes (opcional)
Crea un **`Dockerfile`** basado en:

**`ubuntu`**

Para este ejercicio he creado el siguiente **`Dockerfile`** llamado **`Dockerfile.ejercicio-2-ubuntu`**:

![Captura 11](capturas/captura11.PNG)

Para crear la imagen, ejecuto el siguiente comando:

**` docker build -f ./Dockerfile.ejercicio-2-ubuntu -t ubuntu-ejercicio-2 .`**

![Captura 12](capturas/captura12.PNG)

Se debe modificar el **`Dockerfile`** para instalar **`curl`**:

![Captura 13](capturas/captura13.PNG)

Para crear la imagen, ejecuto el mismo comando de antes:

**` docker build -f ./Dockerfile.ejercicio-2-ubuntu -t ubuntu-ejercicio-2 .`**

![Captura 14](capturas/captura14.PNG)

Se debe volver a modificar el **`Dockerfile`** para instalar **`wget`**:

![Captura 15](capturas/captura15.PNG)

Para crear la imagen, volvemos a ejecutar una vez más el mismo comando:

**` docker build -f ./Dockerfile.ejercicio-2-ubuntu -t ubuntu-ejercicio-2 .`**

![Captura 16](capturas/captura16.PNG)

Vamos a listar las imágenes con el comando **`docker images`**:

![Captura 17](capturas/captura17.PNG)

## Pregunta
¿Qué ocurre con las imágenes anteriores?

Como no se ha cambiado el nombre de la imagen ni se ha añadido ninguna etiqueta, se ha creado una sola imagen (en vez de tres imágenes diferentes) añadiendo las capas necesarias sobre las capas de las imágenes anteriores para crear la nueva imagen.

# 3. Volúmenes persistentes
Ejecuta un contendor de:

**`postgres`**

Usa un volumen **`Docker`** montado en:

**`/var/lib/postgresql/data`**

Para ello, se ejecuta el comando:

**`docker run -d --name postgres-ejercicio-3 -e POSTGRES_PASSWORD=ardilla --mount source=postgres-data,target=/var/lib/postgresql/data postgres`**

![Captura 18](capturas/captura18.PNG)

Señalar que para crear el contenedo, es necesario la variable de entorno **`POSTGRES_PASSWORD`** para establecer la contraseña del superusuario **`postgres`**.

## Crear tabla
Para conectarnos a la base de datos y crear la tabla que indica el ejercicio, hacemos lo siguiente:

- Ejecutamos el comando:

**``**