# ⚡ TaskFlow — Sua Produtividade em Outro Nível

O **TaskFlow** é um gerenciador de tarefas moderno, construído com a estética "Obsidian Glass" (dark mode premium) e focado em uma experiência de usuário fluida e poderosa. Integrado com **Supabase** para persistência real e autenticação segura.

![Dashboard Preview](https://vfuanaecbqobocstsgzh.supabase.co/storage/v1/object/public/assets/preview.png)

## ✨ Funcionalidades

- 🔒 **Autenticação Completa:** Sistema de login e cadastro seguro via Supabase Auth.
- 💾 **Persistência em Nuvem:** Seus dados são salvos em tempo real no banco de dados Supabase.
- 🎨 **Design Obsidian Glass:** Interface premium com glassmorphism, gradientes vibrantes e micro-animações.
- 📊 **Análises & Métricas:** Dashboard interativo com taxa de conclusão, distribuição por categoria e prioridade.
- 📅 **Calendário Inteligente:** Visualize suas entregas em uma grade mensal interativa.
- 🏷️ **Categorização e Prioridades:** Organize tarefas por Trabalho, Pessoal ou Estudos com níveis de urgência.
- ✅ **Checklist Animado:** Feedback visual instantâneo ao concluir tarefas.
- 📱 **Totalmente Responsivo:** Experiência perfeita em desktop, tablet e mobile.

## 🚀 Stack Tecnológica

| Camada | Tecnologia |
| :--- | :--- |
| **Frontend** | React 18 + Vite |
| **Estilização** | Tailwind CSS v3 |
| **Backend/DB** | Supabase (PostgreSQL) |
| **Autenticação** | Supabase Auth |
| **Ícones** | Lucide React |
| **Roteamento** | React Router DOM |

## 🛠️ Configuração e Instalação

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/MBARUDI/Lista-de-Tarefas.git
   cd Lista-de-Tarefas
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   ```

3. **Configure as variáveis de ambiente:**
   Crie um arquivo `.env` na raiz com suas chaves do Supabase:
   ```env
   VITE_SUPABASE_URL=sua_url_aqui
   VITE_SUPABASE_ANON_KEY=sua_chave_anon_aqui
   ```

4. **Inicie o servidor de desenvolvimento:**
   ```bash
   npm run dev
   ```

## 🗄️ Estrutura do Banco de Dados (SQL)

Para que o app funcione, execute o seguinte script no SQL Editor do seu projeto Supabase:

```sql
create table tasks (
  id uuid default gen_random_uuid() primary key,
  user_id uuid references auth.users(id) default auth.uid(),
  title text not null,
  category text not null,
  priority text not null,
  "dueDate" date,
  completed boolean default false,
  "createdAt" timestamp with time zone default timezone('utc'::text, now()) not null
);

-- Habilitar RLS
alter table tasks enable row level security;

-- Políticas de Segurança
create policy "Users can only see their own tasks" on tasks for select using (auth.uid() = user_id);
create policy "Users can only insert their own tasks" on tasks for insert with check (auth.uid() = user_id);
create policy "Users can only update their own tasks" on tasks for update using (auth.uid() = user_id);
create policy "Users can only delete their own tasks" on tasks for delete using (auth.uid() = user_id);
```

---
Desenvolvido por **[MBARUDI](https://github.com/MBARUDI)**.
