### 로컬용 도커 네트워크 생성

```shell
 docker network create p-ser-network
```

### zookeeper 컨테이너 실행

```shell
 docker run -p 2181:2181 -e ZOOKEEPER_CLIENT_PORT=2181 --network p-ser-network --name zookeeper confluentinc/cp-zookeeper:7.0.1
```

### kafka 컨테이너 실행

```shell
 docker run -p 9092:9092 -e KAFKA_INTER_BROKER_LISTENER_NAME=INTERNAL -e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=INTERNAL:PLAINTEXT,EXTERNAL:PLAINTEXT -e KAFKA_ADVERTISED_LISTENERS=INTERNAL://kafka:29092,EXTERNAL://localhost:9092 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --network p-ser-network --name kafka confluentinc/cp-kafka:7.0.1
```

### redis 컨테이너 실행

```shell
 docker run -p 6379:6379 --network p-ser-network --name redis redis --requirepass 1234
```

### k8s

```shell
 kubectl apply -k ./k8s
```
