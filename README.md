# Semana OmniStack 11.0

Contém o código apresentado na Semana OmniStack 11.0 e algumas anotações sobre as aulas.

# Aula 1
  ## Iniciando a aplicação NodeJS
    $ mkdir ws-omnistack-11.0
    $ cd ws-omnistack-11.0
    $ mkdir backend
    $ cd backend
    
   criar o arquivo `package.json`
   
    $ npm init -y
   
   instalar o framework `express` para interpretar parâmetros e configurar rotas
   
    $ npm install express
  
  ## Hello World com NodeJS
  
   criar arquivo `index.js` dentro da pasta `backend`, este será o arquivo principal da aplicação
   
   importando as funcionalidades do `express`
      
      const express = require('express');
   
   variável para armazenar aplicação
   
      const app = express();
      
   configurar a variável para acesso em `localhost:3333`
   
      app.listen(3333);
      
   executando aplicação
   
      $ node index.js
      
   obs: ao acessar `localhost:3333` têm-se o erro `cannot GET /` por nenhuma rota ter sido definida
   
   definindo rotas com `json`
   
      const app = express();
      
      app.get('/', (request, response) => {
          return response.json({
            evento: "Semana OmniStack 11.0",
            aluno: "Giovana Niehues"
          });
      });
 
  ## Iniciando React
  
   sair da pasta `backend`
   
      $ cd ..
   
   criando a estrutura básica do React na pasta `frontend` e entrar na pasta
   
      npx create-react-app frontend
      cd frontend
      
   iniciando a aplicação
   
      $ npm start
      
   modificar a linha `11` do arquivo `src/App.js` para alterar a mensagem apresentada para
   
      <p>
        Olá Mundo!
      </p>
      
 # Aula 2
   ## Acessar a pasta backend e iniciar a aplicação
   
      $ cd ws-omnistack-11.0 
      $ cd backend
      $ node index.js
      
   acessar a aplicação em `localhost:3333`
   
   na rota `localhost:3333/users`, `/users` é o recurso. O recurso geralmente está associado com uma tabela no banco de dados ou entidade
   
  ## Métodos HTTP
    
   **GET:** Buscar/listar uma informação do backend. Sempre é requisitado ao acessar uma rota
   **POST:** Criar uma informação no backend
   **PUT:** Alterar uma informação no backend
   **DELETE:** Deletar uma informação no backend
   
   em `backend/index.js`, alterar o método `GET` para `POST` e adicionar o recurso `/users`, da seguinte forma:
   
     app.post('/users', (request, response) => {
        return response.json({
          evento: "Semana OmniStack 11.0",
          aluno: "Giovana Niehues"
        });
   
   apenas o método `get` é acessado através da requisição de rota do navegador, portanto, para visualizar o retorno dos outros métodos será utilizado o aplicativo [Insomnia](https://insomnia.rest/)
   
   após instalar o aplicativo, abrir o mesmo e criar uma nova requisição com `CTRL + N` e selecionar o método `POST`
   
   inserir a rota `http://localhost:3333/users` e selecionar `SEND` para observar o resultado do `JSON` enviado pelo backend. Obs: reiniciar o node
   
## Tipos de Parâmetros

   em `backend/index.js`, voltar o método de `POST` para `GET`, da seguinte forma:
   
      ```
     app.get('/users', (request, response) => {
        return response.json({
          evento: "Semana OmniStack 11.0",
          aluno: "Giovana Niehues"
        });
        ```
   
   **Query Paramns:** Parâmetros nomeados enviados na rota após o símbolo "?" (Filtros, paginação, etc). Ex: `http://localhost:3333/users?page=2&name=Giovana&idade=20`

   no `Insomnia`, alterar o método de `POST` para `GET` e inserir a rota `http://localhost:3333/users?aluno=Giovana`, verificar a resposta `JSON`

   para visualizar requisições, alterar o trecho de código no `index.js` para 
      
      app.get('/users', (request, response) => {
      const params = request.query;

      console.log(params);

      return response.json({
         evento: 'Semana OmniStack 11.0',
         aluno: 'Giovana Niehues'
      });
      });
      

   após isso, no `Insomnia`, alterar a rota para `http://localhost:3333/users?name=Giovana` e verificar a requisição no console

   **Route Params:** Parâmetros utilizados para identificar recursos
  
  para visualizar requisições, alterar o trecho de código no `index.js` para 
      
      app.get('/users/:id', (request, response) => {
      const params = request.params;

      console.log(params);

      return response.json({
         evento: 'Semana OmniStack 11.0',
         aluno: 'Giovana Niehues'
      });
      });
      


   após isso, no `Insomnia`, alterar a rota para `http://localhost:3333/users/1` e verificar a requisição no console

   **Request Body:** Corpo da requisição, utilizado para criar ou alterar recursos

   alterar o trecho no `index.js` para 

      app.post('/users', (request, response) => {
      const body = request.body;

      console.log(body);

      return response.json({
         evento: 'Semana OmniStack 11.0',
         aluno: 'Giovana Niehues'
      });
      });

   e adicionar no início do fonte, para que o `node` possa transformar o `JSON` num objeto `JavaScript` e mostrá-lo em sua saída no console

      app.use(express.json());

   no `Insomnia`, alterar o método de `GET` para `Post` e `Body` para `JSON`, inserir a rota `http://localhost:3333/users` e digitar no corpo da requisição

      {
         "name": "Giovana Niehues",
         "idade": 20
      }
   
   verificar o resultado no console

## Nodemon

   o nodemon automatiza a reinicialização do `node` toda vez em que um arquivo é alterado. Para instalar o `nodemon`

      $ npm install nodemon -D

   a opção `-D` do comando significa que irá adicionar o `nodemon` apenas para desenvolvimento

   no arquivo `backend/package.json` alterar a linha `7` de

      "test": "echo \"Error: no test specified\" && exit 1"

   para

      "start": "nodemon index.js"

   assim, pode-se iniciar o `node` com 

      $ npm start

## Bancos de Dados

   **SQL:** MySQL, SQLite, PostgreSQL, Oracle, Microsoft SQL Server (Bancos de dados relacionais)
   
   **NoSQL:** MongoDB, CouchDB, etc (Bancos de dados não relacionais)

   o banco utilizado será o `SQLite`

   ### Maneiras de utilizar o SQL:

   **Driver:** Requisições utilizando linguagem `SQL`
   **Query Builder:** Requisições escritas em javascript (Ao mudar de banco de `SQL` não é neccessário realizar alterações na query)

   utilizaremos o [Knex.JS](http://knexjs.org/) como builder. Para instalação do mesmo basta realizar os seguintes comandos

      $ npm install knex --save
      $ npm install sqlite3

   para a criação do arquivo de configuração do banco de dados `knexfile.js` execute o seguinte comando

      $ npx knex init

## Organizar arquivos

   antes de iniciar o desenvolvimento do backend, adicionar os arquivos criados para a pasta `backend/src/`
   * criar a pasta `backend/src/`
   * adicionar o arquivo `index.js` para a pasta `src`
   * alterar em `package.json` para o novo caminho de index.js
      start": "nodemon src/index.js"
   * criar, dentro da pasta `src` o arquivo `routes.js` para armazenar as rotas da aplicação
   * mover as rotas para o arquivo `routes` e importar o mesmo para o arquivo `index.js`

   código do arquivo `routes.js` até agora

      const express = require('express');
      const routes = express.Router();

      routes.post('/users', (request, response) => {
      const body = request.body;

      console.log(body);

      return response.json({
         evento: 'Semana OmniStack 11.0',
         aluno: 'Giovana Niehues'
      });
      });

      module.exports = routes;  

   código do arquivo `index.js` até agora

      const express = require('express');
      const routes = require('./routes');

      const app = express();

      app.use(express.json());
      app.use(routes);

      app.listen(3333);

   criar a pasta `database` dentro de `src` e modificar o arquivo `knexfile.js` para

      development: {
         client: 'sqlite3',
         connection: {
            filename: './src/database/db.sqlite'
         }
      },

   obs: nas rotas `./` significa que o arquivo indicado está na mesma pasta. Para voltar uma pasta seria `../` e assim por diante

### Entidades
   breve análise de entidades que serão as tabelas do banco de dados

   * **ONG**
   * **Caso (Incident)**

### Funcionalidades

   * Login de ONG
   * Logout de ONG
   * Cadastro de ONG
   * Cadastrar novos casos
   * Deletar casos
   * Listar casos específicos de uma ONG

### Mobile

   * Listar todos os casos
   * Entrar em contato com a ONG (WhatsApp e Email)

## Criar as tabelas

   as tabelas serão criadas utilizando a funcionabilidade `mobile` do pacote `knex`
   
   * criar a pasta `migrations` dentro de `database`
   * modificar o arquivo `knexfile.js` e adicionar, abaixo de connextion

       migrations: {
         directory: './src/database/migrations'
      }

   para criar a tabela `ONGS` (create_ongs.js), executar o comando

      $ npx knex migrate:make create_ongs

   para que não ocorra o aviso apresentado no console, adicionar no arquivo `knexfile.js` após migrations:

      useNullAsDefault: true,

   utilizando a documentação do [Knex.JS](http://knexjs.org/) pode-se criar a tabela `ongs` no arquivo criado `create_ongs`. obs: procurar por ".primary" pode ajudar a achar a documentação necessária

   no arquivo `create_ongs` modificar o método `up`, responsável pela criação da tabela, inserindo os campos da tabela com seus tipos

      exports.up = function(knex) {
      return knex.schema.createTable('ongs', function (table) {
         table.string('id').primary();
         table.string('name').notNullable();
         table.string('email').notNullable();
         table.string('whatsapp').notNullable();
         table.string('city').notNullable();
         table.string('uf', 2).notNullable();
      });
      };

   o método `down` serve para deletar a tabela caso ocorra algum problema, portanto, modificar o metodo `down` da seguinte forma

      exports.down = function(knex) {
         return knex.schema.dropTable('ongs');
      };

   para executar o código e criar a tabela no banco de dados, executar

      $ npx knex migrate:latest

   criar a próxima tabela 

      $ npx knex migrate:make create_incidents

   no arquivo `create_incidents`, modificar para

      exports.up = function(knex) {
      return knex.schema.createTable('incidents', function (table) {
         table.increments();

         table.string('title').notNullable();
         table.string('description').notNullable();
         table.decimal('value').notNullable();

         table.string('ong_id').notNullable();

         table.foreign('ong_id').references('id').inTable('ongs');
      });
      };

      exports.down = function(knex) {
      return knex.schema.dropTable('incidents');
      };

   obs: a tabela `incidents` possui um campo de identificação autoincrementável e está relacionada a tabela `ongs` pela chave estrangeira `ong_id`

   e para executar o código e criar a tabela no banco de dados, executar o comando

      $ npx knex migrate:latest

   para descobrir os comandos no knex basta executar

      $ npx knex

   caso faça algo errado e queira voltar atrás, executar

      $ npx knex migrate:rollback

### Criar rotas para cadastrar ONGS no banco de dados

   alterar o recurso no arquivo `routes.js` para `/ongs`. Como é um método para adicionar algo no banco, o método usado é `POST`

      routes.post('/ongs', (request, response) => {
      const data = request.body;

      console.log(data);

      return response.json();
      });

   no `Insomnia` deletar a requisição teste e criar uma pasta chamada `ONGS`, criar uma requisição chamada `Create` dentro da pasta `ONGS` com método `POST` e corpo `JSON`. Adicionar a rota `http://localhost:3333/ongs`

   no corpo da requisição do `Insomnia` adicionar o seguinte trecho e enviar, visualizar o retorno no console

      {
         "name": "FRADA",
         "email": "frada@gmail.com",
         "whatsapp": "988058728",
         "city": "Joinville",
         "uf": "SC"
      }

   alterar o arquivo `routes.js`

      const express = require('express');
      const crypto = require('crypto');
      const routes = express.Router();

      routes.post('/ongs', (request, response) => {
      const {name, email, whatsapp, city, uf } = request.body;

      const id = crypto.randomBytes(4).toString('HEX');

      return response.json();
      });

      module.exports = routes;

   criar o arquivo `connections.js` dentro da pasta `database` para estabelecer a conexão com o banco

      const knex = require('knex');
      const configuration = require('../../knexfile');

      const connection = knex(configuration.development);

      module.exports = connection;

   importar `connections.js` para `routes.js`

      const express = require('express');
      const crypto = require('crypto');
      const connection = require('./database/connections')
      const routes = express.Router();

      routes.post('/ongs', async (request, response) => {
      const {name, email, whatsapp, city, uf } = request.body;

      const id = crypto.randomBytes(4).toString('HEX');

      await connection('ongs').insert({
         id,
         name,
         email,
         whatsapp,
         city,
         uf,
      });

      return response.json({ id });
      });

      module.exports = routes;

   novamente acesse o `Insomnia` e execute a requisição. Caso dê erro por não encontrar a tabela `ongs`, deletar o arquivo `db.sqlite` e executar novamente o comando

      $ npx knex migrate:latest

   então executar novamente a requisição no `Insomnia` e verificar que o `id` da `ong` é retornado

   adicionar no arquivo `routes.js` o seguinte trecho 

      routes.get('/ongs', async (request, response) => {
      const ongs = await connection('ongs').select('*');

      return response.json(ongs);
      });

   no `Insomnia`, duplicar a requisição existente e nomear a nova requisição como "List", com método `GET` e `No Body`. Então enviar a requisição e verificar que a ONG foi cadastrada no banco de dados

   -- tempo de aula 1:01:20



   


   


    

   

   


   




   


      
      
   
