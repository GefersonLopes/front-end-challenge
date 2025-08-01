# XXXXXXXXXXX 🚀

> Aplicação React de XXXXXXX.

[![CI](https://github.com/seu-usuario/control361/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/seu-usuario/control361/actions/workflows/ci-cd.yml)
[![Docker](https://img.shields.io/badge/docker-ready-blue)](#docker)
[![Deploy on Vercel](https://vercel.com/button)](https://vercel.com/)

---

## 📋 Sumário

- [XXXXXXXXXXX 🚀](#xxxxxxxxxxx-)
  - [📋 Sumário](#-sumário)
  - [🧐 Sobre](#-sobre)
  - [✨ Funcionalidades](#-funcionalidades)
  - [🛠️ Pré-requisitos](#️-pré-requisitos)
  - [⚡ Instalação](#-instalação)
  - [🔑 Variáveis de Ambiente](#-variáveis-de-ambiente)
  - [🧑‍💻 Desenvolvimento Local](#-desenvolvimento-local)
  - [🐳 Uso com Docker](#-uso-com-docker)
    - [Dockerfile.dev (desenv)](#dockerfiledev-desenv)
    - [Docker Compose](#docker-compose)
  - [💻 CI/CD](#-cicd)
  - [🚀 Deploy no Vercel](#-deploy-no-vercel)
  - [🗂️ Estrutura de Pastas](#️-estrutura-de-pastas)

---

## 🧐 Sobre

Este repositório contém a aplicação **Control361**, desenvolvida em React + TypeScript, gerenciador global de estado com Zustand, formulários com React Hook Form + Zod e exibição de marcadores no mapa via Google Maps API.

---

## ✨ Funcionalidades

- Filtro por status (rastreados / outros).
- Busca por placa ou frota.
- Mapas interativos com pins e infowindows.
- Estado global via Zustand.
- Validação de formulários com Zod.

---

## 🛠️ Pré-requisitos

- **Node.js** >= 18
- **npm** >= 8
- **Docker** (para ambiente conteinerizado)
- **Docker Compose** (opcional para dev local)
- **Conta no Vercel** (para deploy)

---

## ⚡ Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/GefersonLopes/control361
   cd control361
   ```
2. Instale as dependências:
   ```bash
   npm ci
   ```
3. Crie um arquivo `.env` na raiz, copiando de `.env.example`:
   ```bash
   cp .env.example .env
   ```
4. Ajuste as variáveis de ambiente conforme necessário.

---

## 🔑 Variáveis de Ambiente

As seguintes variáveis devem estar definidas no seu `.env`:

```dotenv
VITE_GOOGLE_MAPS_API_KEY=...   # Chave da Google Maps JavaScript API
VITE_API_CLIENT_KEY=...        # Token de autenticação do client
VITE_BASE_URL_API_CLIENT=...   # URL base da API backend
VITE_GOOGLE_MAPS_COORDINATES_URL="https://www.google.com/maps/search/?api=1&query="
```

> Mantenha o `.env` fora do controle de versão!

---

## 🧑‍💻 Desenvolvimento Local

Execute em modo de desenvolvimento com Vite e hot-reload:

```bash
npm run dev        # serve http://localhost:5173/
```

Ou via Docker Compose:

```bash
docker compose up --build
#Após build, acesse http://localhost:5173
```

---

## 🐳 Uso com Docker

### Dockerfile.dev (desenv)

- **EXPOSE** 5173
- Comando: `CMD ["npm", "run", "dev"]`

### Docker Compose

```yaml
services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile.dev
    volumes:
      - ./:/app
      - /app/node_modules
    ports:
      - "5173:5173"
    environment:
      - VITE_GOOGLE_MAPS_API_KEY=${VITE_GOOGLE_MAPS_API_KEY}
      - VITE_API_CLIENT_KEY=${VITE_API_CLIENT_KEY}
      - VITE_BASE_URL_API_CLIENT=${VITE_BASE_URL_API_CLIENT}
      - VITE_GOOGLE_MAPS_COORDINATES_URL=${VITE_GOOGLE_MAPS_COORDINATES_URL}
```

Para rodar:

```bash
docker compose up --build
```

---

## 💻 CI/CD

Fluxo configurado via GitHub Actions:

1. **CI**
   - Checkout do código
   - Setup Node.js
   - Cache npm
   - `npm ci`, `npm run lint`, `npm test`, `npm run build`
   - Upload de artefato `build/`

2. **Docker Build & Push** (on push em `main`)
   - Download do build
   - `docker build -f Dockerfile` → imagem tageada por commit SHA + `latest`
   - Push no Docker Hub (opcional)

3. **Deploy no Vercel**
   - Ação `amondnet/vercel-action@v20` usando `vercel.json` e secrets:
     - VERCEL_TOKEN, VERCEL_ORG_ID, VERCEL_PROJECT_ID

Arquivo: `.github/workflows/ci-cd.yml`

---

## 🚀 Deploy no Vercel

O deploy utiliza Docker no Vercel, via `vercel.json`:

```json
{
  "version": 2,
  "builds": [{ "src": "Dockerfile", "use": "@vercel/docker" }],
  "routes": [{ "src": "/(.*)", "dest": "/" }]
}
```

Defina as mesmas variáveis de ambiente no painel Vercel (Production & Preview).

---

## 🗂️ Estrutura de Pastas

```
XXXXXXXXXXX/
├── .env.example
├── Dockerfile
├── Dockerfile.dev
├── docker-compose.yml
├── package.json
├── public/
└── src/
    ├── components/
    ├── hooks/
    ├── pages/
    ├── store/
    └── utils/
```
