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

---

# 44. Interface Visual para o MongoDB

Até aqui toda a interação com o banco foi feita via terminal.

Para ambientes de desenvolvimento e ensino, uma interface gráfica acelera a exploração dos dados, facilita a leitura dos documentos e reduz erros de digitação em queries.

Nesta etapa o projeto ganha um terceiro serviço: o **Mongo Express**.

## O que é o Mongo Express

Mongo Express é uma interface web open-source escrita em Node.js que se conecta a qualquer instância MongoDB e roda diretamente no browser.

Equivalência com outras ferramentas:

| Banco | Ferramenta visual |
|---|---|
| PostgreSQL | pgAdmin |
| MySQL | phpMyAdmin |
| MongoDB | Mongo Express |

## O que é possível fazer

- Visualizar bancos e collections em tempo real
- Ler, criar, editar e deletar documentos
- Executar queries sem abrir o terminal
- Exportar e importar dados em JSON

---

# 45. Atualizar o docker-compose.yml com Mongo Express

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

  mongo-express:
    image: mongo-express:latest

    container_name: mongo_express_aula

    ports:
      - "8081:8081"

    environment:
      ME_CONFIG_MONGODB_SERVER: mongo
      ME_CONFIG_MONGODB_PORT: 27017
      ME_CONFIG_BASICAUTH_USERNAME: admin
      ME_CONFIG_BASICAUTH_PASSWORD: admin123
      ME_CONFIG_OPTIONS_EDITORTHEME: dracula

    depends_on:
      - mongo

    restart: unless-stopped

volumes:
  mongo_data:
```

---

# 46. Explicando o Serviço mongo-express

## image

```yaml
image: mongo-express:latest
```

Usa a imagem oficial do Mongo Express do Docker Hub.

Não é necessário criar um `Dockerfile` para ela.

---

## ports

```yaml
ports:
  - "8081:8081"
```

Expõe a interface web na porta `8081` do host.

O acesso será feito em:

```text
http://localhost:8081
```

---

## environment

Variáveis que configuram a conexão e o acesso:

| Variável | Função |
|---|---|
| `ME_CONFIG_MONGODB_SERVER` | Nome do serviço MongoDB na rede Docker |
| `ME_CONFIG_MONGODB_PORT` | Porta do MongoDB |
| `ME_CONFIG_BASICAUTH_USERNAME` | Usuário para login na interface |
| `ME_CONFIG_BASICAUTH_PASSWORD` | Senha para login na interface |
| `ME_CONFIG_OPTIONS_EDITORTHEME` | Tema do editor de documentos |

---

## depends_on

```yaml
depends_on:
  - mongo
```

O Mongo Express aguarda o MongoDB iniciar antes de subir.

---

## restart

```yaml
restart: unless-stopped
```

Reinicia o container automaticamente em caso de falha, sem precisar rodar `docker compose up` novamente.

---

## Por que o servidor é "mongo" e não "localhost"

Dentro da rede do Docker Compose, cada serviço é acessado pelo nome declarado no arquivo.

`localhost` dentro de um container aponta para o próprio container, nunca para outro serviço.

---

# 47. Subir o Ambiente com os Três Serviços

Executar:

```bash
docker compose up --build
```

Ou em segundo plano:

```bash
docker compose up -d --build
```

---

# 48. Verificar os Três Containers em Execução

```bash
docker ps
```

Resultado esperado:

```text
docker_api_aula
mongo_db_aula
mongo_express_aula
```

---

# 49. Acessar o Mongo Express

Abrir no navegador:

```text
http://localhost:8081
```

Credenciais de acesso:

```text
Usuário: admin
Senha:   admin123
```

O que será exibido na interface:

- Lista de todos os bancos de dados
- Collections dentro de cada banco
- Documentos em formato JSON com paginação
- Botões para criar, editar e deletar documentos
- Editor de queries com syntax highlighting

---

# 50. Ver Logs do Mongo Express

```bash
docker compose logs mongo-express
```

---

# 51. Estrutura Final com Mongo Express

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
├── docker-compose.yml      ← inclui mongo-express
├── package.json
└── package-lock.json
```

---

# 52. Fluxo da Aplicação com Interface Visual

```text
Navegador/Postman
        ↓
API Node.js  (:3000)
        ↓
   Mongoose
        ↓
   MongoDB  (:27017)
        ↓
Volume Docker

             ↑
  Mongo Express (:8081)
  [acesso visual direto ao banco]
```

---

# 53. Schema do Model Task

O model `Task` foi criado em `src/models/task.model.js`.

Abaixo está a estrutura completa de cada campo armazenado na collection `tasks`.

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `_id` | ObjectId | Auto | Gerado automaticamente pelo MongoDB |
| `title` | String | Sim | Título da tarefa. Trim aplicado. |
| `description` | String | Não | Descrição detalhada. Trim aplicado. |
| `completed` | Boolean | Não | Status de conclusão. Default: `false` |
| `createdAt` | Date | Auto | Gerado por `timestamps: true` |
| `updatedAt` | Date | Auto | Atualizado automaticamente no save |

---

# 54. O que é ObjectId

O `_id` é gerado automaticamente pelo MongoDB em formato hexadecimal de 24 caracteres.

Exemplo:

```text
"_id": "64abc1234def5678901234ab"
```

---

# 55. O que são timestamps

A opção `{ timestamps: true }` instrui o Mongoose a adicionar e gerenciar automaticamente os campos `createdAt` e `updatedAt`.

Não é necessário declarar esses campos no Schema.

---

# 56. Exemplo de Documento no MongoDB

Um documento da collection `tasks` armazenado no banco tem este formato:

```json
{
  "_id":         "64abc1234def5678901234ab",
  "title":       "Estudar Docker",
  "description": "Finalizar o módulo de Docker Compose",
  "completed":   false,
  "createdAt":   "2024-01-15T10:30:00.000Z",
  "updatedAt":   "2024-01-15T10:30:00.000Z",
  "__v":         0
}
```

O campo `__v` é o `versionKey` adicionado pelo Mongoose para rastrear versões do documento.

---

# 57. Queries Básicas — Create

## Criar um documento

```javascript
const task = await Task.create({
  title: 'Estudar Docker',
  description: 'Ver aula de Docker Compose',
  completed: false
})
```

---

## Criar múltiplos documentos

```javascript
const tasks = await Task.insertMany([
  { title: 'Tarefa 1' },
  { title: 'Tarefa 2', completed: true },
  { title: 'Tarefa 3', description: 'Com descrição' }
])
```

---

# 58. Queries Básicas — Read

## Buscar todos os documentos

```javascript
const tasks = await Task.find()
```

---

## Buscar por ID

```javascript
const task = await Task.findById('64abc...')
```

---

## Buscar com filtro

```javascript
// Apenas tasks concluídas
const done = await Task.find({ completed: true })

// Apenas tasks pendentes
const pending = await Task.find({ completed: false })
```

---

## Ordenar resultados

```javascript
// Mais recentes primeiro
const tasks = await Task
  .find()
  .sort({ createdAt: -1 })
```

---

## Selecionar campos específicos

```javascript
// Retorna apenas title e completed
const tasks = await Task
  .find()
  .select('title completed')
```

---

# 59. Filtros e Busca Avançada

## Busca por texto com regex

```javascript
const tasks = await Task.find({
  title: { $regex: 'docker', $options: 'i' }
})
```

A opção `i` torna a busca insensível a maiúsculas e minúsculas.

---

## Paginação com skip e limit

```javascript
const page  = 2   // página desejada
const limit = 10  // itens por página

const tasks = await Task
  .find()
  .skip((page - 1) * limit)
  .limit(limit)
  .sort({ createdAt: -1 })
```

---

## Operadores de comparação

| Operador | Significado | Exemplo |
|---|---|---|
| `$eq` | igual a | `{ completed: { $eq: true } }` |
| `$ne` | diferente de | `{ completed: { $ne: true } }` |
| `$gt` | maior que | `{ count: { $gt: 5 } }` |
| `$gte` | maior ou igual | `{ count: { $gte: 5 } }` |
| `$lt` | menor que | `{ count: { $lt: 10 } }` |
| `$in` | dentro de lista | `{ status: { $in: ['a', 'b'] } }` |
| `$nin` | fora de lista | `{ status: { $nin: ['c'] } }` |

---

# 60. Queries Básicas — Update

## Atualizar um documento por ID

```javascript
const updated = await Task.findByIdAndUpdate(
  '64abc...',
  { $set: { completed: true } },
  { new: true, runValidators: true }
)
```

## Explicação das opções

```text
new: true          → retorna o documento APÓS a atualização
runValidators: true → aplica as validações definidas no Schema
```

---

## Atualizar múltiplos documentos

```javascript
await Task.updateMany(
  { completed: false },
  { $set: { completed: true } }
)
```

---

## Operadores de update

| Operador | Função | Exemplo |
|---|---|---|
| `$set` | Define valor de campo | `{ $set: { title: 'Novo' } }` |
| `$unset` | Remove campo do documento | `{ $unset: { description: '' } }` |
| `$inc` | Incrementa número | `{ $inc: { views: 1 } }` |
| `$push` | Adiciona item a array | `{ $push: { tags: 'novo' } }` |
| `$pull` | Remove item de array | `{ $pull: { tags: 'antigo' } }` |

---

# 61. Queries Básicas — Delete

## Deletar por ID

```javascript
await Task.findByIdAndDelete('64abc...')
```

---

## Deletar com filtro

```javascript
// Remove todas as tasks concluídas
await Task.deleteMany({ completed: true })

// Remove apenas uma task que corresponda ao filtro
await Task.deleteOne({ title: 'Tarefa antiga' })
```

---

# 62. Aggregate Pipeline

O Aggregate Pipeline é a forma mais poderosa de consulta no MongoDB.

Ele processa documentos em etapas chamadas stages, onde a saída de uma etapa alimenta a próxima.

---

## Contar tasks por status

```javascript
const stats = await Task.aggregate([
  {
    $group: {
      _id: '$completed',
      total: { $sum: 1 }
    }
  }
])

// Resultado:
// [{ _id: false, total: 7 }, { _id: true, total: 3 }]
```

---

## Tasks criadas por dia

```javascript
const byDay = await Task.aggregate([
  {
    $group: {
      _id: {
        $dateToString: {
          format: '%Y-%m-%d',
          date: '$createdAt'
        }
      },
      count: { $sum: 1 }
    }
  },
  { $sort: { _id: -1 } }
])
```

---

## Pipeline com múltiplos stages

```javascript
// Tasks recentes não concluídas — top 5
const result = await Task.aggregate([
  { $match:   { completed: false } },
  { $sort:    { createdAt: -1 } },
  { $limit:   5 },
  { $project: { title: 1, createdAt: 1 } }
])
```

---

## Stages mais utilizados

| Stage | Função |
|---|---|
| `$match` | Filtra documentos (equivalente ao WHERE) |
| `$group` | Agrupa e calcula ($sum, $avg, $count) |
| `$sort` | Ordena os resultados |
| `$limit` | Limita a quantidade de documentos |
| `$skip` | Pula N documentos (paginação) |
| `$project` | Seleciona ou calcula campos |
| `$lookup` | Faz JOIN com outra collection |
| `$unwind` | Expande arrays em documentos separados |

---

# 63. Visualizando Dados via Mongo Express

## Navegar até a collection tasks

- Acesse `http://localhost:8081`
- Clique no banco `docker_api_aula`
- Clique na collection `tasks`
- Os documentos serão exibidos em JSON com paginação

---

## Criar um documento pela interface

- Clique em **New Document**
- Preencha o JSON no editor
- Clique em **Save**

---

## Editar um documento

- Clique no ícone de lápis ao lado do documento
- Edite os campos no editor JSON
- Clique em **Save**

---

## Executar uma query personalizada

- Clique em **Find** no topo da collection
- Digite o filtro no campo Query:

```json
{ "completed": false }
```

- Clique em **Find** para executar

---

# 64. Comandos Principais desta Etapa

| Comando | Função |
|---|---|
| `docker compose up --build` | sobe API, MongoDB e Mongo Express |
| `docker compose up -d --build` | sobe em background |
| `docker compose logs mongo-express` | mostra logs do Mongo Express |
| `docker compose down` | remove todos os containers |
| `http://localhost:8081` | acessa interface do Mongo Express |
| `Task.create({ title: '...' })` | cria um documento |
| `Task.find()` | busca todos os documentos |
| `Task.findById(id)` | busca por ID |
| `Task.find({ completed: true })` | busca com filtro |
| `Task.find().sort({ createdAt: -1 })` | busca ordenada |
| `Task.find().skip(10).limit(5)` | paginação |
| `Task.findByIdAndUpdate(id, { $set: {...} })` | atualiza por ID |
| `Task.updateMany({}, { $set: {...} })` | atualiza em massa |
| `Task.findByIdAndDelete(id)` | remove por ID |
| `Task.deleteMany({ completed: true })` | remove com filtro |
| `Task.aggregate([...])` | executa pipeline de aggregation |

---

# 65. Resultado Esperado

Ao final desta etapa, o aluno terá:

- Três serviços rodando em Docker Compose: API, MongoDB e Mongo Express
- Interface visual para explorar e editar dados sem usar o terminal
- Schema do model Task completamente documentado
- Domínio das operações CRUD com Mongoose
- Uso de filtros, paginação e seleção de campos
- Queries de update com operadores `$set`, `$unset`, `$inc`
- Queries de aggregate com múltiplos stages
- Fluxo completo: API → Mongoose → MongoDB → Mongo Express

---

# 66. Próximos Passos

Após esta estrutura, o projeto pode evoluir para:

- Controllers e Services separados para o CRUD de tasks
- Rotas RESTful completas (GET, POST, PUT, DELETE)
- Validação de dados com Joi ou express-validator
- Autenticação com JWT
- Documentação automática com Swagger / OpenAPI
- Cache com Redis
- Testes automatizados com Jest e Supertest
- CI/CD com GitHub Actions
- Deploy em nuvem (Railway, Render, AWS, GCP)
- Kubernetes para orquestração em produção
