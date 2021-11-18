<h1>Kafka</h1>

<p>Para os testes está sendo usado esse docker-compose:</p>

```
version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - '2181:2181'
  kafka:
    image: wurstmeister/kafka
    container_name: Kafka
    ports:
      - '9092:9092'
    environment:
      KAFKA_ADVERTISED_HOST_NAME: localhost
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9093,OUTSIDE://localhost:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: INSIDE:PLAINTEXT,OUTSIDE:PLAINTEXT
      KAFKA_LISTENERS: INSIDE://0.0.0.0:9093,OUTSIDE://0.0.0.0:9092
      KAFKA_INTER_BROKER_LISTENER_NAME: INSIDE
```

<h3>Acessar o kafka no docker (através de um terminal bash):</h3>
```
- docker-compose exec kafka bash
 - acesse a pasta: cd opt/kafka/bin
```

<h3>Cria tópico:</h3>
```
kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic LOJA_NOVO_PEDIDO
```

<h3>Listar tópicos:</h3>
```
kafka-topics.sh --list --bootstrap-server localhost:9092
```

<h3>Descrever tópicos (ver partições, réplicas, líder, brokers sincronizados)</h3>
```
kafka-topics.sh --describe --bootstrap-server localhost:9092
```

<h3>Enviar mensagem para o tópico:</h3>
```
kafka-console-producer --broker-list localhost:9092 --topic LOJA_NOVO_PEDIDO
```

<h3>Consumir mensagem enviada:</h3>
```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic LOJA_NOVO_PEDIDO --from-beginning
```

<h3>Alterar partições em um tópico</h3>

```
kafka-topics.sh --alter --zookeeper localhost:2181 --topic ECOMMERCE_NEW_ORDER --partitions 3
```

