## create a docker network

`$ docker network create todo-net`

## build images for todo-mysql and todo-server

`$ docker build -t todo-mysql:1.0 -f Docker/Dockerfile.msql .`
`$ docker build -t todo-server:1.0 -f Docker/Dockerfile.node .`

## running mysql container

```
$  docker run --network todo-net --name todo-mysql -v /mysql_server_data:/var/lib/mysql -p 3306:3306 -d todo-mysql:1.0

```

## running server container

```
$ docker run --network todo-net --name todo-server -v ${PWD}:/app -v /app/node_modules -p 3000:3000 todo-server:1.0
```

### running proxy container

```
$ docker run --network todo-net --name todo-proxy -it -p 80:80 todo-proxy:1.0

```

<!--
/////////////////////////////////////////////////

Environments for the server node
PORT=3000
SQLITE_DB_LOCATION='todo.db'
MYSQL_HOST='todo-mysql'
MYSQL_USER='todo'
MYSQL_PASSWORD='todo1234'
MYSQL_DB='tododb'
NODE_ENV='prod' ## use 'test' form sqlite database

//////////////////////////////////////////////////
-->
