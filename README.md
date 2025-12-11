# beSyS — Documentação de Arquitetura

## 1. Visão Geral

O beSyS é um sistema completo para gestão de operações comerciais, composto por backend, frontends e módulos compartilhados, organizados em um **monorepo Turborepo**. A arquitetura foi projetada para ser escalável, modular e fácil de manter.

---

## 2. Arquitetura de Alto Nível

```
                 ┌────────────────────┐
                 │   Portal Cliente   │
                 │      (App 2)       │
                 └─────────┬──────────┘
                           |
                           v
┌──────────────┐     ┌──────────────┐
│ Admin / PDV  │ --> │    Backend    │ --> PostgreSQL
│   (App 1)    │     │   (NestJS)    │
└──────┬───────┘     └──────────────┘
       |                 ▲
       └─────────────────┘
```

* **App 1 (Admin/PDV)** consome rotas autenticadas e envia eventos internos.
* **App 2 (Cliente)** envia pedidos, agendamentos e recebe confirmações.
* **Backend** centraliza regras de negócio e persistência.
* **PostgreSQL** é o banco principal.

---

## 3. Monorepo com Turborepo

Estrutura:

```
besys/
├─ apps/
│  ├─ admin/
│  ├─ client/
│  └─ backend/
├─ packages/
│  ├─ ui/
│  ├─ api-types/
│  ├─ config/
│  ├─ tsconfig/
│  └─ eslint/
└─ turbo.json
```

### Benefícios:

* Reutilização de código (UI, tipagens, regras comuns)
* Builds mais rápidos com caching
* Padronização de lint, tsconfig e libs

---

## 4. Comunicação

### 4.1 REST API

* Todas as chamadas seguem `/api/v1/...`.
* Backend expõe controllers modulares.

### 4.2 WebSockets (futuro)

* Eventos de pedidos, caixa e agenda enviados em tempo real.

---

## 5. Segurança da Arquitetura

* JWT + refresh tokens
* RBAC por roles e guards
* Sanitização de entrada
* Rate limit + CORS

---

## 6. Banco de Dados

Modelo com entidades principais:

```
User -- Company -- Product -- Order -- OrderItem
                      |          └─ CashRegister
              Appointment
```

* **Prisma** como ORM
* Migrations versionadas

---

## 7. Fluxos Principais

### 7.1 Venda no PDV

```
Operador -> Seleciona itens -> Envia venda -> API registra -> Caixa atualiza
```

### 7.2 Pedido do Cliente

```
Cliente -> Pedido -> API -> Notificação PDV -> Confirmação
```

### 7.3 Agendamento

```
Cliente -> Serviço -> Data/hora -> API valida -> PDV aprova
```

---

## 8. Deploy

### Backend

* Docker + Postgres
* CI/CD GitHub Actions

### Frontend

* Admin: Vercel ou Netlify
* Cliente: Vercel (web) ou Play Store/TestFlight (mobile)

### Banco

* Railway, Render, Supabase ou RDS

---

## 9. Roadmap de Arquitetura

* [ ] Adicionar mensageria (Kafka/NATS) em escala
* [ ] Multi-tenancy completo (esquema por empresa)
* [ ] CDN para assets
* [ ] Cache Redis
