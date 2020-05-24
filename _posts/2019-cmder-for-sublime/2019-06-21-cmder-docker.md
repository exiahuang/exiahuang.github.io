---
categories:
- CmderForSublime
- develop
date: 2019/06/21 22:22:22
layout: post
tags:
- CmderForSublime
- Docker
title: Cmder for Docker
update_date: 2020/05/24 14:04:58

---

# Cmder for Docker

If you install cmder, you can use docker in sublime text.
Use docker easily in sublime text!

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/EapWSdgQ1js" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## docker command

![github setting](http://salesforcexytools.com/mystatic/media/CmderForSublime/CmderForSublime-Docker.png)


| Lable | Command | Description |
| ---- | ---- | ---- |
| docker:images:digests:docker_image | docker images --digests ${input:docker_image_name} |  |
| docker:image:inspect | docker image inspect ${input:docker_image_name} | Inspect and see volume |
| docker:help | docker | Show commands & management commands |
| docker:version | docker version | Docker version info |
| docker:info | docker info | Show info like number of containers, etc |
| docker:container:ls | docker container ls | List running containers |
| docker:ps | docker ps |  |
| docker:container:ls:all | docker container ls -a | List all containers (Even if not running) |
| docker:container:ls:name-only | docker ps --format "{{.Names}}" --all | List all containers (Name Only) |
| docker:container:logs | docker container logs ${select:docker_container_name} | Get logs (Use name or ID) |
| docker:container:top | docker container top ${select:docker_container_name} | List processes running in container |
| docker:image:ls | docker image ls | List the images we have pulled |
| docker:images:grep_by_name | docker images ${input:docker_image_name} | List the images we have pulled |
| docker:pull | docker pull ${input:docker_image_name} | We can also just pull down images |
| docker:image:remove | docker image rm ${input:docker_image_name_or_id} | Remove image |
| docker:stop:all | docker stop $(docker ps -aq) | Stop all running containers, Work in linux |
| docker:container:rm:all | docker rm $(docker ps -aq) | Remove all containers, Work in linux |
| docker:image:remove:all | docker rmi $(docker images -a -q) | Remove all images, Work in linux |
| docker:container:inspect | docker container inspect ${select:docker_container_name} | Inspect and View info on container |
| docker:container:inspect:format | docker container inspect --format '{{ .NetworkSettings.IPAddress }}' ${select:docker_container_name} | Specific property (--format) |
| docker:container:stats | docker container stats ${select:docker_container_name} | Performance stats (cpu, mem, network, disk, etc) |
| docker:container:start | docker container start ${select:docker_container_name} | Start container |
| docker:container:start:attach | docker container start -ai ${select:docker_container_name} | Access an already created container, start with -ai |
| docker:container:restart | docker container restart ${select:docker_container_name} | Restart container |
| docker:container:stop | docker container stop ${select:docker_container_name} | Stop container |
| docker:container:rm | docker container rm ${select:docker_container_name} | Remove container (Can not remove running containers, must stop first) |
| docker:container:rm:force | docker container rm -f ${select:docker_container_name} | To remove a running container use force(-f) |
| docker:container:exec:attach:shell | docker container exec -it ${select:docker_container_name} /bin/sh -c "[ -e /bin/bash ] && /bin/bash &#124;&#124; /bin/sh" | attach shell |
| docker:container:create | docker container run -it -d --name ${input:new_docker_container_name} ${input:exist_docker_image} | Create and run a container in background |
| docker:container:create:include_network | docker container run -it -d --name ${input:docker_container} --network ${input:docker_network_name} ${input:docker_image} | Create container on network |
| docker:container:create:example | docker container run -it -d --name ${input:new_docker_container_name} ${select:docker_image} | Some docker container example, Alpine is a very small Linux distro good for docker |
| docker:container:create:nginx | docker container run -it -d -p 9090:80 --name nginx nginx | NGINX container |
| docker:container:create:ubuntu | docker container run -it -d --name ubuntu ubuntu | ubuntu container |
| docker:container:create:alpine | docker container run -it -d --name alpine alpine | Alpine container |
| docker:container:create:apache | docker container run -it -d -p 8080:80 --name apache httpd | APACHE container |
| docker:container:create:mongodb | docker container run -it -d -p 27017:27017 --name mongo mongo | MONGODB container |
| docker:example:mysql | docker container run -it -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql | MYSQL container |
| docker:container:port | docker container port ${select:docker_container_name} | Get port |
| docker:network:ls | docker network ls | List networks |
| docker:network:inspect | docker network inspect ${input:docker_network_name} | Inspect network |
| docker:network:create | docker network create ${input:docker_network_name} | Create network |
| docker:network:connect:container | docker network connect ${input:docker_network_name} ${select:docker_container_name} | Connect existing container to network |
| docker:network:disconnect:container | docker network disconnect ${input:docker_network_name} ${select:docker_container_name} | Disconnect container from network |
| docker:image:tag:retag | docker image tag ${input:old_docker_image_name} ${input:new_docker_image_name} | Retag existing image |
| docker:image:push:to_dockerhub | docker image push ${input:docker_image_tag} | Upload to dockerhub |
| docker:login | docker login | docker login |
| docker:image:build | docker image build -t ${input:REPONAME} . | build image build |
| docker:volume:ls | docker volume ls | Check volumes |
| docker:volume:prune | docker volume prune | Cleanup unused volumes |
| docker-compose:up:background | docker-compose up -d | run in background |
| docker-compose:up | docker-compose up | run in front |
| docker-compose:down | docker-compose down | To cleanup |



## docker config



this is the setting of `Cmder For Sublime`

```json
{
	"tasks" : [
	//////////////////////////Docker Command Start/////////////////////////////////
		{
			"desc" : "",
			"label" : "docker:images:digests:docker_image",
			"encoding" : "UTF-8",
			"command": "docker images --digests ${input:docker_image_name}"
		},
		{
			"desc" : "Inspect and see volume",
			"label" : "docker:image:inspect",
			"encoding" : "UTF-8",
			"command": "docker image inspect ${input:docker_image_name}"
		},

		// Docker Commands, Help & Tips
		{
			"desc" : "Show commands & management commands",
			"label" : "docker:help",
			"encoding" : "UTF-8",
			"command" : "docker"
		},
		{
			"desc" : "Docker version info",
			"label" : "docker:version",
			"encoding" : "UTF-8",
			"command" : "docker version"
		},
		{
			"desc" : "Show info like number of containers, etc",
			"label" : "docker:info",
			"encoding" : "UTF-8",
			"command" : "docker info"
		},

		// WORKING WITH CONTAINERS
		{
			"desc" : "List running containers",
			"label" : "docker:container:ls",
			"encoding" : "UTF-8",
			"command" : "docker container ls"
		},
		{
			"label" : "docker:ps",
			"encoding" : "UTF-8",
			"command" : "docker ps"
		},
		{
			"desc" : "List all containers (Even if not running)",
			"label" : "docker:container:ls:all",
			"encoding" : "UTF-8",
			"command" : "docker container ls -a"
		},
		{
			"desc" : "List all containers (Name Only)",
			"label" : "docker:container:ls:name-only",
			"encoding" : "UTF-8",
			"command" : "docker ps --format \"{{.Names}}\" --all"
		},
		{
			"desc" : "Get logs (Use name or ID)",
			"label" : "docker:container:logs",
			"encoding" : "UTF-8",
			"command" : "docker container logs ${select:docker_container_name}"
		},
		{
			"desc" : "List processes running in container",
			"label" : "docker:container:top",
			"encoding" : "UTF-8",
			"command" : "docker container top ${select:docker_container_name}"
		},
		// IMAGE COMMANDS
		{
			"desc" : "List the images we have pulled",
			"label" : "docker:image:ls",
			"encoding" : "UTF-8",
			"command" : "docker image ls"
		},
		{
			"desc" : "List the images we have pulled",
			"label" : "docker:images:grep_by_name",
			"encoding" : "UTF-8",
			"command" : "docker images ${input:docker_image_name}"
		},
		{
			"desc" : "We can also just pull down images",
			"label" : "docker:pull",
			"encoding" : "UTF-8",
			"command" : "docker pull ${input:docker_image_name}"
		},
		{
			"desc" : "Remove image",
			"label" : "docker:image:remove",
			"encoding" : "UTF-8",
			"command" : "docker image rm ${input:docker_image_name_or_id}"
		},
		// only work in linux/mac
			{
				"desc" : "Stop all running containers, Work in linux",
				"label" : "docker:stop:all",
				"encoding" : "UTF-8",
				"command" : "docker stop $(docker ps -aq)"
			},
			{
				"desc" : "Remove all containers, Work in linux",
				"label" : "docker:container:rm:all",
				"encoding" : "UTF-8",
				"command" : "docker rm $(docker ps -aq)"
			},
			{
				"desc" : "Remove all images, Work in linux",
				"label" : "docker:image:remove:all",
				"encoding" : "UTF-8",
				"command" : "docker rmi $(docker images -a -q)"
			},
		// only work in linux/mac


		// CONTAINER INFO
		{
			"desc" : "Inspect and View info on container",
			"label" : "docker:container:inspect",
			"encoding" : "UTF-8",
			"command" : "docker container inspect ${select:docker_container_name}"
		},
		{
			"desc" : "Specific property (--format)",
			"label" : "docker:container:inspect:format",
			"encoding" : "UTF-8",
			"command" : "docker container inspect --format '{{ .NetworkSettings.IPAddress }}' ${select:docker_container_name}"
		},
		{
			"desc" : "Performance stats (cpu, mem, network, disk, etc)",
			"label" : "docker:container:stats",
			"os_termial" : true,
			"command" : "docker container stats ${select:docker_container_name}"
		},

		// ACCESSING CONTAINERS
		{
			"desc" : "Start container",
			"label" : "docker:container:start",
			"command" : "docker container start ${select:docker_container_name}"
		},
		{
			"desc" : "Access an already created container, start with -ai",
			"label" : "docker:container:start:attach",
			"os_termial" : true,
			"command" : "docker container start -ai ${select:docker_container_name}"
		},
		{
			"desc" : "Restart container",
			"label" : "docker:container:restart",
			"command" : "docker container restart ${select:docker_container_name}"
		},
		{
			"desc" : "Stop container",
			"label" : "docker:container:stop",
			"encoding" : "UTF-8",
			"command" : "docker container stop ${select:docker_container_name}"
		},
		{
			"desc" : "Remove container (Can not remove running containers, must stop first)",
			"label" : "docker:container:rm",
			"encoding" : "UTF-8",
			"command" : "docker container rm ${select:docker_container_name}"
		},
		{
			"desc" : "To remove a running container use force(-f)",
			"label" : "docker:container:rm:force",
			"encoding" : "UTF-8",
			"command" : "docker container rm -f ${select:docker_container_name}"
		},
		{
			"desc" : "attach shell",
			"label" : "docker:container:exec:attach:shell",
			"os_termial" : true,
			"command" : "docker container exec -it ${select:docker_container_name} /bin/sh -c \"[ -e /bin/bash ] && /bin/bash || /bin/sh\""
		},

		{
			"desc" : "Create and run a container in background",
			"label" : "docker:container:create",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d --name ${input:new_docker_container_name} ${input:exist_docker_image}"
		},
		{
			"desc" : "Create container on network",
			"label" : "docker:container:create:include_network",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d --name ${input:docker_container} --network ${input:docker_network_name} ${input:docker_image}"
		},
		{
			// (use sh because it does not include bash)
			// (alpine uses apk for its package manager - can install bash if you want)
			"desc" : "Some docker container example, Alpine is a very small Linux distro good for docker",
			"label" : "docker:container:create:example",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d --name ${input:new_docker_container_name} ${select:docker_image}"
		},
		{
			"desc" : "NGINX container",
			"label" : "docker:container:create:nginx",
			"encoding" : "UTF-8",
			// (-p 80:80 is optional as it runs on 80 by default)
			// -it : Allocate a pseudo-TTY
			// Error starting userland proxy: mkdir /port/tcp:0.0.0.0:9090:tcp:172.17.0.2:80: input/output error.
			// please restart docker
			// http://127.0.0.1:9090
			"command" : "docker container run -it -d -p 9090:80 --name nginx nginx"
		},
		{
			"desc" : "ubuntu container",
			"label" : "docker:container:create:ubuntu",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d --name ubuntu ubuntu"
		},
		{
			"desc" : "Alpine container",
			"label" : "docker:container:create:alpine",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d --name alpine alpine"
		},
		{
			"desc" : "APACHE container",
			"label" : "docker:container:create:apache",
			"encoding" : "UTF-8",
			// http://127.0.0.1:8080
			"command" : "docker container run -it -d -p 8080:80 --name apache httpd"
		},
		{
			"desc" : "MONGODB container",
			"label" : "docker:container:create:mongodb",
			"encoding" : "UTF-8",
			"command" : "docker container run -it -d -p 27017:27017 --name mongo mongo"
		},
		{
			"desc" : "MYSQL container",
			"label" : "docker:example:mysql",
			"encoding" : "UTF-8",
			// docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
			"command" : "docker container run -it -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql"
		},

		// NETWORKING
		{
			"desc" : "Get port",
			"label" : "docker:container:port",
			"encoding" : "UTF-8",
			"command" : "docker container port ${select:docker_container_name}"
		},
		{
			"desc" : "List networks",
			"label" : "docker:network:ls",
			"encoding" : "UTF-8",
			"command" : "docker network ls"
		},
		{
			// "bridge" is default
			"desc" : "Inspect network",
			"label" : "docker:network:inspect",
			"encoding" : "UTF-8",
			"command" : "docker network inspect ${input:docker_network_name}"
		},
		{
			"desc" : "Create network",
			"label" : "docker:network:create",
			"encoding" : "UTF-8",
			"command" : "docker network create ${input:docker_network_name}"
		},
		{
			"desc" : "Connect existing container to network",
			"label" : "docker:network:connect:container",
			"encoding" : "UTF-8",
			"command" : "docker network connect ${input:docker_network_name} ${select:docker_container_name}"
		},
		{
			"desc" : "Disconnect container from network",
			"label" : "docker:network:disconnect:container",
			"encoding" : "UTF-8",
			"command" : "docker network disconnect ${input:docker_network_name} ${select:docker_container_name}"
		},

		// IMAGE TAGGING & PUSHING TO DOCKERHUB

		// tags are labels that point ot an image ID

		{
			"desc" : "Retag existing image",
			"label" : "docker:image:tag:retag",
			"command" : "docker image tag ${input:old_docker_image_name} ${input:new_docker_image_name}"
		},

		{
			"desc" : "Upload to dockerhub",
			"label" : "docker:image:push:to_dockerhub",
			"command" : "docker image push ${input:docker_image_tag}"
		},

		{
			"desc" : "docker login",
			"label" : "docker:login",
			"os_termial" : true,
			"command" : "docker login"
		},
		{
			"desc" : "build image build",
			"label" : "docker:image:build",
			"command" : "docker image build -t ${input:REPONAME} ."
		},
		// VOLUMES
		{
			"desc" : "Check volumes",
			"label" : "docker:volume:ls",
			"encoding" : "UTF-8",
			"command" : "docker volume ls"
		},
		{
			"desc" : "Cleanup unused volumes",
			"label" : "docker:volume:prune",
			"os_termial" : true,
			"command" : "docker volume prune"
		},
		// DOCKER COMPOSE
		{
			"desc" : "run in background",
			"label" : "docker-compose:up:background",
			"encoding" : "UTF-8",
			"command" : "docker-compose up -d"
		},
		{
			"desc" : "run in front",
			"label" : "docker-compose:up",
			"os_termial" : true,
			"command" : "docker-compose up"
		},
		{
			"desc" : "To cleanup",
			"label" : "docker-compose:down",
			"encoding" : "UTF-8",
			"command" : "docker-compose down"
		},

	//////////////////////////Docker Command End/////////////////////////////////


	],
    "custom_env" : {

        "docker_container_name" :[	"nginx", "ubuntu", "alpine", "mongo", "mysql", "apache",
        							// please add your docker container!
        						],
        "docker_image" : [	"nginx", "ubuntu", "alpine", "mongo", "mysql", "apache",],
        "docker_port" : "-p 80:80",
    }
}
```


## Docker base command

### docker:version

docker version

```java
Client: Docker Engine - Community
 Version:           18.09.2
 API version:       1.39
 Go version:        go1.10.8
 Git commit:        6247962
 Built:             Sun Feb 10 04:12:31 2019
 OS/Arch:           windows/amd64
 Experimental:      false
Server: Docker Engine - Community
 Engine:
  Version:          18.09.2
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       6247962
  Built:            Sun Feb 10 04:13:06 2019
  OS/Arch:          linux/amd64
  Experimental:     false
```

### docker image ls

```java
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
alpine                     latest              4d90542f0623        41 hours ago        5.58MB
n-app1                     latest              691ebed3c301        4 weeks ago         1.03GB
mongo                      latest              5976dac61f4f        5 weeks ago         411MB
mongo-express              latest              85c118fcceb3        5 weeks ago         96.9MB
node                       latest              502d06d3bfdf        6 weeks ago         906MB
adminer                    latest              72d8abcace43        3 months ago        83.2MB
mysql                      5.7                 e47e309f72c8        4 months ago        372MB
docker4w/nsenter-dockerd   latest              2f1c802f322f        8 months ago        187kB
```


### docker:container:ls


```java
[2019-06-21 23:05:09][info] docker container ls
[2019-06-21 23:05:09][info] ********************************************************************************
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
328b3bd12a48        mongo               "docker-entrypoint.s…"   4 weeks ago         Up 35 minutes       0.0.0.0:27017->27017/tcp            nodejsapp_mongo_1
b11eb4786e4e        mongo-express       "tini -- /docker-ent…"   4 weeks ago         Up 35 minutes       0.0.0.0:8081->8081/tcp              nodejsapp_mongo-express_1
ffad5a94bb4c        mysql:5.7           "docker-entrypoint.s…"   3 months ago        Up 35 minutes       0.0.0.0:3306->3306/tcp, 33060/tcp   mysql_db_1

```

docker:container:ls:name-only

```java
nginx
n-app1
nodejsapp_mongo_1
nodejsapp_mongo-express_1
mysql_db_1
```

### docker:container:create:nginx

```java

[2019-06-21 23:05:09][info] ********************************************************************************
[2019-06-21 23:05:26][info] docker container run -it -d -p 9090:80 --name nginx nginx
[2019-06-21 23:05:26][info] ********************************************************************************
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
fc7181108d40: Pulling fs layer
c4277fc40ec2: Pulling fs layer
780053e98559: Pulling fs layer
780053e98559: Verifying Checksum
780053e98559: Download complete
c4277fc40ec2: Verifying Checksum
c4277fc40ec2: Download complete
fc7181108d40: Verifying Checksum
fc7181108d40: Download complete
fc7181108d40: Pull complete
c4277fc40ec2: Pull complete
780053e98559: Pull complete
Digest: sha256:bdbf36b7f1f77ffe7bd2a32e59235dff6ecf131e3b6b5b96061c652f30685f3a
Status: Downloaded newer image for nginx:latest
c010a31f462e4259af2b6ad97b270903c8b72324c518e9ccc6b843b2f6df2958

```

### check container and image

`docker container ls` and `docker images nginx`

```java
[2019-06-21 23:06:02][info] ********************************************************************************
[2019-06-21 23:06:10][info] docker container ls
[2019-06-21 23:06:10][info] ********************************************************************************
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
c010a31f462e        nginx               "nginx -g 'daemon of…"   9 seconds ago       Up 8 seconds        0.0.0.0:9090->80/tcp                nginx
328b3bd12a48        mongo               "docker-entrypoint.s…"   4 weeks ago         Up 36 minutes       0.0.0.0:27017->27017/tcp            nodejsapp_mongo_1
b11eb4786e4e        mongo-express       "tini -- /docker-ent…"   4 weeks ago         Up 36 minutes       0.0.0.0:8081->8081/tcp              nodejsapp_mongo-express_1
ffad5a94bb4c        mysql:5.7           "docker-entrypoint.s…"   3 months ago        Up 36 minutes       0.0.0.0:3306->3306/tcp, 33060/tcp   mysql_db_1
[2019-06-21 23:06:29][info] ********************************************************************************
[2019-06-21 23:06:40][info] docker images nginx
[2019-06-21 23:06:40][info] ********************************************************************************
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              719cd2e3ed04        10 days ago         109MB

```

### docker:container:exec:attach:shell

```java
[2019-06-21 23:06:40][info] ********************************************************************************
[2019-06-21 23:06:49][info] docker container exec -it nginx /bin/sh -c "[ -e /bin/bash ] && /bin/bash || /bin/sh"

```