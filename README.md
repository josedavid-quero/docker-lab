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

A partir de la versión 18 de postgres se recomienda montar el volumen en **`/var/lib/postgresql`**, por tanto, se ejecuta el comando:

**`docker run -d --name postgres-ejercicio-3 -e POSTGRES_PASSWORD=ardilla --mount source=postgres-data,target=/var/lib/postgresql postgres`**

![Captura 18](capturas/captura18.PNG)

Señalar que para crear el contenedo, es necesario la variable de entorno **`POSTGRES_PASSWORD`** para establecer la contraseña del superusuario **`postgres`**.

Podemos ver cómo se ha creado el contenedor y está en ejecución:

![Captura 19](capturas/captura19.PNG)

## Crear tabla

- Conéctate a la base de datos:

Para conectarnos a la base de datos ejecutamos el siguiente comando:

**`docker exec -it postgres-ejercicio-3 psql -U postgres`**

![Captura 20](capturas/captura20.PNG)

- Crea la tabla:

Una vez que ya estamos dentro, lanzamos directamente la sentencia para crear la tabla:

![Captura 21](capturas/captura21.PNG)

- Inserta un registro:

Hacemos lo mismo que para la creación de la tabla:

![Captura 22](capturas/captura22.PNG)

Comprobamos que la tabla se ha creado y el registro se ha insertado correctamente:

![Captura 23](capturas/captura23.PNG)

## Comprobación

1. Para el contenedor
2. Elimina el contenedor
3. Crea un nuevo contenedor usando **el mismo volumen**

![Captura 24](capturas/captura24.PNG)

- Comprueba que los datos siguen existiendo.

En primer lugar accedo al contenedor y, una vez dentro, ejecuto la sentencia:

**`SELECT * FROM items;`**

![Captura 25](capturas/captura25.PNG)

# 4. Bind mounts

Crea un archivo en tu máquina:

**`ìndex.html`**

Ejemplo:

**`<h1>Hola Docker</h1>`**

![Captura 26](capturas/captura26.PNG)

Ejecuta un contenedor **`nginx`**:

- mapea el puerto **`80`**
- monta el archivo en:

**`/usr/share/nginx/html/index.html`**

Para hacer esto, ejecuto el siguiente comando:

**`docker run -d --name nginx-ejercicio-4 --mount type=bind,source=C:\CursoDocker\clase-docker\docker-lab\index.html,target=/usr/share/nginx/html/index.html -p 8080:80 nginx`**

![Captura 27](capturas/captura27.PNG)

Abre el navegador:

![Captura 28](capturas/captura28.PNG)

Se muestra el contenido de mi **`index.html`**

Pregunta:

¿Qué ocurre si modificas el archivo **`index.html`** en tu máquina?

Al cambiar mi **`index.html`**:

![Captura 29](capturas/captura29.PNG)

Se actualiza el contenido del navegador, ya que se está sirviendo el mismo **`index.html`**:

![Captura 30](capturas/captura30.PNG)

# 5. Auditando volúmenes (opcional)

Investiga:

¿Qué comando permite ver **dónde guarda Docker los datos de un volumen**?

**`docker volume inspect <mi_volumen>`**

Por ejemplo:

![Captura 31](capturas/captura31.PNG)

# 6. Creando redes privadas

## Crea una red llamada:

**`my-net`**

Para hacer esto, ejecutamos el comando:

**`docker network create my-net`**

![Captura 32](capturas/captura32.PNG)

## Arranca dos contenedores **`ubuntu`** en esa red.

Instala ping si es necesario.

- Para arrancar el primer contenedor, ejecuto el comando:

**`docker run -it --name ubuntu-ejercicio6-1 --network my-net ubuntu bash`**

![Captura 33](capturas/captura33.PNG)

- Para instalar ping, dentro del contenedor ejecuto:

**`apt-get update && apt-get install -y iputils-ping`**

![Captura 34](capturas/captura34.PNG)

- Procedo de la misma forma para el segundo contenedor, al que llamo ubuntu-ejercicio6-2:

![Captura 35](capturas/captura35.PNG)

## Desde un contenedor intenta hacer:

**`ping otro_contenedor`**

Para conocer las direcciones IP de los contenedores, ejecutamos el comando:

**`docker network inspect my-net`**

![Captura 36](capturas/captura36.PNG)

- Desde el contenedor **`ubuntu-ejercicio6-1`** podemos hacer ping al contenedor **`ubuntu-ejercicio6-2`** utilizando su ip o su nombre:

![Captura 37](capturas/captura37.PNG)

- De la misma forma podemos hacerlo desde el contenedor **`ubuntu-ejercicio6-2`** al contenedor **`ubuntu-ejercicio6-1`**

![Captura 38](capturas/captura38.PNG)

## Pregunta

¿Los contenedores pueden comunicarse entre sí?

Como se puede ver en las capturas, se pueden comunicar entre sí. También lo pueden hacer por nombre, ya que todos los contenedores dentro de una misma red creada por mi se pueden comunicar entre sí a través de su nombre gracias al servidor DNS integrado en **`Docker`**.

# 7. Red none (opcional)

## Investiga:

¿Para qué serviría ejecutar un contenedor con red:

**`none`**

Sirve para aislar completamente al contenedor de la red cuando sabemos que el proceso no necesita red y se quiere garantizar que no tendrá acceso a ella.

Algunos casos de uos prácticos son:

- Seguridad: ejecutar procesos sin riesgo de conexiones externas.
- Pruebas aisladas: verificar que una app no dependa de Internet.
- Procesamiento offline: tareas locales como compresión, conversión de archivos, compilación, etc.
- Entornos restringidos: evitar filtración de datos o accesos no autorizados.
- Entornos de compilación: Builds que no deben descargar dependencias en tiempo de ejecución.
- Análisis de malware: Estudiar software sospechoso sin que pueda "llamar a casa".