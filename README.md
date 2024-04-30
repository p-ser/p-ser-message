### 로컬용 도커 네트워크 생성

```shell
 docker network create kafka-network
```

### zookeeper 컨테이너 실행

```shell
 docker run -p 2181:2181 --network p-ser-network --name zookeeper digitalwonderland/zookeeper
```

### kafka 컨테이너 실행

```shell
 docker run -p 9092:9092 -e KAFKA_ADVERTISED_HOST_NAME=localhost -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --network p-ser-network --name kafka wurstmeister/kafka
```

### redis 컨테이너 실행

```shell
 docker run -p 6379:6379 --network p-ser-network --name redis redis
```

### k8s

```shell
 kubectl apply -k ./k8s
```
