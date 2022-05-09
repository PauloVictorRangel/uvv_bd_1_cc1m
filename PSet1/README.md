# - Pset1 -
### Aprendendo sobre Sistema de Controle de Versão, implementação de projetos lógicos e utilização de SGBD relacionais.
---

*Aluno: Paulo Victor Rangel da Silva Cruz*

*Professor: Abrantes Araujo Silva Filho*

*Monitora: Suellen Miranda Amorim*

---

[GIT](#git) •
[GitHub](#github) •
[Elmasri](#elmasri) •
[PostgreSQL](#postgresql) •
[MariaBD/MySQL](#mariabdmysql)


## GIT
O `GIT` é um **Sistema de Controle de Versão*. Um *Sistema de Controle de Versão** é um sistema registra todas as alterações feitas em um
código fonte.

Ele permite saber quem, quando e porquê uma determinada alteração no código foi feita e mantém um histórico recuperável de todo o código fonte.

No decorrer do projeto o `GIT` foi utilizado para *criar, **alterar* e *enviar* arquivos para dentro deste repositório, no `GitHub`.


## GitHub
O `GitHub` é uma plataforma de hospedagem de códigos fonte com controle de versão usando o `GIT`.

Essas são algumas funções do GitHub:
* `Repositório`: diretório onde os seus arquivos ficam armazenados.
* `Branch`: cópia do diretório para desenvolvimento isolado.
* `Pull Request`: é quando você informa que irá implantar as mudanças no seu branch ao diretório.

Foi orientado pelo professor Abrantes a hospedagem do projeto no `GitHub` e a criação de um subdiretório para a documentação do projeto em linguagem Markdown.

## Elmasri 
#### Implementação do projeto lógico

Foi proposto a criação e implementação do projeto lógico apresentado nos capítulos 5 e 6 do livro Sistemas de Banco de Dados, 7ª edição, dos autores Elmasri & Navathe.

Para a criação do projeto lógico, foi utilizado o SQL Power Architect, uma ferramenta de modelagem e perfil de dados.

A partir desse projeto lógico criado no SQL Power Architect foram gerados dois scripts para os SGBD: **PostgreSQL* e *MariaBD*/*MySQL**.

Ambos os scripts apresentam suas tabelas e colunas comentadas de acordo com os anexos fornecidos pelo professor Abrantes.

## PostgreSQL

O **PostgreSQL** é uma ferramenta que atua como sistema de gerenciamento de bancos de dados relacionados. Tem o papel de gerenciar os dados desses bancos de maneira organizada e eficaz, rodando e gravando todas as informações que ficam registradas nesses compartimentos.

Neste projeto, foi proposto autilização do **PostgreSQL** para a criação de um banco de dados, implementação do projeto lógico e a implementação dos dados.

Como informado pelo professor, o primeiro passo é a criação de um usuário. Portanto, segue abaixo os comandos utilizados para a criação desse usuário.

>[!NOTE]
>
> Todos os comandos foram executados por meio de um terminal Linux.

* `createuser`: Comando para criar a role do usuário.
* `dPs`: Privilégios concedidos ao usuário criado.
* Senha para o usuário criado: 123456
* `psql`: Comando para acessar ao banco de dados do PostgreSQL.
* Senha para o usuário postgres: computacao@raiz.
* `\du`: Comando psql para visualizar os usuários já criados.

Com o usuário já criado, agora podemos criar o banco de dados de acordo com os passos informados no **Pset1**. 

![comando create database postgreSQL]

Agora que o banco de dados foi criado, está na hora de criar o `schema`, local onde será armazenado o script com os comandos para a implementação do projeto lógico.

![comando create database postgreSQL]

Com isso, finalizamos a etapa de criação dentro do **PostgreSQL**. Com o `schema` criado, podemos implementar o projeto lógico dentro do banco de dados postgres.

O script completo com os comandos de criação e implementação se encontra dentro deste subdiretório [Pset1]
## MariaBD/MySQL

O **MariaDB* é um sistema de gerenciamento de banco de dados que surgiu como fork do *MySQL*. Na maioria dos aspectos o *MariaDB* vai funcionar exatamente como o *MySQL**. Ambos são capazes de criar um banco de dados para armazenamento e manipulação de dados, definindo a relação de cada tabela.

Neste projeto, foi proposto a utilização do **MariaBD*/*MySQL** para a criação de um banco de dados, implementação do projeto lógico e a implementação dos dados.

Como informado pelo professor, o primeiro passo é a criação de um usuário. Portanto, segue abaixo os comandos utilizados para a criação desse usuário.

>[!NOTE]
>
> Todos os comandos foram executados por meio de um terminal Windows.

![Comando create user MySQL]

* `create user`: Comando para criar o usuário.
* `grant`: Comando que concede os privilégios ao usuário.
* `system mysql`: Comando para trocar de usuário.

Com o usuário já criado, agora podemos criar o banco de dados de acordo com os passos informados no **Pset1**.

![Comando create database MySQL]

Com isso, finalizamos a etapa de criação dentro do **MariaBD*/*MySQL**. Com o banco de dados criado, podemos implementar o projeto lógico e os dados.

O script completo com os comandos de criação e implementação se encontra dentro deste subdiretório [Pset1]
