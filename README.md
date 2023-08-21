# Local Docker DB Cheatsheet

- [MySQL](#mysql)
- [Redis](#redis)
- [PostgreSQL](#postgresql)
- [MongoDB](#mongodb)
- [DynamoDB](#dynamodb)


## MySQL

### MySQL 5.7

Start a detached server at host port 3306

```
docker run --name=mysql57 -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 -d mysql/mysql-server:5.7
```

For M1 Macs

```
docker run --platform linux/amd64 --name=mysql57 -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 -d mysql/mysql-server:5.7
```

Connect to docker container

```
docker exec -it mysql57 mysql -p
```

Create superuser

```
create user looi@'%' identified by 'password';
grant all on *.* to looi@'%';
flush privileges;
```

### MySQL 8.0

Start a detached server at host port 3307

`docker run --name=mysql80 -e MYSQL_ROOT_PASSWORD=password -p 3307:3306 -d mysql/mysql-server:8.0 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci`

Connect to docker container

`docker exec -it mysql80 mysql -p`

Create superuser

```
create user looi@'%' identified by 'password';
grant all on *.* to looi@'%';
flush privileges;
```

## Redis

### Redis 5.0

Start a detached redis server at host port 6379

`docker run --name=redis1 -p 6379:6379 -d redis:5.0`

### RedisInsight

Start a detached redis insight server at host port 8001

`docker run -d --name=redisinsight -v redisinsight:/db -p 8001:8001 redislabs/redisinsight:latest`

## PostgreSQL

### PostgreSQL 12.7

Start a detached server at host port 5432

`docker run --name postgres12 -e POSTGRES_PASSWORD=password -d -p 5432:5432 postgres:12.7`

Connect to the container

`docker exec -it postgres12 psql --username postgres --password`

Connect as default user

`psql --host=127.0.0.1 --username=postgres --password`

Create superuser

`create user looi with superuser password 'password';`

## MongoDB

### MongoDB 6.0

Start a detached server at host port 27017

`docker run -d --name mongodb1 -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo:6.0`

## DynamoDB

Start a detached dynamodb-local server at port 8000

`docker run -d --name=dynamodb1 -p 8000:8000 amazon/dynamodb-local:latest`

# Selenium

## Selenium Chrome

Start a remote standalone selenium chrome

`docker run --name selenium1 -d -p 4444:4444 -p 7900:7900 --shm-size="2g" selenium/standalone-chrome:96.0`
