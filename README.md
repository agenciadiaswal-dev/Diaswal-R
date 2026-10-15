# Diaswal — rotina, alimentação, finanças e Amigo IA

Aplicação web responsiva em React + TypeScript + Vite, com configuração PWA e integração Supabase.

## Requisitos

- Node.js 20+
- Projeto Supabase
- NPM

## Executar localmente

```bash
npm install
cp .env.example .env
# Edite .env com a URL do projeto e a chave pública/anon do Supabase
npm run dev
```

Para criar a versão de produção: `npm run build`; para testar: `npm run preview`.

## Configurar Supabase

1. Crie um projeto em https://supabase.com.
2. Em **Project Settings → API**, copie a Project URL e a chave publicável/anon para `.env`.
3. Abra **SQL Editor** e execute `supabase/migrations/0001_initial_schema.sql`.
4. Em **Authentication → Providers**, confirme que Email está habilitado.
5. Para produção, configure URL de site e redirect URLs em **Authentication → URL Configuration**.
6. Em **Database → Replication**, confirme que as tabelas desejadas estão habilitadas no Realtime se o projeto não aplicar a publicação do SQL automaticamente.

**Segurança:** nunca use `service_role` no navegador. A migração habilita RLS e políticas por `auth.uid()` em todas as tabelas privadas. Revise políticas e testes de acesso antes de produção.

## O que já está no protótipo

- Tela de login/cadastro por e-mail e senha via Supabase Auth.
- Layout responsivo com navegação inferior mobile e navegação lateral desktop.
- Rotina com estados concluído/procrastinado, XP ilustrativo, contador de ofensiva e criação de alarmes.
- Refeições e widget clicável de água.
- Cadastro de despesas, gráfico por categoria e meta de economia.
- Amigo IA com respostas locais de demonstração, usando contexto de tarefas e gastos.
- Manifest e service worker via `vite-plugin-pwa`.

## Importante: itens para completar antes de lançar

- Ações de refeições, água, chat, XP/ofensiva e metas precisam de integração completa com o banco. A estrutura SQL já contempla essas tabelas, mas a UI inicial ainda mantém algumas dessas interações localmente.
- Para respostas generativas reais, crie uma função de servidor/Edge Function que chame o provedor de IA. Não coloque chaves privadas no frontend.
- Notificações de alarme exigem permissões do navegador e estratégia de agendamento; uma PWA não garante alarmes exatos em segundo plano em todos os celulares.
- Pagamentos mensais: integrar um provedor (por exemplo, Stripe ou Mercado Pago) com checkout e webhook no servidor; não considerar a interface de assinatura como controle de acesso. O projeto inicial ainda não cobra assinaturas.
- Adicionar testes de autorização RLS, estados de erro/loading, política de privacidade, termos, exclusão/exportação de conta e revisão de acessibilidade.
- Ícones SVG estão incluídos como ícones PWA de base; substitua por PNGs de 192 e 512 pixels se necessário para compatibilidade máxima em lojas/navegadores.

## Estrutura

- `src/App.tsx` — aplicação e fluxos principais
- `src/styles.css` — interface responsiva
- `src/supabase.ts` — cliente Supabase
- `supabase/migrations/0001_initial_schema.sql` — tabelas e segurança RLS
- `vite.config.ts` — configuração PWA
