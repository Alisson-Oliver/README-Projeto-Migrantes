## Documentação do Backend - MigraHelp

### 1.🔍 Introdução

O backend da aplicação **MigraHelp** será responsável por gerenciar todas as operações relacionadas aos usuários (migrantes e organizações), autenticação, armazenamento de dados e fornecimento da API REST para comunicação com dois aplicativos (um para as organizações e outro para os migrantes). A API REST será desenvolvida com **Node.js** e utilizaremos **PostgreSQL** como banco de dados relacional para armazenar as informações de usuários e entidades. O banco de dados será hospedado no **Tembo**.

**Objetivo do projeto:** trata-se de um app para conectar o migrante às organizações comunitárias e instituições e ongs de amparo ao migrante, e uma agenda cultural para integrar o migrante à comunidade de Salvador.

---

### 2.⚙️ Ferramentas e Tecnologias

Para a construção da API REST, utilizaremos **Node.js**. Os módulos que usaremos para o projeto são:

*   [**Express**](https://www.npmjs.com/package/express): Framework para criar APIs REST, facilitando o roteamento e a manipulação de requisições.
*   [**pg**](https://www.npmjs.com/package/pg): Driver oficial do PostgreSQL para Node.js, que permite interações com o banco de dados.
*   [**Sequelize**](www.npmjs.com/package/sequelize): Um ORM (Object-Relational Mapping) que simplifica o gerenciamento de dados no banco de dados PostgreSQL, permitindo manipulações de tabelas e consultas de forma mais intuitiva.
*   [**JWT (JSON Web Tokens)**](https://www.npmjs.com/package/jsonwebtoken): Usado para a autenticação e criação de sessões seguras, permitindo que as credenciais dos usuários sejam transportadas de forma segura entre cliente e servidor.
*   [**Bcrypt**](https://www.npmjs.com/package/bcrypt): Responsável por criptografar (hashing) senhas antes de armazená-las no banco de dados, aumentando a segurança dos dados dos usuários.
*   [**Dotenv**](https://www.npmjs.com/package/dotenv): Gerenciador de variáveis de ambiente que permite armazenar de forma segura chaves secretas e credenciais do banco de dados sem deixá-las expostas no código.
*   [**Axios**](https://www.npmjs.com/package/axios): Biblioteca para consumir APIs externas, facilitando a comunicação entre a aplicação e serviços de terceiros.
*   [**Mocha**](https://www.npmjs.com/package/mocha)**/**[**Chai**](https://www.npmjs.com/package/chai): Ferramentas de testes unitários que serão utilizadas juntas para garantir o funcionamento correto da API.
*   [**Joi**](https://www.npmjs.com/package/joi): Biblioteca de validação de dados que facilita a definição de esquemas para validar a estrutura e os tipos de dados recebidos nas requisições, garantindo que os dados atendam a critérios específicos antes de serem processados.
*   [**generate-password**](https://www.npmjs.com/package/generate-password)**:** Módulo que permite gerar senhas seguras e personalizadas, oferecendo opções para especificar o comprimento da senha, incluir caracteres especiais, letras maiúsculas e minúsculas, e números.

_Além dos módulos acima, outros pacotes poderão ser utilizados conforme necessário para atender aos requisitos do projeto._

### ➕ Ferramentas Adicionais

Além dos módulos essenciais, utilizaremos as seguintes ferramentas para auxiliar no desenvolvimento e validação da API:

*   **Postman**: Ferramenta utilizada para testar as rotas da API, realizar requisições e garantir que os endpoints estejam funcionando corretamente.
*   **PostgreSQL**: Banco de dados relacional que armazenará as informações da aplicação, garantindo a integridade e segurança dos dados.

#### Observação

Seguiremos boas práticas de validação e tratamento de erros, utilizando bibliotecas adicionais quando necessário.

---

### 3\. 📁 Estrutura do Projeto

#### Diretórios:

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/b0a55a20c75e0a4a7e031897060609ce4cf76de3629ff17f.png)                           

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/805623d6998d56e919fbb97221b98282dd88a21d5111e3d8.png)

#### Descrição dos Diretórios:

1.  **config/**:
    *   Armazena configurações da aplicação, como a conexão com o banco de dados, variáveis relacionadas à autenticação e outras configurações gerais.
2.  **controllers/**:
    *   Contém os “controladores”, que são responsáveis por receber as requisições, processá-las e devolver as respostas adequadas. Eles geralmente fazem chamadas para os serviços.
3.  **middlewares/**:
    *   Contém middlewares para tarefas específicas, como autenticação, validação de tokens JWT, limitação de requisições (rate limiting), etc.
4.  **models/**:
    *   Armazena os modelos do banco de dados (usando Sequelize, por exemplo). Esses modelos representam as tabelas no banco de dados e definem as interações com os dados.
5.  **routes/**:
    *   Define as rotas da API. Cada arquivo contém as rotas relacionadas a uma entidade, como `migrantes`, `autenticação`, etc.
6.  **services/**:
    *   Contém a lógica de negócio que é chamada pelos controladores. Eles geralmente lidam com operações mais complexas que envolvem interações com o banco de dados e outras camadas da aplicação.
7.  **tests/**:
    *   Armazena os testes unitários e de integração. Podemos utilizar bibliotecas como `Mocha` e `Chai` para testar as funcionalidades da API.
8.  **utils/**:
    *   Contém funções auxiliares e utilitárias, como validadores e constantes usadas ao longo do projeto.
9.  **app.js**:
    *   Arquivo principal da aplicação. Aqui o servidor é configurado, middlewares são aplicados e as rotas são carregadas.

---

### 4.🗄️ Configurações do Banco de dados

#### Banco de Dados: PostgreSQL

*   Nome do banco dados: `migrantes_db`
*   Host: `db_host`
*   Porta: `5432`
*   Dialeto: `postgres`
*   Usuário: `db_user`
*   Senha: `db_password`

As variáveis de ambiente (`DB_NOME, DB_USUARIO, DB_SENHA, DB_HOST`) serão definidas em um arquivo `.env`.

#### Exemplo da .env:

```plaintext
DB_NOME=migrantes_db
DB_HOST=tembo.io
DB_PORTA=5432
DB_DIALETO=postgres
DB_USUARIO=postgres
DB_SENHA=senhaSegura123
```

---

### 5.🗃️ Estrutura do Banco de Dados

_O diagrama ainda está em fase de modificações…_

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/3d798371b542bc37d8af8946ce90335db213688854af974f.png)

Diagrama do Banco de dados: [https://lucid.app/lucidchart/ac75eb44-b924-494b-b852-c9fd823b9d75/view](https://lucid.app/lucidchart/ac75eb44-b924-494b-b852-c9fd823b9d75/view)

#### Script para criação das tabelas:

_O script SQL ainda está em fase de modificações…_

```plaintext
-- CREATE DATABASE migrantes_db;

-- Criando a tabela endereco
CREATE TABLE endereco(
    id SERIAL PRIMARY KEY,  
    cep VARCHAR(8) NOT NULL UNIQUE,
    bairro VARCHAR(100) NOT NULL,
    cidade VARCHAR(50) NOT NULL,
    uf VARCHAR(3) NOT NULL 
);

-- Criando a tabela estado_civil
CREATE TABLE estado_civil(
    id SERIAL PRIMARY KEY,
    estado_civil VARCHAR(100) NOT NULL
);

-- Criando a tabela nacionalidade
CREATE TABLE nacionalidade(
    id SERIAL PRIMARY KEY,
    nacionalidade VARCHAR(100) NOT NULL
);

-- Criando a tabela categoria
CREATE TABLE categoria(
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100) NOT NULL,  
    descricao TEXT  
);

-- Criando a tabela organizacao
CREATE TABLE organizacao(
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    nome_fantasia VARCHAR(100) NOT NULL,
    cnpj VARCHAR(15) NOT NULL,
    telefone_obrigatorio VARCHAR(20) NOT NULL,
    telefone_opcional VARCHAR(20),
    email VARCHAR(100) NOT NULL,
    descricao TEXT NOT NULL,
    
    numero_endereco VARCHAR(5),
    completo_endereco TEXT NOT NULL,
    
    endereco_completo_id INT,  
    categoria_id INT, 
    FOREIGN KEY(endereco_completo_id) REFERENCES endereco(id),  
    FOREIGN KEY (categoria_id) REFERENCES categoria(id)  
);

-- Criando a tabela migrante
CREATE TABLE migrante(
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100), 
    telefone VARCHAR(20),
    identificacao VARCHAR(30),
    data_nascimento DATE NOT NULL,
    genero VARCHAR(20) CHECK (genero IN ('Masculino', 'Feminino', 'Outro')) NOT NULL,  
    
    hash_senha VARCHAR(60) NOT NULL, 

    organizacao_id INT, 
    estado_civil_id INT, 
    nacionalidade_id INT,  
    FOREIGN KEY(organizacao_id) REFERENCES organizacao(id),
    FOREIGN KEY(estado_civil_id) REFERENCES estado_civil(id),
    FOREIGN KEY(nacionalidade_id) REFERENCES nacionalidade(id),
    UNIQUE(email, identificacao)
);
```

---

### 6.🔁 Rotas principais da API

Abaixo estão as rotas principais para as operações CRUD:

#### Rotas de Migrantes:

| Operação | Rota | Função | Status Code |
| --- | --- | --- | --- |
| GET | **/migrantes** | Lista todos os migrantes | 200 OK, 404 Not Found |
| POST | **/migrantes** | Cria um novo migrante | 201 Created, 400 Bad Request |
| PUT | **/migrantes/:id** | Atualiza os dados de um migrante | 200 OK, 404 Not Found, 400 Bad Request |
| DELETE | **/migrantes/:id** | Deleta um migrante específico | 204 No Content, 404 Not Found |

#### Rotas de Organizações:

| Operação | Rota | Função | Status Code |
| --- | --- | --- | --- |
| GET | **/organizacoes** | Lista todas as organizações | 200 OK, 404 Not Found |
| POST | **/organizacoes** | Cria uma nova organização | 201 Created, 400 Bad Request |
| PUT | **/organizacoes/:id** | Atualiza os dados de uma organização | 200 OK, 404 Not Found, 400 Bad Request |
| DELETE | **/organizacoes/:id** | Deleta uma organização específica | 204 No Content, 404 Not Found |

#### Rotas de Autenticação:

| Operação | Rota | Função | Status Code |
| --- | --- | --- | --- |
| POST | **/login** | Realiza login e gera um token JWT | 200 OK, 401 Unauthorized, 400 Bad Request |
| POST | **/cadastrar** | Cria um novo usuário com hash de senha | 201 Created, 400 Bad Request, 409 Conflict |

#### HTTP Códigos de Status

**Status de Resposta**:

*   **200 OK**: Requisição bem-sucedida.
*   **201 Created**: Recurso criado com sucesso.
*   **204 No Content**: Requisição bem-sucedida, mas sem conteúdo retornado.
*   **400 Bad Request**: A requisição contém erros de validação.
*   **401 Unauthorized**: Falha na autenticação.
*   **404 Not Found**: Recurso não encontrado.
*   **409 Conflict**: Conflito com o estado atual do recurso.
*   → Todas as respostas serão acompanhadas com os seus devidos status.  
     
    
    ![HTTP: Response status code. Aprendi uma coisa: só se conhece… | by Maycon  Alves | React Brasil | Medium](https://miro.medium.com/v2/resize:fit:920/1*yrMWEpUC-hXED7oGD0j2og.jpeg)
    

---

### 7.🚦 Autenticação e Armazenamento de Tokens

#### JSON (JSON WEB TOKEN)

*   Para autenticar usuários, será gerado um token **JWT** no login. Esse token será armazenado no banco de dados local do dispositivo móvel.
    
    ##### Exemplo de geração de token:
    
    ```javascript
    const jwt = require('jsonwebtoken');
    const token = jwt.sign({ userId: user.id }, process.env.JWT_SECRET);
    ```
    
    #### Armazenamento de token (Mobile):
    
    *   Após o login na aplicação mobile, o token JWT será armazenado localmente, permitindo um login persistente.
    *   O usuário será deslogado se ele fizer isso manualmente.

---

### 8.🛠️ Validação e Tratamento de Erros

Utilizaremos middleware para validação de entradas e tratamento de erros.

#### Validação de dados

→ Utilizaremos o **Joi** para fazer a validação.

### Tratamento de erros:

→ Um middleware será utilizado para capturar erros não tratados e retornar respostas adequadas.

#### Fluxo proposto para o cadastro de um usuário:

1.  **Gerar uma senha numérica** de **8 dígitos** usando o módulo `generate-password`.
2.  **Validar os dados de entrada** e a senha gerada usando o `Joi`.
3.  **Criptografar a senha** gerada usando o `bcrypt`.
4.  **Salvar o usuário no banco de dados** com o Sequelize.

---

### 9\. <img src="https://github.com/onemarc/tech-icons/blob/main/icons/postman.svg" width="20"> Testes com Postman

Realizaremos testes de todas as rodas da API utilizando o Postman, Os testes incluirão:

*   **Login e Autenticação** (validação de JWT)
*   **Operações CRUD** (migrantes, organizações)
*   **Validação de entradas inválidas**
    
    Também serão configurados testes unitários com **Mocha/Chai** para garantir que as funções principais da API estão funcionando conforme esperado.
    

---

### 10.🔒 Segurança

Devemos garantir a segurança da API REST mesmo não tendo dados extremamente sensíveis e mesmo em cenários onde o número de usuários é reduzido. As seguintes práticas recomendadas podem ser implementas para fortalecer a segurança:

#### Autenticação e Autorização

*   Uso de Tokens JWT;
*   Níveis de Acesso: Definir diferentes níveis de acesso para usuários e administradores.

#### Criptografia de dados

*   Hash de Senhas: Utilizaremos o bcrypt para isso. A senha será gerada possuindo 8 caracteres. Ex: 12737193.

#### Validação de dados

*   Validação de entradas usando o **Joi;**

#### Limitação de Taxa

*   Implementar Rate Limiting: Utilizar middleware para limitar o número de requisições que um usuário pode fazerem um determinado período.

#### Proteção contra Ataque Comuns

*   Proteção contra Injeções usando uma ORM (Sequelize).

---

### 11\. <img src="https://github.com/onemarc/tech-icons/blob/main/icons/docker.svg" width="20"> Utilização do Docker

→ Utilizaremos o Docker como uma ferramenta essencial para o desenvolvimento e implantação da aplicação.

#### O que é Docker?

O Docker é uma plataforma que permite criar, implantar e executar aplicações em contêineres. Um contêiner é uma unidade leve e portátil que inclui tudo o que uma aplicação precisa para funcionar, como código, bibliotecas e dependências. Isso garante que a aplicação tenha um desempenho consistente em diferentes ambientes, desde o desenvolvimento até a produção.

##### **Por que usar Docker?** [://stack.desenvolvedor.expert/appendix/docker/porque.html](https://stack.desenvolvedor.expert/appendix/docker/porque.html)

---

### 12.✅ Considerações finais

Neste documento, oferecemos uma visão abrangente do desenvolvimento da API REST para a aplicação **MigraHelp**, abordando desde a arquitetura até as práticas de segurança. Embora algumas modificações ainda sejam necessárias, discutiremos essas questões em conjunto com nosso orientador e a turma para garantir que todos estejam alinhados.

Este documento servirá como um guia de referência para o desenvolvimento e manutenção da API **MigraHelp**, assegurando que todas as etapas do processo sejam seguidas de maneira organizada e eficiente.
