# Contenedores

### Crear un contenedor
Para crear un nuevo contenedor Docker a partir de una imagen específica, pero sin iniciarlo automáticamente. 

```
docker create --name <nombre contenedor> <nombre imagen>:<tag>
```
Crear el contenedor  **srv-web** usando la imagen nginx version alpine
# COMPLETAR
````
PS C:\Users\User> docker create --name srv-web nginx:alpine
0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83
````

Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

Crear el contenedor usando la imagen hello-world
# COMPLETAR
````

PS C:\Users\User> docker create hello-world
90823ba9dde8cd7593c657520932b34dbd4a6c5a42fa6be38e0dc4b6588a3fd8
````

### Listar los contenedores ejecutándose o no

```
docker ps -a
```

### Para iniciar un contenedor

```
docker start <nombre contenedor o identificador>
```
Iniciar el contenedor srv-web 
# COMPLETAR
````
PS C:\Users\User> docker start srv-web
srv-web
````
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

Crear y ejecutar inmediatamente el contenedor **srv-web2** usando la imagen nginx:alpine
# COMPLETAR

**¿Qué sucede luego de la ejecución del comando?**
# COMPLETAR  
````
el contenedor se ejecuta y sale el mensaje start worker process con un numero de ejecucion en m caso el 37 y no puedo ejecutar nada mas hasta detenrlo
````

Cuando ejecutas un contenedor en primer plano sin la opción -d (modo detach), el contenedor captura la entrada estándar (stdin) del terminal, lo que significa que el terminal queda "atrapado" y no puedes introducir más comandos hasta que detengas el contenedor.

### Para crear un contenedor y ejecutarlo inmediatamente sin estar vinculados al mismo
-d: Es la opción que indica a Docker que ejecute el contenedor en segundo plano (en modo "detach").
Cuando un contenedor se ejecuta en segundo plano, Docker devuelve el control al terminal inmediatamente después de iniciar el contenedor, lo que permite al usuario seguir ejecutando otros comandos en el mismo terminal sin que el contenedor detenga la interacción.

```
docker run -d --name <nombre contenedor> <nombre imagen>:tag
```
Crear y ejecutar inmediatamente el contenedor **srv-web3** en modo detach usando la imagen nginx:alpine
# COMPLETAR
````
docker run -d --name srv-web3 nginx:alpine
6e9e72295868d56186e71b70873c27e38c4a042bc807b4c6e43155831c70a649
````

### Para eliminar un contenedor

```
docker rm <nombre contenedor>
```
Eliminar el contenedor que se creó a partir de la imagen hello-world 
# COMPLETAR
````
Primero para verificar debemos buscar el contenedor que tiene dicha imagen con el siguiente comando
docker ps -a

PS C:\Users\User> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
6e9e72295868   nginx:alpine   "/docker-entrypoint.…"   11 minutes ago   Up 11 minutes               80/tcp    srv-web3
36bda26f0e76   nginx:alpine   "/docker-entrypoint.…"   18 minutes ago   Exited (0) 12 minutes ago             srv-web2
d60160c2458b   hello-world    "/hello"                 2 days ago       Exited (0) 2 days ago                 tender_dubinsky
90823ba9dde8   hello-world    "/hello"                 2 days ago       Created                               optimistic_grothendieck    
0318718335f6   nginx:alpine   "/docker-entrypoint.…"   2 days ago       Exited (255) 18 hours ago   80/tcp    srv-web
1883dd500d41   nginx          "/docker-entrypoint.…"   2 days ago       Exited (0) 2 days ago                 peaceful_nightingale


En este caso a buscarlo podemos notar que su nombre es tender_dubinsky y su comando /hello
docker rm teneder_dubinsky
````
Verificar que el contenedor que se eliminó
# COMPLETAR

````
para verificar qeu se elimino el contenedor tenemos que volver a utilizar el comando
docker ps -a
al ejecutarlo podemos apreciar que se elimino el contenedor especificado se elimino
PS C:\Users\User> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
6e9e72295868   nginx:alpine   "/docker-entrypoint.…"   11 minutes ago   Up 11 minutes               80/tcp    srv-web3
36bda26f0e76   nginx:alpine   "/docker-entrypoint.…"   18 minutes ago   Exited (0) 12 minutes ago             srv-web2
90823ba9dde8   hello-world    "/hello"                 2 days ago       Created                               optimistic_grothendieck    
0318718335f6   nginx:alpine   "/docker-entrypoint.…"   2 days ago       Exited (255) 18 hours ago   80/tcp    srv-web
1883dd500d41   nginx          "/docker-entrypoint.…"   2 days ago       Exited (0) 2 days ago                 peaceful_nightingale
````

### Para eliminar un contenedor que esté ejecutándose

```

docker rm -f <nombre contenedor>
```
Eliminar el contenedor **srv-web3** 
# COMPLETAR
````
Pra eliminarlo se usa el comando
PS C:\Users\User> docker rm -f srv-web3
srv-web3
````

Verificar que el contenedor que se eliminó
# COMPLETAR
````
para verificar que se elimino se usa el comando
PS C:\Users\User> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
36bda26f0e76   nginx:alpine   "/docker-entrypoint.…"   24 minutes ago   Exited (0) 18 minutes ago             srv-web2
90823ba9dde8   hello-world    "/hello"                 2 days ago       Created                               optimistic_grothendieck    
0318718335f6   nginx:alpine   "/docker-entrypoint.…"   2 days ago       Exited (255) 18 hours ago   80/tcp    srv-web
1883dd500d41   nginx          "/docker-entrypoint.…"   2 days ago       Exited (0) 2 days ago                 peaceful_nightingale       

````

### Para inspecionar un contenedor 

Inspeccionar el contenedor **srv-web** 
# COMPLETAR
````
para inspeccionar usamos el siguiente comando
PS C:\Users\User> docker inspect srv-web
>>
[
    {
        "Id": "0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83",
        "Created": "2024-10-09T22:25:18.78447365Z",
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
            "ExitCode": 255,
            "Error": "",
            "StartedAt": "2024-10-09T22:30:36.22697507Z",
            "FinishedAt": "2024-10-12T03:21:17.526688704Z"
        },
        "Image": "sha256:2140dad235c130ac861018a4e13a6bc8aea3a35f3a40e20c1b060d51a7efd250",
        "ResolvConfPath": "/var/lib/docker/containers/0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83/resolv.conf",     
        "HostnamePath": "/var/lib/docker/containers/0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83/hostname",
        "HostsPath": "/var/lib/docker/containers/0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83/hosts",
        "LogPath": "/var/lib/docker/containers/0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83/0318718335f697027f68f9c65eee03342653ac3e734277ca7e6f9a3ca38d2b83-json.log",
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
                8,
                107
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
            "Hostname": "0318718335f6",
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
                    "NetworkID": "921b62eb633d4d0874c138c4b49810d3fab044abf2bcd146b48cf41657c23597",
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
PS C:\Users\User>
````
