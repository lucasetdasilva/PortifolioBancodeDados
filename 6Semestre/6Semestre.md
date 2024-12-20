## SPC Grafeno
### 6° Semestre • 2024-2
<p>Parceiro Acadêmico: <a href="https://spcgrafeno.com.br/">SPC Grafeno</a></p>
<p align = "center"><img src= "Images/spc.jpeg" width="350" height="200"></p>
<p>A solução proposta consiste em uma aplicação web que realiza a análise de duplicatas dos clientes da SPC Grafeno. A partir da identificação dessas duplicatas, foi desenvolvida uma Inteligência Artificial capaz de entender os comportamentos dos clientes, considerando aspectos como recorrência, frequência e valor das duplicatas geradas. Com os resultados fornecidos pela IA, a SPC Grafeno poderá adotar as estratégias mais eficazes para cada cliente.</p>
<br>

## Tecnologias Utilizadas
* __Python:__ Linguagem de programação backend;
* __JavaScript:__ Linguagem de programação backend e frontend;
* __Vue:__ Framework, da linguagem JavaScript, progressivo para construção de interfaces de usuário, que facilita a criação de aplicações web interativas e dinâmicas com uma abordagem reativa;
* __HTML:__ É a linguagem de marcação padrão usada para estruturar e apresentar conteúdo na web;
* __CSS:__ Liguagem de estilização da aplicação web;
* __Mongo DB:__ Banco de dados NoSQL, orientado a documentos, que armazena dados em formato JSON flexível, permitindo alta escalabilidade e desempenho em ambientes de grandes volumes de dados;
* __PostgreSQL:__ Banco de dados relacional de código aberto, altamente confiável e extensível, que suporta SQL avançado e recursos como transações ACID e tipos de dados personalizados.
<br><br>

## Contribuições Pessoais
### Exportação de dados do usuário
<p>Para assegurar o cumprimento da Lei Geral de Proteção de Dados (LGPD), foi implementada na aplicação a funcionalidade de exportação dos dados dos usuários. Essa funcionalidade garante que os usuários possam acessar seus dados pessoais a qualquer momento. Além disso, caso haja inconsistências ou não conformidades, o usuário tem a possibilidade de realizar as correções necessárias, proporcionando maior transparência e controle sobre suas informações.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Foi realizada a criação de uma API View chamada ExportCSVAPIView, que tem como objetivo gerar e fornecer um arquivo CSV com os dados de um membro do sistema. A classe utiliza a permissão AllowAny, permitindo o acesso sem restrições. Quando uma requisição GET é feita, o código tenta obter o id_user (identificador do usuário) a partir dos parâmetros da URL. Primeiro, ele valida se o id_user é um ObjectId válido. Se não for, retorna um erro 400 (requisição inválida). Caso o ID seja válido, tenta localizar o membro correspondente no banco de dados usando esse ID. Se o membro não for encontrado, retorna um erro 404 (não encontrado), e se houver qualquer outro erro, é retornado um erro 500 (erro interno).</p>
  
<p>Após encontrar o membro, o código serializa os dados desse usuário usando o MemberSerializer, que converte o objeto em um formato de dicionário. Em seguida, um arquivo CSV é gerado com esses dados. A resposta HTTP é configurada para ser um arquivo de texto no formato CSV, e o cabeçalho do arquivo inclui o nome do usuário e as chaves do dicionário como nomes das colunas. As informações do membro são então escritas no CSV como valores nas linhas abaixo do cabeçalho. Finalmente, o arquivo CSV é retornado como resposta para que o usuário possa baixá-lo.</p> 
<br>

<p>Abaixo é apresentado a  API View que exporta os dados em formato CSV:</p>

``` python
class ExportCSVAPIView(APIView):
    permission_classes = [AllowAny]  # Defina as permissões conforme necessário
    def get(self, request, *args, **kwargs):
        id_user = kwargs.get('_id')
        # Verifica se id_user é um ObjectId válido
        if not ObjectId.is_valid(id_user):
            return Response({"detail": "ID inválido."}, status=status.HTTP_400_BAD_REQUEST)
        try:
            # Usa o ObjectId para buscar o membro
            member = Member.objects.get(_id=ObjectId(id_user))
        except Member.DoesNotExist:
            return Response({"detail": "Usuário não encontrado!"}, status=status.HTTP_404_NOT_FOUND)
        except Exception as e:
            return Response({"detail": f"Erro interno: {str(e)}"}, status=status.HTTP_500_INTERNAL_SERVER_ERROR)
        # Converte o objeto em dicionário
        serializer = MemberSerializer(member)
        data = serializer.data
        # Cria uma resposta HTTP com o CSV
        response = HttpResponse(content_type='text/csv')
        response['Content-Disposition'] = f'attachment; filename="{id_user}_data.csv"'
        # Cria um escritor CSV
        writer = csv.writer(response)
        # Escreve o cabeçalho (nomes das colunas)
        writer.writerow(data.keys())
        # Escreve os dados do membro
        writer.writerow(data.values())
        return response

``` 
</details>
<br>

### Criação de modelo de Inteligência Artificial (Modelo de Regressão)
<p>Como parte dos requisitos obrigatórios do projeto, foi necessário desenvolver um modelo de Inteligência Artificial. A equipe decidiu testar diferentes modelos para identificar qual se adequaria melhor à aplicação. Para isso, foi criado um modelo de IA de regressão, com o objetivo de prever a quantidade de notas canceladas nos meses futuros.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Durante a análise da base de dados fornecida pela SPC Grafeno, identificou-se a possibilidade de criar uma Inteligência Artificial baseada nas colunas de criação de nota fiscal (created_at) e estado da nota fiscal (state). O objetivo principal do modelo desenvolvido foi prever a quantidade de notas fiscais canceladas nos meses futuros. Para isso, realizou-se inicialmente o tratamento dos dados, que incluiu a remoção de valores nulos e a conversão dos tipos de dados, garantindo a integridade e consistência da base. Em seguida, a base foi dividida em dois subconjuntos: 80% dos dados foram reservados para o treinamento e 20% para o teste.</p>
<p>O modelo escolhido foi uma Árvore Aleatória de Regressão (Random Forest Regressor), que foi treinado utilizando os dados preparados. Após o treinamento, o modelo foi empregado para prever os cancelamentos de notas fiscais nos meses futuros, utilizando o conjunto de teste como referência. A avaliação do modelo foi realizada por meio de métricas como Acurácia e o Erro Absoluto Percentual Médio (MAPE), que forneceram uma análise detalhada do desempenho da solução.</p>
<br>

<p>Abaixo é mostrado a criação do modelo de Inteligência Artificial de Regressão:</p>

``` python
# Seleção das variáveis preditoras e variável alvo
X = monthly_cancellations[['mes_x','ano_x'] + [col for col in monthly_cancellations.columns if col.startswith('state_')]]
y = monthly_cancellations['total_canceladas']

# Divisão dos dados em conjuntos de treino e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Criação e treinamento do modelo de Floresta Aleatória de Regressão
model = RandomForestRegressor(n_estimators=100, random_state=42)
model.fit(X_train, y_train)
```
  
</details>
<br>

### Criação de Servidor
<p>Após a criação da Inteligência Artificial de Agrupamento, foi necessária a construção de um servidor para integrar os resultados gerados pelo modelo com o sistema da SPC Grafeno. Este servidor converte os resultados da IA em formato JSON, permitindo sua transmissão para o backend, que, por sua vez, os encaminha ao frontend. Com a conclusão do servidor, a SPC Grafeno terá acesso à exibição dos resultados provenientes da IA diretamente na interface do sistema. Esses resultados permitirão identificar os clientes agrupados em clusters e, assim, realizar os descontos apropriados de forma mais estratégica e eficiente.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>O modelo de IA utilizado na aplicação é baseado em agrupamento, no qual os clientes da SPC Grafeno são organizados em quatro clusters. Cada cluster é definido por características específicas, como Recência, Frequência e Valor das duplicatas criadas pelos clientes. Os resultados gerados pela IA são armazenados em uma tabela. No entanto, para que o backend possa transmitir esses dados ao frontend, foi necessário desenvolver um servidor utilizando o framework Flask. O servidor foi projetado para disponibilizar os resultados da IA em formato JSON por meio de requisições do tipo GET.</p>
<p>A comunicação do servidor é configurada para operar na porta 5000, garantindo a integração eficiente entre as diferentes camadas da aplicação e permitindo a visualização dos resultados no frontend.</p>
<br>

<p>Abaixo é mostrado o código-fonte para a criação do servidor:</p>

``` python
from flask import Flask, jsonify
from kmeans import df_rfm_clip_scaled  # Importando o resultado da IA 

app = Flask(__name__)

@app.route('/api/clustering', methods=['GET'])
def get_clustering_results():
    try:
        results = df_rfm_clip_scaled.copy()
        results['participant_id'] = df_rfm_clip_scaled.index
        return jsonify(results.to_dict(orient='records'))  # Retorna os dados como JSON
    except Exception as e:
        return jsonify({"error": str(e)}), 500
    
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)  # O servidor roda na porta 5000
```

</details>
<br>

<br>

### Pré processamento dos dados para utilização na IA de Regressão
<p>Uma etapa crucial no desenvolvimento de uma Inteligência Artificial é o pré-processamento dos dados do dataset. Essa etapa envolve a limpeza e a transformação dos dados, garantindo que estejam consistentes, livres de ruídos e prontos para análise. Sem esse processo, os resultados da IA podem não condizer com a realidade, comprometendo a precisão e a utilidade das previsões ou análises.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
<p>Após a definição clara da problemática que a Inteligência Artificial deve resolver, foi realizado o pré-processamento dos dados do dataset, uma etapa essencial para garantir a precisão e confiabilidade nos resultados previstos pela IA. Durante esse processo, diversos tratamentos foram aplicados para preparar os dados adequadamente. A conversão dos tipos de dados das colunas foi realizada para assegurar que cada dado fosse interpretado corretamente pelo modelo. Além disso, os dados foram agrupados por mês para calcular a quantidade de duplicatas canceladas mensalmente, proporcionando uma análise temporal dos padrões de cancelamento.</p>
<p>Também foi aplicada a técnica de One-Hot Encoding na coluna state, transformando a variável categórica em variáveis binárias e facilitando a integração dessas informações no modelo de IA. Esses tratamentos foram fundamentais para preparar os dados e permitir a construção de um modelo mais robusto e preciso.</p> 
<br>

<p>Abaixo é mostrado um exemplo de pré processamento de dados:</p>

``` python
data['created_at'] = pd.to_datetime(data['created_at'])

# Filtrar as notas canceladas usando a coluna 'state'
data['canceladas'] = data['state'].apply(lambda x: 1 if x == 'canceled' else 0)

# Aplicar One-Hot Encoding na coluna 'state' no dataframe original
estado_dummies = pd.get_dummies(data['state'], prefix='state')
data = pd.concat([data, estado_dummies], axis=1)

# Extração do mês e ano da data de criação
data['mes'] = data['created_at'].dt.month
data['ano'] = data['created_at'].dt.year

# Agrupar os dados por mês para obter a quantidade de notas canceladas mensalmente
data.set_index('created_at', inplace=True)
monthly_cancellations = data.resample('ME')['canceladas'].sum().reset_index(name='total_canceladas')

# Extrair características do mês e ano para a previsão
monthly_cancellations['mes'] = monthly_cancellations['created_at'].dt.month
monthly_cancellations['ano'] = monthly_cancellations['created_at'].dt.year

# Agrupar por mês e somar os valores das dummies de estado
monthly_data = data.resample('M').sum(numeric_only=True).reset_index()

# Merge de `monthly_cancellations` com `monthly_data` para incluir `total_canceladas`
monthly_cancellations = pd.merge(monthly_cancellations, monthly_data, on='created_at', how='left')
```
  
</details>
<br>

<hr></hr>
<br><br>

## Aprendizados
<p>Durante o desenvolvimento do projeto, tive a oportunidade de aprender e praticar diversos conceitos de Inteligência Artificial, como o tratamento de dados e a criação de um modelo de Regressão utilizando o algoritmo de Floresta Aleatória. Além disso, adquiri conhecimento e experiência na implementação do conceito de exportação de dados do usuário, em conformidade com a Lei Geral de Proteção de Dados (LGPD), utilizando o framework Django. De forma geral, consegui assimilar a maior parte do conteúdo abordado em sala de aula e aplicá-lo de maneira prática ao longo do desenvolvimento do projeto, consolidando tanto meu aprendizado quanto minhas habilidades técnicas. </p>

<h3 align = "center">Hard Skills</h3>

<table align="center">
    <tr>
      <th width="300px">Tecnologia/Metodologia</th>
      <th width="300px">Classificação</th>
    </tr>
    <tr>
      <td>Árvore Aleatória de Regressão (Python)</td>
      <td>Sei fazer com Ajuda</td>
    </tr>
    <tr>
      <td>Framework Flask</td>
      <td>Sei fazer com Ajuda</td>
    </tr>
    <tr>
      <td>Criação de Endpoint (Framework Django)</td>
      <td>Sei fazer com Ajuda</td>
    </tr>
    <tr>
      <td>Pré processamento de dados para utilização em IA</td>
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
      <td>Resolução de Problemas</td>
      <td>Precisei identificar, analisar e encontrar soluções para os problemas encontrados durante o desenvolvimento das minhas tarefas</td>
    </tr>
    <tr>
      <td>Comunicação Assertiva</td>
      <td>Precisei me comunicar de forma clara e exata, para que eu e meus colegas tivéssemos trocas de conhecimento eficientes</td>
    </tr>
    <tr>
      <td>Aprendizagem Contínua</td>
      <td>Precisei me aprofundar em conceitos que não tinha familiaridade</td>
    </tr>
    <tr>
      <td>Adaptabilidade</td>
      <td>Precisei me adaptar as tecnologias de IA para concluir as minhas tarefas</td>
    </tr>
</table>

## Outros projetos:

#### 1° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/1Semestre/1Semestre.md">Mó Viagem</a>
#### 2° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/2Semestre/2Semestre.md">PRO4Jobs</a>
#### 3° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/3Semestre/3Semestre.md">Sistema Gerenciador de Vendas</a>
#### 4° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/4Semestre/4Semestre.md">Predial</a>
#### 5° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/5Semestre/5Semestre.md">Tecsus</a>
