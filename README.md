# 🎨 beSyS — **Documentação dos Frontends (Admin & Cliente)**

## 🌟 1. Introdução

O **beSyS** possui **dois frontends principais**, cada um projetado para um público e fluxo diferente:

1. 🖥️ **App 1 — Admin/PDV (React Web)**
2. 📱 **App 2 — Portal do Cliente (React Web ou React Native)**

Este documento descreve arquitetura, tecnologias, estrutura de pastas, UX e integrações.

---

## 🛠️ 2. Tecnologias Principais

### 🖥️ App 1 — Admin / PDV

* ⚛️ **React + Vite**
* 🧩 **TypeScript**
* 🎨 **Tailwind CSS**
* 🔄 **React Query** (fetch + cache)
* 🧠 **Zustand** para estado global
* 🧱 **ShadCN UI** (opcional, para componentes modernos)

### 📱 App 2 — Cliente

* 🌐 **React (Web)** *ou* 📱 **React Native**
* 🧩 **TypeScript**
* 🎨 **Tailwind / Nativewind**
* 🔄 **React Query**

---

## 🗂️ 3. Estrutura de Pastas

### 🖥️ Admin (Web)

```
apps/admin/
├─ public/
├─ src/
│  ├─ pages/        # Páginas principais
│  ├─ components/   # Componentes reutilizáveis
│  ├─ hooks/        # Hooks customizados
│  ├─ services/
│  │   └─ api.ts    # Instância da API
│  ├─ store/        # Zustand
│  ├─ contexts/
│  ├─ layouts/
│  ├─ utils/
│  └─ main.tsx
└─ package.json
```

### 📱 Client (Web ou Mobile)

```
apps/client/
├─ src/
│  ├─ screens/      # Telas principais
│  ├─ components/   # Botões, cards, inputs...
│  ├─ routes/       # Stack/Router
│  ├─ hooks/
│  ├─ services/
│  │   └─ api.ts
│  ├─ store/
│  ├─ utils/
│  └─ main.tsx (web) ou App.tsx (mobile)
└─ package.json
```

---

## 🛒 4. Fluxos do Cliente

### 4.1 🍽️ Cardápio

```
Cliente → Lista de produtos → Detalhes → Adicionar ao carrinho
```

### 4.2 🛍️ Carrinho

```
Carrinho → Revisão → Enviar pedido → Aguardar confirmação do PDV
```

### 4.3 📅 Agendamento

```
Seleciona serviço → Escolhe a data → Horários disponíveis
               → Enviar agendamento → Aguardar aprovação
```

---

## 🔗 5. Integração com Backend

Todas as chamadas seguem o padrão:

```
/api/v1/*
```

### 📡 Instância da API

```ts
import axios from "axios";
export const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
});
```

### 📥 Exemplo de uso

```ts
const { data } = await api.get("/products");
```

---

## 🔐 6. Autenticação

* 🔑 **JWT**
* 🔒 Armazenamento seguro: `localStorage` (web) / SecureStore (mobile)
* 🔄 Interceptors configurados com `Authorization: Bearer <token>`

---

## 🖥️ 7. UI/UX do Admin

Principais telas:

* 🔐 Login
* 📊 Dashboard
* 💳 PDV (vendas)
* 💰 Caixa
* 📅 Agenda interna
* 🛒 Produtos / Serviços
* ⚙️ Configurações da empresa

---

## 📱 8. UI/UX do Cliente

* 🏠 Home
* 🍽️ Cardápio
* 🛍️ Carrinho
* 👤 Minha conta
* 📦 Histórico de pedidos
* 📅 Agendamentos

---

## 🧭 9. Roadmap Frontend

### 🖥️ Admin

* [ ] 🎨 Tema customizável (cores, fontes, logos)
* [ ] 🖨️ Integração com impressora térmica
* [ ] ⚡ Modo offline para vendas

### 📱 Cliente

* [ ] 🔔 Push notifications
* [ ] 💳 Wallet + histórico avançado
* [ ] ✨ Modo dark opcional

---

Se quiser adicionar **diagramas**, **fluxos ilustrados**, **componentização padrão** ou **guides de UX**, posso gerar também!
