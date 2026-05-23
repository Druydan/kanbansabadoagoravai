# 🚀 Guia de Deploy no Render — Kanban Board

Este guia contém todas as informações e o passo a passo necessário para realizar o deploy com sucesso da aplicação Kanban na plataforma **Render**. 

O projeto foi revisado e totalmente padronizado com as melhores práticas de produção, incluindo suporte a variáveis de ambiente (`process.env`) e persistência segura de dados.

---

## 🛠️ Alterações de Padronização Realizadas

Para preparar a aplicação para a nuvem, as seguintes modificações foram implementadas no código-fonte:

1. **Porta Dinâmica (`server.js`)**:
   - Alterado de `3000` fixo para `process.env.PORT || 3000`. O Render define automaticamente a porta ideal na variável `PORT`.
2. **Chave Secreta JWT Segura (`server.js`)**:
   - O segredo do JWT agora consome `process.env.SECRET_KEY`. Caso não esteja configurado, utiliza um fallback seguro apenas para desenvolvimento.
3. **Caminho de Banco de Dados Flexível (`server.js`)**:
   - Criada a variável de ambiente `DATA_DIR` (`process.env.DATA_DIR || __dirname`). Isso permite apontar os arquivos de banco de dados (`users.json`, `tasks.json`, `revoked_tokens.json`) para um **Disco Persistente** no Render, evitando perda de dados a cada restart do servidor.
4. **URL da API Relativa (`public/index.html`)**:
   - A constante `API_URL` foi mudada de `http://localhost:3000/api` para simplesmente `/api` (URL relativa). A aplicação agora detecta e consome o próprio domínio de onde está sendo executada, eliminando erros de CORS no navegador em produção.

---

## 💾 O Desafio da Persistência (Flat-File JSON)

Como este projeto utiliza arquivos locais `.json` como banco de dados:
* ⚠️ **Aviso**: Por padrão, instâncias gratuitas no Render possuem um sistema de arquivos *efêmero* (reseta a cada deploy ou quando o servidor entra em modo de suspensão após inatividade).
* 🛡️ **Solução**: Para garantir que seus usuários e tarefas criados **nunca sejam perdidos**, utilizaremos a funcionalidade de **Persistent Disk** (Disco Persistente) do Render ou definiremos a pasta de persistência em um diretório montado.

---

## 📋 Passo a Passo para o Deploy no Render

Siga as etapas abaixo para colocar sua aplicação no ar em poucos minutos:

### Passo 1: Enviar as Atualizações para o GitHub
Certifique-se de que os novos arquivos e correções estão atualizados no seu repositório:
```bash
git add -A
git commit -m "chore: preparar projeto para deploy no Render"
git push origin main
```

### Passo 2: Criar um Novo Web Service no Render
1. Acesse o painel do [Render](https://dashboard.render.com/) e faça login.
2. Clique no botão **New +** (no canto superior direito) e selecione **Web Service**.
3. Conecte sua conta do GitHub (caso ainda não esteja conectada) e selecione o repositório **`kanbansabadoagoravai`** (ou o nome do seu repositório ativo).

### Passo 3: Configurar os Parâmetros Básicos do Serviço
Na tela de criação, preencha com as seguintes informações:

*   **Name**: `kanban-jwt` (ou outro nome de sua escolha)
*   **Region**: Selecione a mais próxima de você (ex: `Ohio (us-east-2)` ou `Frankfurt`)
*   **Branch**: `main`
*   **Language/Runtime**: `Node`
*   **Build Command**: `npm install`
*   **Start Command**: `npm start`
*   **Instance Type**: `Free` (ou superior)

### Passo 4: Configurar Variáveis de Ambiente (Environment Variables)
Role a página até a seção **Advanced** e clique em **Add Environment Variable**. Adicione as seguintes chaves:

| Key | Value | Descrição |
| :--- | :--- | :--- |
| `NODE_ENV` | `production` | Define que o Node está rodando em modo produção. |
| `SECRET_KEY` | `sua-chave-ultra-secreta-aqui` | Uma senha longa e aleatória usada para assinar os tokens JWT de login. |
| `DATA_DIR` | `/data` | **(Crucial)** Aponta o diretório dos arquivos JSON para o disco persistente que montaremos a seguir. |

### Passo 5: Adicionar um Disco Persistente (Opcional - Recomendado)
*Nota: Discos persistentes no Render exigem o plano pago básico (Starter), mas garantem que as tarefas nunca sumam. Se usar a versão 100% Free, os dados durarão até a máquina reiniciar.*

Para adicionar o disco (caso utilize plano pago):
1. Ainda na aba **Advanced** de criação (ou nas configurações após o deploy), localize a opção **Disks**.
2. Clique em **Add Disk**.
3. Configure:
   *   **Name**: `kanban-storage`
   *   **Mount Path**: `/data`
   *   **Size**: `1 GiB` (mais que suficiente para milhares de arquivos de texto json).
4. Salve a configuração.

### Passo 6: Iniciar o Deploy!
1. Clique no botão **Create Web Service** no final da página.
2. O Render iniciará a build e o download das dependências. Acompanhe os logs no painel.
3. Quando a mensagem `Your service is live` aparecer, seu sistema estará totalmente online!

---

## 🧪 Como Testar a Aplicação Online

1. O Render fornecerá uma URL pública parecida com: `https://kanban-jwt.onrender.com`.
2. Abra essa URL no seu navegador.
3. Clique em **REGISTRAR** e crie uma conta de teste.
4. Faça o login e tente adicionar tarefas, trocar prioridades e arrastá-las entre as colunas.
5. Faça o logout para garantir que a revogação de tokens JWT está funcionando normalmente.

---
<p align="center">
  Pronto para o lançamento! 🚀
</p>
