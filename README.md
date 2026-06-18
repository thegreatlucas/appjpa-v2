# appjpa-v2 — CRM Saúde de Carteira

Sistema CRM para acompanhamento da saúde de carteira comercial — instância independente para uma nova equipe/gestor.

> Esta é uma cópia isolada do projeto [appJPA](https://github.com/thegreatlucas/appJPA), com banco de dados próprio no Supabase, sem compartilhamento de dados com a equipe original.

---

## Como configurar do zero

### 1. Criar o banco no Supabase

1. Acesse [supabase.com](https://supabase.com) e crie um **novo projeto**
2. Vá em **SQL Editor → New query**
3. Cole o conteúdo do arquivo [`supabase_setup.sql`](./supabase_setup.sql) e clique em **Run**
4. Todas as tabelas e políticas de acesso serão criadas automaticamente

### 2. Configurar as credenciais no app

No arquivo `index.html`, localize o bloco `SUPABASE CONFIG` (por volta da linha 1230) e substitua:

```js
const SUPABASE_URL = 'COLE_AQUI_A_URL_DO_SEU_PROJETO_SUPABASE';
const SUPABASE_KEY = 'COLE_AQUI_A_ANON_KEY_DO_SEU_PROJETO_SUPABASE';
```

Esses valores estão no **Dashboard Supabase → Project Settings → API**:
- **Project URL** → vai para `SUPABASE_URL`
- **anon / public key** → vai para `SUPABASE_KEY`

### 3. Deploy

Faça push para a branch `main`. O GitHub Actions irá automaticamente:
- Atualizar a data do último deploy neste README
- Publicar o app via **GitHub Pages**

Ative o GitHub Pages em: **Settings → Pages → Source: Deploy from a branch → `gh-pages`**

---

## Estrutura

```
index.html          — App completo (SPA vanilla JS + CSS)
supabase_setup.sql  — Script SQL para criar o banco (idempotente)
.github/workflows/
  deploy.yml        — CI/CD: deploy automático na main → GitHub Pages
```

---

## Tabelas do banco

| Tabela | Descrição |
|---|---|
| `usuarios` | Login, senha e role (gestor/vendedor) |
| `clientes` | Carteira de clientes com histórico |
| `contatos` | Registros de contato por cliente |
| `justificativas` | Justificativas de não-compra |
| `classificacoes` | Classificação por tipo de cliente |
| `tratativas` | Desfechos de tratativas |
| `proc_retencao_hist` | Histórico de clientes recuperados |
| `obs_coordenador` | Observações do gestor para vendedores |
| `metas` | Metas de positivação por mês |
| `positivacao_atual` | Métricas do mês atual |

---

## Roles de acesso

- **Gestor** — acesso total: importação de base, cadastro de vendedores, metas, todas as carteiras
- **Vendedor** — vê apenas sua própria carteira e registra contatos/justificativas

> **Último deploy:** 18/06/2026 20:01 (commit `8ea216d`)
