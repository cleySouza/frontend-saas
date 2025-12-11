# 🎨 Frontend — Admin Dashboard (Next.js)
### 🎯 Objetivo

Construir o painel administrativo inicial:

- Tela de login
- Integração com Auth Service
- Dashboard inicial
- Gestão básica do usuário e tenant

## 🚀 Stack Técnica

- **Next.js (App Router)**
- **React**
- **Shadcn UI**
- **TailwindCSS**
- **Axios (com interceptors)**
- **Jotai para estado global**

## 📁 Estrutura
```
apps/admin-dashboard/
├── app/
│   ├── login/
│   ├── dashboard/
│   └── layout.tsx
├── components/
├── lib/
└── package.json
```

## 🔗 Fluxos do Frontend

**Login**
- Enviar email, senha e tenantSlug
- Receber token
- Salvar token no state
- Redirecionar para dashboard

**Dashboard**
- Verificação de token
- Fetch de dados iniciais
- Layout base do painel
