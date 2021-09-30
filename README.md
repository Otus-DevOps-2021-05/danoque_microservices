# danoque_microservices
danoque microservices repository

## Домашнее задание №15-16. Технология контейнеризации. Введение в Docker. Docker под капотом

### Запуск первого докер контейнера Hello-World

```
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1165f221234: Pull complete
Digest: sha256:776b0895d5e2fcd5e80bcdd607adc45461ba11143ef3df531174bf00679f43fe
Status: Downloaded newer image for hello-world:latest


### Рассмотрим основные команды для взаимодействия

Список запущенных контейнеров:

```bash
docker ps
```

Список всех контейнеров:

```bash
docker ps -a
```

Список сохраненных образов:

```bash
docker images
```

Команда run создает и запускает контейнер из image:

```bash
docker run -it ubuntu:18.04 /bin/bash
```

Сортировка контейнеров по дате создания:

```bash
docker ps -a --format "table {{.ID}}\t{{.Image}}\t{{.CreatedAt}}\t{{.Names}}"
```

Запуск остановленного контейнера:

```bash
docker start <u_container_id>
```

attach подсоединяет терминал к созданному контейнеру:

```bash
docker attach <u_container_id>
```

Запуск процесса внутри контейнера:

```bash
docker exec -it <u_container_id> bash
```

Создание image из контейнера:

```bash
docker commit <u_container_id> yourname/ubuntu-tmp-file
```

### Выполним создание image из контейнера

Создание image:

```bash
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker commit 4babfbfd5179 danoque/ubuntu-tmp-file
sha256:fjd63f8a8d593c3c1a3f6fjg743e6a3f119e17165f6g02ebc61a57fhd63hdjcx
```
выведем список образов:

```bash
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker images
REPOSITORY                TAG       IMAGE ID       CREATED        SIZE
danoque/otus-reddit       1.0       abdcfa63347c   7 weeks ago    646MB
reddit                    latest    e151e7920ff5   7 weeks ago    646MB
danoque/ubuntu-tmp-file   latest    cd0bf7e6b940   7 weeks ago    63.1MB
ubuntu                    18.04     39a8cfeef173   2 months ago   63.1MB
hello-world               latest    d1165f221234   2 months ago   13.3kB
```

### Задание со *

Выполним сравнение вывода двух команд и исследуем контейнер:
```
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker inspect 4babfbfd5179
[
    {
        "Id": "4hfjduf75g791d8b8506a03bc386f7dhd54haa0488ba203ff94a57d8jhf51fxb",
        "Created": "2021-07-29T18:18:54.9688137Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 3861,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-07-29T19:44:35.3451252Z",
            "FinishedAt": "2021-07-29T19:45:28.7651247+03:00"
        },
        "Image": "sha256:4hf6dfeef1730fhdnc62kzafe12368560fe62ef9d517808855f7bda798jf6dfga",
        "ResolvConfPath": "/var/snap/docker/common/var-lib-docker/containers/4babfbfd51791d8b8506a03bc386c128a208a90488ba203ff94a57d8dfa1afe4/resolv.conf",
        "HostnamePath": "/var/snap/docker/common/var-lib-docker/containers/4babfbfd51791d8b8506a03bc386c128a208a90488ba203ff94a57d8dfa1afe4/hostname",
        "HostsPath": "/var/snap/docker/common/var-lib-docker/containers/4babfbfd51791d8b8506a03bc386c128a208a90488ba203ff94a57d8dfa1afe4/hosts",
        "LogPath": "/var/snap/docker/common/var-lib-docker/containers/3jfbvnc6730791d8b8506a03bc386c128a208a90488ba203ff94a57d8dfa1afe4/4babfbfd51791d8b8506a03bc386c128a208a90488ba203ff94a57d8dfa1afe4-json.log",
        "Name": "/cool_elgamal",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
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
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
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
                "/sys/firmware"
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
            "Data": {
                "LowerDir": "/var/snap/docker/common/var-lib-docker/overlay2/bf80d30195dc261d894a371e9672949e4044294af1bd99c99549db9a711ca045-init/diff:/var/snap/docker/common/var-lib-docker/overlay2/51024c3a7ac7b0bfc29ac22720cf818e97dc872ac7f926249c3878dc35cabcd1/diff",
                "MergedDir": "/var/snap/docker/common/var-lib-docker/overlay2/bf80d30195dc261d894a371e9672949e4044294af1bd99c99549db9a711ca045/merged",
                "UpperDir": "/var/snap/docker/common/var-lib-docker/overlay2/bf80d30195dc261d894a371e9672949e4044294af1bd99c99549db9a711ca045/diff",
                "WorkDir": "/var/snap/docker/common/var-lib-docker/overlay2/bf80d30195dc261d894a371e9672949e4044294af1bd99c99549db9a711ca045/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "4babfbfd5179",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu:18.04",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "14dc3635995c0076526dc79978f04c267aa41764b54c2bad78d9104f55667464",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/run/snap.docker/netns/14dc3635995c",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "09a01a02e46cb3ef4be9890b9db8f86c4e6456a92d5f7787bb37871995956f3f",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "f8478e15573c5cb64f4c26283c55dce7595ff896ccc7c948d5819e79a840d0bb",
                    "EndpointID": "09a01a02e46cb3ef4be9890b9db8f86c4e6456a92d5f7787bb37871995956f3f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

Исследование образа:

```
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker inspect d1165f221234
[
    {
        "Id": "sha256:4kg8gi5489fgj3493c3c1a3f6d94a93e6a3f119e17965f6f02eb89ui9fghir58954g",
        "RepoTags": [
            "denis_petrov/ubuntu-tmp-file:latest"
        ],
        "RepoDigests": [],
        "Parent": "sha256:74hfyd63hf894ce93cefe12368560fe62ef9d517808855f7bda79a1eb697",
        "Comment": "",
        "Created": "2021-08-11T15:31:45.5264088Z",
        "Container": "a3578c0271dcb8506a03bc386c128a208a90488ba203ff94a57d8dfa1h8fhf6",
        "ContainerConfig": {
            "Hostname": "4babfbfd5179",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu:18.04",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "19.03.13",
        "Author": "",
        "Config": {
            "Hostname": "a3578c0271dc",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu:18.04",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 63137505,
        "VirtualSize": 63137505,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/snap/docker/common/var-lib-docker/overlay2/51024c3a7ac7b0bfc29ac22720cf818e97dc872ac7f926249c3878dc35cabcd1/diff",
                "MergedDir": "/var/snap/docker/common/var-lib-docker/overlay2/955a9dbbf53a4c00a53e48ab5571e57e26ebfaaceebd8c435b4f5f726eaa6214/merged",
                "UpperDir": "/var/snap/docker/common/var-lib-docker/overlay2/955a9dbbf53a4c00a53e48ab5571e57e26ebfaaceebd8c435b4f5f726eaa6214/diff",
                "WorkDir": "/var/snap/docker/common/var-lib-docker/overlay2/955a9dbbf53a4c00a53e48ab5571e57e26ebfaaceebd8c435b4f5f726eaa6214/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:54yrththw6ryh4h5454fe31c79cdf54470afe4dg54uh4f4y89g4r89rg89q423i",
                "sha256:w54hq34q344h6rj67w46db4b7fc8f9eb7eea34dffdcbc1506f3b3489rguh9g48"
            ]
        },
        "Metadata": {
            "LastTagTime": "2021-07-29T18:55:45.5627452+03:00"
        }
    }
]
```
Контейнер и образ различаются следующим образом, что контейнер является экземпляром образа. Именно контейнер содержит верхний слой доступный для записи, а непосредственно в образе содержатся слои только для чтения.
Можно создать еще один неизменный слой контейнера поверх исходного образа, т.е. на основе контейнера создаётся образ, в который сохранится текущее состояние контейнера.


### Docker rm & rmi
# удалит все незапущенные контейнеры
```bash
docker rm $(docker ps -a -q) 
```
# удалит все образы
```
docker rmi $(docker images -q) 
```

### Docker machine

Создание машины:
```
docker-machine create <имя>
```
После создания хоста и установки на нем Docker engine, работать с удаленным Docker'ом можно с помощью команды:

```bash
eval $(docker-machine env <имя>)
```

Эта же команда переключается между разными машинами.

Переключение на локальный докер:
```bash
eval $(docker-machine env --unset)
```

Удаление:
```bash
docker-machine rm <имя>
```
### Выполним сборку образа

```bash
docker build -t reddit:latest .

Sending build context to Docker daemon  7.168kB
Step 1/11 : FROM ubuntu:18.04
18.04: Pulling from library/ubuntu
...
Successfully built 0192d5086c2e
Successfully tagged reddit:latest
```
Запустим контейнер:

``` bash
docker run --name reddit -d --network=host reddit:latest
```

### Работа с Docker HUB

Загрузка образа в Docker HUB

```bash
$ docker push danoque/otus-reddit:1.0

```
Локально запусти Docker образа из репозитория Docker HUB:

```bash
docker run --name reddit -d -p 9292:9292 danoque/otus-reddit:1.0
Unable to find image 'danoque/otus-reddit:1.0' locally
1.0: Pulling from danoque/otus-reddit
```
```
danoque@danoque:~/Devops/Docker/danoque_microservices/dockermonolith$ docker ps
CONTAINER ID   IMAGE                     COMMAND       CREATED       STATUS                     PORTS     NAMES
520a9e38971d   danoque/otus-reddit:1.0   "/start.sh"   7 weeks ago   Exited (1) 7 weeks ago               reddit2
```

# ДЗ 17. Docker. Микросервисы

Подключимся к ранее созданному Docker host’у:

```
$ docker-machine ls
$ eval $(docker-machine env docker-host)
```
Локально сохраним файлы в каталог src, он станет главным рабочим каталогом, в котором расположатся:
post-py - сервис отвечающий за написание постов
comment - сервис отвечающий за написание комментариев
ui - веб-интерфейс, работающий с другими сервисами

Применим линтер для оптимизации Dockerfile на примере comment:

```
danoque@danoque:~/Devops/docker-3/src/comment$ hadolint Dockerfile 
Dockerfile:2 DL3008 warning: Pin versions in apt get install. Instead of `apt-get install <package>` use `apt-get install <package>=<version>`
Dockerfile:2 DL3009 info: Delete the apt-get lists after installing something
Dockerfile:2 DL3015 info: Avoid additional packages by specifying `--no-install-recommends`
Dockerfile:6 DL3020 error: Use COPY instead of ADD for files and folders
```
Постараемся исправить все недочёты + перепишем команды для RUN под более легкий alpine:

FROM ruby:2.3-alpine

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

COPY Gemfile* $APP_HOME/
RUN apt-get update -qq --no-install-recommends\
&& apt-get install -y --no-install-recommends\
&& build-essential --no-install-recommends\
&& bundle install --no-install-recommends\
&& apt-get clean && rm -rf /var/lib/apt/lists/*


COPY . $APP_HOME


ENV COMMENT_DATABASE_HOST comment_db
ENV COMMENT_DATABASE comment

CMD ["puma"]

Выполним анологичные манипуляции с Dockerfile для "post" и "ui".
Выполним сборку приложения:
Скачаем последний образ MongoDB:
```
docker pull mongo:latest
```
Соберем образы с нашими сервисами:
```
docker build -t danoque/post:1.0 ./post-py
docker build -t danoque/comment:1.0 ./comment
docker build -t danoque/ui:1.0 ./ui
```
Создадим специальную сеть для приложения:
```
docker network create reddit
```
И запустим наши контейнеры:
```
docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db -v reddit_db:/data/db mongo:latest
docker run -d --network=reddit --network-alias=post danoque/post:1.0
docker run -d --network=reddit --network-alias=comment danoque/comment:1.0
docker run -d --network=reddit -p 9292:9292 danoque/ui:2.0
```
Проекты успешно собираются и сервис доступен.Теперь, чтобы добавить возможность сохранения постов после остановки и запуска контейнеров выполним следующие инструкции:

Выключим старые копии контейнеров:
```
docker kill $(docker ps -q)
```
Запустим новые копии контейнеров:

```
docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db -v reddit_db:/data/db mongo:latest
docker run -d --network=reddit --network-alias=post danoque/post:1.0
docker run -d --network=reddit --network-alias=comment danoque/comment:1.0
docker run -d --network=reddit -p 9292:9292 danoque/ui:2.0
```



#Домашнее задание №18 Сетевое взаимодействие Docker контейнеров. Docker Compose. Тестирование образов
##15 ДЗ: Практика работы с основными типами Docker сетей. Декларативное описание Docker инфраструктуры при помощи Docker Compose.
###Подключаемся к ранее созданному docker host’у
```
> docker-machine ls
NAME
ACTIVE
docker-host
-
DRIVER
google
STATE
Running
URL
SWARM
tcp://<docker-host-ip>:2376
DOCKER
v17.09.0-ce
```
```
> eval $(docker-machine env docker-host)
```

Создадим bridge-сеть в docker (флаг --driver указывать не обязательно, т.к. по-умолчанию используется bridge:
```
> docker network create reddit --driver bridge
Запустим наш проект reddit с использованием bridge-сети
> docker run -d --network=reddit mongo:latest
> docker run -d --network=reddit <your-dockerhub-login>/post:1.0
> docker run -d --network=reddit <your-dockerhub-login>/comment:1.0
> docker run -d --network=reddit -p 9292:9292 <your-dockerhub-login>/ui:1.0
```

На самом деле, наши сервисы ссылаются друг на друга по dns-
именам, прописанным в ENV-переменных (см Dockerfile). В текущей
инсталляции встроенный DNS docker не знает ничего об этих
именах.
Решением проблемы будет присвоение контейнерам имен или
сетевых алиасов при старте:
```
--name <name> (можно задать только 1 имя)
--network-alias <alias-name> (можно задать множество алиасов)
```

Остановим старые копии контейнеров:
```
> docker kill $(docker ps -q)
```
Запустим новые:
```
> docker run -d --network=reddit --network-alias=post_db --network-
```
```
alias=comment_db mongo:latest
> docker run -d --network=reddit --network-alias=post danoque/post:
1.0
> docker run -d --network=reddit --network-alias=comment
comment:1.0
danoque/
> docker run -d --network=reddit -p 9292:9292 danoque/ui:1.0
```

Давайте запустим наш проект в 2-х bridge сетях. Так , чтобы сервис ui
не имел доступа к базе данных в соответствии со схемой ниже. Остановим старые копии контейнеров:
```
> docker kill $(docker ps -q)
```
Создадим docker-сети:
```
> docker network create back_net --subnet=10.0.2.0/24
> docker network create front_net --subnet=10.0.1.0/24
```

Docker при инициализации контейнера может подключить к нему только 1 сеть.
При этом контейнеры из соседних сетей не будут доступны как в DNS, так
и для взаимодействия по сети. Поэтому нужно поместить контейнеры post и comment в обе сети.
Дополнительные сети подключаются командой:
```
> docker network connect <network> <container>
```
Подключим контейнеры ко второй сети:
```
> docker network connect front_net post
> docker network connect front_net comment
```

Давайте посмотрим как выглядит сетевой стек Linux в
текущий момент, опираясь на схему из предыдущего
слайда:
1) Зайдём по ssh на docker-host и установите пакет bridge-utils:
```
> docker-machine ssh docker-host
> sudo apt-get update && sudo apt-get install bridge-utils
```
3) Выполним:
```
> docker network ls
```
4) Найдём ID сетей, созданных в рамках проекта:
```
yc-user@docker-host6:~$ sudo docker network ls
NETWORK ID     NAME        DRIVER    SCOPE
884aeb9b795a   back_net    bridge    local
0873e63bbe3a   bridge      bridge    local
7a467eadfd14   front_net   bridge    local
4ecd432d4a5e   host        host      local
9b1eaacf4bba   none        null      local
36b3d5878b6c   reddit      bridge    local
cd7674c32c9e   reddit2     bridge    local
```

4) Выполним :
```
> ifconfig | grep br
```
```
yc-user@docker-host6:~$ ifconfig | grep br
br-36b3d5878b6c: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
br-7a467eadfd14: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.1.1  netmask 255.255.255.0  broadcast 10.0.1.255
br-884aeb9b795a: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.1  netmask 255.255.255.0  broadcast 10.0.2.255
br-cd7674c32c9e: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.19.0.1  netmask 255.255.0.0  broadcast 172.19.255.255
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet 10.130.0.7  netmask 255.255.255.0  broadcast 10.130.0.255
```
5) Найдём bridge-интерфейсы для каждой из сетей. Просмотрим
информацию о каждом.
6) Выберим любой из bridge-интерфейсов и выполним команду. Ниже
пример вывода:
```
yc-user@docker-host6:~$ brctl show br-36b3d5878b6c
bridge name	bridge id		STP enabled	interfaces
br-36b3d5878b6c		8000.0242945cd971	no	
```
```
yc-user@docker-host6:~$ brctl show br-7a467eadfd14
bridge name	bridge id		STP enabled	interfaces
br-7a467eadfd14		8000.02424f04624b	no		veth5fbc5bc
							veth660913e
							veth95e90f0
```


```
yc-user@docker-host6:~$ brctl show br-884aeb9b795a
bridge name	bridge id		STP enabled	interfaces
br-884aeb9b795a		8000.02420e790119	no		veth026f3cb
							veth3db4cb7
							vethd29882b
```

```
yc-user@docker-host6:~$ brctl show br-cd7674c32c9e
bridge name	bridge id		STP enabled	interfaces
br-cd7674c32c9e		8000.0242da6fbc64	no		
```

7) Давайте посмотрим как выглядит iptables. Выполним:
```
yc-user@docker-host6:~$ sudo iptables -nL -t nat
Chain PREROUTING (policy ACCEPT)
target     prot opt source               destination         
DOCKER     all  --  0.0.0.0/0            0.0.0.0/0            ADDRTYPE match dst-type LOCAL

Chain INPUT (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
DOCKER     all  --  0.0.0.0/0           !127.0.0.0/8          ADDRTYPE match dst-type LOCAL

Chain POSTROUTING (policy ACCEPT)
target     prot opt source               destination         
MASQUERADE  all  --  10.0.1.0/24          0.0.0.0/0           
MASQUERADE  all  --  10.0.2.0/24          0.0.0.0/0           
MASQUERADE  all  --  172.19.0.0/16        0.0.0.0/0           
MASQUERADE  all  --  172.17.0.0/16        0.0.0.0/0           
MASQUERADE  all  --  172.18.0.0/16        0.0.0.0/0           
MASQUERADE  tcp  --  10.0.1.2             10.0.1.2             tcp dpt:9292

Chain DOCKER (2 references)
target     prot opt source               destination         
RETURN     all  --  0.0.0.0/0            0.0.0.0/0           
RETURN     all  --  0.0.0.0/0            0.0.0.0/0           
RETURN     all  --  0.0.0.0/0            0.0.0.0/0           
RETURN     all  --  0.0.0.0/0            0.0.0.0/0           
RETURN     all  --  0.0.0.0/0            0.0.0.0/0           
DNAT       tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:9292 to:10.0.1.2:9292
```
Цепочка Docker и правила DNAT отвечают за перенаправление трафика на адреса уже конкретных контейнеров.

Выполним команду:
```
yc-user@docker-host6:~$ ps ax | grep docker-proxy
 3886 ?        Sl     0:00 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 9292 -container-ip 10.0.1.2 -container-port 9292
 3893 ?        Sl     0:00 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 9292 -container-ip 10.0.1.2 -container-port 9292
11380 pts/0    S+     0:00 grep --color=auto docker-proxy
```
### DOCKER-COMPOSE
Отметим, что docker-compose поддерживает интерполяцию (подстановку) переменных окружения. В данном случае это переменная USERNAME.
Поэтому перед запуском необходимо экспортировать значения данных переменных окружения.
Остановим контейнеры, запущенные на предыдущих шагах:
```
> docker kill $(docker ps -q)
```
Выполним:
```
> export USERNAME=danoque
> docker-compose up -d
Creating src_comment_1 ... done
Creating src_ui_1      ... done
Creating src_post_1    ... done
Creating src_post_db_1 ... done
```
```
> danoque@danoque:~/Devops/docker-3/src$ docker-compose ps
    Name                  Command             State                    Ports                  
----------------------------------------------------------------------------------------------
src_comment_1   puma                          Up                                              
src_post_1      python3 post_app.py           Up                                              
src_post_db_1   docker-entrypoint.sh mongod   Up      27017/tcp                               
src_ui_1        puma                          Up      0.0.0.0:9292->9292/tcp,:::9292->9292/tcp
```

### Задания:
1)Изменить docker-compose под кейс с множеством сетей, сетевых алиасов. Параметризируем с помощью переменных окружений.Параметризованные параметры запишим в отдельный файл c расширением .env:
• порт публикации сервиса ui
• версии сервисов

### Параметризация сетей в Docker-Compose
Для определения имени проекта базовое имя проекта задаётся через COMPOSE_PROJECT_NAME также в файле .ENV.
