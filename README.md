# Projeto criado para o Programa Desenvolve
Este projeto foi criado a fim de mostrar um pouco da minha evolução e toda ajuda que obtive. Meus mentores gravaram vídeos e ensinaram como utilizar essa ferramenta (GitHub) na qual eu nem sabia abrir ao iniciar o programa Desenvolve. Além disso, aprendi comandos em Python, como utilizar algumas bibliotecas e como criar bancos de dados utilizando PostgreeSQL e SQLServer. 
<br><br>
Durante a jornada tivemos lives que ensinaram hard skills e soft skills. Em uma dessas lives realizamos uma tarefa no Python onde criamos gráficos a partir de dados públicos do ENEM.
<br><br>
Por fim, reuni meus conhecimentos sobre Python, SQL e criação de gráficos para construir esse projeto.<br>
<br>
<br>
<br>

## Apresentação do Projeto<br>
A empresa Teclalol produz teclados, mouses e mousepads personalizados para Gamers e apaixonados por tecnologia. 

Até o momento, a Teclalol faz controle das vendas através do site de Ecommerce, porém como alguns pedidos presenciais começaram a ser solicitados, a empresa decidiu criar um Banco de Dados para facilitar a busca por informações. A Teclalol é uma empresa pequena e conta com 4 funcionários. Um funcionário é responsável pelo acompanhamento do Ecommerce, 2 funcionários são responsáveis pela produção dos produtos e o quarto funcionário administra os valores recebidos, contas a pagar e pedidos de suprimentos aos fornecedores.

O funcionário que acompanha o Ecommerce ficará responsável pelo banco de dados e tem pouco conhecimento em SQL, mas gosta de plotar seus gráficos utilizando o Jupyter notebook.
<br>
<br>

## Objetivos

1) Criar um Banco de Dados chamado "PythonSQL" utilizando SQLServer para uma empresa fictícia chamada "Teclalol"
2) Criar conexão entre o SQLServer e o Python utilizando o Jupyter notebook
3) inserir dados no Banco de Dados através do Jupyter notebook
4) Ler tabelas do SQL no Jupyter
5) Plotar um gráfico de Barras 
<br>
<br>

## Etapas do Processo

1) Criar um Banco de Dados chamado "PythonSQL" utilizando SQLServer para uma empresa fictícia chamada "Teclalol"

Acessar o SQLServer e criar um Banco de Dados chamado PythonSQL utilizando o comando abaixo:

'''

    CREATE DATABASE PythonSQL

'''

* Em alguns bancos de dados como PostegreeSQL precisamos terminar o comando inserindo ponto e vírgula (;), porém o SQLServer não exige isso.

Após criarmos nosso Banco de Dados, precisamos criar as primeiras tabelas: "Produtos" e "Vendas"

'''

    CREATE TABLE Produtos(
        id_produto INT,
        nome_produto VARCHAR(100),
        desc_produto VARCHAR(100),
        cor VARCHAR(50),
        preco_unitario DECIMAL(10,2),
        qtd_estoque INT
     )
    
    
    CREATE TABLE Vendas(
        id_venda INT,
        data_venda DATE,
        cliente VARCHAR(100),
        produto VARCHAR(100),
        preco DECIMAL(10,2),
        quantidade INT
    )
    
'''

O banco de dados está vazio, então iniciamos inserindo alguns dados na tabela Produtos, conforme o comando abaixo:

'''

    INSERT INTO Produtos(
      id_produto, 
      nome_produto, 
      desc_produto, 
      cor, 
      preco_unitario, 
      qtd_estoque) VALUES(
      1,
      'Teclado Minnie',
      'Teclado 44,3x2x13,6cm',
      'Rosa',
      180,
      5)
  
'''

Após a mensagem de sucesso, podemos inserir o comando insert para verificar nossa tabela

'''

    INSERT
      *
     FROM
      Produtos
  
'''

![Captura de tela 2023-05-17 143442](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/93c156e0-4253-4361-8cdd-583ba147f42b)


<br>
<br>
<br>

2) Criar conexão entre o SQLServer e o Python utilizando o Jupyter notebook

Agora, abriremos o Jupyter notebook, levando em consideração que já está instalado na máquina. Para utilizar o SQL no Python, precisamos instalar e importar a biblioteca pyodbc

'''

    pip install pyodbc


    import pyodbc

'''

Podemos inserir o comando print(pyodbc.drivers()) para verificar os Drivers. Se ocorrer erro nesse processo é porque a biblioteca não está instalada.

![Captura de tela 2023-05-17 144148](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/2265faa8-4bdb-435d-844a-e19f9d1e10d2)


Precisamos agora criar a conexão do SQL com o Python e para isso precisamos inserir o Driver (estamos utilizando o SQLServer), o servidor (Nome do servidor. Você pode digitar "Hostname" CMD do seu computador para confirma) e o nome do Banco de Dados que estamos utilizando.

Precisamos tambem da variável "conexao" para criar nossa conexão com o Banco de Dados, utilizando os dados que inserimos. Podemos inserir um print para recebermos um retorno quando tudo estiver ok com nossa conexão.

'''

    dados_conexao = (
            "Driver={SQL Server};"   
            "Server=Le_Souza;"      
            "Database=PythonSQL;"    
    )

    conexao = pyodbc.connect(dados_conexao)
    print("Conexão bem sucedida!")
    
'''

![Captura de tela 2023-05-17 145027](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/623215b4-efdf-4bb4-b15a-0273412cfc27)

criamos tambem um cursor que vai permitir a utilização dos comandos SQL

'''

    cursor = conexao.cursor()

'''
<br>
<br>
<br>
3) inserir dados no Banco de Dados através do Jupyter notebook



Vamos testar agora nossa conexão inserindo mais dados à nossa tabela Produtos, mas dessa vez diretamente do Python. Vamos criar a cariável comando e inserir o comando que utilizamos anteriormente, mudando apenas os dados do produto.

![Captura de tela 2023-05-17 145439](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/c7a3421e-fffd-4e75-b286-96b1069e9f0e)

![Captura de tela 2023-05-17 145511](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/9d651791-163c-439e-b487-ace5e792e4d2)


Após inserir o comando, colocamos tambem cursor.execute(comando) para executar o comando e cursor.commit() para garantir que foi executado e atualizado efetivando a transação.


Podemos tambem criar variáveis para que nosso insert fique mais fácil de ser preenchido.

'''

    import pyodbc
    
    dados_conexao = (
            "Driver={SQL Server};"
            "Server=Le_Souza;"
            "Database=PythonSQL;"
    )

    conexao = pyodbc.connect(dados_conexao)
    print("Conexão bem sucedida!")

    cursor = conexao.cursor()

    id = 3
    nome = 'Teclado Minnie'
    desc = 'Teclado 44,3x2x13,6cm'
    cor = 'Preto'
    preco = 180
    qtd_estoque = 5

    comando = f"""INSERT INTO Produtos(id_produto, nome_produto, desc_produto, cor, preco_unitario, qtd_estoque) 
    VALUES({id},'{nome}','{desc}','{cor}',{preco},{qtd_estoque})"""

    cursor.execute(comando)
    cursor.commit()

'''

![Captura de tela 2023-05-17 150624](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/be77066f-2bd8-4691-af43-f4ad62cd9929)
<br>
<br>
<br>

4) Ler tabelas do SQL no Jupyter

Inseri alguns dados a mais em nossa tabela de Produtos. Ao todo são 35 produtos cadastrados em nossa base:

![Captura de tela 2023-05-17 152025](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/a351ee9c-6870-4fc2-b69c-cc30c0d7e4fd)

Inseri tambem dados em nossa tabela de Vendas, apenas 5 vendas para não deixar nossa tabela vazia:

![Captura de tela 2023-05-17 154154](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/c3a841a8-f3b3-416d-bd79-a6b5c9909915)
<br>

Para conseguirmos importar nossos dados e plotar nossos gráficos, precisamos de alguma bibliotecas. Como já vimos precisamos da pyodbc, mas tambem precisamos instalar e importar as bibliotecas pandas e matplotlib.

'''

    import pyodbc
    import pandas as pd
    import matplotlib

'''

Com as bibliotecas importadas nós podemos então inserir nosso comando SQL. Nesse caso vou ler as colunas de nome_produto e qtd_estoque da tabela Produtos. Feito isso, criamos uma variável "dados" para inserir a função read da biblioteca Pandas, onde vamos linkar nosso comando à nossa conexao.

'''

    dados_conexao = (
            "Driver={SQL Server};"
            "Server=Le_Souza;"
            "Database=PythonSQL;"
    )

    conexao = pyodbc.connect(dados_conexao)
    print("Conexão bem sucedida!")


    comando_sql = "SELECT nome_produto, qtd_estoque FROM Produtos"

    dados = pd.read_sql(comando_sql, conexao)

'''

Pode aparecer uma mensagem de alerta, mas podemos prosseguir com o comando display(dados) que conseguiremos visualizar nossa tabela.

![Captura de tela 2023-05-17 162015](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/81f18084-ebfe-4bbc-8430-949bf88e7a8d)

<br>
<br>
<br>
5) Plotar um gráfico de Barras 

O próximo passo é agrupar nossa tabela por nome_produto e inserir a função SUM (soma)

'''

    dados.groupby('nome_produto').sum()

'''

Esse comando irá organizar nossa tabela por Nome e mostrará quantos itens temos te acordo com cada nome

![Captura de tela 2023-05-17 162209](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/0acea461-f6c4-4d1b-9f34-878e766e3ec1)

Essa função deverá ser guardada em uma variável e depois podemos chamar nossa tabela utilizando o comando display

![Captura de tela 2023-05-17 162544](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/ca678efc-e237-4a12-af0b-6a4240cb765f)

Por fim, utilizamos a função plot para gerar nosso gráfico de barras:

'''

    Produtos_por_Nome.plot(kind='bar')

'''

![Captura de tela 2023-05-17 162740](https://github.com/Leticia-Souza94/Projeto_Desenvolve/assets/112443902/55a6c748-e6bf-40d4-9d83-f883f629d2fc)


## Conclusão

Podemos observar visualmente a quantidade de produtos que temos divididos por nome, sem levar em conta as suas categorias como "cor" ou "descrição". Foi um aprendizado rico e com certeza com mais tempo e conhecimento, poderá ser melhorado.



