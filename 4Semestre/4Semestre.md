## 4° Semestre • 2023-2
### Predial
<p>Parceiro Acadêmico: <a href="https://www.jaia.software/">Jaia Software</a></p>
<p align = "center"><img src= "Images/jaia.png" width="380" height="220"></p>

<p>O projeto envolve desenvolver uma aplicação web voltada para o gerenciamento de inspeções prediais, onde o cliente faz um pedido de inspeção, e a empresa cria uma ordem de serviço com base nessa solicitação. Na plataforma, o inspetor poderá registrar de forma detalhada suas observações sobre o ambiente do cliente, gerando um documento final com essas informações. Além disso, o administrador terá a capacidade de criar checklists específicos para diferentes departamentos, além de gerenciar funcionários e departamentos, realizando operações como cadastro, exclusão, visualização e edição.</p>

## Tecnologias Utilizadas

* __Java:__ Linguagem de programação backend;
* __JavaScript:__ Linguagem de programação backend e frontend;
* __Vue:__ Framework, da linguagem JavaScript, progressivo para construção de interfaces de usuário, que facilita a criação de aplicações web interativas e dinâmicas com uma abordagem reativa;
* __HTML:__ É a linguagem de marcação padrão usada para estruturar e apresentar conteúdo na web;
* __CSS:__ Liguagem de estilização da aplicação web;
* __Oracle:__ Sistema Gerenciador de Banco de Dados utilizado para armazenar as informações da aplicação web.
<br><br>

## Contribuições Pessoais
### Cadastro de requisições dos clientes
<p>Quando um cliente deseja solicitar uma inspeção predial em seu ambiente corporativo, com foco no bem-estar dos colaboradores, ele pode utilizar a aplicação web para abrir uma nova requisição. Nessa etapa, o cliente especificará o que precisa ser inspecionado. Após o cadastro, a requisição é enviada à empresa responsável pela inspeção, que analisará os detalhes e, com base nisso, criará uma Ordem de Serviço (OS). </p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>A requisição dos clientes aborda muitas camadas a serem desenvolvidas. Entre essas camadas se encontra o framework Vue (frontend), utilizado para a criação de 	interfaces de usuário. Para que este framework funcione de maneira correta, ele deve apresentar e exibir as informações que estão armazenadas no banco de dados ao 	usuário. Isso só é possível pois o Vue utiliza caminhos para se comunicar com o backend da aplicação, que consegue acessar o banco de dados e obter ou exibir os 	dados necessários na tela do usuário. Para a criação das requisições dos clientes, deve-se primeiro criar um formulário para o preenchimento das informações por 	parte do cliente. Feito isso, foi necessário criar variavéis no Vue para armazenar essas informações.</p> 
<p>Por último, foi criada uma função assícrona que obtém as informações de um determinado usuário, utilizando o método "get", em seguida foi realizado o método 	"post", para enviar o cadastro de requisição para o backend, que depois passará a informação ao banco de dados. Com base na resposta do método "get", foi possível 	obter o campo "Id" do cliente. Sem este campo não seria possível o cadastro da requisição, pois é necessário a informação de quem a solicitou, para que o 		administrador do sistema consiga criar a Ordem de Serviço.</p>
 <p>Abaixo é mostrado a transferência de dados de requisições do cliente do Vue para o Java:</p>

 ```javascript
  		async function createRequisition(){
  		  cliente.value = (await axios.get("http://localhost:8080/cliente/" + cnpjValue.value)).data;
                  await axios.post("http://localhost:8080/requisicao/"+ cliente.value.id,
                                    {
                                      nome:nameValue.value,
                                      inspecao:inspectionValue.value,
                                      descricao:describeValue.value,
                                      status:statusReqValue.value,
                                      data_abertura: dateValue.value
                                     }).then(response => {
                                       console.log(response)
                                     })
                }
```
</details>
<br>

### Atualização de funcionários
<p>Um método de atualização de dados de funcionários permite que administradores modifiquem informações desatualizadas ou incorretas, como nome e email. Esse método geralmente envolve a criação de um endpoint que recebe os dados atualizados e, a partir de uma consulta ao banco de dados, altera as informações do funcionário. Esse processo facilita a manutenção de dados precisos, garantindo que o sistema esteja sempre atualizado e ajudando na gestão eficiente dos colaboradores.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Para que seja realizada a alteração dos dados de um determinado cliente, é necessário encontrar o registro do mesmo e por fim realizar as alterações desejadas. A linguagem backend (Java) deve obter estas informações dentro do banco de dados. Quando uma solicitação de atualização vem para o sistema, por meio de um endpoint HTTP PUT para a URL "/atualizar/{cpf}", o método "atualizarFuncionario" é acionado. Ele recebe o CPF do funcionário na URL (@PathVariable) e os novos dados do funcionário no corpo da requisição (@RequestBody). O método chama o serviço "funcionarioService.atualizarFuncionario(cpf,novoFuncionario)" para processar e atualizar o funcionário. Se a atualização for bem-sucedida, o método retorna o objeto Funcionario atualizado com status 200 (OK). Caso o funcionário não seja encontrado, retorna status 404 (Not Found).</p>	

<p>Abaixo é mostrado o método de atualização de um funcionário:</p>
 
```java
@PutMapping("/atualizar/{cpf}")
    public ResponseEntity<Funcionario> atualizarFuncionario(
        @PathVariable Integer cpf, 
        @RequestBody Funcionario novoFuncionario
    ) {
        Funcionario funcionarioAtualizado = funcionarioService.atualizarFuncionario(cpf, novoFuncionario);
        
        if (funcionarioAtualizado != null) {
            return ResponseEntity.ok(funcionarioAtualizado);
        } else {
            return ResponseEntity.notFound().build();
        }
    }
```
 
</details>
<br>

### Listagem de funcionários
<p>Um método de visualização de dados de funcionários permite que administradores acessem informações atualizadas sobre os colaboradores, como nome e email. Geralmente, esse método envolve a criação de um endpoint que consulta o banco de dados e apresenta os dados de forma estruturada. Pode incluir filtros para facilitar a busca por informações específicas, ajudando na gestão eficiente dos funcionários e na tomada de decisões.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>O endpoint mapeado pela anotação @GetMapping("/listarporcpf/{cpf}") expõe uma rota HTTP GET que recebe um parâmetro dinâmico, o CPF, diretamente na URL. O {cpf} é uma variável de caminho (path variable) que o Spring Boot automaticamente captura e passa como argumento para o método do controlador. No caso do projeto desenvolvido, a variável cpf é do tipo Integer.</p>
<p>O método buscarFuncionarioPorCpf chama o serviço funcionarioService.buscarPorCpf(cpf), que é responsável por buscar no banco de dados um funcionário cujo CPF corresponda ao valor passado. Se o funcionário for encontrado, o método retorna um ResponseEntity com status HTTP 200 (OK) e o objeto Funcionario no corpo da resposta. O Spring converte automaticamente esse objeto em formato JSON, que é o formato esperado em APIs RESTful.</p>

<p>Abaixo é mostrado o método de visualização de um funcionário:</p>
 
```java
@GetMapping("/listarporcpf/{cpf}")
    public ResponseEntity<Funcionario> buscarFuncionarioPorCpf(@PathVariable Integer cpf) {
        Funcionario funcionario = funcionarioService.buscarPorCpf(cpf);
        return ResponseEntity.ok(funcionario);
    }
```
</details>
<br>

### Deleção de funcionário
<p>A deleção de um funcionário é o processo de remover permanentemente os dados de um funcionário do sistema, geralmente a partir de um identificador único, como o CPF. Esse processo envolve a exclusão dos registros relacionados ao funcionário no banco de dados, tornando esses dados inacessíveis para futuras operações ou consultas.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>O endpoint HTTP DELETE /deletar/{cpf} tem como objetivo permitir que o sistema exclua um funcionário utilizando o CPF como identificador único. Quando um cliente faz uma requisição DELETE para esse endpoint, o Spring Boot mapeia o CPF da URL para o método do controlador. O CPF é passado como parâmetro para o serviço funcionarioService, que contém a lógica de negócios para deletar o funcionário no banco de dados. Esse tipo de operação de deleção é crucial para manter a integridade e a precisão dos dados no sistema, especialmente em sistemas que precisam de manutenção contínua e atualizações regulares de registros. Além disso, deve-se tomar cuidado para garantir que apenas usuários autorizados, administradores, tenham permissão para realizar exclusões de dados, para evitar problemas de segurança.</p>

<p>Abaixo é mostrado um método de exclusão de um funcionário:</p>

```java
 @DeleteMapping("/deletar/{cpf}")
    public void deletarFuncionario(@PathVariable Integer cpf){
        funcionarioService.deletarFuncionario(cpf);
    }
```
</details>
<hr></hr>

## Aprendizados
<p>Como desenvolvedor pude continuar a aperfeiçoar meus conhecimentos em relação a modelagem e estruturação de bancos de dados, além de compreender melhor como funciona o mapeamento de tabelas, utilizando a linguagem Java. Também pude realizar a construção de casos de testes para verficar e validar se a aplicação estava se comportando de maneira esperada com base nos requisitos do sistema, assim garantindo a qualidade ao cliente. </p>

<h3 align = "center">Hard Skills</h3>

<table align="center">
    <tr>
      <th width="300px">Tecnologia/Metodologia</th>
      <th width="300px">Classificação</th>
    </tr>
    <tr>
      <td>Mapeamento de tabelas (Spring Boot)</td>
      <td>Sei fazer com Ajuda</td>
    </tr>
    <tr>
      <td>Modelagem de Banco de Dados</td>
      <td>Sei fazer com Autonomia</td>
    </tr>
    <tr>
      <td>Criação de rotas REST</td>
      <td>Sei fazer com Ajuda</td>
    </tr>
    <tr>
      <td>Criação de cadastro de requisição</td>
      <td>Sei fazer com Autonomia</td>
    </tr>
</table>

<h3 align = "center">Soft Skills</h3>

<table align="center">
    <tr>
      <th width="300px">Habilidade</th>
      <th width="300px">Descrição</th>
    </tr>
    <tr>
      <td>Planejamento</td>
      <td>Precisei planejar minhas atividades para entregá-las no prazo</td>
    </tr>
    <tr>
      <td>Aprendizagem contínua</td>
      <td>Precisei aprender a implementar o mapeamento de tabelas na linguagem Java</td>
    </tr>
    <tr>
      <td>Trabalho em equipe</td>
      <td>Precisei estar constantemente em contato com meus colegas para entender o que cada um estava fazendo</td>
    </tr>
    <tr>
      <td>Inteligência Emocional</td>
      <td>Precisei controlar minhas emoções para que não interferissem no meu desempenho</td>
    </tr>
</table>

<hr></hr>
<br>

## Outros projetos:

#### 1° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/1Semestre/1Semestre.md">Mó Viagem</a>
#### 2° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/2Semestre/2Semestre.md">PRO4Jobs</a>
#### 3° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/3Semestre/3Semestre.md">Sistema Gerenciador de Vendas</a>
#### 5° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/5Semestre/5Semestre.md">Tecsus</a>
#### 6° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/6Semestre/6Semestre.md">SPC Grafeno</a>
