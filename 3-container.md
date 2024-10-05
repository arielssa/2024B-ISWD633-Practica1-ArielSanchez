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

### Salida:

```
bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a
```

Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

### Actividad 2: Crear el contenedor usando la imagen hello-world

### Comandos:

```
docker pull hello-world
docker create hello-world:latest
```

### Salida:

```
74a84e28dcd286ea83092fec120176c02ea7aefa490f1b964d13a01a02ea7901
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

### Salida:

```
srv-web
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

### Salida:

```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/10/05 03:06:21 [notice] 1#1: using the "epoll" event method
2024/10/05 03:06:21 [notice] 1#1: nginx/1.27.2
2024/10/05 03:06:21 [notice] 1#1: built by gcc 13.2.1 20240309 (Alpine 13.2.1_git20240309) 
2024/10/05 03:06:21 [notice] 1#1: OS: Linux 5.15.153.1-microsoft-standard-WSL2
2024/10/05 03:06:21 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/10/05 03:06:21 [notice] 1#1: start worker processes
2024/10/05 03:06:21 [notice] 1#1: start worker process 30
2024/10/05 03:06:21 [notice] 1#1: start worker process 31
2024/10/05 03:06:21 [notice] 1#1: start worker process 32
2024/10/05 03:06:21 [notice] 1#1: start worker process 33
2024/10/05 03:06:21 [notice] 1#1: start worker process 34
2024/10/05 03:06:21 [notice] 1#1: start worker process 35
2024/10/05 03:06:21 [notice] 1#1: start worker process 36
2024/10/05 03:06:21 [notice] 1#1: start worker process 37
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

### Salida:

```
1d035f2f3053a8a60f45216ac3bd9011e463500fc553377f394e8d7df9b0a919
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

### Salida:

```
gracious_ishizaka
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

### Salida:

```
srv-web3
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

### Salida:

```
[
    {
        "Id": "bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a",
        "Created": "2024-10-05T02:46:04.757753273Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-10-05T02:52:49.556079085Z",
            "FinishedAt": "2024-10-05T02:54:19.795017918Z"
        },
        "Image": "sha256:2140dad235c130ac861018a4e13a6bc8aea3a35f3a40e20c1b060d51a7efd250",
        "ResolvConfPath": "/var/lib/docker/containers/bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a/hostname",
        "HostsPath": "/var/lib/docker/containers/bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a/hosts",  
        "LogPath": "/var/lib/docker/containers/bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a/bc100d90ab59983a3f1f15f04d49e18fb0cc36d2be6d7465b013a2cd3974675a-json.log",
        "Name": "/srv-web",
        "RestartCount": 0,
        "Driver": "overlayfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                14,
                123
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": null,
            "Name": "overlayfs"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "bc100d90ab59",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.27.2",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=0.8.6",
                "NJS_RELEASE=1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:alpine",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers \u003cdocker-maint@nginx.com\u003e"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "",
            "SandboxKey": "",
            "Ports": {},
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "",
                    "DriverOpts": null,
                    "NetworkID": "70b7dd8a26108c561564cc9e6f85cc8758b2893c6b6fdb61f30deadbd87ff02f",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        }
    }
]
```
