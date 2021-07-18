# Docker Cheatsheet
Location of docker installation:  
`/var/lib/docker`
## Getting Started
```
docker run
    CMD sleep 5 #Overrides CLI
    ENTRYPOINT ['sleep'] #Appends subsequent
--entrypoint NEW_CMD
--mount type=bind,source=HOST,target=CONTAINER
```

## Networking
```
docker network create

docker network
```
## Building Images
```
docker build .
-t LOCAL:NAME   #Tagging images
```

## Managing images
```
docker image pull       #Pull an image from docker repo
docker image push       #Push an image to docker repo

docker image inspect    #Look at the details of the dockerimage
docker image list       #List all image in this system

docker image import     #Build a system image from tarball
docker build            #Build a system image from dockerfile

docker image save       #Export an image to tar
docker load             #Load an image from tar
docker prune            #Remove all unused image
```

## Managing containers
```
docker container create IMAGE   #Create container from image

docker container start
    -p HOST:CONTAINER       #Port forwarding
    -v HOST:CONTAINER       #Volume mapping
    -e ENV_VAR=FOO          #Environment Variable
    --restart {no,on-failure,always,unless-stoped}

docker container stop

docker container list       #Show running container
docker container list -a    #Show all container

docker container inspect CONTAINER
docker container logs CONTAINER
docker container cp LOCAL:CONTAINER

docker container exec -it CONTAINER CMDS
```

## Frequently Used Docker Images

### MySQL: https://hub.docker.com/_/mysql
```
docker run --name my-mysql -d \
    -e MYSQL_ROOT_PASSWORD=$PASSWORD \
    -p 3306:3306 \
    -v $HOST_FOLDER:/var/lib/mysql \
    -v /my/custom:/etc/mysql/conf.d \
    --character-set-server=utf8mb4 \
    --collation-server=utf8mb4_unicode_ci \
mysql:latest
```

### PostgreSQL: https://hub.docker.com/_/postgres
```
docker run --name my-postgres -d \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v /custom/mount:/var/lib/postgresql/data \
    -p 5432:5432 \
postgres:latest
```

### MongoDB: https://hub.docker.com/_/mongo
```
docker run --name my-mongo -d \
    -e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
    -e MONGO_INITDB_ROOT_PASSWORD=secret \
    -v /my/own/datadir:/data/db \
    -p 27017:27017 \
mongo:latest
```

### Redis: https://hub.docker.com/_/redis
```
docker run --name my-redis -d \
    -p 6379:6379 \
    -v /myredis/conf/redis.conf:/usr/local/etc/redis/redis.conf \
redis:latest
```
