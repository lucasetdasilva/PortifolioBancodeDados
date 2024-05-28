# Portifólio das API's - Lucas Emanoel
<p>O portfólio tem como objetivo documentar todos os API's (Aprendizagem por Projeto Integrado) para fins educacionais além de servir como trabalho de graduação para a obtenção do diploma de tecnólogo em Banco de Dados proposto pela Faculdade de Tecnologia de São José dos Campos.<p></p>
<hr></hr>

## Sumário
[Sobre mim](#sobre-mim)

<hr></hr>

## Sobre mim
<p align="center"><img src= "Images/fotominha.png" width="420" height="300"></p>

<p>Me chamo Lucas Emanoel Teixeira Engracio da Silva, tenho 20 anos. Sou técnico em Desenvolvimento de Sistemas pela Etec Profa.
Ilza Nascimento Pintusa - SJC e atualmente estou matriculado no 5° Semestre do curso tecnólogo em Banco de Dados na FATEC de 
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
<img src= "Images/logo.png" width="300" height="300">
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
* __Pyttsx3__:.
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
<p>Esta funcionalidade permite ao usuário armazenar informações sobre locais que deseja visitar, incluindo o nome do município, estado e seus principais pontos turísticos. Esses detalhes são salvos em um arquivo .txt, possibilitando que o usuário acesse sua lista de desejos e planeje um roteiro personalizado com base em suas preferências registradas.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>A lista de desejos é feita por meio da criação de um arquivo .txt, sendo que a própria aplicação cria este arquivo. Após a criação do mesmo, a aplicação pede algumas informações sobre o local que ele deseja visitar </p>
</details>
<br>

### Utilização de API para obter previsão do tempo
<p>Esta funcionalidade consiste em </p>
<hr></hr>
<br><br>

## Aprendizados
