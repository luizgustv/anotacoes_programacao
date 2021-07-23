<h1>Docker - anotações gerais</h1>

<h3>Comandos:</h3>

<h4>Docker:</h4>

<p>docker pull [image] &#8594; baixar uma imagem a partir dos registros do Docker Hub;</p>

<p>docker images &#8594; visualizar as imagens que você já baixou anteriormente;</p>

<p>docker run [image] &#8594; startar um container de acordo com a imagem desejada;</p>

<p>docker run -p[host post]:[container port] &#8594; permite configurar uma porta para se conectar diretamente ao container (ex: docker run -p8080:80)</p>

<p>docker stop [container name] &#8594; para o container;</p>

<p>docker ps &#8594; mostra os container que estão rodando no momento. Adicionando o prefixo <b>-a</b> (docker ps -a) é possível ver os container que já foram criados;</p>

<p>docker logs [container name or id] &#8594; permite ver os logs gerados pelo serviço </p>

<p>Alguns prefixos:</p>
<ul>
<li>-d, --detach &#8594; starta o container em background e print o id do container </li>
<li>-p, --publish list  &#8594; permite conectar a porta do container com a porta do host</li>
<li> --name &#8594; permite dar um nome ao container </li>
</ul>

<p>exemplo de uso:</p>
```
docker run -p6000:6379 --name redis -d redis
```

<p>docker network &#8594; rede interna do docker que ao criar, permite que containers conectados a ela se comuniquem apenas utilizando o id/nome do container (não necessitando especificar, endereço ip, porta...)
</p>

<ul>
<li>docker network ls &#8594; lista as redes disponíveis</li>
<li>docker network create mongo-network &#8594; cria um docker network
</li>
</ul>

<p>exemplo de uso:</p>

```
Rodando o mongo db:
docker run -p 27017:27017 -d \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=root \
--name mongodb  \
--net mongo-network \
mongo

Rodando mongo express:
docker run -d \
-p 8080:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=root \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express

ambos estão na mesma rede (mongo-network)
```

<h4>Docker Compose: </h4>
<p>Também é possível estruturar os serviços que se deseja utilizar com o docker e executa-los sob um único comando. É o chamado Docker Compose, que nada mais é que um "orquestrador" de container de Dockers. Esse regimento é feito através de um arquivo chamado docker-compose (ou o nome que preferir) que está no formato YAML.
</p>

docker-compose &#8594; permite orquestrar um conjunto de containers

<ul>
<li>-f &#8594; especificar arquivo docker-compose</li>
<li>up &#8594; startar todos os serviços que estão no arquivo</li>
<li>down &#8594; encerra todos os serviços e remove os containers, networks utilizados</li>
</ul>

<p>Exemplo de um arquivo docker-compose:</p>
```
# Versão do docker-compose
version: '3'
# Serviços a serem containerzados
services:
  # Nome do serviço
  mongodb:
    image: mongo
    # Reiniciar o serviço caso esse deslige por alguma razão
    restart: always
    # HOST:CONTAINER
    ports:
      - 27017:27017
    # Variáveis utilizadas pelo serviço
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
    # mongo-express não será inicializado até o serviço mongodb inicializar
    depends_on:
      - mongodb
```

<h4>Dockerfile</h4>

<p>Além de utilizar imagens de terceiros, podemos também criar nossa própria imagem (de uma aplicação em java, por exemplo). Um dockerfile nada mais é do que um arquivo que descreve as etapas que o Docker precisa para gerar uma imagem, o que inclui a instalação de pacotes, criação de diretórios, definição de variáveis de ambiente, entre outras coisas.</p>

<p>Abaixo temos uma tabela, onde

Image Enviroment Blueprint  | Dockerfile
---|---
start the app with: "node server.js"| CMD ["node","server.js"]
set MONGO_DB_USERNAME=admin set MONGO_DB_USERNAME =password | ENV MONGO_DB_USERNAME=admin \ MONGO_DB_USERNAME =password
install node  | FROM node
create home/app folder| RUN mkdir -p /home/app
copy curent folder files to /home/app| COPY . /home/app

Para gerar uma imagem, utilizamos o seguinte o comando:

```
docker build . -t [imagem]:[tag] -f /d/Programacao/anotacoes_programacao/docker/arquivos/Dockerfile
```

<p>Exemplo de imagem gerada pelo comando acima:</p>

```
#baixa a dependência node, que é a base para conseguir rodar a aplicação
FROM node:13-alpine

#setando as variáveis de ambiente
ENV ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    ME_CONFIG_MONGODB_ADMINPASSWORD=password

#criando um novo diretório
RUN mkdir -p /home/app

#copiando todos os arquivos de onde o arquivo Dockerfile está para o diretório recém criado
COPY . /home/app

# define o diretório padrão em que irão ocorrer os próximos comandos (nesse caso pro /home/app)
WORKDIR /home/app

RUN npm install

CMD ["node", "server.js"]
```

<ul>
<li>-t &#8594; define nome e opcionalmente uma combinação de nome:tag para a imagem. No exemplo, defimos um nome para a imagem e a versão da mesma</li>
<li>:version &#8594; define a versão da imagem</li>
<li> . &#8594; o "dot" denota a localização dockerfile</li>
</ul>

<p>para startar a imagem: </p>
```
docker run [imagem]
```

<p>Com o container em funcionando, podemos acessar a interface bash de um container</p>

```
comando no windows CMD:
  docker exec -it f5f11a9f7ccd /bin/sh

comando no bash:
  docker exec -it f5f11a9f7ccd //bin/sh
```

<p>Agora que conseguimos rodar a aplicação a partir de sua imagem docker, o proxímo passo poderia ser adicionar suas configurações em um docker compose e roda-los junstamente com os serviços necessários. Um problema comum é conectar os endpoints entre serviços. Por exemplo, digamos que precisamos conectar a aplicação a um banco de dados. O endpoint da aplicação foi declarado no application.properties:</p>

```
aws:
  endpoint: "${AWS_ENDPOINT:http://localhost:8000}"
```
<p>O endpoint é uma variável externa ou http://localhost:8000 . Porém se utilizamos a segunda opção não obteremos sucesso.</p>

```
 poc-micronaut:
    image: poc_micronaut_service:1.0
    environment:
      - AWS_ENDPOINT=http://localhost:8000
```

<p>Isso porque no docker intenamente o valor endpoint do banco de dados é diferente do que foi preenchido.</p>

```
Exemplo do endpoint interno
Server Running: http://15c9d8622494:80
```

<p>Para corrigir essa opção algumas opções:</p>

```
Declarar como host.docker.internal:
- AWS_ENDPOINT=http://host.docker.internal:8000
ou
Declarar o nome do serviço conforme foi declarado no docker-compose:
- AWS_ENDPOINT=http://dynamodb:8000
```

<h4>Docker Volumes</h4>
<p>Em muitos casos queremos manter as informações obtidas em um banco de dados que é inicializado pelo docker, porém quando o container é parado e reiniciado os dados são apagados. Para evitar que isso ocorra, podemos criar volumes e armazenas as informações geradas pelo container.</p>

<p>Podemos fazer tanto através do domando docker run -v, como definindo por docker-compose:</p>

```
#lista de volumes que serão usados pelo docker-compose
volumes:
  mongo-data:
    #o volume será criado em uma partição do sistema que foi startado o serviço
    driver: local

#declarar uso do volume em um serviço:

#Nome do serviço
mongodb:
  image: mongo
  # Reiniciar o serviço caso esse deslige por alguma razão
  restart: always
  # HOST:CONTAINER
  ports:
  - 27017:27017
  # Variáveis utilizadas pelo serviço
  environment:
    - MONGO_INITDB_ROOT_USERNAME=admin
    - MONGO_INITDB_ROOT_PASSWORD=password
  volumes:
  #host volume name / caminho dentro do container (/data/db é o caminho padrão do mongodb para arzenar os dados salvos)
  - mongo-data:/data/db
```

<h3>Referências utilizadas:</h3>

<ul>
<li> <a href="https://www.youtube.com/watch?v=3c-iBn73dDE">Docker Tutorial for Beginners [FULL COURSE in 3 Hours]</a></li>
<li><a href="https://betterprogramming.pub/how-does-docker-port-binding-work-b089f23ca4c8">Docker bind port</a></li>
<li><a href="https://hub.docker.com/">Docker Hub (para baixar imagems)</a></li>
<li><a href="http://www.macoratti.net/19/02/dock_imgfile1.htm">Docker - Criando uma imagem com Dockerfile</a></li>
</ul>