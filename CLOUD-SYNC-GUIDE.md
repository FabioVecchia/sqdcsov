# Como ativar a atualização ao vivo PC ↔ celular com o Supabase

## Por que os dados não eram os mesmos antes?

A primeira versão usava `localStorage`. Esse armazenamento existe apenas no navegador/dispositivo de cada pessoa. Os dados digitados no PC nunca eram enviados para o GitHub nem para o celular. O GitHub Pages apenas entrega os arquivos HTML/CSS/JavaScript; ele não é um banco de dados.

Esta versão acrescenta o **Supabase Cloud Sync + Realtime**. Depois de configurado, o PC e o celular leem o mesmo registro do painel e recebem as atualizações automaticamente.

## Passo 1 — Criar o projeto no Supabase

1. Abra https://supabase.com e entre na sua conta.
2. Escolha **New project**.
3. Informe um nome, por exemplo `alfa-valves-sqdcp`.
4. Escolha a região mais próxima e aguarde o projeto ficar pronto.

## Passo 2 — Criar a tabela e as policies

1. No Supabase, abra o **SQL Editor**.
2. Clique em **New query**.
3. Copie todo o conteúdo do arquivo `SUPABASE-SETUP.sql`.
4. Clique em **Run**.
5. Confira se o último resultado mostra o registro `pt-alfa-valves-indonesia-main`.

O script também registra a tabela no Supabase Realtime.

## Passo 3 — Preencher a configuração do site

1. No Supabase, abra **Project Settings → API** ou o menu **Connect**.
2. Copie:
   - a **Project URL**
   - a **Publishable key** ou a antiga **anon public key**
3. Abra o arquivo `supabase-config.js` no repositório do GitHub.
4. Preencha como no exemplo abaixo:

```js
window.SUPABASE_CONFIG = {
  url: 'https://PROJECT-REF.supabase.co',
  anonKey: 'sb_publishable_xxxxxxxxx',
  dashboardId: 'pt-alfa-valves-indonesia-main'
};
```

5. Faça o commit da alteração na branch usada pelo GitHub Pages.
6. Aguarde o status de **Actions/Deployments** terminar.

> Nunca coloque a `service_role key`. Use somente a Publishable key ou a anon public key.

## Passo 4 — Primeira sincronização e verificação

> Importante: como os dados mais recentes hoje estão no localStorage do PC, faça a primeira abertura a partir **desse PC**. Mantenha a página do painel fechada no celular até concluir o item 2.

1. Abra o site no PC que guarda os dados mais recentes e faça um hard refresh (`Ctrl+Shift+R`).
2. Aguarde o indicador à direita do título mudar para **“Ao vivo • Nuvem sincronizada”**. Os dados locais do PC passam a ser os dados iniciais da nuvem se o banco ainda estiver vazio.
3. Depois disso, abra o site no celular e atualize a página.
4. O indicador no celular também deve mudar para **“Ao vivo • Nuvem sincronizada”**.
5. Altere um valor pelo PC.
6. Em condições normais, o celular recebe a atualização automaticamente em poucos segundos, sem importar Excel.

Se o indicador continuar em **“Modo local • Nuvem não configurada”**, o arquivo `supabase-config.js` no GitHub Pages ainda não tem a URL/key ou a versão publicada não é a mais recente.

Se o indicador mostrar **“Nuvem desconectada”**:

- confira a URL e a key;
- confira se o `SUPABASE-SETUP.sql` já foi executado;
- confira se o nome da tabela é `sqdcp_dashboard`;
- veja as mensagens de erro no Console do navegador;
- verifique se o projeto do Supabase não está pausado.

## Comportamento da sincronização

O que é sincronizado:

- todos os dados mensais;
- as metas de KPI;
- o plano de ação;
- os feriados personalizados.

O que continua sendo específico de cada dispositivo:

- o idioma;
- o tema claro/escuro;
- a página/categoria que está aberta;
- o mês que está sendo exibido.

Se a internet cair, as alterações continuam salvas no navegador e o painel tenta reenviá-las quando a conexão com a nuvem voltar.

## Nota de segurança do modo PÚBLICO

A configuração atual segue a escolha de **acesso público sem login**. Isso significa que qualquer pessoa que conheça a URL do site pode ler e alterar os dados pelo site/API. Esse modo é prático, mas não serve para dados confidenciais.

Para um uso em produção com mais segurança, recomenda-se que a próxima versão use o Supabase Authentication, de modo que o público só possa visualizar e a equipe precise fazer login para alterar os dados.
