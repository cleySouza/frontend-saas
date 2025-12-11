# beSyS — Documentação dos Frontends (Admin & Cliente)

## 1. Introdução

O beSyS possui **dois frontends**:

1. **App 1 — Admin/PDV (React Web)**
2. **App 2 — Portal do Cliente (React Web ou React Native)**

Este documento detalha a arquitetura, pastas, tecnologias e integrações.

---

## 2. Tecnologias Principais

### App 1 — Admin / PDV

* **React + Vite**
* **TypeScript**
* **Tailwind CSS**
* **React Query** para chamadas à API
* **Zustand** para estado
* **ShadCN (opcional)**

### App 2 — Cliente

* **React (Web)** ou **React Native**
* **TypeScript**
* **Tailwind (ou Nativewind no mobile)**
* **React Query**

---

## 3. Estrutura de Pastas

### Admin (Web)

```
apps/admin/
├─ public/
├─ src/
│  ├─ pages/
│  ├─ components/
│  ├─ hooks/
│  ├─ services/
│  │   └─ api.ts
│  ├─ store/
│  ├─ contexts/
│  ├─ layouts/
│  ├─ utils/
│  └─ main.tsx
└─ package.json
```

### Client (Web ou Mobile)

```
apps/client/
├─ src/
│  ├─ screens/
│  ├─ components/
│  ├─ routes/
│  ├─ hooks/
│  ├─ services/
│  │   └─ api.ts
│  ├─ store/
│  ├─ utils/
│  └─ main.tsx (web) ou App.tsx (mobile)
└─ package.json
```

---

## 4. Fluxos do Cliente

### 4.1 Cardápio

```
[Cliente] -> Lista de produtos -> Detalhe -> Adicionar ao carrinho
```

### 4.2 Carrinho

```
Carrinho -> Revisão -> Enviar pedido -> Aguardar confirmação
```

### 4.3 Agendamento

```
Seleciona serviço -> Escolhe data -> Horários disponíveis -> Enviar agendamento
```

---

## 5. Integração com Backend

Todas as chamadas seguem padrão:

```
/api/v1/*
```

Helpers de consumo:

```ts
import axios from "axios";
export const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
});
```

Uso:

```ts
const { data } = await api.get("/products");
```

---

## 6. Autenticação

* Login via **JWT**
* Armazenamento seguro: `localStorage` (web) / SecureStore (mobile)
* Interceptor adiciona `Authorization: Bearer token`

---

## 7. UI/UX do Admin

Principais telas:

* Login
* Dashboard
* PDV (vendas)
* Caixa
* Agenda interna
* Produtos/serviços
* Configurações da empresa

---

## 8. UI/UX do Cliente

* Home
* Cardápio
* Carrinho
* Minha conta
* Histórico de pedidos
* Agendamentos

---

## 9. Roadmap Frontend

### Admin

* [ ] Tema customizável
* [ ] Impressão/PDV
* [ ] Modo offline

### Cliente

* [ ] Push notifications
* [ ] Wallet / histórico avançado
