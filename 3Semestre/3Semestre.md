### Sistema Gerenciador de Vendas

##### 3° Semestre • 2023-1

<p>Parceiro Acadêmico: <a href="https://fatecsjc-prd.azurewebsites.net/">Dom Rock</a></p>
<br>
<img src= "3Semestre/domrock.png" width="800" height="130">
<br><br>

<p>O Sistema Gerenciador de Vendas é uma aplicação web voltada para o armazenamento e gerenciamento de vendas realizadas por vendedores. O intuito da aplicação é coletar os dados das vendas e transformar em valor de negócio por meio da geração de insights (gráficos), com isso deixando mais fácil de entender o que realmente está acontecendo com os dados.</p>
<p>O sistema também dispõe de um algoritmo que prevê quanto um vendedor precisa vender com base na quantidade planejada de vendas e o que realmente foi realizado.</p>

## Tecnologias Utilizadas

* __JavaScript:__ Linguagem de programação frontend;
* __React:__ Framework do JavaScript;
* __Java:__ Linguagem de programação backend;
* __SpringBoot:__ Framework do Java para o mapeamento de tabelas do banco de dados;
* __MySQL:__ SGBD utilizado para o armazenamento de dados;
* __TypeScript:__ Framework do JavaScript; 
* __Tailwind CSS:__ Linguagem de estilização da aplicação web.
<br><br>  

## Contribuições Pessoais

### Mapeamento de Tabelas
<p>Para que a linguagem de programação Java possa interpretar as informações armazenadas dentro de um Banco de Dados foi necessário realizar o mapeamento das tabelas da aplicação.</p>

<details>
<summary><h4>Mais detalhes</h4></summary>
<p> O mapeamento de tabelas é um conceito em que associamos classes Java a tabelas de um banco de dados relacional. O mesmo tem como objetivo trazer visibilidade dos dados armazenados dentro do banco de dados para o usuário final da aplicação, com o intuito de realizar consultas, atualizações, criações ou deleções (CRUD). O mapeamento utiliza uma especificação do Java chamada JPA(Java Persistence API) que tem como função persistir os dados na aplicação, para utilizá-la precisamos criar anotações. A linguagem back-end Java transforma tabelas em classes por meio da anotação "@entity" e "@Table(name = "nome_da_tabela_no_banco_de_dados")". </p>
 <p>Para transformar colunas do banco de dados em atributos do Java, precisamos utilizar a anotação "@Column(name = "nome_da_coluna_no_banco_de_dados)", também podemos utilizar a anotação "@Id" que serve para declarar a chave primária de uma tabela. Outra anotação muito importante é a "@GeneratedValue(strategy = GenerationType.IDENTITY)", ela deve ser utilizada quando a chave primária é auto incrementada, ou seja, quando criamos um registro a chave primária é preenchida automaticamente.</p>
 
<p>Abaixo é mostrado um exemplo de mapameamento da tabela de Produto:</p>

 ```java
package com.main.api.model;

import java.util.List;

import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.OneToMany;
import jakarta.persistence.Table;
import lombok.Getter;
import lombok.Setter;
@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})
@Entity
@Getter
@Setter
@Table(name = "produto")
public class Produto {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	@Column(name= "id")
	private Long id;
	
	@Column(name = "nome")
	private String nome;
	
	@Column(name = "valor")
	private double valor;
	
	@OneToMany(mappedBy = "fk_sku_venda")
	private List<Venda> vendas;
	
}
```
</details>
<br>

### Criação de rotas REST
<p>A arquitetura REST é um estilo arquitetural que fornece diretrizes para o design e interação de sistemas distribuídos na web.</p>

<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Em uma arquitetura REST, os recursos, que podem ser objetos, serviços ou conceitos, são identificados por URIs (Uniform Resource Identifiers). As operações sobre esses recursos são realizadas por meio dos métodos HTTP padrão, como GET para recuperar informações, POST para criar novos recursos, PUT para atualizar recursos existentes e DELETE para removê-los.</p>
<p>A arquiteura REST foi de extrema importância no projeto, pois com ela podemos fazer a conexão entre o back-end e o front-end da aplicação web. Em outras palavras, significa que o back-end puxa as informações do banco de dados, processa as informações e em seguida transfere essas informações para o front-end, onde o usuário da aplicação pode executar ações que podem modificar, criar, deletar ou apenas visualizar estes dados, respeitando o privilégio de cada usuário no sistema.</p>

<p> Abaixo é mostrado um exemplo de uma rota REST que mostra todos os produtos:</p>

 ```java
@GetMapping("/list")
	public List<Produto> findAll() {
		return produtoRepository.findAll();
	}
```
</details>
<br>

### Modelagem do Banco de Dados
<p>Todo sistema por mais simples que aparenta ser, necessita de um banco de dados para que as informações relevantes que percorrem a aplicação não sejam perdidas.</p>

<details>
 <summary><h4>Mais detalhes</h4></summary>
<p> A primeira etapa que precisei realizar foi o Modelo de Entidade Reacional, ou DER, que tem como objetivo mostrar como deve ser o fluxo de dados dentro do banco de dados. Foi necessário fazer um levantamento de entidades, atributos e quais entidades possuem relacionamentos, levando em consideração o contexto do projeto. Depois de levantar esses quesitos é necessário estudar a cardinalidade entre as entidades, pois com base nela surgirão chaves estrangeiras e tabelas de relação no Modelo de Entidade Relacional.
</p>
<p>Após a finalição do DER se faz necessário a criação do Modelo de Entidade Relacional, ou MER, que tem como objetivo criar tabelas e seus relacionamentos como base no modelo conceitual feito anteriormente. Sendo assim, as entidades se tornam tabelas e os atributos viram campos. Com base na cardinalidade das tabelas é necessário criar novas tabelas e criar chaves estrangeiras, isso ajuda o banco a manter sua consistência e diminuir redundâncias.
</p> 
<br>
 
<p>Abaixo é mostrado o Diagrama de Entidade Relacional da aplicação:</p>
<br>
<p align="center"> <img src= "3Semestre/der.png" width="450" height="300"></p>
</details>
<br>

### Atualização Planejamento de Vendas

<p>Quando um vendedor acessa a aplicação, uma das funções que ele pode realizar é o planejamento de suas vendas. Essa função se faz necessária para o entendimento das vendas de um determinado vendedor, pois o mesmo poderá compreender se está lucrando mais ou menos durante um determinado período de tempo. </p>

<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Uma das principais responsabilidades que um vendedor tem durante sua jornada na aplicação é o planejamento de vendas. Na aplicação um vendedor pode cadastrar um planejamento de suas vendas, ou seja, quanto ele acha que irá vender em um período de três meses para frente. Para realizar o cadastro é preciso ter mapeado as tabelas relacionadas as vendas, depois disso é necessário a construção da classe Controller (rotas REST) e a interface Repository (Queries). Na classe Controller deve ser criado um método de cadastro do planejamento de vendas. Por meio da URL passada pelo método é possível obter as informações e gravá-las dentro do banco de dados. Para que isso se concretize é necessário também utilizar a anotação "@PostMapping" responsável por cadastrar objetos no banco de dados. </p>
<p>Para cada mês que passar o vendedor terá que atualizar o planejamento, adicionando o que realmente foi vendido em um determinado mês. Para isso deve ser criado na classe Controller um método de atualização, por meio da anotação "@PutMapping". Com o cadastro e a atualização do planejamento de vendas de um determinado vendedor, é gerado um dashboard em que é mostrado três linhas: um para o planejamento de vendas, um para o que realmente foi vendido e uma para a predição. Com este dashboard o vendedor poderá entender em qual situação ele se encontra e conseguirá tomar as melhores decisões para o seu negócio.</p>

<p>Abaixo é mostrado a implementação do método de atualização do planejamento de vendas:</p>

 ```java
@PutMapping("/update/{vendaId}")
	public ResponseEntity<String> atualizarVenda(@PathVariable Long vendaId,
			@RequestParam double first_real_qtd,
			@RequestParam double second_real_qtd,
			@RequestParam double third_real_qtd) {

		Optional<Venda> vendaOptional = vendaRepository.findById(vendaId);

		if (vendaOptional.isPresent()) {
			Venda vendaEncontrada = vendaOptional.get();
			vendaEncontrada.setFirst_real_qtd(first_real_qtd);
			vendaEncontrada.setSecond_real_qtd(second_real_qtd);
			vendaEncontrada.setThird_real_qtd(third_real_qtd);

			vendaRepository.save(vendaEncontrada);

			return ResponseEntity.ok("Venda atualizada com sucesso!");
		} else {
			return ResponseEntity.notFound().build();
		}
	}

```
</details>

<hr></hr>

## Aprendizados 

<p>Como Scrum Master da minha equipe pude entender como deve ser realizado a organização de uma equipe, sempre conversando com os demais membros para entender suas necessidades em relação ao desenvolvimento do projeto, ou seja, tive que observar se as tarefas estavam sendo realizadas como o esperado, se os membros da equipe estavam com impedimentos externos ou internos e como poderia amenizar a situação. Ser Scrum Master mostrou para mim que a comunicação é a chave para se construir confiança uns com os outros, pois o ponto que todos estão em sincronia o projeto e consequentemente o produto final teram uma qualidade superior ao esperado pelo cliente.</p>
<p>Como desenvolvedor pude aprimorar meus conhecimentos em modelagem de dados, além de estudar e aplicar os conhecimentos que adquiri com o framework SpringBoot, para o desenvolvimento do back-end da aplicação.</p> 

### - Hard Skills:
* Criação de rota REST (método PUT)
* Desenvolvimento Back-end utilizando o framework SpringBoot, pertencente a linguagem Java
* Modelagem de Banco de Dados

### - Soft Skills:
* Comunicação
* Organização
* Inteligência Emocional
<hr></hr>
<br>
