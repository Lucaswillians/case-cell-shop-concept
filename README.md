# Case Cell Shop

Projeto fullstack de uma loja de capinhas para celular.

O sistema foi dividido em dois repositórios:

* Backend API
* Frontend Web

## Repositórios

### Backend API

[case-cell-shop-api](https://github.com/Lucaswillians/case-cell-shop-api?utm_source=chatgpt.com)

### Frontend Web

[case-cell-shop-web](https://github.com/Lucaswillians/case-cell-shop-web?utm_source=chatgpt.com)

---

# Tecnologias utilizadas

## Frontend

* React
* TypeScript
* React Router DOM
* TailwindCSS
* React Query
* Lucide React

## Backend

* Node.js
* NestJS
* TypeORM
* PostgreSQL
* Docker
* Jest
* redis

---

# Como rodar o projeto

## 1. Clone os repositórios

```bash
git clone https://github.com/Lucaswillians/case-cell-shop-api.git

git clone https://github.com/Lucaswillians/case-cell-shop-web.git
```

---

# Backend

Entre no projeto da API:

```bash
cd case-cell-shop-api
```

## Configure o `.env`

Crie um arquivo `.env` na raiz do projeto:

```env
DB_HOST=localhost
DB_PORT=5434
DB_USERNAME=admin
DB_PASSWORD=admin
DB_NAME=casecell
```

---

## Suba o PostgreSQL com Docker

```bash
docker compose up -d
```

O banco poderá ser acessado via:

* Beekeeper Studio
* pgAdmin
* localhost

---

## Rodar o backend

Instale as dependências:

```bash
npm install
```

Depois execute:

```bash
npm run start:dev
```

---

## Rodar os testes

```bash
npm run test
```

---

# Popular o banco com produtos

O frontend depende de produtos cadastrados previamente no banco de dados.

Após subir a API, utilize uma ferramenta como:

* Insomnia
* Postman

para criar os produtos manualmente via API.

---

# Insomnia (API Testing)

Este projeto já inclui um arquivo de configuração do Insomnia com todas as rotas da API organizadas.

---

## 📦 Arquivo incluído no projeto

Na raiz do backend, você encontrará:

```txt
/insomnia/case-cell-shop.yaml
```

Esse arquivo contém todas as requisições da API:

* Products
* Orders
* Fluxos completos de criação e consulta

---

## 📥 Instalar o Insomnia

Para testar a API, é necessário instalar o Insomnia:

👉 https://insomnia.rest/download

O Insomnia está disponível para:

* macOS
* Windows
* Linux

---

## 🚀 Como importar a collection

Após instalar o Insomnia:

1. Abra o aplicativo
2. Clique em **Import**
3. Selecione o arquivo:

```txt
case-cell-shop.yaml
```

4. Todas as rotas serão carregadas automaticamente

---

## ⚙️ Pré-requisitos para testes

Antes de usar as requisições:

### Suba o banco de dados:

```bash
docker compose up -d
```

### Inicie a API:

```bash
npm run start:dev
```

---

## Endpoint para criar produtos

```http
POST /products
```

Exemplo:

```http
POST http://localhost:3000/products
```

Body:

```json
{
  "name": "capinha macsafe",
  "description": "capa para iphone 17 macsafe",
  "quantity": 10,
  "price": 250
}
```

---

## Exemplo com outra capinha

```json
{
  "name": "capinha homem aranha",
  "description": "capa para iphone 17 tema homem aranha",
  "quantity": 40,
  "price": 50
}
```

---

Após criar os produtos, o frontend já conseguirá listar os itens automaticamente na tela inicial.

abaixo esta anexado exemplo do insomnia utilizado para baixar:

[Uploading Insomnia_2026-05-28.yaml…]()


---

# Frontend

Entre no projeto web:

```bash
cd case-cell-shop-web
```

## Instale as dependências

```bash
npm install
```

## Rode o frontend

```bash
npm run dev
```

---

# Funcionalidades

* Listagem de produtos
* Carrinho de compras
* Checkout
* Criação de pedidos
* Histórico de pedidos
* Visualização de detalhes do pedido
* Cancelamento de pedidos

---

# Fluxo da aplicação

```txt
Produtos -> Carrinho -> Checkout -> Pedido confirmado
```

---

Rotas para o back end:

# API Routes

## Products

### Listar produtos

```http id="71f7mf"
GET /products
```

Retorna todos os produtos disponíveis.

---

### Buscar produto por ID

```http id="vzzdmo"
GET /products/:id
```

Exemplo:

```http id="4g41s5"
GET /products/81fb1da9-4373-4fb8-8f1b-382c86ead671
```

---

### Criar produto

```http id="e5j21j"
POST /products
```

Body:

```json id="hqjlb6"
{
  "name": "capinha macsafe",
  "description": "capa para iphone 17 macsafe",
  "quantity": 10,
  "price": 250
}
```

---

### Atualizar produto

```http id="2h4q5j"
PATCH /products/:id
```

Body:

```json id="6h2nrv"
{
  "quantity": 5
}
```

---

### Remover produto

```http id="h1v2xh"
DELETE /products/:id
```

---

# Orders

## Listar pedidos

```http id="gc4d5o"
GET /orders
```

Retorna todos os pedidos realizados.

---

## Buscar pedido por ID

```http id="y9cn9z"
GET /orders/:id
```

Exemplo:

```http id="iholnr"
GET /orders/ea9cdf36-dabf-4f71-b145-ce6bfd27c85c
```

---

## Criar pedido

```http id="40i4mb"
POST /orders
```

Body:

```json id="y4h5v8"
{
  "customerName": "Lucas",
  "street": "Rua A",
  "city": "Barra Velha",
  "zipCode": "88390000",
  "items": [
    {
      "productId": "81fb1da9-4373-4fb8-8f1b-382c86ead671",
      "quantity": 1
    }
  ]
}
```

---

## Cancelar pedido

```http id="n5r7rf"
PATCH /orders/:id/cancel
```

Exemplo:

```http id="j0g8xr"
PATCH /orders/ea9cdf36-dabf-4f71-b145-ce6bfd27c85c/cancel
```

---

# Exemplos de resposta

## GET /orders

```json id="xj8scc"
[
  {
    "id": "ea9cdf36-dabf-4f71-b145-ce6bfd27c85c",
    "customerName": "LUCAS WILLIAN DE SOUZA SERPA",
    "street": "a",
    "city": "Joinville",
    "zipCode": "98098908",
    "status": "approved",
    "totalPrice": "250.00",
    "createdAt": "2026-05-28T22:13:10.979Z",
    "items": [
      {
        "id": "599a78d9-a55b-48c8-84c3-ef558c02768e",
        "productName": "capinha macsafe",
        "quantity": 1,
        "unitPrice": "250.00",
        "totalPrice": "250.00"
      }
    ]
  }
]
```


---

# Prompts utilizados:

## prompt para estruturação do projeto:

```
Quero que você me ajude a construir e entender um projeto fullstack de e-commerce chamado "Case Cell Shop".

Vou usar:

FRONTEND:
- React + TypeScript
- React Router DOM
- React Query (ou hooks customizados)
- TailwindCSS

BACKEND:
- Node.js com NestJS
- TypeORM
- PostgreSQL
- Docker

OBJETIVO:
Uma loja simples de capinhas de celular com fluxo completo:

1. Listagem de produtos
2. Seleção de produto
3. Carrinho de compras
4. Checkout (envio de pedido)
5. Confirmação do pedido
6. Histórico de pedidos
7. Detalhe de pedido
8. Cancelamento de pedido

---

Quero que você atue como um mentor técnico me guiando passo a passo.

Quero que você:

### 1. Me ajude a desenhar o fluxo da aplicação
- como os dados passam entre telas no frontend
- como o carrinho deve funcionar sem Redux
- como persistir estado entre rotas

### 2. Me ajude a construir o backend
- quais endpoints preciso criar primeiro
- como estruturar controllers, services e entities no NestJS
- como modelar Order com itens dentro

### 3. Me ajude a integrar frontend com backend
- como consumir API corretamente
- como lidar com loading, error e success
- como tipar corretamente as respostas

---

IMPORTANTE:
- Não pule etapas
- Explique como se eu estivesse construindo o projeto do zero
- Sempre me diga alternativas (simples vs avançado)
- Foque em boas práticas reais de mercado

Vamos começar pelo planejamento geral do sistema.
```

--- 

## prompt para enteder o relacionamento entre produtos e pedidos
```
Estou construindo um backend de e-commerce com NestJS + TypeORM + PostgreSQL.

Tenho as entidades:

- Order
- Product
- OrderItem

---

##  Objetivo

Quero entender profundamente como funciona o relacionamento entre:

- Order (pedido)
- OrderItem (itens do pedido)
- Product (produto)

---

##  Problema real

Preciso garantir que:

- Um pedido pode ter vários itens
- Cada item referencia um produto
- O item deve armazenar snapshot do preço no momento da compra
- O estoque do produto deve ser atualizado ao criar o pedido

---

##  O que quero entender antes do código

Explique como um dev senior:

1. Por que OrderItem é obrigatório nesse cenário
2. Como esse modelo funciona no banco relacional
3. Como garantir consistência de estoque + pedidos

---

##  Depois quero implementação NestJS + TypeORM

Quero ver:

### Order Entity
- id
- customerName
- address fields
- status
- totalPrice
- relation OneToMany com OrderItem

### Product Entity
- id
- name
- price
- stock

### OrderItem Entity
- id
- order (ManyToOne)
- product (ManyToOne)
- quantity
- unitPrice (snapshot)
- totalPrice

---

## Regras de negócio

- Order calcula totalPrice automaticamente
- Product stock é reduzido ao criar Order

```

---
## prompt para integração das rotas com react query

```
Quero que você me ajude a implementar e estruturar as rotas do frontend de um projeto React + TypeScript usando React Router DOM e React Query.

Estou construindo um e-commerce chamado "Case Cell Shop".

---

## STACK
- React + TypeScript
- React Router DOM v6
- React Query (TanStack Query)
- Axios (ou fetch)
- TailwindCSS

---

## FLUXO DA APLICAÇÃO

Quero essas rotas:

### Públicas
- /products → listagem de produtos
- /cart → carrinho de compras
- /checkout → confirmação do pedido
- /history → histórico de pedidos
- /history/:id → detalhe do pedido

---

## BACKEND (já existe)
Tenho uma API com as seguintes rotas:

### Products
- GET /products
- GET /products/:id
- POST /products
- PATCH /products/:id
- DELETE /products/:id

### Orders
- GET /orders
- GET /orders/:id
- POST /orders
- PATCH /orders/:id/cancel

---

## O QUE EU QUERO QUE VOCÊ FAÇA

Quero que você atue como um mentor técnico e me ajude a:

### 1. Estruturar React Query corretamente
- como criar o QueryClient
- como configurar o provider
- como organizar hooks (useProducts, useOrders etc.)

---

### 2. Criar hooks com React Query
Quero hooks organizados como:

- useProducts()
- useProduct(id)
- useOrders()
- useOrder(id)
- useCreateOrder()
- useCancelOrder()

Explique como separar query e mutation corretamente.

---

### 3. Integrar com React Router
- como passar dados entre rotas (cart → checkout)
- quando usar state vs query cache
- como evitar perda de dados no fluxo

---

### 4. Fluxo de checkout
Quero entender:
- como pegar dados do carrinho
- como enviar POST /orders
- como invalidar cache do React Query depois da compra
- como redirecionar para tela de sucesso

---

### 5. Boas práticas
- onde colocar hooks
- onde colocar services de API
- como tipar respostas corretamente
- como lidar com loading/error states

---

## IMPORTANTE
- Explique antes de codar
- Me mostre estrutura de pastas ideal
- Me mostre alternativas simples vs escaláveis
- Não pule etapas
- Pense como um dev senior me orientando

Vamos começar pela estrutura base do React Query + rotas.
```

## IA para auxilio na construção das telas

## 🤖 AI-assisted development

Parte da interface do frontend foi estruturada com auxílio da ferramenta:

- v0 by Vercel (https://v0.dev)

A ferramenta foi utilizada para acelerar a criação de componentes e layouts baseados em React + Tailwind, servindo como base inicial para evolução manual do projeto.

Todo o código foi revisado, adaptado e ajustado para se adequar à arquitetura do sistema e integração com React Query e API backend.


# Autor

Lucas Willian de Souza Serpa
