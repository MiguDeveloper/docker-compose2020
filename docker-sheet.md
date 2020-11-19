### config-server

```shell
./mvnw clean package
.\mvnw clean package

docker build -t config-server:v1 .
docker network create redspringclod
docker run -p 8888:8888 --name config-server --network redspringcloud config-server:v1
```

### servicio-eureka-server

```shell
./mvnw clean package
docker build -t servicio-eureka-server:v1 .
docker run -p 8761:8761 --name servicio-eureka-server --network redspringcloud servicio-eureka-server:v1
```

### mysql

```shell
docker pull mysql:8
docker run -p 3306:3306 --name microservicios-mysql8 --network redspringcloud -e MYSQL_ROOT_PASSWORD=sasa -e MYSQL_DATABASE=db_springboot_cloud -d mysql:8 --default-authentication-plugin=mysql_native_password
docker logs -f microservicios-mysql8
```

### postgresql

```shell
docker pull postgres:12-alpine
docker run -p 5432:5432 --name microservicios-postgres12 --network springcloud -e POSTGRES_PASSWORD=sasa -e POSTGRES_DB=db_springboot_cloud -d postgres:12-alpine
docker logs -f microservicios-postgres12
```

### servicio-productos

```shell
./mvnw clean package -DskipTests
docker build -t servicio-productos:v1 .
docker run -P --network redspringcloud servicio-productos:v1
```

### servicio-zuul-server

```shell
./mvnw clean package -DskipTests
docker build -t servicio-zuul-server:v1 .
docker run -p 8090:8090 --network redspringcloud servicio-zuul-server:v1
```

### servicio-usuarios

```shell
./mvnw clean package -DskipTests
docker build -t servicio-usuarios:v1 .
docker run -P --network redspringcloud servicio-usuarios:v1
```

### servicio-oauth

```shell
./mvnw clean package -DskipTests
docker build -t servicio-oauth:v1 .
docker run -p 9100:9100 --network redspringcloud servicio-oauth:v1
```

### servicio-item

```shell
./mvnw clean package -DskipTest
docker build -t servicio-item:v1
docker run -p 8002:8002 -p 8005:8005 -p 8007:8007 --network redspringcloud servicio-item:v1
```

### rabbitmq

```shell
docker pull rabbitmq:3.8-management-alpine
docker run -p 15672:15672 -p 5672:5672 --name microservicios-rabbitmq38 --network redspringcloud -d rabbitmq:3.8-management-alpine

docker logs -f microservicios-rabbitmq38
```

### zipkin (crear carpeta con Dockerfile adjunto con el Jar)

```shell
docker build -t zipkin-server:v1
docker run -p 9411:9411 --name zipkin-server --network redspringcloud -e RABBIT_ADDRESSES=microservicios-rabbitmq38:5672 -e STORAGE_TYPE=mysql -e MYSQL_USER=zipkin -e MYSQL_PASS=zipkin -e MYSQL_HOST=microservicios-mysql8 zipkin-server:v1
```

### Comandos docker basicos

```shell
# detener y eliminar todos los contenedores
docker stop $(docker ps -q)
docker rm $(docker ps -aq)

# eliminar imagenes
docker rmi $(docker images -aq)
```
