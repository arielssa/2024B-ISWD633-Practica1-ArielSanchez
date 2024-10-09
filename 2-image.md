# Imagen
Es un archivo único que contiene todos los programas, librerías, dependencias y configuraciones necesarias para instalar y/o ejecutar una aplicación o un conjunto de aplicaciones.
![Imagen](img/imagen.PNG)


## ¿Cuál es la relación entre una imagen y un contenedor? 
La imagen contiene todo lo necesario (programas, dependencias librerías) para que el contenedor pueda ejecutarse.
Al crear un contenedor se debe especificar la imagen que se desea.

![Imagen y contenedores](img/imagenContenedores.JPG)
## Comandos para imágenes

### Descargar imagen
Descarga la última versión de la imagen disponible en el registro de Docker.

```
docker pull <nombre imagen> 
```

Descarga una versión específica de la imagen, cada imagen tiene etiquetas (tags) para diferentes versiones.
Una imagen puede tener la etiqueta latest para representar la última versión, si no se especifica una etiqueta se hará referencia a la versión latest.

```
docker pull <nombre imagen>:<tag>
```

### Actividad 1: Descargar la imagen **hello-world**

### Comando: 
```
docker pull hello-world
```
### Actividad 2: **¿Qué es nginx**
#### Es un software de servidor web diseñado para manejar solicitudes HTTP y HTTPS.

### Actividad 3: Descargar la imagen  **nginx** en la versión **alpine**

### Comando:
```
docker pull nginx:alpine
```
### Actividad 4: Listar imágenes

### Comando:

```
docker images
```

### Salida:

![Listado de imágenes](img/listadoContenedores.png)

**Identificadores**

En Docker, se utilizan varios identificadores para diferenciar de manera única los elementos del sistema, como imágenes, contenedores, volúmenes y redes. Estos identificadores son generados automáticamente por Docker y son únicos dentro del contexto del sistema Docker en el que se encuentran. 

### Inspeccionar una imagen
El comando docker inspect se utiliza para obtener información detallada sobre un objeto de Docker específico, como un contenedor, una imagen, un volumen o una red.  Proporciona información en formato JSON sobre el objeto especificado.

```
docker inspect <nombre imagen>
docker inspect <nombre imagen>:<tag>
```

### Actividad 5: Inspeccionar la imagen hello-world 

### Comando:

```
docker inspect hello-world
```

### Actividad 6: **¿Con qué algoritmo se está generando el ID de la imagen**

#### El ID de una imagen de Docker se genera utilizando un algoritmo criptográfico de hashing SHA-256. 

### Filtrar imágenes

```
docker images | grep <termino a buscar>

```

### Para eliminar una imagen
Eliminar permanentemente la imagen de tu sistema Docker.

```
docker rmi <nombre imagen>:<tag>
```

### Actividad 7: Eliminar la imagen hello-world 

### Comando:

```
docker rmi hello-world:latest
```

-f: Es la opción para forzar la eliminación de la imagen incluso si hay contenedores en ejecución que utilizan esa imagen.
Cuando eliminas una imagen Docker, Docker no elimina automáticamente los contenedores que se han creado a partir de esa imagen. Esto significa que, aunque hayas eliminado la imagen, el contenedor seguirá ejecutándose normalmente.  
**Considerar**
Eliminar una imagen no afecta a los contenedores que se han creado a partir de esa imagen, a menos que esos contenedores dependan de archivos o configuraciones específicas de la imagen eliminada. En ese caso, es posible que los contenedores se comporten de manera inesperada después de eliminar la imagen.
Es una buena práctica detener y eliminar todos los contenedores que dependan de una imagen antes de eliminar la imagen en sí.

```
docker rmi -f <nombre imagen>:<tag>
```

