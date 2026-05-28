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

# Autor

Lucas Willian de Souza Serpa
