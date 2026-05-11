# Guia Completo — Estrutura Inicial de API Node.js + Docker

# Objetivo

Este guia apresenta um passo a passo completo para preparar a estrutura inicial de uma API utilizando:

- Node.js
- Express
- Docker
- Docker Compose

A proposta é criar um ambiente moderno e preparado para expansão futura com:

- MongoDB
- APIs RESTful
- Autenticação
- Deploy
- Microsserviços

---

# 1. Instalar o Node.js

Baixe a versão LTS do Node.js:

https://nodejs.org

Após instalar, verifique no terminal:

```bash
node -v
```

```bash
npm -v
```

---

# 2. Criar a pasta do projeto

```bash
mkdir docker-api-aula
```

```bash
cd docker-api-aula
```

---

# 3. Inicializar o projeto Node.js

```bash
npm init -y
```

Isso criará automaticamente o arquivo:

```text
package.json
```

---

# 4. Instalar dependências principais

Instalar Express e dotenv:

```bash
npm install express dotenv
```

Instalar nodemon para desenvolvimento:

```bash
npm install nodemon --save-dev
```

---

# 5. Criar a estrutura inicial

Criar pasta principal:

```bash
mkdir src
```

Criar subpastas:

```bash
mkdir src/routes,src/controllers,src/services,src/config,src/models,src/middlewares
```

Estrutura esperada:

```text
docker-api-aula/
│
├── src/
│   ├── config/
│   ├── controllers/
│   ├── middlewares/
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── app.js
│
├── package.json
└── package-lock.json
```

---

# 6. Criar o arquivo principal da aplicação

Criar:

```text
src/app.js
```

Conteúdo:

```javascript
require('dotenv').config()

const express = require('express')

const app = express()

app.use(express.json())

app.get('/', (req, res) => {
  res.json({
    message: 'API funcionando com Node.js, Express e Docker'
  })
})

const PORT = process.env.PORT || 3000

app.listen(PORT, () => {
  console.log(`Servidor rodando na porta ${PORT}`)
})
```

---

# 7. Configurar scripts do package.json

Editar o arquivo:

```text
package.json
```

Conteúdo:

```json
{
  "name": "docker-api-aula",
  "version": "1.0.0",
  "main": "src/app.js",

  "scripts": {
    "start": "node src/app.js",
    "dev": "nodemon src/app.js"
  },

  "dependencies": {
    "dotenv": "^16.0.0",
    "express": "^4.18.2"
  },

  "devDependencies": {
    "nodemon": "^3.0.0"
  }
}
```

---

# 8. Criar o arquivo .env

Criar:

```text
.env
```

Conteúdo:

```env
PORT=3000
```

---

# 9. Testar a API localmente

Executar:

```bash
npm run dev
```

Acessar no navegador:

```text
http://localhost:3000
```

Resposta esperada:

```json
{
  "message": "API funcionando com Node.js, Express e Docker"
}
```

---

# 10. Instalar Docker

## Windows

Instalar:

- Docker Desktop

Verificar instalação:

```bash
docker --version
```

```bash
docker compose version
```

---

# 11. Criar o Dockerfile

Na raiz do projeto, criar:

```text
Dockerfile
```

Conteúdo:

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

# 12. Explicando o Dockerfile

## FROM

Imagem base:

```dockerfile
FROM node:20-alpine
```

---

## WORKDIR

Define diretório interno:

```dockerfile
WORKDIR /app
```

---

## COPY

Copia arquivos:

```dockerfile
COPY . .
```

---

## RUN

Executa comandos:

```dockerfile
RUN npm install
```

---

## EXPOSE

Documenta porta:

```dockerfile
EXPOSE 3000
```

---

## CMD

Comando inicial:

```dockerfile
CMD ["npm", "start"]
```

---

# 13. Criar o .dockerignore

Criar:

```text
.dockerignore
```

Conteúdo:

```text
node_modules
npm-debug.log
.git
.env
```

---

# 17. Criar docker-compose.yml

Criar:

```text
docker-compose.yml
```

Conteúdo:

```yaml
services:

  api:
    build: .

    container_name: docker_api_aula

    ports:
      - "3000:3000"

    environment:
      - PORT=3000
```

---

# 18. Executar Docker Compose

Subir ambiente:

```bash
docker compose up --build
```

Rodar em background:

```bash
docker compose up -d --build
```

---

# 19. Derrubar ambiente

```bash
docker compose down
```

---

# 20. Estrutura Final Esperada

```text
docker-api-aula/
│
├── src/
│   ├── config/
│   ├── controllers/
│   ├── middlewares/
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── app.js
│
├── .dockerignore
├── .env
├── Dockerfile
├── docker-compose.yml
├── package.json
└── package-lock.json
```

---

# 21. Fluxo Completo do Projeto

## Desenvolvimento local

```bash
npm run dev
```

## Build Docker

```bash
docker build -t docker-api-aula .
```

## Rodar container

```bash
docker run -p 3000:3000 docker-api-aula
```

## Rodar com Compose

```bash
docker compose up --build
```

---

# 22. Próximos Passos

Após esta estrutura inicial, o projeto pode evoluir para:

- MongoDB
- APIs RESTful completas
- CRUD
- JWT
- Swagger
- Redis
- Nginx
- CI/CD
- Deploy em nuvem
- Kubernetes

---

# 23. Boas Práticas

- Utilizar `.dockerignore`
- Utilizar imagens Alpine
- Separar ambientes
- Utilizar variáveis de ambiente
- Não salvar segredos no código
- Utilizar Docker Compose para múltiplos serviços
- Modularizar a API

---

# 24. Principais Comandos Docker

| Comando | Função |
|---|---|
| docker build | buildar imagem |
| docker run | executar container |
| docker ps | listar containers |
| docker stop | parar container |
| docker rm | remover container |
| docker logs | visualizar logs |
| docker exec | acessar container |
| docker compose up | subir ambiente |
| docker compose down | derrubar ambiente |

---

# 25. Resultado Esperado

Ao final deste processo o aluno será capaz de:

- Criar APIs Node.js
- Dockerizar aplicações
- Trabalhar com containers
- Criar ambientes reproduzíveis
- Utilizar Docker Compose
- Preparar aplicações modernas para deploy

---

# 26. Adicionando MongoDB ao Projeto com Docker Compose

Nesta etapa, o projeto deixa de executar apenas a API e passa a executar dois serviços:

- API Node.js
- Banco de dados MongoDB

A comunicação entre eles será feita pelo Docker Compose.

---

# 27. Instalar Mongoose

O Mongoose será utilizado para conectar a API ao MongoDB e criar schemas/models.

```bash
npm install mongoose
```

---

# 28. Atualizar o arquivo .env

Atualize o arquivo:

```text
.env
```

Conteúdo:

```env
PORT=3000
MONGO_URL=mongodb://mongo:27017/docker_api_aula
```

## Explicação

```text
mongo
```

é o nome do serviço MongoDB definido no `docker-compose.yml`.

Dentro da rede do Docker Compose, a API acessa o banco pelo nome do serviço, e não por `localhost`.

---

# 29. Criar arquivo de conexão com o MongoDB

Criar o arquivo:

```text
src/config/database.js
```

Conteúdo:

```javascript
const mongoose = require('mongoose')

async function connectDatabase() {
  try {
    await mongoose.connect(process.env.MONGO_URL)

    console.log('MongoDB conectado com sucesso')
  } catch (error) {
    console.error('Erro ao conectar no MongoDB:', error.message)
    process.exit(1)
  }
}

module.exports = connectDatabase
```

---

# 30. Atualizar o arquivo src/app.js

Substitua o conteúdo de:

```text
src/app.js
```

por:

```javascript
require('dotenv').config()

const express = require('express')
const connectDatabase = require('./config/database')

const app = express()

app.use(express.json())

connectDatabase()

app.get('/', (req, res) => {
  res.json({
    message: 'API funcionando com Node.js, Express, Docker e MongoDB'
  })
})

const PORT = process.env.PORT || 3000

app.listen(PORT, () => {
  console.log(`Servidor rodando na porta ${PORT}`)
})
```

---

# 31. Criar um Schema/Model de Exemplo

Criar o arquivo:

```text
src/models/task.model.js
```

Conteúdo:

```javascript
const mongoose = require('mongoose')

const taskSchema = new mongoose.Schema(
  {
    title: {
      type: String,
      required: true,
      trim: true
    },

    description: {
      type: String,
      trim: true
    },

    completed: {
      type: Boolean,
      default: false
    }
  },
  {
    timestamps: true
  }
)

module.exports = mongoose.model('Task', taskSchema)
```

---

# 32. Atualizar o docker-compose.yml com MongoDB

Substitua o conteúdo do arquivo:

```text
docker-compose.yml
```

por:

```yaml
services:

  api:
    build: .

    container_name: docker_api_aula

    ports:
      - "3000:3000"

    env_file:
      - .env

    depends_on:
      - mongo

    volumes:
      - .:/app
      - /app/node_modules

  mongo:
    image: mongo:latest

    container_name: mongo_db_aula

    ports:
      - "27017:27017"

    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

---

# 33. Explicando o docker-compose.yml com MongoDB

## Serviço api

Representa a aplicação Node.js.

```yaml
api:
  build: .
```

O Docker Compose constrói a imagem da API usando o `Dockerfile`.

## Serviço mongo

```yaml
mongo:
  image: mongo:latest
```

Cria um container usando a imagem oficial do MongoDB.

## depends_on

```yaml
depends_on:
  - mongo
```

Indica que a API depende do serviço MongoDB.

## volume do MongoDB

```yaml
volumes:
  - mongo_data:/data/db
```

Garante persistência dos dados do banco.

Mesmo que o container seja removido, os dados continuam salvos no volume.

---

# 34. Subir API + MongoDB

Executar:

```bash
docker compose up --build
```

Ou em segundo plano:

```bash
docker compose up -d --build
```

---

# 35. Verificar containers em execução

```bash
docker ps
```

Resultado esperado:

```text
docker_api_aula
mongo_db_aula
```

---

# 36. Ver logs da API

```bash
docker compose logs api
```

---

# 37. Ver logs do MongoDB

```bash
docker compose logs mongo
```

---

# 38. Acessar o container da API

```bash
docker exec -it docker_api_aula sh
```

---

# 39. Acessar o container do MongoDB

```bash
docker exec -it mongo_db_aula mongosh
```

Dentro do MongoDB:

```javascript
show dbs
```

```javascript
use docker_api_aula
```

```javascript
show collections
```

---

# 40. Estrutura Final com MongoDB

```text
docker-api-aula/
│
├── src/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   ├── middlewares/
│   ├── models/
│   │   └── task.model.js
│   ├── routes/
│   ├── services/
│   └── app.js
│
├── .dockerignore
├── .env
├── Dockerfile
├── docker-compose.yml
├── package.json
└── package-lock.json
```

---

# 41. Fluxo da Aplicação com Docker + MongoDB

```text
Navegador/Postman
        ↓
API Node.js
        ↓
Mongoose
        ↓
MongoDB
        ↓
Volume Docker
```

---

# 42. Comandos Principais do Pipeline com MongoDB

| Comando | Função |
|---|---|
| `npm install mongoose` | instala integração com MongoDB |
| `docker compose up --build` | sobe API e MongoDB |
| `docker compose up -d --build` | sobe em background |
| `docker compose logs api` | mostra logs da API |
| `docker compose logs mongo` | mostra logs do MongoDB |
| `docker compose down` | remove containers |
| `docker volume ls` | lista volumes |
| `docker exec -it mongo_db_aula mongosh` | acessa MongoDB |

---

# 43. Resultado Esperado

Ao final desta etapa, o aluno terá:

- API Node.js dockerizada
- MongoDB executando em container
- Conexão da API com o banco
- Schema criado com Mongoose
- Persistência de dados com volume Docker
- Ambiente reproduzível com Docker Compose
