<h1>Docker</h1>

<h3>Comandos:</h3>

<p>docker pull [image] &#8594; baixar uma imagem a partir dos registros do Docker Hub;</p>

<p>docker images &#8594; visualizar as imagens que você já baixou anteriormente;</p>

<p>docker run [image] &#8594; startar um container de acordo com a imagem desejada;</p>

<p>docker run -p[host post]:[container port] &#8594; permite configurar uma porta para se conectar diretamente ao container (ex: docker run -p8080:80)</p>

<p>docker stop [container name] &#8594; para o container;</p>

<p>docker ps &#8594; mostra os container que estão rodando no momento. Adicionando o prefixo <b>-a</b> (docker ps -a) é possível ver os container que já foram criados;</p>

<p>docker logs [container name or id] &#8594; permtie ver os logs gerados pelo serviço </p>

<p>Alguns prefixos:</p>
<ul>
<li>-d, --detach &#8594; starta o container em background e print o id do container </li>
<li>-p, --publish list  &#8594; permite conectar a porta do container com a porta do host</li>
<li> --name &#8594; permite dar um nome ao container </li>
</ul>


<h3>Referências utilizadas:</h3>

<ul>
<li> <a href="https://www.youtube.com/watch?v=3c-iBn73dDE">Docker Tutorial for Beginners [FULL COURSE in 3 Hours]</a></li>
<li><a href="https://betterprogramming.pub/how-does-docker-port-binding-work-b089f23ca4c8">Docker bind port</a></li>

</ul>

1:10:07