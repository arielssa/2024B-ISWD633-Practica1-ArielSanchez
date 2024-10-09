# Contenedores

### Crear un contenedor
Para crear un nuevo contenedor Docker a partir de una imagen específica, pero sin iniciarlo automáticamente. 

```
docker create --name <nombre contenedor> <nombre imagen>:<tag>
```
### Actividad 1: Crear el contenedor  **srv-web** usando la imagen nginx version alpine

### Comando:

```
docker create --name srv-web nginx:alpine
```

Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

### Actividad 2: Crear el contenedor usando la imagen hello-world

### Comandos:

```
docker pull hello-world
docker create hello-world:latest
```

### Nombre asignado:

```
gracious_ishizaka
```

### Listar los contenedores ejecutándose o no

```
docker ps -a
```

### Para iniciar un contenedor

```
docker start <nombre contenedor o identificador>
```
### Actividad 3: Iniciar el contenedor srv-web 

### Comando:

```
docker start srv-web
```

### Listar los contenedores ejecutándose
```
docker ps 
docker ps | grep <nombre contenedor>
```

### Para detener un contenedor

```
docker stop <nombre contenedor>
```

### Para crear un contenedor y ejecutarlo inmediatamente

```
docker run --name <nombre contenedor> <nombre imagen>:<tag>
```
![Ecosistema de Docker](img/dockerRun.PNG)

### Actividad 4: Crear y ejecutar inmediatamente el contenedor **srv-web2** usando la imagen nginx:alpine

### Comando:

```
docker run --name srv-web2 nginx:alpine
```

### Actividad 5: **¿Qué sucede luego de la ejecución del comando?**

### El proceso no termina. Hay varias razones por las que no termina: el servicio no se detiene para atender conexiones entrantes o Nginx está esperando solicitudes HTTP entrantes en sus puertos configurados.

Cuando ejecutas un contenedor en primer plano sin la opción -d (modo detach), el contenedor captura la entrada estándar (stdin) del terminal, lo que significa que el terminal queda "atrapado" y no puedes introducir más comandos hasta que detengas el contenedor.

### Para crear un contenedor y ejecutarlo inmediatamente sin estar vinculados al mismo
-d: Es la opción que indica a Docker que ejecute el contenedor en segundo plano (en modo "detach").
Cuando un contenedor se ejecuta en segundo plano, Docker devuelve el control al terminal inmediatamente después de iniciar el contenedor, lo que permite al usuario seguir ejecutando otros comandos en el mismo terminal sin que el contenedor detenga la interacción.

```
docker run -d --name <nombre contenedor> <nombre imagen>:tag
```
### Actividad 6: Crear y ejecutar inmediatamente el contenedor **srv-web3** en modo detach usando la imagen nginx:alpine

### Comando:

```
docker run -d --name srv-web3 nnginx:alpine
```

### Para eliminar un contenedor

```
docker rm <nombre contenedor>
```
### Actividad 7: Eliminar el contenedor que se creó a partir de la imagen hello-world 

### Comando:

```
docker rm gracious_ishizaka
```

### Actividad 8: Verificar que el contenedor que se eliminó

### Comando:

```
docker ps -a
```

### Salida:

```
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS                      PORTS     NAMES
1d035f2f3053   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute           80/tcp    srv-web3 
846c72fb5818   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago       Exited (0) 2 minutes ago              srv-web2 
bc100d90ab59   nginx:alpine   "/docker-entrypoint.…"   35 minutes ago       Exited (0) 26 minutes ago             srv-web  
```

### Para eliminar un contenedor que esté ejecutándose

```
docker rm -f <nombre contenedor>
```
### Actividad 9: Eliminar el contenedor **srv-web3** 

### Comando:

```
docker rm -f srv-web3
```

### Actividad 10: Verificar que el contenedor que se eliminó

### Comando:

```
docker ps -a
```

### Salida:

```
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
846c72fb5818   nginx:alpine   "/docker-entrypoint.…"   16 minutes ago   Exited (0) 3 minutes ago              srv-web2     
bc100d90ab59   nginx:alpine   "/docker-entrypoint.…"   36 minutes ago   Exited (0) 28 minutes ago             srv-web   
```

### Para inspecionar un contenedor 

### Actividad 11: Inspeccionar el contenedor **srv-web** 

### Comando:

```
docker inspect srv-web
```
