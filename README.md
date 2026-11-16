# S+QDCP Command Center
## PT. ALFA VALVES INDONESIA

**Versão 1.2 — Regras de cores diárias + Supabase Cloud Sync/Realtime**

Painel (dashboard) web estático para acompanhar **Segurança (Safety), 5S, Qualidade (Quality), Entrega (Delivery), Custo (Cost) e Pessoas (People)** ao longo de um mês inteiro.

## Recursos

- Visão geral com seis cartões de KPI, em que os dias do mês formam o contorno das letras **S, 5, Q, D, C, P**.
- Regras de cor dos dias, por prioridade: **vermelho** se houver quase acidente (Near Miss) ou acidente em Segurança; **azul** para sábado, domingo, feriado nacional e folga coletiva; **verde** se os dados foram preenchidos e a meta foi atingida; **amarelo** se os dados foram preenchidos, mas a meta não foi atingida; **cinza** se ainda não há dados.
- Se uma ocorrência de Segurança acontecer em fim de semana ou feriado, o marcador continua **vermelho**, para que a ocorrência não fique escondida pela cor do dia de folga.
- Lançamento direto em tabelas na web para todos os dias do mês.
- Importação/exportação de planilha Excel com seis abas: `SAFETY`, `5S`, `QUALITY`, `DELIVERY`, `COST`, `PEOPLE`.
- Gerador de modelo Excel conforme o mês ativo.
- Cálculo automático de FTP (aprovação na 1ª vez), testes e pintura realizados, horas adicionais e presença.
- Configuração das metas de KPI e de feriados personalizados.
- Plano de ação por categoria.
- Tema escuro (padrão) e tema claro, com barra lateral recolhível.
- Fontes Inter, Space Grotesk e JetBrains Mono servidas da própria pasta (`vendor/fonts`), sem depender da internet.
- Interface em português (padrão), indonésio e inglês.
- Download da visão geral em PDF A3 paisagem.
- Layout responsivo para desktop, tablet e celular.
- Armazenamento local como reserva quando a internet cai.
- **Supabase Cloud Sync + Realtime** para atualização ao vivo entre PCs e celulares.

## Como executar

### Jeito mais fácil

Abra o `index.html` em um navegador moderno (Chrome, Edge ou Firefox).

### Com um servidor web local

```bash
python3 -m http.server 4173 --bind 0.0.0.0
```

Depois abra `http://localhost:4173`.

## Envio para a hospedagem

Envie **todo o conteúdo desta pasta**, incluindo a pasta `vendor` (com a subpasta `vendor/fonts`), para a pasta pública da hospedagem (por exemplo, `public_html`). Não é preciso PHP, Node.js nem processo de build. Para sincronizar entre dispositivos, crie um projeto no Supabase e siga o `CLOUD-SYNC-GUIDE.md`.

Funciona bem em:

- cPanel/hospedagem compartilhada
- Netlify Drop
- GitHub Pages
- Cloudflare Pages
- servidor de intranet estático

## Fluxo do Excel

1. Escolha o mês no cabeçalho.
2. Abra **Dados diários**.
3. Clique em **Modelo Excel** para baixar uma planilha em branco com a quantidade de dias do mês ativo.
4. Preencha a planilha sem alterar o nome das abas nem a ordem das colunas.
5. Clique em **Importar Excel** e escolha o arquivo.
6. Clique em **Baixar Excel** para fazer um backup dos dados do navegador.

Os arquivos gerados pelo painel podem ser importados de volta no painel. A coluna de datas pode conter datas nativas do Excel, formato ISO ou formatos de data comuns.

## Troca de mês

- Escolher um novo mês cria automaticamente um período separado.
- Os dados do mês anterior não se perdem ao trocar de mês.
- O botão **Limpar mês** apaga somente os dados diários do mês que está ativo.
- Metas, plano de ação, tema, idioma e feriados personalizados não são apagados.

## Calendário de feriados

O calendário embutido traz os feriados nacionais e as folgas coletivas (*cuti bersama*) da Indonésia em 2026, com base no SKB 3 Menteri (decreto conjunto de três ministérios). Os fins de semana são sempre detectados automaticamente. Para outros anos ou para feriados da empresa, abra **Metas de KPI → Calendário de feriados** e adicione as datas manualmente.

Fonte do calendário de 2026: Secretaria de Estado da República da Indonésia — https://setneg.go.id/baca/index/inilah_skb_3_menteri_libur_nasional_dan_cuti_bersama_2026

## Atualização ao vivo entre PC e celular

O painel é compatível com o Supabase Realtime. Siga o passo a passo completo em **`CLOUD-SYNC-GUIDE.md`**:

1. Crie um projeto no Supabase.
2. Execute o `SUPABASE-SETUP.sql`.
3. Preencha a Project URL e a Publishable/anon key em `supabase-config.js`.
4. Faça o commit no GitHub e aguarde o GitHub Pages concluir a publicação.
5. Confira se o indicador mudou para **“Ao vivo • Nuvem sincronizada”**.

Sem a configuração do Supabase, o painel continua funcionando em modo local, mas os dados do PC e do celular não serão os mesmos. Faça backups periódicos com **Baixar Excel**.

A configuração SQL incluída usa acesso público sem login, conforme a escolha atual. Para dados de produção com mais segurança, use o Supabase Authentication e restrinja a permissão de edição.
