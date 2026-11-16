# Checklist de atualização do GitHub Pages — Live Sync v1.2

1. Baixe e extraia o pacote da versão Live Sync.
2. No Supabase, execute o `SUPABASE-SETUP.sql` pelo SQL Editor.
3. Preencha `url` e `anonKey` em `supabase-config.js`.
4. Envie/substitua os seguintes arquivos no repositório do GitHub:
   - `index.html`
   - `app.js`
   - `styles.css`
   - `supabase-config.js`
   - `SUPABASE-SETUP.sql`
   - `CLOUD-SYNC-GUIDE.md`
   - `README.md`
   - `vendor/supabase.min.js`
   - `vendor/fonts/` (pasta inteira — fontes usadas pelo layout)
5. Confira se os arquivos antigos da pasta vendor continuam lá:
   - `vendor/xlsx.full.min.js`
   - `vendor/html2canvas.min.js`
   - `vendor/jspdf.umd.min.js`
6. Aguarde a seção **Deployments → github-pages** ficar com o status verde.
7. Feche o painel no celular por enquanto.
8. No PC que guarda os dados mais recentes, pressione `Ctrl+Shift+R` e aguarde o indicador **Ao vivo • Nuvem sincronizada**.
9. Depois que o PC estiver sincronizado, abra/atualize o painel no celular.
10. Se o celular ainda carregar a versão antiga, limpe o cache do site ou abra a URL com um parâmetro temporário, por exemplo:

```
https://NOME-USUARIO.github.io/NOME-REPO/?v=1.2
```

Esse parâmetro não altera os dados; ele só ajuda a forçar o navegador a buscar a versão publicada mais recente.
