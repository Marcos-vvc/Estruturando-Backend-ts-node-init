# Estruturando-Backend-ts-node-init

🏁 Start - Criando as pastas do projeto e o index.ts

💻 Comando: `mlkdir build src`

- Já criar um arquivo TypeScript chamado index.ts dentro da pasta /src

#

## 1. Criando o tsconfig.json

💻 Comando: `tsc --init  (é preciso ter o Typescript (tsc) instalado globalmente)`
``` JSON
{
  "compilerOptions": {
    "target": "es2017", 
    "experimentalDecorators": true, 
    "emitDecoratorMetadata": true, 
    "module": "commonjs",
    "rootDir": "./src", 
    "outDir": "./dist", 
    "removeComments": true, 
    "esModuleInterop": true, 
    "forceConsistentCasingInFileNames": true, 
    "strict": true, 
    "resolveJsonModule": true,
    "skipLibCheck": true 
  }
}
```
:arrow_forward: [O que é o tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
#

## 2. Criando o package.json
💻 Comando: `npm init -y (o -y  cria um package.json com configurações padrão)`

``` JSON
// dentro do package.json podemos criar scripts. Já pode adicionar o start: 

"scripts": {
		"start": "tsc && node ./build/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
},

// o script start combina dois comandos:
// 1. tsc -> transpila os arquivos Typescript
// 2. node + [path] -> executa o arquivo passado (index.js, criado na transpilação)
```
Agora, o comando **npm start** já transpila o index.ts e executa o index.js.
#
## 3. Instalando o ts-node-dev e o typescript como dev dependencies
💻 Comando: 3 `npm i ts-node-dev -D`

💻 Comando: 4 `npm i typescript -D`
``` JSON
// dentro do package.json, adicionar um script para rodarmos o ts-node-dev:

"scripts": {
		"dev": "ts-node-dev ./src/index.ts",
		"start": "tsc && node ./build/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
},
```
Agora, o comando **npm run dev** já deixa o programa rodando sem interrupção.
#
## 4. Instalando os módulos EXPRESS e CORS
💻 Comando: 5 `npm i express cors (adicionando os dois ao mesmo tempo)`

💻 Comando: 6 `npm i @types/express @types/cors -D (+ tipos)`
``` TypeScript
// dentro do index.ts, fazer importações e ativar o Express e Cors.

import express, {Express} from 'express'
import cors from 'cors'

const app: Express = express();

app.use(express.json());
app.use(cors());

// a função express() inicia a aplicação web com express
// os .use() ativam os módulos de Bodyparser e Cors
```
#
## 5. Criando o servidor:
``` TypeScript
// esse código + essa importação para criar o servidor:
// por performance, é bom o servidor ser o último trecho de código do documento


import { AddressInfo } from "net";

const server = app.listen(process.env.PORT || 3003, () => {
    if (server) {
       const address = server.address() as AddressInfo;
       console.log(`Server is running in http://localhost: ${address.port}`);
    } else {
       console.error(`Failure upon starting server.`);
    }
});
```
#
## 6. Instalando o **Dotenv** e criando um arquivo **.env**
💻 Comando: 7 `npm i dotenv`
``` TypeScript
// importar e configurar o dotenv no index.ts

import dotenv from "dotenv";

dotenv.config();
```
Crie um arquivo .env
``` TypeScript
// no arquivo .env:

DB_HOST = 
DB_USER = 
DB_PASS = 
DB_NAME =

// DB_HOST: adicionar o endereço do localhost
// DB_USER: adicionar o user
// DB_PASS: adicionar a senha
// DB_NAME: adicionar o schema
```
#
## Exemplo Final:
``` TypeScript
// no index.ts:

import express, { Express } from "express";
import knex from "knex";
import cors from "cors";
import dotenv from "dotenv";
import { AddressInfo } from "net";

dotenv.config();

const app: Express = express();
app.use(express.json());
app.use(cors());

const server = app.listen(process.env.PORT || 3003, () => {
    if (server) {
       const address = server.address() as AddressInfo;
       console.log(`Server is running in http://localhost: ${address.port}`);
    } else {
       console.error(`Failure upon starting server.`);
    }
});
```
