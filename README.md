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



## Домашнее задание №20 Устройство Gitlab CI.
ДЗ 16: Gitlab CI. Построение процесса непрерывной интеграции

###  Создание виртуальной машины при помощи web-консоли, установка Docker-Machine и запуск контейнера
Запустим GitLab с помощью Docker, в команде определим все необходимые значения: IP, password, директории под Data Volume; в hostname укажем IP адрес ВМ.

```
docker run -d -v $GITLAB_HOME/config:/etc/gitlab -v $GITLAB_HOME/logs:/var/log/gitlab -v $GITLAB_HOME/data:/var/opt/gitlab --hostname 62.84.123.174 -p 443:443 -p 80:80 -p 2222:22 -e GITLAB_ROOT_EMAIL="root@local" -e GITLAB_ROOT_PASSWORD="danoquedanoque" -e EXTERNAL_URL="62.84.123.174" --name gitlab --restart unless-stopped gitlab/gitlab-ce:latest
```

Чтобы использовать репозиторий проекта GitLab, добавим ещё один remote к нашему локальному microservices-репозиторию:
```
git checkout -b gitlab-ci-1
git remote add gitlab http://<your-vm-ip>/homework/example.git
git push gitlab gitlab-ci-1
```


### Определение CI/CD Pipeline.

Пайплайн для GitLab определяется в файле .gitlab-ci.yml. Создайте его в
корне репозитория. И запушим его:
```
git add .gitlab-ci.yml
git commit -m 'add pipeline definition'
git push gitlab gitlab-ci-1
```

Теперь, если перейти в раздел
CI/CD -> Pipelines , мы увидим что пайплайн попытался запуститься, но находится в статусе pending или stuck , так как у нас пока нет раннеров.

### Cоздим и зарегистририруем раннер.

Для регистрации нужен токен. Увидеть его можно в настройках проекта: Settings -> CI/CD -> Pipelines -> Runners и посмотреть на секцию Set up a specific Runner manually .
На сервере, где работает Gitlab CI, выполним команду:
```
docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
```
```
docker exec -it gitlab-runner gitlab-runner register --url http://62.84.123.174 --non-interactive --locked=false --name DockerRunner --executor docker --docker-image alpine:latest --registration-token MyF5jQjszAqd6aRw9MGs --tag-list "linux,xenial,ubuntu,docker" --run-untagged
```
В настройках появится новый раннер, а пайплайн будет запущен.


### Добавим Reddit  в репозиторий:
Добавм исходный код reddit в репозиторий:
```
git clone https://github.com/express42/reddit.git && rm -rf ./reddit/.git
git add reddit/
git commit -m "Add reddit app"
git push gitlab gitlab-ci-1
```

Изменим описание пайплайна в .gitlab-ci.yml:
```
image: ruby:2.4.2
stages:
...
variables:
DATABASE_URL: 'mongodb://mongo/user_posts'
before_script:
- cd reddit
- bundle install
...
test_unit_job:
stage: test
services:
- mongo:latest
script:
- ruby simpletest.rb
```
В папке reddit создадим simpletest.rb: https://gist.github.com/Nklya/d70ff7c6d1c02de8f18bcd049e904942

И добавим библиотеку rack-test для тестирования в файл reddit/Gemfile.
Сделаем push в GitLab и убедимся что test_unut_job проводит тесты.

Изменим пайплайн таким образом, чтобы deploy_job стал определением окружения dev, на которое условно будет выкатываться каждое изменение в коде проекта.

Переименуем stage deploy в review, а deploy_job заменим на deploy_dev_job и определим окружение в ней

Если после успешного завершения пайплайна с определением окружения перейти в Operations -> Environments , то там появится определение первого окружения

PHOTO 2


### Staging и Production

Определим два новых этапа: stage и production. Первый будет
содержать задачу, имитирующую выкатку на окружение staging, второй - на
production.


Определим эти задачи таким образом, чтобы они запускались вручную,
с помощью аргумента when: manual. И На странице окружений должны появиться окружения staging и production.

Директива only описывает список условий, которые должны быть истинны, чтобы job мог запуститься. Регулярное выражение слева означает, что должен стоять semver тэг в git, например 2.4.10 .

Изменения без указания тэга запустят пайплайн без задач staging и
production.
Изменение, помеченное тэгом в git, запустит полный пайплайн.
```
git commit -am '#4 add logout button to profile page'
git tag 2.4.10
git push gitlab gitlab-ci-1 --tags
```

Gitlab CI позволяет определить динамические окружения. Эта мощная
функциональность позволяет вам иметь выделенный стенд для, например,
каждой feature-ветки в git.
Определяются динамические окружения с помощь переменных, доступных в .gitlab-ci.yml

Добавим ещё одну задачу. Эта задача определяет динамическое окружение для каждой ветки в репозитории, кроме ветки master.
```
...
branch review:
stage: review
script: echo "Deploy to $CI_ENVIRONMENT_SLUG"
environment:
name: branch/$CI_COMMIT_REF_NAME
url: http://$CI_ENVIRONMENT_SLUG.example.com
only:
- branches
except:
- master
staging
```
Теперь на каждую ветку в git, отличную от master, Gitlab CI будет определять новое окружение.




