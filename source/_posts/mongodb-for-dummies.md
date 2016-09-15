---
title: Primeiros passos com o MongoDB
banner: /images/posts/banner/2013_mongodb.png
date: 2013-12-17
tags: tutorial, banco de dados, MongoDB
categories: Tutorial
snippet: O que é o MongoDB? Onde ele vive e do que se alimenta? Vamos descobrir tudo isso e muito mais agora!
language: pt
layout: post
---

## O que é MongoDB?

MongoDB é um projeto _open-source_ de banco de dados orientado a documentos, que fornece alta performance, disponibilidade e escalabilidade automático.

### Banco de Dados Orientado a Documento

Um registro no MongoDB é um documento, que é uma estrutura composta por pares de chaves e valores. Os documentos utilizados pelo MongoDB são similares aos objetos JSON. Os valores dos campos podem conter outros documentos, _arrays_, e _arrays_ de documentos.

Exemplo de um documento MongoDB

      {
        name: "Cassio",
        age: 23,
        gender: "M",
        interests: ["MongoDB", "Node.js", "JavaScript"]
      }

### Quais as vantagens?

- Os documentos (ou objetos) correspondem ao tipo nativo de dados em diversas linguagens de programação.
- Documentos e _arrays_ incorporados reduzem a necessidade de se fazer _joins_.
- Por se tratar de um esquema dinâmico, suporta polimorfismo.

## Instalação o MongoDB no Windows (64-bit)

Existem 3 versões diferentes do MongoBD para download no [site oficial](http://www.mongodb.org). Para checar qual versão você deve baixar, abra o _prompt_ de comando no Windows e digite o seguinte comando:

      wmic os get osarchitecture

Após isso vá até a página de _downloads_ do site e baixe a versão correspondente.

Concluído o _download_ acesse a pasta onde o arquivo foi salvo e extraia o conteúdo da pasta.

É recomendável que você mova o conteúdo para outro diretório. O ideal é que a pasta do MongoDB fique no `C:\` da seguinte forma:

      C:\mongodb

## Rodando o MongoDB

O MongoDB necessita de um diretório de `data` onde ele armazenará os arquivos. Por padrão o MongoDB utiliza uma pasta chamada `data`. Recomenda-se que esta pasta seja criada no `C:\`:

      cd C:\
      md data
      cd data
      md db

### Iniciando o MongoDB

Utilizando o _prompt_ de comando, rode o seguinte comando:

      C:\mongodb\bin\mongod.exe

### Conectando ao MongoDB

Para se conectar ao MongoDB abra outro _prompt_ de comando e execute o seguinte comando:

      C:\mongodb\bin\mongo.exe

Após isso o `mongo.exe` conectará automaticamente ao `mongod.exe` e rodando no _localhost_ na porta `27017` por padrão. No _prompt_ do `mongo.exe` rode os seguintes comandos para inserir um novo registro na coleção (_collection_) `test` na base de dados padrão `test`e depois para recuperar esse registro:

      db.test.save( { a : 1 } )
      db.test.find()

### Utilizando o MongoDB como um serviço do Windows

Apesar de serem opcionais, os passos a seguir são altamente recomendados e considerados boas práticas.

1) Crie um diretório específico para armazenar o _log_ do MongoDB.

      md C:\mongodb\log

2) Crie um arquivo de configuração para a opção `logpath` do MongoDB:

      echo logpath=C:\mongodb\log\mongo.log > C:\mongodb\mongod.cfg

### Instalando e rodando o MongoDB como Serviço do Windows

Para instalar o serviço do MongoDB execute o seguinte comando através do _prompt_ de comando:

      C:\mongodb\bin\mongod.exe --config C:\mongodb\mongod.cfg --install

Para rodar o serviço, execute:

      net start MongoDB

### Parando ou removendo o serviço do MongoDB

Para parar o serviço do MongoDB, execute:

      net stop MongoDB

Para remover o serviço do MongoDB, execute:

      C:\mongodb\bin\mongod.exe --remove

## Primeiros Passos com o MongoDB

No _prompt_ de comando do Windows inicie o Mongo através do seguinte comando:

      mongo

Por padrão o `mongo` procura por uma base de dados na porta `27017` no _localhost_. Para conectar em um servidor diferente ou utilizar outra porta user as opções `--host` e `--port`.

## Comandos úteis

Verificar qual banco de dados está sendo utilizado no momento:

      db

Exibir uma lista de banco de dados:

      show dbs

Trocar de banco de dados:

      use db_name

Para exibir o manual do MongoDB:

      help

### Criando coleções e inserindo documentos

Primeiramente deve-se criar os documentos que serão inseridos na coleção. Para fazer isso utiliza-se o seguinte comando:

      document_id = { field : value }

Criaremos dois documentos de exemplo:

      j = { name : "mongo" }
      k = { x : 3 }

Para ver as coleções já existentes utiliza-se o comando:

      show collections

Com os documentos que serão inseridos criados, devemos executar o comando que irá inserí-los na coleção:

      db.collection.insert()

No caso acima iremos inserir os documentos na coleção `testData`:

      db.testData.insert(j)
      db.testData.insert(k)

Para conferir se os documentos foram inseridos corretamente na coleção utiliza-se o seguinte comando:

      db.collection.find()

No caso do exemplo acima:

      db.testData.find()

### Inserindo um novo Usuário

Para inserir um novo usuário, selecione em qual banco de dados você irá inserir o novo usuário, utilizando o comando

      use db_name

Após isso execute o comando a seguir para inserir um novo usuário

      db.addUser('admin', '12345')

Para utilizar a autenticação de usuário feche o servidor, para isso pode-se usar o comando `db.shutdownServer()`, e abra-o novamente utilizando o parâmetro `--auth`

      C:\mongodb\bin\mongod.exe --auth

Após isso o MongoDB solicitará que você entre com o nome de usuário e senha para acessar o banco.

Basicamente é isso. Ainda pretendo utilizar o MongoDB em aplicações mais elaboradas, mas já deu para perceber que é uma ferramenta bem poderosa. Para quem quiser ler mais sobre o assunto, separei alguns links nas referências deste artigo.

## Referências

[MongoDB Manual](http://docs.mongodb.org/manual/tutorial/getting-started/)

[Learn Mongo](http://learnmongo.com/posts/quick-tip-mongodb-users/)
