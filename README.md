# Semana OmniStack 11.0

Contém o código apresentado na Semana OmniStack 11.0 e algumas anotações sobre as aulas.

# Aula 1
  ## Iniciando a aplicação NodeJS:
    $ mkdir semana-omnistack-11
    $ cd semana-omnistack-11
    $ mkdir backend
    $ cd backend
    
   criar o arquivo `package.json`
   
    $ npm init -y
   
   instalar o framework `express` para interpretar parâmetros e configurar rotas
   
    $ npm install express
  
  ## Hello World com NodeJS:
  
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
      
   
   
