### 로컬용 도커 네트워크 생성

```shell
 docker network create p-ser-network
```

### zookeeper 컨테이너 실행

```shell
 docker run -p 2181:2181 -e ALLOW_ANONYMOUS_LOGIN=yes --network p-ser-network --name zookeeper bitnami/zookeeper:3.9
```

### kafka 컨테이너 실행

```shell
 docker run -p 9092:9092 -e ALLOW_ANONYMOUS_LOGIN=yes -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_CFG_BROKER_ID=0 -e KAFKA_ZOOKEEPER_PROTOCOL=PLAINTEXT -e KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=EXTERNAL:PLAINTEXT,PLAINTEXT:PLAINTEXT -e KAFKA_CFG_LISTENERS=PLAINTEXT://:29092,EXTERNAL://:9092 -e KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://kafka:29092,EXTERNAL://localhost:9092 --network p-ser-network --name kafka bitnami/kafka:3.4
```

### redis 컨테이너 실행

```shell
 docker run -p 6379:6379 --network p-ser-network --name redis redis --requirepass 1234
```

### k8s

```shell
 kubectl apply -k ./k8s
```
