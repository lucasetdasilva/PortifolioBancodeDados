# Portifólio das API's - Lucas Emanoel
<p>O portfólio tem como objetivo documentar todos os API's (Aprendizagem por Projeto Integrado) para fins educacionais, além de servir como trabalho de graduação para a obtenção do diploma de tecnólogo em Banco de Dados proposto pela Faculdade de Tecnologia de São José dos Campos.</p>
<hr></hr>

## Sumário
[Sobre mim](#sobre-mim)

<hr></hr>

## Sobre mim
<p align="center"><img src= "Images/fotominha.png" width="420" height="300"></p>

<p>Me chamo Lucas Emanoel Teixeira Engracio da Silva, tenho 20 anos. Sou técnico em Desenvolvimento de Sistemas pela Etec Profa.
Ilza Nascimento Pintusa - SJC e atualmente estou matriculado no 6° Semestre do curso tecnólogo em Banco de Dados na FATEC de 
São José dos Campos.</p>

<p>Possuo um grande conhecimento na área da tecnologia da informação, já tendo aprendido a construir softwares desktop, aplicações mobile, sistemas embarcados e aplicações web. Porém a minha maior paixão é na área de dados, construindo, manipulando e gerenciando um banco de dados.</p>

<p>Atualmente sou Analista de Testes na empresa Saipher ATC, que tem como ramo de atuação a construção de softwares para auxiliar no trabalho do trafégo aéreo dos aeródromos brasileiros.</p> 

<p align="center"> • <a href="https://www.linkedin.com/in/lucas-emanoel-teixeira-engracio-da-silva-ab5611234/">Linkedin</a> • <a href="https://github.com/lucasetdasilva">Github</a> • </p>

<br>
<hr></hr>

## Meus Projetos
### Mó Viagem
##### 1° Semestre • 2022-1
<p>Parceiro Acadêmico: <a href="https://fatecsjc-prd.azurewebsites.net/">Faculdade de Tecnologia de São José dos Campos</a></p>
<p align = "center"><img src= "Images/logo.png" width="300" height="300"></p>
<p>A aplicação Mó Viagem é uma assistente virtual de viagens, que tem como objetivo auxiliar o planejamento de viagens futuras. O usuário pode pedir informações, pontos turísticos, curiosidades e deixar registrado quais os próximos destinos ele quer conhecer entre outras funcionalidades. É possível também perguntar a previsão do tempo para cada destino.</p>

## Tecnologias Utilizadas

* __Python:__ Linguagem de programação backend;
* __SpeechRecognition:__ Tecnologia que permite um dispositivo ou sistema reconhecer e interpretar a fala humana;
* __PyAudio:__ Biblioteca do Python que fornece uma interface para trabalhar com aúdio;
* __API OpenWeather:__ Interface de programação de aplicativos fornecida pela OpenWeather, que permite acesssar dados metereológicos em tempo real e previsões do tempo para qualquer lugar do mundo;
* __Pandas:__ Biblioteca do Python para análise e manipulação de dados;
* __Wikipédia:__ Biblioteca do Python que permite pesquisar e recuperar conteúdo da Wikipédia;
* __Requests:__ Biblioteca do Python para fazer requisições HTTP de forma simplificada;
* __Translator:__ Biblioteca que traduz textos para diferentes idiomas;
* __Holidays:__ Biblioteca que fornece informações sobre feriados em diversos países;
* __Re:__ Biblioteca do Python que permite pesquisar e manipular texto usando expressões regulares;
* __Webbrowser:__ Biblioteca do Python que permite abrir de maneira fácil URLs em navegadores da web padrão do sistema;
* __Pyttsx3__: Biblioteca do Python que fornece uma interface para síntese de voz.
<br><br>  

## Contribuições Pessoais 
### Transformação de texto para voz
<p>Para permitir a comunicação por voz com o usuário, a aplicação deve ser capaz de transformar texto em voz usando tecnologias específicas. Isso implica a integração de sistemas de síntese de voz que convertem o texto fornecido pela aplicação em uma saída de áudio natural e compreensível.
Essas tecnologias facilitam a interação entre o usuário e a aplicação, permitindo que o usuário ouça informações, respostas e instruções fornecidas pela aplicação de forma clara e concisa. Essa capacidade de comunicação por voz torna a interação com a aplicação mais intuitiva e acessível, além de oferecer uma experiência mais envolvente e dinâmica para o usuário.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p> Como a aplicação se trata de uma assistente virtual, se espera que a mesma se comunique com o usuário por meio de voz, para que o usuário tenha uma experiência lúdica e de fácil compreensão. Por meio da biblioteca Pyttsx3 do Python, é possível tranformar textos em voz. Sua lógica é bem simples, deve ser iniciado o mecanismo de síntese de voz, depois deve ser passado o texto que deve ser tranformado em voz e por fim o programa aguarda até que todo o texto tenha sido falado antes de prossegir.</p>
  <p>Abaixo é mostrado uma aplicação simples de como funciona a tranformação de texto para voz:</p>
  
  ```python
  def convertFala(texto):
  engine = pyttsx3.init()
  engine.say(texto)
  engine.runAndWait()
  ```
</details>
<br>

### Leitura de arquivo Excel
<p>A assistente virtual oferece uma funcionalidade de busca de agências de viagem por categorias, visando facilitar a escolha e compra de pacotes turísticos. Com base em suas preferências, como gastronomia, opções para toda a família, ecoturismo ou parques temáticos, a assistente apresenta uma seleção de agências relevantes.
Cada opção inclui o nome da agência, um breve descritivo sobre seus serviços e uma ligação direta para acessar a página inicial da agência, onde você pode explorar mais detalhes e planejar sua viagem com facilidade.
Essa função visa proporcionar uma experiência mais personalizada e conveniente, ajudando o usuário a encontrar agências que correspondam aos seus interesses específicos e tornando o processo de reserva de viagens mais intuitivo e agradável.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para que seja possível mostrar as agências para o usuário, é preciso criar um arquivo no Excel para armazenar estes dados. O Python possui uma biblioteca chamada Pandas, em que é possível realizar a manipulação, leitura e análise de dados, sendo uma ferramenta poderosa. A aplicação utiliza esta ferramenta para ler um arquivo Excel que possui 
  informações de agências de viagem de diferentes categorias e exibe para o usuário.</p>
  <p>Abaixo é mostrado um exemplo que foi utilizado a leitura de um arquivo Excel:</p>
  
```python
  elif "pesquisar agências" in texto:
      convertFala("Qual tipo de viagem você prefere")
      print("1- Ecoturismo")
      print("2- Para toda família")
      print("3- Gastronômico")
      print("4- Parques temáticos")

      col_names =['gastronomico', 'descricaog', 'urlg', 'aventura', 'descricaoa', 'urla', 'familia', 'descricaof', 'urlf', 'parque', 'descricaop', 'urlp']
      tabela = pd.read_excel('api.xlsx', names = col_names)

      rec = sr.Recognizer()

      with sr.Microphone() as mic:
          print("Escolha um para prosseguir")
          rec.adjust_for_ambient_noise(mic)
          audio = rec.listen(mic)
      opcao = rec.recognize_google(audio, language="pt-BR")

      if "ecoturismo" in opcao:
          convertFala("Essas são as opções de viagens de Ecoturismo")
          eco = tabela['aventura'][:]
          print(eco)
          print("\n")
          convertFala("Caso tenha se interessado em alguma agência, clique no link para ser redirecionado para o site")
          eco2 = tabela['urla'][:]
          print(eco2)

          convertFala("Quer ver a descrição das agências")

          rec = sr.Recognizer()

          with sr.Microphone() as mic:
              print("Escolha um para prosseguir")
              rec.adjust_for_ambient_noise(mic)
              audio = rec.listen(mic)
          escolha = rec.recognize_google(audio, language="pt-BR")

          if "sim" in escolha:
              convertFala("Aqui está")
              desc = tabela['descricaoa']
              print(desc)

          elif "não" in escolha:
              convertFala("Tudo bem")

          else:
              convertFala("Não entendi")
```
</details>
<br>

### Lista de Desejos
<p>Esta funcionalidade permite que o usuário armazene informações sobre locais que deseja visitar, incluindo o nome do município, estado e seus principais pontos turísticos. Essas informações são salvas em um arquivo .txt, possibilitando que o usuário acesse sua lista de desejos e planeje um roteiro personalizado com base em suas preferências registradas.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>A lista de desejos é feita por meio da criação de um arquivo .txt, sendo que a própria aplicação cria e atualiza este arquivo. Após a criação do mesmo, a aplicação pede algumas informações sobre o local que ele deseja visitar. O usuário fala as informações, a aplicação converte a fala em texto e armazena as informações dentro do arquivo. De um ponto de vista mais técnico, é necessário que a aplicação crie um arquivo .txt, em seguida a aplicação pergunta ao usuário que ação ele deseja realizar na lista de desejos, visualizar a lista de desejos ou adicionar um novo destino. Caso o usuário opte por visualizar a lista desejos, a aplicação lê o arquivo .txt e mostra na tela as informações dos destinos, além de responder por voz também. Se o usuário optar por adicionar um novo destino, a aplicação irá dizer para o usuário falar sobre o local desejado, em seguida a aplicação abre a edição do arquivo .txt e armazena as informações que foram ditas pelo o usuário. Para deletar ou editar alguma informação da lista de desejos, é necessário que o usuário abra o arquivo e realize as ações que deseja executar.</p>
  <p>Abaixo é mostrado como a lista de desejos é realizada na aplicação:</p>
  
  ```python
    elif "desejo" in texto:
            convertFala("Você deseja visualizar a lista ou adicionar")
            print("\n")
            print("1- Visualizar")
            print("2- Adicionar")
            print("\n")

            rec = sr.Recognizer()

            with sr.Microphone() as mic:
                print("Escolha uma opção: ")
                rec.adjust_for_ambient_noise(mic)
                audio = rec.listen(mic)

            resposta = rec.recognize_google(audio, language="pt-BR")

            if ("visualizar" in resposta):
                arquivo = open('lista.txt', 'r')
                print("----Lista de Desejos----")

                for linha in arquivo:
                    print(linha.rstrip())
                    convertFala(linha.rstrip())

                print("Para retirar um destino da lista, vá até o arquivo lista.txt e elimine o que desejar")
                convertFala("Para retirar ou alterar um destino da lista, vá até o arquivo lista.txt e elimine ou altere o que desejar")
                arquivo.close()

            elif ("adicionar" in resposta):
                from classe import listadesejo
                arquivos.append(listadesejo())
                arquivo = open('lista.txt', 'a')

                convertFala("Qual cidade você deseja visitar")
                rec = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Qual o nome da cidade: ")
                    rec.adjust_for_ambient_noise(mic)
                    audio = rec.listen(mic)

                nomecidade = rec.recognize_google(audio, language="pt-BR")

                arquivos[contador].setnomecidade(nomecidade)

                convertFala("Qual o nome do estado brasileiro")
                rec2 = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Qual o nome do estado: ")
                    rec2.adjust_for_ambient_noise(mic)
                    audio = rec2.listen(mic)

                estado = rec2.recognize_google(audio, language="pt-BR")

                arquivos[contador].setestado(estado)

                convertFala("Quais são os pontos turísticos")
                rec3 = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Quais os pontos turísticos: ")
                    rec3.adjust_for_ambient_noise(mic)
                    audio = rec3.listen(mic)

                ponto = rec3.recognize_google(audio, language="pt-BR")

                arquivos[contador].setponto(ponto)

                arquivo.write("--------------------" + "\n")
                arquivo.write("Nome da Cidade:" + arquivos[contador].getnomecidade() + "\n")
                arquivo.write("Nome do Estado:" + arquivos[contador].getestado() + "\n")
                arquivo.write("Pontos Turísticos:" + arquivos[contador].getponto() + "\n")
                arquivo.write("--------------------" + "\n")
                arquivo.close()

                print("Destino adicionado com sucesso")
                convertFala("Destino adicionado com sucesso")
            else:
                convertFala("Não entendi, poderia repetir")
  ```
</details>
<br>

### Utilização de API para obter previsão do tempo
<p>A aplicação oferece uma funcionalidade integrada que permite aos usuários acessar e visualizar dados meteorológicos de qualquer localidade do mundo por meio do serviço oferecido pelo site OpenWeather. Essa função é essencial para os usuários planejarem suas viagens com mais eficiência e conforto.  Com acesso à previsão do tempo, é possível saber se o lugar estará quente, frio ou com um clima agradável durante a estadia planejada. Essas informações ajudam os usuários a se prepararem adequadamente, levando em consideração as condições meteorológicas esperadas.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para que seja possível obter os dados metereológicos de um determinado local, a aplicação deve ter uma integração com o OpenWeather, que se trata de um site que possui dados metereológicos de todo o mundo. Este site disponibiliza uma API (Interface de Programação de Aplicações) para que os desenvolvedores possam obter informações metereológicas e apliquem em seus projetos. No caso do projeto desenvolvido, o usuário fala qual cidade ele deseja saber a previsão do tempo, a aplicação faz uma requisição utilizando a API juntamente com o nome da cidade para obter os dados metereológicos. Como resposta, o OpenWeather retorna a temperatura do local em tempo real na escala de temperatura Kelvin, ou seja, antes da aplicação exibir e dizer a temperatura para o usuário, é necessário fazer uma conversão para Celsius. Após a conversão, a aplicação fala e exibe a temperatura e a condição metereológica do local (ensolarado, nublado etc). Por fim, dependendo da temperatura, a aplicação dá dicas de como se preparar para o clima da cidade.</p>
  <p>Abaixo é apresentado a utilização da API para obter os dados metereológicos:</p>

  ```python
    if "previsão do tempo" in texto:
            convertFala("Para onde você pretende ir")
            api = "a143cba82f2ee6901732e51ece9014df"
            rec = sr.Recognizer()
            
            with sr.Microphone() as mic:
                print("ouvindo")
                rec.adjust_for_ambient_noise(mic)
                audio = rec.listen(mic)
            
            cidade = rec.recognize_google(audio, language="pt-BR")
            
            url = f"https://api.openweathermap.org/data/2.5/weather?q={cidade}&appid={api}"
            req = requests.get(url)
            requisicao_dic = req.json()
            tempo = requisicao_dic['weather'][0]['description']
            temperatura = requisicao_dic['main']['temp']
            converter = (temperatura - 273.15) // 1
            clima = tradutor(tempo)
            convertFala(f"Em {cidade} faz agora {converter} graus Celsius")
            convertFala(f"A condição climática é {clima}")
            print(f"Temperatura agora em {cidade} é {converter} °C")
            print(f"Condição climática agora em {cidade} é {clima}")

            if (converter >= 28):
                convertFala("Passe um filtro solar e beba bastante água, hoje será um dia quente")

            elif (converter <= 15):
                convertFala("Melhor se agasalhar, hoje o dia vai estar frio")

            elif (converter >= 16 and converter <= 27):
                convertFala("Hoje o clima estará agradável, aproveite")
  ```
</details>  
<hr></hr>
<br><br>

## Aprendizados
<p>Durante o projeto de API, atuei como Scrum Master, auxiliando meus colegas no desenvolvimento de suas atividades, além de atuar como um facilitador, tirando impedimentos que podem atrasar os prazos das atividades. Pude entender e aplicar fundamentos básicos do Scrum que ajudaram a equipe a se comprometer com o projeto e entregar um projeto simples e de qualidade.</p>
<p>Também atuei como desenvolvedor, elaborando e construindo implementações do projeto. Pude aumentar o meu conhecimento na linguagem Python e utilizá-la para diferentes propósitos. Além de compreender como funciona a lógica de programação, conceitos de repetição, conceitos de condicionais entre outros paradigmas da programação.</p>

### - Hard Skills:
* Conhecimento e aprofundamento de lógica de programação na linguaguem Python
* Desenvolvimento de API para obtenção de recursos
* Compreensão na manipulação de dicionários
* Desenvolvimento de aplicação que compreende a fala humana e pode se comunicar com o usuário por voz

### - Soft Skills:
* Empatia
* Colobaração
* Autonomia
* Proatividade
<hr></hr>

### PRO4Jobs
##### 2° Semestre • 2022-2
<p>Parceiro Acadêmico: <a href="https://www.pro4tech.com.br/">PRO4TECH</a></p>
<p align = "center"><img src= "2Semestre/logo2sem.png" width="250" height="250"></p>
<p>PRO4Jobs é uma aplicação desenvolvida para desktop e tem como principal intuito ajudar no controle e gerenciamento de vagas de emprego. O candidato realiza sua autenticação e pode encontrar, analisar e se canditar a vagas de emprego que possui interesse. Por outro lado, o RH consegue analisar os currículos dos candidatos para uma determinada vaga, além de poder aprovar ou reprovar os mesmos. </p>

## Tecnologias Utilizadas

* __Java:__ Linguagem de programação back-end;
* __Java Swing:__ Conjunto de bibliotecas da linguagem Java, utilizado para construção de interfaces gráficas de usuário (GUIs);
* __MySQL:__ Sistema Gerenciador de Banco de Dados utilizado para armazenar os dados provenientes da aplicação desenvolvida.
<br><br>

## Contribuições Pessoais
### Cadastro de vagas de emprego
<p>Esta é uma das principais funcionalidades da aplicação, pois é necessário o cadastro de vagas de emprego para que os candidatos possam analisá-las e se candidatarem. A responsabilidade da criação de uma vaga de emprego é do RH da empresa, que deverá detalhar os componentes que fazem parta da mesma. Entre os campos que uma vaga de emprego deve possuir temos, o nome, uma breve descrição, pretensão salarial, cargo e experiência necessária que o candidato deve ter.  </p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para criar uma nova vaga de emprego, foi necessário compreender a estrutura das tabelas do banco de dados desenvolvido, além de possuir um conhecimento básico da linguagem de programação Java. Primeiramente, no banco de dados, foi criada uma nova tabela destinada a armazenar as informações relacionadas à vaga de emprego. Em seguida, foi desenvolvida uma classe em Java que funciona como um Data Transfer Object (DTO) para armazenar temporariamente os dados da vaga.

Após isso, uma nova classe em Java foi criada para inserir registros dentro do banco de dados. Dentro desta classe, foi implementado um método específico que chama outro método de outra classe para estabelecer a conexão com o banco de dados. Depois, um comando SQL foi escrito para cadastrar as vagas de emprego no banco. As informações sobre a vaga de emprego são coletadas por meio de uma interface gráfica (GUI). Esta interface coleta os dados e os passa para a classe que armazena temporariamente essas informações.

A classe que contém o método de cadastro de vagas no banco então coleta os dados do DTO e os incorpora ao comando SQL. Finalmente, este método executa o comando no banco de dados, criando a nova vaga de emprego. Este processo garante que as vagas sejam inseridas corretamente e de maneira eficiente no sistema, facilitando o gerenciamento e a manutenção das informações sobre as oportunidades de emprego disponíveis.  </p>
<p>Abaixo é mostrado o método utilizado para inserir uma vaga de emprego no banco de dados: </p>

  ``` java
    public class VagaDAO {
            Connection conn;
            PreparedStatement pstm;

            public void cadastrarvaga(Vaga obj_cadastro_vaga){
            
            String sql = "insert into vaga(nome_vaga, descricao_vaga, pretencao_salarial, cargo, experiencia_profissional_necessaria, quantidade_candidatos, status) values (?, ?, ?, ?, ?, ?, ?)";
            conn = new ConexaoDAO().conectaBD();
            
            try {
                
                pstm = conn.prepareStatement(sql);
                
                pstm.setString(1,obj_cadastro_vaga.getNome());
                pstm.setString(2,obj_cadastro_vaga.getDescricao());
                pstm.setDouble(3,obj_cadastro_vaga.getSalario());
                pstm.setString(4,obj_cadastro_vaga.getCargo());
                pstm.setString(5,obj_cadastro_vaga.getExpe_prof());
                pstm.setInt(6, 0);
                pstm.setString(7, "ABERTA");
                pstm.execute();
                pstm.close();
                
                JOptionPane.showMessageDialog(null, "Vaga Cadastrada");
                
                
            } catch (SQLException erro) {
                JOptionPane.showMessageDialog(null,"VagaDAO: Cadastrar" + erro);
            
            }
        }
     }
  ```
</details>
<br>

### Criação de Banco de Dados
<p>Como a aplicação possui dados que não podem ser perdidos, foi necessário a construção de um banco de dados relacional. O banco de dados relacional consiste no armazenamento de dados em estruturas que se chamam tabelas, cada tabela deve possuir um identificador único (chave primária), que se trata de um valor que não pode se repetir mais de uma vez, e suas respectivas colunas. Além disso, as tabelas podem ter ligações entre si, e com base nessas relações pode ser necessário a criação de novas tabelas ou a adição de chaves estrangeiras.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para a criação de um banco de dados relacional, foi preciso escolher um SGBD (Sistema Gerenciador de Banco de Dados) que melhor se encaixesse no projeto que foi desenvolvido. O SGBD escolhido foi o MySQL, por se tratar de uma ferramenta simples e fácil de implementar. Após a escolha do SGBD, foi observado a modelagem de dados criada do projeto, porque com ela é criado o script do banco de dados. Em seguida, foi preciso criar um database, onde foi armazenado o banco de dados, depois foram criadas as tabelas e suas respectivas relações. O comando para criar tabelas no MySQL é o "CREATE TABLE", cada coluna deve ter seu nome e o seu tipo de dado que deve ser armazenado (inteiro, texto etc), além de uma chave primária e chave estrangeira (dependendo da relação da tabela com as outras).</p>
  <p>Abaixo é mostrado a criação de uma tabela no banco de dados do projeto:</p>

  ```sql
      create database banco;
      use banco;

      create table candidato(
          cpf varchar(14) not null,
          nome_completo varchar(50) not null,
          data_nascimento date not null,
          email varchar(30) not null,
          telefone bigint not null,
          endereco varchar(60) null,
          pretencao_salarial numeric(7,2) null,
          arquivo blob null,
          senha varchar(3000) not null,
          primary key (cpf)
    );
  ```
</details>
<br>

### Progresso do Candidato
<p>Após um candidato se candidatar a uma vaga de emprego, ele deve ser capaz de visualizar o seu progresso. Isso o ajuda a entender como ele está progredindo em uma determinada vaga. Por sua vez, o RH deve aprovar ou reprovar este candidato, caso seja reprovado, o RH deve enviar um motivo do porque o candidato foi reprovado. Após a reprovação ou aprovação do candidato, ele terá a transparência de ver este retorno.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para implementar a funcionalidade, deve-se ter uma relação entre as tabelas de Candidato e Vaga. Por meio da modelagem de dados foi entendido que as tabelas Candidato e Vaga tem relação entre si, sendo que nenhum ou muitos candidatos podem se candidatar a uma vaga e uma vaga pode ser concorrida por nenhuma ou muitas pessoas. Com base neste tipo de relação, foi necessário criar uma nova tabela contendo as chaves primárias da tabela de Candidato e Vaga, essas mesmas chaves são também ao mesmo tempo chaves estrangeiras. Foi necessário criar um método em Java, que faz a conexão com o banco de dados e altera as colunas status da vaga e motivo, dependendo se o candidato foi aprovado ou reprovado na vaga. Este método chama outro método de uma outra classe para fazer a conexão com o banco de dados e em seguida é executado uma consulta para poder coletar todas as vagas que um determinado candidato se candidatou. O resultado da consulta é armazenada dentro de uma lista, que depois é transferida para uma tabela da interface gráfica, sendo finalmente exibida ao candidato. </p>
  <p>Abaixo é mostrado como é realizada a consulta das vagas relacionadas a um determinado candidato:</p>

  ```java
      public ArrayList<Candidato_Vaga> MostrarVagas(Candidato objcandidato){
        
        String sql = "select v.nome_vaga,cv.status_vaga,cv.motivo from vaga as v "
                + "inner join candidato_vaga as cv on v.id_vaga = cv.fk_id_vaga "
                + "inner join candidato as cand on cand.cpf = cv.fk_cpf where cpf = ?";
        
        conn = new ConexaoDAO().conectaBD();
        
        try{
            pstm = conn.prepareStatement(sql);
            pstm.setString(1, objcandidato.getCPF());
            ResultSet rs = pstm.executeQuery();
            
            while (rs.next()){
                Candidato_Vaga objcv = new Candidato_Vaga();
                objcv.setNome_vaga(rs.getString("nome_vaga"));
                objcv.setStatus(rs.getString("status_vaga"));
                objcv.setMotivo(rs.getString("motivo"));
                lista.add(objcv);
                
            }
           
            
        } catch(SQLException e){
            JOptionPane.showMessageDialog(null, "CandidatoDAO: MostrarVagas" + e);
            return null;
        }
        return lista;
    }
    
    public ResultSet LoginCandidato(Candidato objcandidato){
        String sql = "select * from candidato where cpf = ? and senha = MD5(?)";
        conn = new ConexaoDAO().conectaBD();
        
        try {
            pstm = conn.prepareStatement(sql);
            pstm.setString(1, objcandidato.getCPF());
            pstm.setString(2,objcandidato.getSenha());
            ResultSet rs = pstm.executeQuery();
            return rs;
        } catch(SQLException erro){
            JOptionPane.showMessageDialog(null, "CandidatoDAO" + erro);
            return null;
        }
        
    }
  ```
</details>
<br>

### Autenticação do RH
<p>Uma das funções primordiais ao se desenvolver um sistema é a autenticação, pois é com a mesma que os usuários conseguirão acessar as informações e executar tarefas dentro da aplicação. Para cada perfil de usuário deve ser apresentado páginas diferentes, pois os mesmos exercem funções diferentes na aplicação. Um candidato deve ter a visibilidade de vagas de emprego, progresso de vagas que está concorrendo por exemplo, enquanto uma pessoa do RH é responsável por criar as vagas e aprovar ou reprovar os candidatos.</p>
<details>
  <summary><h4>Mais detalhes</h4></summary>
  <p>A autenticação na aplicação precisa ser capaz de saber quem é um perfil RH e um perfil Candidato, para apresentar as devidas páginas corretamente. Para isso, foi criada uma 
  tela de autenticação unificada, ou seja, todos os usuários da aplicação utilizam a mesma tela para ingressar. Nesta tela foi criado dois campos clicáveis, em que é possível 
  escolher qual perfil de usuário a pessoa é. Em seguida, o usuário preenche os campos de CPF e Senha e clica no botão para entrar na aplicação. Ao clicar no botão, o sistema
  coleta os dados preenchidos pelo usuário e executa uma consulta no banco de dados para saber se o usuário está cadastrado. Caso usuário exista, um pop-up é apresentado dando 
  boas-vindas ao mesmo e abrindo a home page do usuário RH, caso o contrário, é apresentado um pop-up esclarecendo que a o CPF e/ou a senha estão incorretos. </p>
  <p>Abaixo é mostrado como é realizada a consulta para saber se o usuário RH existe no banco de dados:</p>
  
  ```java
      public ResultSet loginRh(Rh objrh) {
    
        conn = new ConexaoDAO().conectaBD();
    
        try {
          
            String sql = "select * from rh where cpf = ? and senha = MD5(?)";
            PreparedStatement pstm2 = conn.prepareStatement(sql);
           
            pstm2.setString(1, objrh.getCpf());
            pstm2.setString(2, objrh.getSenha());
            
            ResultSet rs = pstm2.executeQuery();
            return rs;
        } catch (SQLException erro) {
            JOptionPane.showMessageDialog(null, "RHdao" + erro);
            return null;
        }
    }
```
</details>
<hr></hr>
<br><br>

## Aprendizados
<p>Durante o desenvolvimento do projeto, eu tive o papel de Product Owner, ou seja, tive a função de dialogar constantemente com o cliente parceiro, para esclarecer as dúvidas da equipe, além de mostrar como estava o andamento do projeto. Também tive o papel de levantar os requisitos que deveriam ser desenvolvidos após a reunião de kick-off com o cliente.</p>
<p>Ao mesmo tempo em que fui PO, também atuei na área de desenvolvimento. Fui responsável pela a elaboração do script de criação do banco de dados da aplicação, além de desenvolver as telas e realiazar a conexão entre o back-end e o banco de dados. Pude aperfeiçoar meus conhecimentos na linguagem Java, principalmente na questão de conexão e manipulação do Banco de Dados. Aprendi também a ser mais comunicativo e gerir o tempo de forma adequada para que todas as atividades fossem entregadas dentro do prazo estipulado. </p>

<br>

### - Hard Skills:
* Desenvolvimento de scripts SQL (SGBD MySQL)
* Desenvolvimento na linguagem Java, focado na manipulação e consulta de Banco de Dados
* Utilização do Java Swing para desenvolvimento de páginas desktop
* Auxílio no desnvolvimento da modelagem de dados

### - Soft Skills:
* Organização
* Trabalho em equipe
* Gestão de Tempo
* Inteligência Emocional
<hr></hr>

### Predial
##### 4° Semestre • 2023-2
<p>Parceiro Acadêmico: <a href="https://www.jaia.software/">Jaia Software</a></p>
<p align = "center"><img src= "" width="250" height="250"></p>
