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
mkdir src/routes src/controllers src/services src/config src/models src/middlewares
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

# 14. Buildar a imagem Docker

Executar:

```bash
docker build -t docker-api-aula .
```

---

# 15. Executar container Docker

```bash
docker run -p 3000:3000 docker-api-aula
```

---

# 16. Testar aplicação Dockerizada

Acessar:

```text
http://localhost:3000
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
