<h1>Kafka</h1>


<p>Para os testes está sendo usado esse docker-compose:</p>

<img src="arquivos\docker-compose.png">

<h3>Cria tópico:</h3>

<p>kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic LOJA_NOVO_PEDIDO</p>

<h3>Listar tópicos:</h3>
<p>kafka-topics --list --bootstrap-server localhost:9092</p>

<h3>Enviar mensagem para o tópico:</h3>
<p>kafka-console-producer --broker-list localhost:9092 --topic LOJA_NOVO_PEDIDO</p>

<h3>Consumir mensagem enviada:</h3>
<p>kafka-console-consumer --bootstrap-server localhost:9092 --topic LOJA_NOVO_PEDIDO --from-beginning</p>

