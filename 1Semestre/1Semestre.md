## 1° Semestre • 2022-1
### Mó Viagem
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
<br>

## Outros projetos:

#### 2° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/2Semestre/2Semestre.md">PRO4Jobs</a>
#### 3° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/3Semestre/3Semestre.md">Sistema Gerenciador de Vendas</a>
#### 4° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/4Semestre/4Semestre.md">Predial</a>
#### 5° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/5Semestre/5Semestre.md">Tecsus</a>
#### 6° Semestre: <a href="https://github.com/lucasetdasilva/PortifolioBancodeDados/blob/main/6Semestre/6Semestre.md">SPC Grafeno</a>
