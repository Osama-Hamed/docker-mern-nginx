# Dockerized MERN App

Dockerized mern app using docker and docker compose

## Run the app using docker

### Create a network

```bash
docker network create mern-net
```

### Run mongodb container

```bash
cd mern-app

docker run --name mongodb-con \
 --net mern-net \
 --env-file ./env/mongo.env \
 -v data:/data/db \
 --rm \
 -d \
 mongo
```

### Build the server image

```bash
cd server

docker build -t server-img ./
```

### Run the server container

```bash
docker run --name server-con \
 --net mern-net \
 --env-file ../env/server.env \
 -v "$(pwd):/app" \
 -v /app/node_modules \
 -v logs:/app/logs \
 --rm \
 server-img
```

### Build the client image

```bash
cd client

docker build -t client-img ./
```

### Run the client container

```bash
docker run --name client-con \
 --net mern-net \
 -v "$(pwd)/src:/app/src" \
 --rm \
 -it \
 client-img
```

### Build nginx image

```bash
cd nginx

docker build -t nginx-img ./
```

### Run nginx container

```bash
docker run --name nginx-con \
 --net mern-net \
 -p 5000:80 \
 --rm \
 nginx-img
```

## Run the app using docker compose

### Build the images and start the containers

```bash
docker-compose up --build
```

### Stop the containers

```bash
docker-compose down
```
