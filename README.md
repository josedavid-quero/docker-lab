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