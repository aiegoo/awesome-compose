## Compose sample application

### Use with Docker Development Environments

You can open this sample in the Dev Environments feature of Docker Desktop version 4.12 or later.

[Open in Docker Dev Environments <img src="../open_in_new.svg" alt="Open in Docker Dev Environments" align="top"/>](https://open.docker.com/dashboard/dev-envs?url=https://github.com/docker/awesome-compose/tree/master/nginx-flask-mongo)

### Python/Flask application with Nginx proxy and a Mongo database

Project structure:
```
.
├── compose.yaml
├── flask
│   ├── Dockerfile
│   ├── requirements.txt
│   └── server.py
└── nginx
    └── nginx.conf

```

[_compose.yaml_](compose.yaml)
```
services:
  web:
    build: app
    ports:
    - 80:80
  backend:
    build: flask
    ...
  mongo:
    image: mongo
```
The compose file defines an application with three services `web`, `backend` and `db`.
When deploying the application, docker compose maps port 80 of the web service container to port 80 of the host as specified in the file.
Make sure port 80 on the host is not being used by another container, otherwise the port should be changed.

## Deploy with docker compose

```
$ docker compose up -d
Creating network "nginx-flask-mongo_default" with the default driver
Pulling mongo (mongo:)...
latest: Pulling from library/mongo
423ae2b273f4: Pull complete
...
...
Status: Downloaded newer image for nginx:latest
Creating nginx-flask-mongo_mongo_1 ... done
Creating nginx-flask-mongo_backend_1 ... done
Creating nginx-flask-mongo_web_1     ... done

```

## Expected result

Listing containers must show three containers running and the port mapping as below:
```
$ docker ps
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                  NAMES
a0f4ebe686ff        nginx                       "/bin/bash -c 'envsu…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp     nginx-flask-mongo_web_1
dba87a080821        nginx-flask-mongo_backend   "./server.py"            About a minute ago   Up About a minute                          nginx-flask-mongo_backend_1
d7eea5481c77        mongo                       "docker-entrypoint.s…"   About a minute ago   Up About a minute   27017/tcp              nginx-flask-mongo_mongo_1
```

After the application starts, navigate to `http://localhost:80` in your web browser or run:
```
$ curl localhost:80
Hello from the MongoDB client!
```

Stop and remove the containers
```
$ docker compose down
```

## sample exec cli
>Container ID: f05504ed8149 (llmware)

```bash
docker exec -it f05504ed8149 /bin/bash
# Sample command
echo "Hello from llmware container"
```

> Container ID: 42c5aa9fb058 (milvus)

```bash
docker exec -it 42c5aa9fb058 /bin/bash
# Sample command
echo "Hello from milvus container"


```
Container ID: eb7e4e96894a (milvus-etcd)
```bash
docker exec -it eb7e4e96894a /bin/sh
# Sample command
echo "Hello from milvus-etcd container"


```
Container ID: 64b84ceab0bf (devneo4j)
```bash
docker exec -it 64b84ceab0bf /bin/bash
# Sample command
echo "Hello from devneo4j container


```
Container ID: b6a38a425970 (mongodb)
```bash
docker exec -it b6a38a425970 /bin/bash
# Sample command
echo "Hello from mongodb container"


```
Container ID: 82ec18db5c59 (milvus-minio)
```bash
docker exec -it 82ec18db5c59 /bin/sh
# Sample command
echo "Hello from milvus-minio container"


```

```bash


```

```bash


```
To explore the details and configurations of each container, you will need to access the container's shell and navigate or inspect relevant files or settings. Here's a more detailed approach for each container listed:

### Detailed Instructions for Each Container

#### Container ID: `f05504ed8149` (llmware)

1. **Access the shell:**
    ```bash
    docker exec -it f05504ed8149 /bin/bash
    ```

2. **Run some example commands:**
    - Check running processes:
        ```bash
        ps aux
        ```
    - List directory contents:
        ```bash
        ls -la
        ```
    - View environment variables:
        ```bash
        printenv
        ```

#### Container ID: `42c5aa9fb058` (milvus)

1. **Access the shell:**
    ```bash
    docker exec -it 42c5aa9fb058 /bin/bash
    ```

2. **Run some example commands:**
    - Check Milvus configuration:
        ```bash
        cat /etc/milvus/config.yaml
        ```
    - Check logs:
        ```bash
        tail -f /var/log/milvus/milvus.log
        ```

#### Container ID: `eb7e4e96894a` (milvus-etcd)

1. **Access the shell:**
    ```bash
    docker exec -it eb7e4e96894a /bin/sh
    ```

2. **Run some example commands:**
    - View etcd settings:
        ```bash
        etcdctl get / --prefix --keys-only
        ```
    - Check etcd health:
        ```bash
        etcdctl endpoint health
        ```

#### Container ID: `64b84ceab0bf` (devneo4j)

1. **Access the shell:**
    ```bash
    docker exec -it 64b84ceab0bf /bin/bash
    ```

2. **Run some example commands:**
    - Check Neo4j configuration:
        ```bash
        cat /var/lib/neo4j/conf/neo4j.conf
        ```
    - Check Neo4j logs:
        ```bash
        tail -f /var/log/neo4j/neo4j.log
        ```

#### Container ID: `b6a38a425970` (mongodb)

1. **Access the shell:**
    ```bash
    docker exec -it b6a38a425970 /bin/bash
    ```

2. **Run some example commands:**
    - Access MongoDB shell:
        ```bash
        mongo
        ```
    - Check MongoDB logs:
        ```bash
        tail -f /var/log/mongodb/mongod.log
        ```
    - View MongoDB configuration:
        ```bash
        cat /etc/mongod.conf
        ```

#### Container ID: `82ec18db5c59` (milvus-minio)

1. **Access the shell:**
    ```bash
    docker exec -it 82ec18db5c59 /bin/sh
    ```

2. **Run some example commands:**
    - Check MinIO configuration (usually MinIO runs with environment variables):
        ```bash
        printenv | grep MINIO_
        ```
    - List MinIO server files:
        ```bash
        mc ls myminio/
        ```
    - Check MinIO logs:
        ```bash
        cat /root/.minio.log
        ```

### General Steps for Each Container
1. **Access the container shell using `docker exec -it <container_id> /bin/bash` or `/bin/sh`.**
2. **Navigate the filesystem to relevant configuration or log files.**
3. **Use CLI tools available in the container to inspect or manage the service.**

### Example for NGINX (General Approach)
If you had an NGINX container, the steps would be:
1. **Access the shell:**
    ```bash
    docker exec -it <nginx_container_id> /bin/bash
    ```

2. **Inspect NGINX configuration:**
    ```bash
    cat /etc/nginx/nginx.conf
    ```

3. **Check running NGINX processes:**
    ```bash
    ps aux | grep nginx
    ```

4. **Inspect NGINX logs:**
    ```bash
    tail -f /var/log/nginx/access.log
    tail -f /var/log/nginx/error.log
    ```

These commands and steps will help you explore the configurations and settings of each container. Adjust the file paths and commands according to the specific services and configurations of your containers.
