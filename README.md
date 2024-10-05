## Documentação Mhelp | Back-End

### 1\. 🔍 Introdução

O back-end da aplicação **Mhelp** será responsável por gerenciar todas as operações relacionadas aos usuários (migrantes e organizações), autenticação, armazenamento de dados e fornecimento da API REST para comunicação com dois aplicativos. A API REST será desenvolvida com **Node.js** e utilizaremos **PostgreSQL** como banco de dados relacional para armazenar as informações de usuários e entidades. O banco de dados, a API REST serão hospedados no **Supabase**.

**Objetivo do projeto:** trata-se de um app para conectar o migrante às organizações comunitárias e instituições e ongs de amparo ao migrante.

### 2\. ⚙️ Ferramentas e Tecnologias 
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
*   **Docker**: Plataforma que permite criar, implantar e executar aplicações em contêineres. Usaremos o Docker para facilitar o gerenciamento das dependências e do ambiente de execução da aplicação, garantindo que ela funcione de maneira consistente em diferentes sistemas.

#### Observação

Seguiremos boas práticas de validação e tratamento de erros, utilizando bibliotecas adicionais quando necessário.

---

### 3\. 📁 Estrutura do Projeto - Em reformulação…

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
    *   Contém a lógica de negócio que é chamada pelos controladores. Eles geralmente lidam com operações mais complexas que envolvem interações com o banco de dados e outras camadas da aplicação. **(PROVAVELMENTE NÃO PRECISARÁ)**
7.  **tests/**:
    *   Armazena os testes unitários e de integração. Podemos utilizar bibliotecas como `Mocha` e `Chai` para testar as funcionalidades da API.
8.  **utils/**:
    *   Contém funções auxiliares e utilitárias, como validadores e constantes usadas ao longo do projeto.
9.  **index.js**:
    *   Arquivo principal da aplicação. Aqui o servidor é configurado, middlewares são aplicados e as rotas são carregadas.

---

### 4\. 🗄️ Configurações do Banco de dados - Em reformulação…

#### Banco de Dados: PostgreSQL

*   Nome do banco dados: `migrantes_db`
*   Host: `db_host`
*   Porta: `5432`
*   Dialeto: `postgres`
*   Usuário: `db_user`
*   Senha: `db_password`
*   CA(certificado de autoridade): `db_certificado`

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

#### Certificado SSL no Banco de Dados

A comunicação entre a aplicação **Mhelp** e o **banco de dados PostgreSQL** será protegida através de **SSL**. Isso garante que todos os dados trafegados entre o backend e o banco de dados estejam criptografados, protegendo contra ataques de interceptação e man-in-the-middle. A utilização de SSL é uma prática recomendada em ambientes onde a segurança dos dados é uma prioridade, especialmente ao lidar com informações sensíveis, como as dos migrantes e organizações.

No **arquivo de configuração do Sequelize**, a conexão com o PostgreSQL incluirá a configuração para o uso de SSL. As variáveis de ambiente serão usadas para armazenar as credenciais e certificados necessários, garantindo que as chaves e os certificados SSL não estejam expostos no código. Além disso o arquivo **ca.crt**, ficará no diretório `config`.

#### Exemplo no .env:

```plaintext
DB_CERT_CAMINHO=/caminho/para/diretorio/ca-cert.crt
```

---

### 5\. 🗃️ Estrutura do Banco de Dados

_O diagrama ainda está em fase de modificações…_

_Diagrama do Banco de dados:_ 

![](https://33333.cdn.cke-cs.com/kSW7V9NHUXugvhoQeFaf/images/7f30c9f5b1a61cb1a7b6cb55bb15c17a9d7e3da211277cd7.png)

#### Script para criação das tabelas:

_O script SQL ainda está em fase de modificações…_

```plaintext
-- Script gerado pelo MySQL Workbench em 1 de outubro de 2024

-- Desativar checagens
SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- Criar o banco de dados migrantes_db
CREATE SCHEMA IF NOT EXISTS `migrantes_db` DEFAULT CHARACTER SET utf8;
USE `migrantes_db`;

-- Tabela estado_civil
CREATE TABLE IF NOT EXISTS `estado_civil` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `descricao` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `descricao_UNIQUE` (`descricao`)
) ENGINE = InnoDB;

-- Tabela nacionalidade
CREATE TABLE IF NOT EXISTS `nacionalidade` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `descricao` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `descricao_UNIQUE` (`descricao`)
) ENGINE = InnoDB;

-- Tabela endereco
CREATE TABLE IF NOT EXISTS `endereco` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `cep` VARCHAR(10) NOT NULL,
  `cidade` VARCHAR(40) NOT NULL,
  `estado` VARCHAR(40) NOT NULL,
  `bairro` VARCHAR(100) NOT NULL,
  `logradouro` VARCHAR(150) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `cep_UNIQUE` (`cep`)
) ENGINE = InnoDB;

-- Tabela categoria
CREATE TABLE IF NOT EXISTS `categoria` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `descricao` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `descricao_UNIQUE` (`descricao`)
) ENGINE = InnoDB;

-- Tabela organizacao
CREATE TABLE IF NOT EXISTS `organizacao` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(150) NOT NULL,
  `nome_fantasia` VARCHAR(150) NOT NULL,
  `cnpj` VARCHAR(14) NOT NULL,
  `telefone_obrigatorio` VARCHAR(15) NOT NULL,
  `telefone_opcional` VARCHAR(15),
  `email` VARCHAR(100) NOT NULL,
  `descricao` VARCHAR(1000) NOT NULL,
  `numero_endereco` VARCHAR(10) NOT NULL,
  `complemento_endereco` VARCHAR(150) NOT NULL,
  `endereco_id` INT NOT NULL,
  `categoria_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `cnpj_UNIQUE` (`cnpj`),
  FOREIGN KEY (`endereco_id`) REFERENCES `endereco` (`id`),
  FOREIGN KEY (`categoria_id`) REFERENCES `categoria` (`id`)
) ENGINE = InnoDB;

-- Tabela migrante
CREATE TABLE IF NOT EXISTS `migrante` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(100) NOT NULL,
  `identificacao` VARCHAR(30),
  `registro_migrante` INT UNSIGNED NOT NULL,
  `hash_senha` VARCHAR(12) NOT NULL,
  `data_nascimento` DATE NOT NULL,
  `genero` ENUM('masculino', 'feminino', 'outro') NOT NULL,
  `profissao` VARCHAR(50) NOT NULL,
  `estado_civil_id` INT NOT NULL,
  `nacionalidade_id` INT NOT NULL,
  `organizacao_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  FOREIGN KEY (`estado_civil_id`) REFERENCES `estado_civil` (`id`),
  FOREIGN KEY (`nacionalidade_id`) REFERENCES `nacionalidade` (`id`),
  FOREIGN KEY (`organizacao_id`) REFERENCES `organizacao` (`id`)
) ENGINE = InnoDB;

-- Tabela formulario
CREATE TABLE IF NOT EXISTS `formulario` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `assunto` VARCHAR(255) NOT NULL,
  `descricao` VARCHAR(2000),
  `migrante_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  FOREIGN KEY (`migrante_id`) REFERENCES `migrante` (`id`)
) ENGINE = InnoDB;

-- Tabela usuario_ri
CREATE TABLE IF NOT EXISTS `usuario_ri` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `email` VARCHAR(100) NOT NULL,
  `hash_senha` VARCHAR(20) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `email_UNIQUE` (`email`)
) ENGINE = InnoDB;

-- Tabela documento
CREATE TABLE IF NOT EXISTS `documento` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `caminho_arquivo` VARCHAR(255) NOT NULL,
  `descricao` VARCHAR(255),
  `usuario_ri_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  FOREIGN KEY (`usuario_ri_id`) REFERENCES `usuario_ri` (`id`)
) ENGINE = InnoDB;

-- Restaurar checagens
SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```

---

### 6\. 🔁 Rotas principais da API

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

#### Rotas para PDF:

| Operação | Rota | Função | Status Code |
| --- | --- | --- | --- |
| GET | **/pdf** | Lista todos os PDFs disponíveis para download | 200 OK, 500 Internal Server Error |
| POST | **/pdf** | Salva a URL de um PDF no banco de dados | 201 Created, 400 Bad Request, 409 Conflict |

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

### 7\. 🚦 Autenticação e Armazenamento de Tokens
#### JWT (JSON WEB TOKEN)

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

### 8\. 🛠️ Validação e Tratamento de Erros

*   Um middleware será utilizado para capturar erros não tratados e retornar respostas adequadas.  
    → Utilizaremos o **Joi** para fazer a validação.

#### Fluxo proposto para o cadastro de um usuário:

1.  **Gerar uma senha alfanumérica** de **12 dígitos** usando o módulo `generate-password`.
2.  **Validar os dados de entrada** e a senha gerada usando o `Joi`.
3.  **Criptografar a senha** gerada usando o `bcrypt`.
4.  **Salvar o usuário no banco de dados** com o Sequelize.

---

### 9\. <img src="https://github.com/onemarc/tech-icons/blob/main/icons/postman.svg" width="20" height="20" alt="Postman Icon"> Testes com Postman

Realizaremos testes de todas as rodas da API utilizando o Postman, Os testes incluirão:

*   **Login e Autenticação** (validação de JWT)
*   **Operações CRUD** (migrantes, organizações)
*   **Validação de entradas inválidas**
    
    Também serão configurados testes unitários com **Mocha/Chai** para garantir que as funções principais da API estão funcionando conforme esperado.
    

---

### 10\. 🔒 Segurança 

Devemos garantir a segurança da API REST mesmo não tendo dados extremamente sensíveis e mesmo em cenários onde o número de usuários é reduzido. As seguintes práticas recomendadas podem ser implementas para fortalecer a segurança:

#### Autenticação e Autorização

*   Uso de Tokens JWT fornecidos pelo Supabase;
*   Níveis de Acesso: Definir diferentes níveis de acesso para usuários e administradores.

#### Criptografia de dados

*   Hash de Senhas: Utilizaremos o bcrypt para isso. A senha será gerada possuindo 12 caracteres. Ex: 12737193.

#### Validação de dados

*   Validação de entradas usando o **Joi;**

#### Limitação de Taxa

*   Implementar Rate Limiting: Utilizar middleware para limitar o número de requisições que um usuário pode fazerem um determinado período.

#### Proteção contra Ataque Comuns

*   Proteção contra Injeções usando uma ORM (Sequelize).

---

### 11\. <img src="https://github.com/onemarc/tech-icons/blob/main/icons/docker.svg" width="20" height="20" alt="Docker Icon"> Utilização do Docker

→ Utilizaremos o Docker como uma ferramenta essencial para o desenvolvimento e implantação da aplicação.

#### O que é Docker?

O Docker é uma plataforma que permite criar, implantar e executar aplicações em contêineres. Um contêiner é uma unidade leve e portátil que inclui tudo o que uma aplicação precisa para funcionar, como código, bibliotecas e dependências. Isso garante que a aplicação tenha um desempenho consistente em diferentes ambientes, desde o desenvolvimento até a produção.

##### **Por que usar Docker?** [://stack.desenvolvedor.expert/appendix/docker/porque.html](https://stack.desenvolvedor.expert/appendix/docker/porque.html)

---

### 12\. 🌐 Integração com APIs Externas

No desenvolvimento da aplicação Mhelp, teremos a flexibilidade de integrar diversas APIs externas que poderão enriquecer a funcionalidade do nosso sistema. Dependendo da necessidade, implementaremos uma API externa que resolva o problema.

#### Objetivos da Integração:

*   **Aprimorar a Experiência do Usuário:** Ao utilizar APIs externas, podemos oferecer dados mais precisos e atualizados, melhorando a interação entre migrantes e organizações na plataforma.
*   **Facilitar o Acesso à Informação:** Integrações com APIs de serviços poderão fornecer dados reais sobre serviços que considerarmos necessários.
*   **Aumentar a Funcionalidade do App:** Através de APIs externas, será possível adicionar funcionalidades que auxiliem e agilizem algumas tarefas.

#### Ferramentas e Tecnologias:

Para a implementação das integrações, utilizaremos a biblioteca Axios, que nos permitirá fazer requisições HTTP de forma simplificada. O fluxo de integração com qualquer API externa seguirá as etapas abaixo:

1.  **Requisição da API:** A aplicação realizará uma chamada à API externa utilizando Axios.
2.  **Processamento da Resposta:** Os dados recebidos da API serão processados e integrados à lógica de negócios do sistema.
3.  **Tratamento de Erros:** Implementaremos um tratamento para lidar com possíveis falhas nas requisições, garantindo que a aplicação continue a operar mesmo em caso de indisponibilidade de serviços externos.

#### APIs Externas:

##### **API de CEP**

Para fornecer informações precisas sobre os endereços das organizações, a aplicação Mhelp utilizará uma API externa de consulta de CEP. Essa integração permitirá que a aplicação obtenha dados como bairro, cidade e estado a partir de um CEP fornecido pelo usuário, facilitando o cadastro e a validação de endereços.

Utilizaremos a API **ViaCep** para buscar os dados de endereço.

Essa abordagem nos permitirá adaptar a aplicação de acordo com as necessidades dos usuários.

---

### 13.✅ Considerações finais

Neste documento, oferecemos uma visão abrangente do desenvolvimento da API REST para a aplicação **Mhelp**, abordando desde a arquitetura até as práticas de segurança. Embora algumas modificações ainda sejam necessárias, discutiremos essas questões em conjunto com nosso orientador e a turma para garantir que todos estejam alinhados.

Este documento servirá como um guia de referência para o desenvolvimento e manutenção da API **Mhelp**, assegurando que todas as etapas do processo sejam seguidas de maneira organizada e eficiente.
