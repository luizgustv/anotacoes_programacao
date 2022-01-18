<h1>Clean Architecture</h1>

<p>Premissas:</p>

<ul>
<li>Independência de Framework</li>
<li>Testabilidade</li>
<li>Indenpendência de Interface do Usuário</li>
<li>Indenpendência de banco de dados</li>
<li>Indenpendência de agentes externos</li>
</ul>

<p>As quatro camadas:</p>

<ul>
<li>Entities - nessa camada deve conter o que é pertinente ao sistema em relação a lógica de negócios sendo o mais genérico possível, para que possa ser utilizado por outras camadas. Se encontram aqui os modelos de objeto;</li>
<li>Use Cases - nessa camada ocorre toda a orquestração de dados. Redireciona os dados da aplicação para a regra de negocios para realizar validações, persistência de dados entre outras funções. Deve possui a menor quantidade de dependências externas;</li>
<li>Interface Adapters - responsável por realizar a comunicação entre as entidades e os componentes mais externos da aplicação. É nela que também convertermos os dados vindos de uma camada mais interna, para a mais externa e vice versa. São considerados compoenentes de interface adapter: Controllers, Presenters e Gateways;</li>
<li>Frameworks - geralmente composta de estruturas e ferramentas de banco de dados, web, interface do usuário, etc.</li>
</ul>

<p>Dependency Rule - as camadas externas podem aceessar as mais internas, porém o contrário não existe</p>

<h3>Referências:</h3>
<p><a href="https://www.objective.com.br/insights/clean-architecture-com-mvvm/">Clean Architecture com MVVM: o que é, vantagens e como utilizar em aplicações Android</a></p>

<p><a href="https://balta.io/artigos/clean-code#o-que-%C3%A9-o-clean-code">O que é clean code</a></p>


