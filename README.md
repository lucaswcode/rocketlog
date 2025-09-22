# Rocketlog

API de entregas de encomendas construída com Node.js, Express e Prisma.

## Tecnologias principais

- **Express**: servidor HTTP
- **express-async-errors**: tratamento de erros assíncronos
- **Prisma ORM** (`@prisma/client`/`prisma`): acesso ao PostgreSQL
- **Zod**: validação de esquemas e variáveis de ambiente
- **bcrypt**: hash de senhas
- **jsonwebtoken**: autenticação via JWT
- **TypeScript** + **tsx**: desenvolvimento e execução em TS
- **Jest** + **ts-jest** + **supertest**: testes automatizados

## Arquitetura e padrões

- **Express** com camadas organizadas em `controllers`, `routes` e `middlewares`.
- **Validação** com `zod` (ex.: `src/env.ts`).
- **ORM**: Prisma com `schema.prisma`, enums e relações; migrations versionadas em `prisma/migrations`.
- **Tratamento global de erros** via middleware (`middlewares/error-handling`).

Estrutura (simplificada):

- `src/app.ts`: instancia o Express, registra middlewares e rotas
- `src/server.ts`: sobe o servidor (porta 3333)
- `src/routes/`: definição das rotas
- `src/controllers/`: controladores de cada recurso
- `src/middlewares/`: middlewares (ex.: erros, auth)
- `src/database/`, `src/configs/`, `src/utils/`, `src/types/`: apoio
- `prisma/schema.prisma`: modelos e datasource

## Requisitos

- Node.js 18+
- Docker e Docker Compose (para o PostgreSQL)

## Variáveis de ambiente

Baseie-se em `.env-example` e crie um arquivo `.env` na raiz. Principais variáveis utilizadas:

- `DATABASE_URL`: URL do PostgreSQL (ex.: `postgresql://postgres:postgres@localhost:5432/rocketlog?schema=public`)
- `JWT_SECRET`: segredo usado para assinar tokens JWT

## Banco de dados (PostgreSQL)

Suba o banco com Docker Compose (usa imagem Bitnami):

```bash
docker compose up -d
```

URL padrão esperada pelo projeto (ajuste se necessário):

```
postgresql://postgres:postgres@localhost:5432/rocketlog?schema=public
```

## Prisma

Instale dependências e gere o client/migrations:

```bash
npm install
npx prisma generate
npx prisma migrate dev
```

## Executando em desenvolvimento

```bash
npm run dev
```

- Sobe em `http://localhost:3333`
- Carrega variáveis de `.env`

## Testes

Os testes rodam com Jest/ts-jest e `supertest`.

```bash
npm run test:dev
```

- Padrão de busca: `src/**/*.test.ts`

## Scripts úteis

- `npm run dev`: desenvolvimento com `tsx watch`
- `npm run test:dev`: roda Jest em modo watch (Node em ESM com ts-jest)

## Docker Compose (referência)

Arquivo `docker-compose.yml` expõe o PostgreSQL em `5432` com usuário, senha e banco padrão (`postgres/postgres/rocketlog`).
