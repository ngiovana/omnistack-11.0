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

   importar `connections.js` para `routes.js` e adicionar o seguinte trecho para cadastro de ongs

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

   adicionar no arquivo `routes.js` o seguinte trecho para a listagem de ongs

      routes.get('/ongs', async (request, response) => {
      const ongs = await connection('ongs').select('*');

      return response.json(ongs);
      });

   no `Insomnia`, duplicar a requisição existente e nomear a nova requisição como "List", com método `GET` e `No Body`. Então enviar a requisição e verificar que a ONG foi cadastrada no banco de dados

## Reorganização
   
   criar a pasta `controllers` dentro de `src` e colocar a lógica de cadastro e listagem de ONGS que está em `routes` para o arquivo `OngController.js`, dentro da pasta `controllers`
  
   ### OngController.js

      const connection = require('../database/connections');
      const crypto = require('crypto');

      module.exports = {

      async index(request, response) {
         const ongs = await connection('ongs').select('*');
      
         return response.json(ongs);
      },
      
      async create(request, response) {
         const {name, email, whatsapp, city, uf } = request.body;

         const id = crypto.randomBytes(4).toString('HEX');

         await connection('ongs').insert({
            id,
            name,
            email,
            whatsapp,
            city,
            uf,
         })

         return response.json({ id });
      }
      };

   assim, `routes.js` fica 

      const express = require('express');

      const OngController = require('./controllers/OngController');
      
      const routes = express.Router();

      routes.get('/ongs', OngController.index); 

      routes.post('/ongs', OngController.create);

      module.exports = routes;os métodos que serão exportados desse arquivo para arquivos que utilizarem `OngController.js`

   * em `module exports` estão os métodos que serão exportados aos arquivos que utilizarem `OngController.js`

## Cadastro de incidents
   
   criar o arquivo `IncidentController.js` dentro da pasta `controllers`

   ### IncidentController.js

      const connection = require('../database/connections');

      module.exports = {
      async create(request, response ) {
         const { title, description, value } = request.body;
         const ong_id = request.headers.authorization;

         const [id] = await connection('incidents').insert({
            title,
            description,
            value,
            ong_id,
         });

         return response.json({id});
      }
      };

   a lógica é quase a mesma do arquivo `OngController.js`, porém em `IncidentController.js` utiliza-se header para pegar o valor de `ong_id`, que seria o id da ONG responsável por cadastrar o Incident

   ### routes.js

      const express = require('express');

      const OngController = require('./controllers/OngController');
      const IncidentController = require('./controllers/IncidentController');

      const routes = express.Router();

      routes.get('/ongs', OngController.index); 
      routes.post('/ongs', OngController.create);

      routes.post('/incidents', IncidentController.create);

      module.exports = routes;

   adicionar também a lógica de listagem de incidentes no arquivo `IncidentController.js`, conforme o seguinte trecho

      async index(request, response) {
         const incidents = await connection('incidents').select('*');

         return response.json(incidents);
      },

   e em `routes.js` adicionar o trecho

      routes.get('/incidents', IncidentController.index);

   no `Insomnia`, criar uma pasta chamada `Incidents` e criar uma requisição chamada `Create` com método `POST`, `JSON` e rota `http://localhost:3333/incidents`. Em `Header` adicionar um content-Type `Authorization` e application/json com o ID de uma ong cadastrada. Enviar e verificar que o ID do incident é retornado.

   então, duplicar a requisição, dar nome de `List` com método `GET`, `No Body` e enviar. Verificar que os dados do incidente são retornados.

   ### adicionar o método delete ao IncidentController.js

   no método `delete` deve-se buscar o `id` do incident e o `ong_id` para verificar se o incidente pertence a ong que está logada

   assim em `IncidentController.js` adicionar o trecho

      async delete(request, response) {
      const { id } = request.params; // busca a id do incidente
      const ong_id = request.headers.authorization; // busca a id da ong
      
      const incident = await connection('incidents')
      .where('id', id) // id da requisição igual o id do parametro
      .select('ong_id') // selecionar a coluna ong_id
      .first();

      // se o ong_id do incidente for diferente do ong_id que está logado na aplicação mostra erro
      if (incident.ong_id != ong_id) {
         return response.status(401).json({ error: 'Operation not permitted.' });
      }
      
      await connection('incidents').where('id', id).delete();
      return response.status(204).send();
      
      }

   em `routes.js` adicionar

      routes.delete('/incidents/:id', IncidentController.delete);

   no `Insomnia` duplicar a requisição `Create` da pasta `Incidents` com o nome `Delete` método `Delete`, `No Body`, rota `http://localhost:3333/incidents/1` e em `Header` manter o ID da ong. Obs: caso o id seja diferente não será possível deletar e a mensagem de erro será apresentada.

   enviar e verificar que foi deletado o incidente.

   para listar todos os casos de uma ONG, dentro de `controllers` deve ser criado o arquivo `ProfileController.js` da seguinte forma

      const connection = require('../database/connections');

      module.exports = {
      async index(request, response) {
         const ong_id = request.headers.authorization;

         const incidents = await connection('incidents')
         .where('ong_id', ong_id)
         .select('*');

         return response.json(incidents);
      }
      }

   no `Insomnia` criar uma nova requisição fora das pastas chamada `Profile` com método `GET`, `No Body`, rota `http://localhost:3333/Profile` e, em `Header`, `Authorization` e o ong_id. enviar e verificar que os incidentes da ONG serão listados

   em `routes.js` adicionar os trechos
      
      const ProfileController = require('./controllers/ProfileController');

   e

      routes.get('/profile', ProfileController.index);

### Login da ONG

   para realizar o login da ONG, o arquivo `SessionController.js` deve ser criado na pasta `controllers`, da seguinte forma 

      const connection = require('../database/connections');

      module.exports = {
      async create(request, response) {
         const { id } = request.body;

         const ong = await connection('ongs')
         .where('id', id)
         .select('name')
         .first();

         if(!ong) {
            return response.status(400).json({ error: 'No ONG found with this ID'});
         }

         return response.json(ong);
      }
      }

   em `routes.js` deve ser adicionado os trechos

      const SessionController = require('./controllers/SessionController');

   e

      routes.post('/sessions', SessionController.create);

   no `Insomnia`, dupliccar o `Profile` com nome `Login`, método `POST`, corpo `JSON`, rota `http://localhost:3333/session` e no corpo executar (substituindo o <ong_id> pelo id)

      {
         "id": "<ong_id>"
      }  

   verificar que o nome da ONG foi retornado

### Paginação

   em `IncidentController.js`, para que o método de listagem (index) apresente apenas 5 incidentes por página, deve-se modificar para

      async index(request, response) {
         const { page = 1 } = request.query

         const [count] = await connection('incidents').count(); // conta o número total de incidents

         const incidents = await connection('incidents')
         .join('ongs','ongs.id', '=', 'incidents.ong_id') // id da ong = id do incidente 
         .limit(5)
         .offset((page - 1) * 5) // mostra a cada 5 registros
         .select(['incidents.*', 'ongs.name', 'ongs.email', 'ongs.whatsapp', 'ongs.city', 'ongs.uf']); // seleciona todos os campos de incidents e alguns de ongs, para que o id de ongs não se sobreponha ao id no incident

         response.header('X-Total-Count', count['count(*)']); // Apresenta o total de incidents

         return response.json(incidents);
      },

   no `Insomnia`, cadastrar mais de 5 incidents e listá-los, verificar que na primeira página apenas os primeiros 5 serão listados. Ao adicionar ao recurso `?page=2`, os próximos 5 serão listados, e assim por diante. Em `Header` perceber a presença do item `X-Total-Count` contendo o valor total de incidents

   no terminal, com `CTRL + C` fechar o servidor e instalar o `CORS` para deeterminar quem pode acessar a aplicação com o seguinte comando

      $ npm install cors

   em `index.js` importar o cors com 

      const cors = require('cors');

   e adicionar 

      app.use(cors());

   caso estivesse em produção, seria

      app.use(cors(
         origin: 'http://www.exemplo.com'
      ));

# Aula 3

### Organizando a estrutura

   acessar a pasta frontend

      $ cd frontend
      $ code .

   deletar arquivos que não serão usados neste momento, como `README.md`, `App.css`, `App.test.js`, `index.css`, `logo.svg`, `serviceWorker.js` e `setupTests.js`

   em `index.js` remover as importações dos arquivos `index.css` e `serviceWorker.js` já que os mesmos foram removidos

   remover também o comentários e a chamada do serviceWorker

   em `App.js` remover também as importações dos arquivos deletados e o conteúdo html. No lugar desse conteúdo digitar

      <h1>Hello World</h1>

   dentro da pasta `public`, deletar os arquivos `robots.txt`, `manifest.json` e as logos

   modificar `index.html` para

      <!DOCTYPE html>
      <html lang="en">
      <head>
         <meta charset="utf-8" />
         <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
         <meta name="viewport" content="width=device-width, initial-scale=1" />
         <meta name="theme-color" content="#000000" />
         
         <title>Be The Hero</title>
      </head>
      <body>
         <noscript>You need to enable JavaScript to run this app.</noscript>
         <div id="root"></div>
      </body>
      </html>

   executar o seguinte comando no terminal para executar a aplicação

      $ npm start

   um componente no React é uma função que retorna HTML, JSX é quando o HTML está integrado ao JavaScript

   ## Propriedades

   quando um código se repetir muitas vezes na aplicação ou puder ser isolado sem resultar em diferença no restante da aplicação cria-se um componente novo. Componentes devem ter a primeira letra maiúscula

   criar em `src` um componente `Header.js`

   importar o React com

      import React from 'react';
   
   adicionar em `Header.js` o seguinte trecho

      export default function Header(props) {
      return (
         <header>
            <h1>{props.title}</h1>
         </header>
      );
      }

   após isso, em `App.js` importar a `Header` e substituir a linha que contém o `<h1>Hello World</h1>` por

       <Header title="Semana OmniStack"/>

   obs: ao usar JavaScript no "meio" de HTML sempre deve-se usar chaves {}
   
   * props.children pega todo o texto dentro da tag Header

   ## Estado

   toda vez que o estado for alterado o componente remonta exibindo as novas informações em tela

## Login

   criar uma pasta em `src` chamada `assets` para armazenar a logo e imagens utilizadas

   criar em `src` a pasta `pages` e dentro desta pasta, a pasta `Logon`

   em `Logon` criar os arquivos `index.js` e `styles.css`

   deletar `Header.js` e criar um arquivo em `scr` chamado `global.css` para estilizações obtidas em todas as páginas

   acessar Google Fonts, selecionar o fonte Roboto e em customize selecionar regular 400, medium 500 e bold 700

   em Embed e @Import copiar o import para `global.css`

### Rotas

Instalar o seguinte pacote para lidar com rotas

   $ npm install react-router-dom

e criar em `src` o arquivo `routes.js` para as rotas das páginas

## Conectar o backend com o frontend

   no terminal, acessar a pasta `backend` e dar start no servidor

      $ cd ../backend
      $ npm start

   instalar o cliente http para fazer as chamadas da API axios, com o seguinte comando

      $ npm install axios

   criar em `src` uma pasta `services` e, dentro desta pasta, o arquivo `api.js`, onde será importado o axios e informado a baseURL 

# Aula 3
   
   ## Mobile

   o primeiro passo é instalar o Expo, que vai ser utilizado para criar e visualizar projetos

      $ sudo npm install -g expo-cli

   para criar o projeto com nome `mobile`, executar o seguinte comando

      $ expo init mobile

   entrar na pasta mobile e executar com 

      $ cd mobile
      $ yarn start

   baixar o expo no celular e conectar via qrcode 

   em `mobile/app.json` mudar o `name` para Be The Hero e `slug` para bethehero, pois este não pode conter espaços ou acentos

   o React Native não possui as mesmas tags do HTML, não existe a semântica. O React Native possui a classe `StyleSheet` que tem o método `create` que pode ser utilizado para a criação dos estilos

   todos os elementos possuem `display: flex` como padrão. Escreve-se no estilo camel case 

   não existe herança de estilos no React Native

   acessar a documentação do [React Navigation](https://reactnavigation.org/docs/getting-started)

   para fazer as rotas, instalar o react navigation com o seguinte comando

      $ npm install @react-navigation/native

   para instalar o restante dos pacotes, executar o seguinte comando

      $ expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view

   Acessar [Hello World Navigator](https://reactnavigation.org/docs/hello-react-navigation) e instalar o stack navigator com o seguinte comando

      $ npm install @react-navigation/stack

   para estilização, instalar

      $ expo install expo-constants

   para utilizar o email, instalar o pacote

      $ expo install expo-mail-composer

   para conectar com a API, instalar também o axios no mobile

      $ npm install axios

   para lidar com o valor, executar

      $ npm install intl   

# Aula 4

   para realizar as validações, instalar o celebrate

      $ npm i celebrate

   para testar, instalar o jest com o seguinte comando

      $ npm install jest

   após a instalação, inciar o jest com 

      $ npx jest --init 
      
   respostas das perguntas: Y, node, N, Y

   testes de integração testam o fluxo da rota inteira de integração, testa funcionalidades por completo

   testes unitários testam pedaços da aplicação de forma isolada

   para executar o teste, basta executar

      $ npm test

   para o teste de integração, executar

      $ npm install cross-env

## Deploy
 ### Backend: Node
   * Aplicação experimental, objetivo de teste:  [heroku](https://www.heroku.com/) [tutorial de hospedagem heroku](https://www.youtube.com/watch?v=-j7vLmBMsEU)

   * aplicação maior: [digital ocean](https://www.digitalocean.com/) [deploy digital ocean](https://www.youtube.com/watch?v=ICIz5dE3Xfg)

## Frontend: React

* aplicações pequenas e para testes : [netlify](https://www.netlify.com/)

## Mobile

* [video gerando apk](https://www.youtube.com/watch?v=wYMvzbfBdYI)

## Estudos daqui pra frente:
   * Padrões de código: ESLint, Prettier 
   * Autenticação JWT
   * Style Components
   

   
