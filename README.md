# 📋 Kanban Board — Sistema de Gerenciamento de Tarefas

Um quadro Kanban interativo e completo com autenticação JWT, drag & drop, prioridades, controle de prazos e dashboard em tempo real.

![Node.js](https://img.shields.io/badge/Node.js-v18+-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-4.18-000000?style=flat-square&logo=express&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-FB015B?style=flat-square&logo=jsonwebtokens&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

---

## ✨ Funcionalidades

- **🔐 Autenticação Segura** — Registro e login com senhas criptografadas via `bcrypt` e tokens JWT com expiração de 8h
- **📊 Dashboard Interativo** — Contadores em tempo real de tarefas totais, em andamento, concluídas e em atraso
- **🖱️ Drag & Drop** — Arraste tarefas entre colunas (A Fazer → Fazendo → Concluído) para atualizar o status
- **🏷️ Prioridades** — Classifique tarefas como Baixa, Média ou Alta com indicadores visuais coloridos
- **📅 Controle de Prazos** — Defina datas limite com detecção automática de tarefas em atraso
- **✏️ CRUD Completo** — Crie, edite, exclua e marque tarefas como concluídas
- **🚪 Logout com Revogação** — Tokens são revogados ao sair, impedindo reutilização
- **📱 Responsivo** — Layout adaptável para desktop e mobile

---

## 🛠️ Stack Tecnológica

| Camada     | Tecnologia                        |
|------------|-----------------------------------|
| **Backend**  | Node.js + Express 4.18           |
| **Auth**     | JWT (jsonwebtoken) + bcrypt      |
| **Frontend** | HTML5 + CSS3 + JavaScript Vanilla |
| **Dados**    | Persistência em arquivos JSON    |
| **Fonte**    | JetBrains Mono (Google Fonts)    |

---

## 🚀 Como Executar

### Pré-requisitos

- [Node.js](https://nodejs.org/) v18 ou superior
- npm (incluído com o Node.js)

### Instalação

```bash
# 1. Clone o repositório
git clone https://github.com/Druydan/kanbansabadoagoravai.git

# 2. Acesse a pasta do projeto
cd kanbansabadoagoravai

# 3. Instale as dependências
npm install

# 4. Inicie o servidor
npm start
```

O servidor iniciará em **http://localhost:3000**

> 💡 Para desenvolvimento com hot-reload, use `npm run dev` (requer `nodemon` instalado globalmente).

---

## 📁 Estrutura do Projeto

```
kanbansabadoagoravai/
├── public/
│   └── index.html          # Frontend completo (SPA)
├── server.js               # Servidor Express + API REST
├── users.json              # Banco de dados de usuários
├── tasks.json              # Banco de dados de tarefas
├── revoked_tokens.json     # Tokens JWT revogados
├── package.json            # Dependências e scripts
├── .gitignore              # Arquivos ignorados pelo Git
└── README.md               # Este arquivo
```

---

## 🔗 Endpoints da API

### Autenticação

| Método | Rota                   | Descrição              | Auth |
|--------|------------------------|------------------------|------|
| POST   | `/api/auth/register`   | Cadastrar novo usuário | ❌    |
| POST   | `/api/auth/login`      | Fazer login            | ❌    |
| POST   | `/api/auth/logout`     | Revogar token (logout) | ✅    |

### Tarefas (rotas protegidas 🔒)

| Método | Rota                        | Descrição                          |
|--------|-----------------------------|------------------------------------|
| GET    | `/api/tasks`                | Listar todas as tarefas do usuário |
| POST   | `/api/tasks`                | Criar nova tarefa                  |
| PUT    | `/api/tasks/:id`            | Editar tarefa existente            |
| DELETE | `/api/tasks/:id`            | Excluir tarefa                     |
| PATCH  | `/api/tasks/:id/status`     | Atualizar status (drag & drop)     |
| PATCH  | `/api/tasks/:id/complete`   | Alternar conclusão da tarefa       |

> Todas as rotas protegidas exigem o header: `Authorization: Bearer <token>`

---

## 📦 Dependências

| Pacote           | Versão  | Uso                                  |
|------------------|---------|--------------------------------------|
| `express`        | ^4.18.2 | Framework HTTP para o servidor       |
| `bcrypt`         | ^5.1.1  | Hash seguro de senhas                |
| `jsonwebtoken`   | ^9.0.2  | Geração e validação de tokens JWT    |
| `cors`           | ^2.8.5  | Habilitar Cross-Origin requests      |

---

## 🎨 Interface

O design utiliza uma paleta escura inspirada em IDEs modernas:

- **Fundo**: `#0a0a0f` — tom escuro profundo
- **Destaque**: `#6c63ff` — roxo vibrante para ações principais
- **Sucesso**: `#22c55e` — verde para tarefas concluídas
- **Alerta**: `#f59e0b` — amarelo para tarefas em andamento
- **Perigo**: `#ff4444` — vermelho para atrasos e exclusões

---

## 📝 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar, modificar e distribuir.

---

<p align="center">
  Desenvolvido por <a href="https://github.com/Druydan">@Druydan</a>
</p>
