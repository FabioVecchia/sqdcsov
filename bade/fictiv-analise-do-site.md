# Fictiv (www.fictiv.com) — análise do site e do sistema

Análise feita em 14/11/2026. O site é todo em inglês; os nomes de telas e botões aparecem aqui no original, entre aspas, com a explicação em português.

## Como ler este documento

A Fictiv tem duas partes: o **site público** (`www.fictiv.com`), que qualquer pessoa vê, e a **plataforma** (`app.fictiv.com`), onde o cliente cota, compra e acompanha pedidos depois de fazer login.

- Do site público, li diretamente as páginas principais (lista na seção 14). As demais conheço por trechos da documentação oficial.
- **Não entrei na plataforma**, porque ela exige conta. O que está descrito sobre as telas internas vem da documentação oficial da Fictiv e de uma descrição feita por terceiros.

Por isso cada função traz uma marca de origem:

| Marca | Origem | Quanto confiar |
|---|---|---|
| **S** | Página do site público lida diretamente em 14/11/2026 | É o que o site afirma hoje |
| **A** | Documentação oficial da Fictiv (Central de Ajuda, artigos, notas de versão, Termos), lida por trechos | Oficial, mas vários artigos são de 2021 a 2023 |
| **T** | Descrição de terceiros das telas internas: repositório público `K-Dense-AI/scientific-agent-skills`, pasta `skills/fictiv` (licença MIT, versão de 09/11/2026). O próprio texto diz que se baseia num retrato da plataforma de setembro de 2026 | Não verificada por mim; pode estar desatualizada |

Duas marcas na mesma linha (por exemplo `A T`) indicam que a fonte oficial confirma a função e a de terceiros dá os detalhes de tela. A lista de endereços consultados está na seção 14, e o que ficou sem verificação está na seção 12.

## Sumário

1. Resumo
2. Partes do sistema
3. Site público: mapa de páginas
4. Site público: funções
5. Plataforma: funções
6. Como o sistema funciona, passo a passo
7. Regras de negócio
8. Catálogo de fabricação
9. Central de Ajuda: índice dos artigos
10. Linha do tempo dos recursos
11. Observações técnicas e defeitos notados
12. O que não foi verificado
13. Glossário
14. Fontes

---

## 1. Resumo

A Fictiv é uma empresa americana de fabricação de peças mecânicas sob encomenda. O cliente envia o modelo 3D (CAD) da peça, recebe o preço e uma análise de fabricabilidade (DFM), compra pelo site, e a Fictiv manda fabricar, inspeciona e entrega.

A fabricação é feita por uma rede de fábricas parceiras auditadas (mais de 250, segundo o site). A Fictiv cuida da cotação, da engenharia, da escolha da fábrica, da qualidade e da logística. O site chama esse modelo de "rede gerenciada" (*managed network*) e o diferencia dos marketplaces de leilão: cada pedido vai para um único parceiro escolhido pela Fictiv, sem disputa de lances. `S`

Fundada em 2013 em San Francisco, a Fictiv foi comprada pelo grupo japonês MISUMI por US$ 350 milhões (anúncio de abril de 2025, segundo a imprensa). O site já exibe a marca "MISUMI Americas".

O site resume o funcionamento em quatro etapas `S`:

| Etapa | O que acontece |
|---|---|
| 1. Design | DFM instantâneo ao enviar o arquivo, sugestão de material por IA, desenho 2D gerado automaticamente |
| 2. Quote | Preço instantâneo; peças complexas vão para cotação revisada por engenheiro; ajuste entre prazo e custo |
| 3. Make | IA sugere a fábrica, engenheiros confirmam, qualidade acompanhada na fábrica |
| 4. Deliver | Rastreamento em tempo real, fotos de inspeção antes do envio, impostos de importação informados |

Quem participa:

| Papel | O que faz |
|---|---|
| Cliente (engenheiro ou comprador) | Envia arquivos, configura, aprova o DFM, paga, acompanha, recompra |
| Plataforma | Analisa a geometria, calcula preço e prazo, lê desenhos, sugere a fábrica, guarda documentos |
| Engenheiros de cotação e manufatura da Fictiv | Cotam peças complexas, dão DFM detalhado, tiram dúvidas por chat |
| Gerente de conta | Contato comercial: preços, contratos, requisitos especiais |
| Gerente de programa | Contato do pedido: mudanças, cancelamento, problemas de qualidade |
| Qualidade e logística da Fictiv | Revisam a inspeção, publicam fotos e relatórios, cuidam do envio e da alfândega |
| Fabricante parceiro | Fabrica, inspeciona e envia fotos e medições |

Números divulgados pelo site (as páginas não concordam entre si) `S`:

| Dado | Valores encontrados |
|---|---|
| Peças fabricadas | 40M+ e 42M+ |
| Empresas atendidas | 3.000+, 5.000+ e 6.000+ |
| Parceiros auditados | 240+ e 250+ |
| Regiões de fabricação | 4, 5 e 6; a página inicial lista EUA, China, Índia, Japão e México |
| Combinações de material, processo e acabamento | 4.100+ |
| Índice de sucesso de qualidade | 95,4% |

---

## 2. Partes do sistema

| Parte | Endereço | Para que serve | Fonte |
|---|---|---|---|
| Site público | `www.fictiv.com` | Apresentação, catálogo, conteúdo técnico, captação de clientes | S |
| Plataforma do cliente | `app.fictiv.com` | Cotação, compra, acompanhamento, biblioteca, times | S T |
| Central de Ajuda | `www.fictiv.com/help` (antes `help.fictiv.com`) | 6 coleções de artigos de uso da plataforma | S |
| Materials.AI | `www.fictiv.com/ai/materials` e dentro da plataforma | Assistente de IA para escolha de material | S T |
| Atlas | `atlas.fictiv.com` | Aplicativo separado de análise de peças CNC (preparações, tempo de máquina, ferramental) | T |
| Punchout | integração configurada com a equipe da Fictiv | Liga a plataforma ao sistema de compras da empresa cliente | A |
| Catálogo MISUMI | `misumi.com` (link externo) | Peças de catálogo do grupo controlador | S |

---

## 3. Site público: mapa de páginas

O menu principal tem os grupos **Capabilities**, **Why Fictiv?**, **Solutions**, **Industries**, **Resources** e **Company**, mais os botões **Log In / Sign in** e **Get Instant Quote**. Vi duas versões do menu (seção 11).

| Grupo | Páginas (caminhos) |
|---|---|
| Capabilities | `/capabilities` (visão geral e comparativo de processos); `/capabilities/cnc-machining-services`; `/capabilities/sheet-metal-services`; `/capabilities/3d-printing-services`; `/capabilities/injection-molding-services`; `/capabilities/urethane-casting-services`; `/capabilities/die-casting-services`; `/capabilities/compression-molding-services` |
| Materiais e especificações | `/materials-and-finishes`; `/materials/...` (uma página por material); `/finishes/...` (uma por acabamento); `/specifications/...` (CNC, impressão 3D, injeção, acabamentos) |
| Why Fictiv? | `/why-choose-fictiv`; `/why-choose-fictiv/how-it-works`; `.../our-network`; `.../our-platform`; `.../quality-assurance`; `.../faster-hardware`; `.../compare`; comparativos `.../fictiv-vs-xometry`, `.../fictiv-vs-protolabs`, `.../fictiv-vs-sendcutsend` |
| Solutions | `/production`; `/prototyping`; `/mro-solutions`; `/teams`; `/welding-assembly-capability`; `/tariff`; `/quality-assurance`; `/engineering-services` |
| Industries | `/industries` e uma página por setor: aerospace, robotics, consumer-products, automotive, medical, semiconductor, climate-tech, evtol, industrial-automation |
| Resources | `/resources`; `/articles`; `/case-studies`; `/ebooks`; `/podcasts`; `/masterclass`; `/tools`; `/teardowns`; `/webinars`; `/fictivmade`; `/inside-the-factory`; `/watch/...` (vídeos-guia); `/fictiv-features/...` (vídeos da plataforma); `/topic/...`; `/authors/...` |
| Ferramentas | `/ai/materials`; `/quiz/how-complex-is-your-part`; `/3d-printing-material-selector`; `/tools/...` |
| Central de Ajuda | `/help-center` (redireciona para `/help`); `/help/<coleção>/<artigo>` |
| Company | `/about-us`; `/careers`; `/newsroom`; `/shows-and-events`; `/our-people`; `/contact-us`; `/misumi` |
| Conta | `/signup`; `app.fictiv.com/login` |
| Legal | `/terms`; `/privacy` |
| Campanhas | `/lp-ps/...` (páginas de destino de anúncios) |

---

## 4. Site público: funções

| # | Função | Como aparece | Fonte |
|---|---|---|---|
| 1 | Faixa de novidade | Barra no topo com aviso, link e botão de fechar. Hoje: "Compare pricing for up to 5 quantities in one quote" | S |
| 2 | Menu principal | Submenus por grupo, com destaque de conteúdo (caso de sucesso, guias em PDF) | S |
| 3 | Botões de ação | "Get Instant Quote" e "Get Free Pricing" levam ao cadastro; "Sign in" leva à plataforma; "Talk to Our Team" e "Talk to an Expert" levam ao contato (página ou janela) | S |
| 4 | Cadastro | Página `/signup`; todo botão de cotação passa por ela | S |
| 5 | Contato | Página `/contact-us` com formulário e perguntas frequentes; a resposta é prometida em 1 a 3 dias úteis | A |
| 6 | Pedido de NDA | Janela "Submit an inquiry"; a Fictiv responde por e-mail com os próximos passos | S |
| 7 | Pedido de cotação de produção | Botão "Submit an RFQ", que abre uma janela na página `/production` | S |
| 8 | Páginas de processo | Uma por processo de fabricação, com prazos, materiais e perguntas frequentes | S A |
| 9 | Comparativo de processos | Tabela no hub `/capabilities` para quem não sabe qual processo usar (indicação, materiais, prazo, volume, tolerância) | A |
| 10 | Biblioteca de materiais e acabamentos | Páginas por material e por acabamento, com fichas técnicas | S A |
| 11 | Páginas de especificação | Tolerâncias e regras de projeto por processo | A |
| 12 | Páginas por setor | 9 setores, com casos de sucesso | S |
| 13 | Páginas de solução | Produção, prototipagem, MRO, times, montagem e solda, tarifas, qualidade, serviços de engenharia | S |
| 14 | Comparativos com concorrentes | Tabela de modelos (oficinas, fabricantes digitais, marketplaces, Fictiv) e três confrontos diretos | S |
| 15 | Centro de recursos | Lista de conteúdos com busca e filtros por tema, tipo de conteúdo, função do leitor, setor e processo | S |
| 16 | Tipos de conteúdo | Artigos, casos de sucesso, e-books em PDF, podcasts, Master Class, desmontagens (*teardowns*), webinars, série FictivMade, Inside the Factory, vídeos-guia | S |
| 17 | Ferramentas gratuitas | Materials.AI; quiz de complexidade de peça CNC; seletor de material para impressão 3D; calculadoras de tolerância de injeção, de flexão de viga em balanço, de encaixe (*snap-fit*), de risco da cadeia de suprimentos e de valor da manufatura digital | S |
| 18 | Modelos e listas para baixar | Cronograma de projeto de injeção (Gantt), modelo de D-FMEA, lista de DFM para CNC, 10 regras de DFA, macros para engenheiros | S |
| 19 | Boletim MechStack | Assinatura por e-mail, oferecida na lateral e no fim dos artigos | S |
| 20 | Central de Ajuda | 6 coleções, 69 entradas, bloco de artigos populares e botão "Talk to the Team" | S |
| 21 | Notas de versão | Artigo "What's New on the Fictiv Platform", com as novidades mês a mês | S |
| 22 | Vídeos da plataforma | Série "Fictiv Features": Parts Library, Drawing Annotation Tool, Materials.AI | S |
| 23 | Demonstração interativa | Na página Teams há uma demonstração incorporada da plataforma (rótulo "Storylane") | S |
| 24 | Prova social | Logotipos de clientes, depoimentos, carrossel de casos, números da rede | S |
| 25 | Bloco MISUMI | Apresenta a MISUMI Americas e leva ao catálogo do grupo | S |
| 26 | Páginas da empresa | Sobre, carreiras, imprensa com kit de imprensa, feiras e eventos, equipe em campo | S |
| 27 | Perguntas frequentes | Blocos de FAQ em várias páginas, também publicados em formato legível por buscadores | S A |
| 28 | Links relacionados | Bloco "Also of Interest" no fim de cada página | S |
| 29 | Folheto para baixar | PDF sobre a integração com sistemas de compras, na página Teams | S |

---

## 5. Plataforma: funções

### 5.1 Conta e acesso

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Criar conta | Cadastro gratuito; avisa quando o e-mail já está em uso | S A |
| 2 | Login | Depois de várias tentativas erradas a conta fica bloqueada por um tempo; o sistema avisa quantas tentativas restam | A |
| 3 | Verificação de e-mail | Link enviado por e-mail; aparece na lista de primeiros passos | T |
| 4 | Tipo de conta por e-mail | Conta com e-mail pessoal só enxerga CNC, impressão 3D e chapa. E-mail corporativo verificado libera moldagem, fundição, pagamento por PO, Teams e Materials.AI | T |
| 5 | Página inicial | Atalhos para nova cotação e para a biblioteca, cartão do gerente de conta (nome, e-mail, telefone, "Book a meeting"), lista de primeiros passos e links úteis | T |
| 6 | Minha conta | Editar nome, telefone e senha; ver o e-mail verificado; excluir a conta | T |
| 7 | Permissões financeiras | Pedir prazo de pagamento por PO e isenção de imposto para revenda | A T |
| 8 | Cartões salvos | Guardar e escolher cartões; os dados ficam no Stripe, não na Fictiv | T |
| 9 | Convidar pessoas | Botão "Invite to Fictiv" no topo; também convida ao compartilhar uma cotação | A T |
| 10 | Chat com especialistas | "Chat with us" dentro da peça e links "Contact us" | A |

### 5.2 Criar a cotação e enviar arquivos

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Escolha do processo | 7 cartões. Preço instantâneo: CNC, impressão 3D, fundição em uretano, chapa. Cotação em até 48 h: injeção, moldagem por compressão, fundição sob pressão | T |
| 2 | Envio de arquivos | Arrastar e soltar, ou escolher vários arquivos ou uma pasta | A T |
| 3 | Criação automática | O envio já cria a cotação e abre a página dela | A |
| 4 | Nome da cotação | Nome automático (sobrenome e data), editável pelo ícone de lápis | A T |
| 5 | Formatos aceitos | Janela com a lista por processo (seção 7) | A T |
| 6 | Unidades | Escolha entre milímetros e polegadas, importante para arquivos de malha | S T |
| 7 | Análise de geometria | Roda sozinha após o envio, cerca de 10 a 30 segundos por peça, e depois libera o botão "Configure" | T |
| 8 | Declaração de exportação | No envio o cliente confirma a classificação de controle de exportação | A |
| 9 | Detecção de ITAR | Se houver texto de ITAR num desenho, a cotação e os arquivos são apagados automaticamente | A |
| 10 | Anexar desenho 2D | PDF ligado à peça; o sistema anexa sozinho quando os nomes dos arquivos são parecidos | A |
| 11 | Adicionar peças | Enviar mais arquivos para uma cotação existente | T |
| 12 | Mover peças | "Move to…" leva peças para outra cotação ou cria uma nova | A |
| 13 | Cotação a partir da biblioteca | "New quote from Parts Library" monta a cotação com peças já compradas | A T |
| 14 | Painel de cotações | Lista por data, com status (por exemplo "Ready to purchase"), data de envio e subtotal | A T |
| 15 | Registro de atividade | "View activity log" mostra quem criou, configurou ou compartilhou, com data e hora | A T |
| 16 | Revisões da peça | "Upload part revision" e "View revision history" | A T |
| 17 | Baixar e excluir | Baixar arquivos; excluir peça ou cotação (definitivo) | T |
| 18 | Tour de primeiro uso | Janela "Upload complete! Next steps…" na primeira vez | T |

### 5.3 Configurar a peça

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Visualizador 3D | Gira a peça, mostra as dimensões máximas, modo transparente | A T |
| 2 | Processo, material e quantidade | Material em lista pesquisável por família; "Apply configuration" confirma e mostra o preço unitário | A T |
| 3 | Cor e pós-processamento | Escolhidos junto com o material | A |
| 4 | Filtro de materiais 3D | Etiquetas de aplicação reduzem a lista; ao passar o mouse aparece o resumo de propriedades e a ficha técnica | A |
| 5 | Preenchimento em FDM | Densidade de preenchimento (*infill*) configurável, com efeito no preço e no prazo | A |
| 6 | Acabamentos | Só lista os válidos para o material; mostra quanto cada um soma em dias e em preço; permite vários | A T |
| 7 | Tratamento térmico | Têmpera, cementação e revenimento como opções de acabamento em aços e titânio | A |
| 8 | Mascaramento | "Add masking" protege áreas do acabamento | T |
| 9 | Detecção de roscas | Encontra os furos e oferece, para cada um, as roscas padrão que cabem naquele diâmetro (UNC/UNF, métrica, ACME, trapezoidal, BSP) | A T |
| 10 | Gerador de desenho 2D | Cria o desenho a partir do modelo, por processo, com notas de tolerância e acabamento; o texto é editável | S A |
| 11 | Anotação de desenho | Marcar no navegador as cotas e requisitos críticos | S |
| 12 | Leitura do desenho | Identifica tolerâncias apertadas, furos, ferragens e unidades mistas no PDF e destaca o que encontrou | A |
| 13 | Conciliação de desenho | "Drawings Reconciliation" preenche a configuração a partir do PDF; itens não resolvidos ficam em laranja | S T |
| 14 | Tolerâncias | Padrão ISO 2768 médio incluído; tolerâncias mais apertadas vêm do desenho | T |
| 15 | Inspeções | Relatório padrão incluído; relatório avançado (CMM, laser ou óptico) como adicional | A T |
| 16 | Certificados | Certificado de conformidade e certificado de material como adicionais, com preço automático | A T |
| 17 | Requisitos especiais | Inspeção de primeira peça (FAI), relatórios sob medida e instalação de ferragens são pedidos pelo chat | A T |
| 18 | Insertos roscados | Instalação de insertos a quente em peças impressas em 3D | A |
| 19 | Cores sob medida | Cor por código Pantone ou RAL em alguns materiais | A |
| 20 | Configuração em massa | Marcar várias peças e aplicar o mesmo processo, material e acabamento | A T |

### 5.4 Análise de fabricabilidade (DFM)

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | DFM automático | Algoritmos de geometria avaliam a peça no envio; peças complexas passam por engenheiros de cotação | A |
| 2 | Aviso na peça | Selo colorido com a quantidade de itens e link "View feedback" | A T |
| 3 | Destaque no modelo | Clicar na mensagem mostra a região afetada no visualizador 3D | A |
| 4 | Tipos de aviso | Paredes finas, cantos internos arredondados, profundidade de corte ou de furo, rosca fora do padrão, empenamento, região inalcançável, necessidade de eletroerosão, entre outros | T |
| 5 | Responder ao DFM | Enviar revisão da peça ou abrir chat com a equipe | A |
| 6 | Avisos não bloqueiam | O preço continua visível e a compra é permitida com avisos em aberto | T |
| 7 | DFM de impressão 3D | Limitado à verificação de paredes finas | A |
| 8 | Relatório de DFM de injeção | Em slides por tema, com status "Warning", "Approval required" ou "Revision required"; visão 3D e 2D | A |
| 9 | Anotar e aprovar | O cliente responde slide a slide e anota; anotações do cliente em vermelho, as da Fictiv em verde-azulado | A |
| 10 | Avisar a Fictiv | Botão "Close and notify" ao terminar a revisão; e-mail quando há relatório novo | A |
| 11 | Histórico de DFM | Relatórios de todas as revisões da peça ficam guardados | A |
| 12 | DFM no PDF e na recompra | O DFM sai no PDF da cotação e é levado para a cotação de recompra | A |
| 13 | Estimativa de injeção | Ao cotar uma peça em impressão 3D, mostra quanto custaria por unidade se fosse injetada | A |

### 5.5 Preço, quantidade, prazo e região

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Preço instantâneo | Preço por peça e total, recalculado a cada mudança | S A |
| 2 | Declaração de uso | Antes de ver o preço o cliente informa se as peças são protótipo ou uso comercial | T |
| 3 | Várias quantidades | Até 5 faixas de quantidade na mesma cotação, comparando preço unitário, total, prazo e economia | S T |
| 4 | Opções de prazo | Seis opções: América do Norte e exterior, cada uma em mais rápido, padrão e econômico; caixa "USA only" | A T |
| 5 | Prazo por peça | Aba "Select individual lead times" permite misturar produção local e no exterior | A |
| 6 | Datas | Mostra a data de envio e a data estimada de entrega | A T |
| 7 | Custo com importação | Em pedidos internacionais, impostos e frete aparecem antes da compra | S |
| 8 | Preço preferencial | Etiqueta verde nas peças com desconto negociado; antes e depois no PDF | A |
| 9 | Otimizador de prazo | Informa-se a data desejada e o sistema mostra o que remover ou trocar para cumpri-la | A |
| 10 | Resumo | Produção, frete, imposto, total, data de envio e endereço | T |
| 11 | Comparação de processos | CNC, impressão 3D e fundição lado a lado, com materiais alternativos | S |

### 5.6 Cotação manual (RFQ)

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Pedir cotação | "Request quote" aparece quando alguma peça precisa de revisão humana; os preços ficam ocultos até a resposta | A T |
| 2 | O que dispara | Peça complexa, desenho com requisitos apertados, material sob medida, arquivo com vários corpos, moldagem e fundição, programas de produção | S T |
| 3 | Revisão por engenheiros | Analisam a peça e os desenhos e devolvem DFM, dicas de custo e perguntas como anotações no modelo 3D | A |
| 4 | Prazo de resposta | O site promete a maioria em até 2 dias úteis; a descrição de terceiros cita cerca de 2 horas úteis para CNC e 24 a 48 h para moldagem e fundição | S T |
| 5 | Representante de vendas | Atribuído automaticamente a quem ainda não tem | A |
| 6 | Bloqueio após o pedido | Roscas e desenhos não podem mais ser editados | T |
| 7 | Aviso de retorno | E-mail quando a cotação fica pronta | T |

### 5.7 Compartilhar e colaborar

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Compartilhar cotação | Por link ou por e-mail; quem recebe pode ver, editar e comprar | A |
| 2 | Nota e PDF | O convite pode levar um recado e o PDF da cotação; o campo sugere destinatários anteriores | A |
| 3 | Encaminhar ao comprador | "Forward to Purchaser" manda a cotação ao setor de compras com instruções para fechar o pedido | A |
| 4 | Baixar PDF | "Download quote", com o DFM incluído | A |
| 5 | Validade do convite | O convite expira em 5 dias e exige conta | T |
| 6 | Aviso de cotação comprada | A página avisa quando a cotação já virou pedido | A |

### 5.8 Fechar o pedido e pagar

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Endereço de entrega | Endereços salvos ou novo; o telefone é validado | A T |
| 2 | Frete | Opções de transportadora depois de informar o endereço; aceita conta própria do cliente | A T |
| 3 | Horário de corte | Faixa mostra quanto tempo falta para o pedido entrar na produção do dia | T |
| 4 | Cartão de crédito | Cartão salvo ou novo, processado pelo Stripe; aba para Google Pay | A T |
| 5 | Pedido de compra (PO) | Depois da aprovação de crédito: enviar o PDF do PO e digitar o número; aceita PO global | A |
| 6 | Outros pagamentos | Transferência, ACH e depósito direto enquanto o crédito não é aprovado | A |
| 7 | Isenção de imposto | Caixa a marcar em cada pedido; o imposto sai do total | A T |
| 8 | Forma de importação | Fictiv como importadora (DDP) ou envio por conta do cliente (EXW) | S T |
| 9 | Resumo do pedido | Produção, frete, imposto e total; em injeção separa ferramental, peças e amostras | A T |
| 10 | Confirmar | "Place order" só habilita com endereço, frete e pagamento definidos | T |
| 11 | Enviar ao sistema de compras | "Send to Punchout" leva os itens para o carrinho do sistema de compras da empresa | A |

### 5.9 Pedidos: acompanhamento e documentos

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Lista de pedidos | Página "Orders" com miniaturas das peças | A |
| 2 | Busca | Por nome do pedido, nome do arquivo ou número do PO | A |
| 3 | Rastreador de etapas | "View order detail" mostra a etapa atual, atualizada automaticamente | A |
| 4 | Rastreio do envio | Aba "Track Shipment" com status, número de rastreio e link da transportadora | A |
| 5 | Rever a configuração | Processo, material, acabamento e quantidade de cada peça; desenho para baixar | A |
| 6 | Modelo 3D do pedido | Abre o visualizador com o DFM e as roscas definidas | A |
| 7 | Fotos de inspeção | Fotos em alta resolução das peças reais, publicadas antes do envio | S A |
| 8 | Documentos de qualidade | Relatório de inspeção, certificado de conformidade e certificado de material para baixar | A |
| 9 | Recibo e fatura | Confirmação do pedido em PDF; fatura para pedidos com PO | A T |
| 10 | Informações alfandegárias | Em pedidos produzidos no exterior, formulário a preencher após a compra, com contagem regressiva de 48 h | A |
| 11 | Gerente de programa | Contato dedicado indicado no pedido | A |

### 5.10 Depois do pedido

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Pedir cancelamento | Pelo gerente de programa ou por `hello@fictiv.com`; só é atendido se a produção não começou | A |
| 2 | Alterar endereço ou frete | Possível até a data de envio | A |
| 3 | Mudança de engenharia (ECO) | Alteração de projeto, material ou prazo; costuma ter taxa e efeito no prazo | A |
| 4 | Reclamação de qualidade | Pedir autorização de devolução (RMA); a Fictiv conserta, refaz ou devolve o valor | A |

### 5.11 Biblioteca e recompra

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Biblioteca de peças | Guarda toda peça comprada com a configuração validada | S A |
| 2 | Busca e filtros | Por número da peça, arquivo, pedido, molde ou PO; filtro por data e comprador | T |
| 3 | Ficha da peça | Número e descrição editáveis; abas de revisões compradas, cotações ativas e atividade | T |
| 4 | Controle de revisão | Ao enviar um arquivo repetido, oferece usar a revisão existente, criar nova revisão ou tratar como peça nova | T |
| 5 | Recomprar da biblioteca | "Add to quote" em uma ou várias peças, para cotação nova ou existente | A |
| 6 | Recomprar de um pedido | "Reorder" gera a cotação já configurada | S T |
| 7 | Biblioteca de moldes | Lista os moldes do cliente; recomprar peças do molde ou pedir modificação | A T |
| 8 | Compartilhar peça | Adicionar a peça a espaços de trabalho | T |

### 5.12 Fictiv Teams

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Conta da empresa | Reúne os usuários da mesma empresa; mostra membros ativos e pendentes | A |
| 2 | Espaços de trabalho | "Team Workspaces" por time, projeto ou departamento; qualquer membro cria quantos quiser | A |
| 3 | Membros | Adicionar, remover, sair ou excluir o espaço; todo membro tem permissão total | A |
| 4 | Pedir entrada | Solicitar acesso a um espaço existente; qualquer membro aprova | A |
| 5 | Lista de espaços | Todos os espaços, com quantidade de cotações e pedidos, criador e membros | A |
| 6 | Cotações e pedidos do time | Criar no espaço ou adicionar os existentes; cada cotação fica em um só espaço; todos veem, editam, compram e recompram | A |
| 7 | Cotações privadas | Criadas em "My Quotes" ficam fora dos times | A |
| 8 | Busca dinâmica | Por arquivo, número do PO, número do pedido, comprador, dono da cotação ou e-mail | S A |
| 9 | Controles entre times | "Multi-Team Controls" dão visão das compras e dos acessos por projeto ou departamento | S A |
| 10 | Análise de gastos | "Team Spend Analytics" mostra gasto e economia do time ao longo do tempo | A |
| 11 | Repositório de documentos | Documentos de qualidade, DFM, arquivos de projeto, faturas e relatórios num só lugar | S |
| 12 | Recursos exclusivos | Otimizador de prazo, preço preferencial e Punchout só existem em contas Teams | A T |

### 5.13 Comércio exterior e conformidade

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | DDP e importadora | A Fictiv assume alfândega, tarifas e conformidade; o cliente vê o custo final antes de comprar | S |
| 2 | Controle de exportação | EAR99 e 9E991 seguem pelo site; outras classificações vão por formulário próprio, analisado por vendas e conformidade | A |
| 3 | Bloqueio de ITAR | Não aceita ITAR; ao marcar ITAR no envio, a cotação e os dados são apagados | A |
| 4 | NDA | Aceita acordo de confidencialidade a pedido do cliente | S |
| 5 | Anonimização | Remove dados de identificação dos modelos e desenhos antes de mandar ao parceiro | A |
| 6 | Guias de tarifas | Artigos de ajuda sobre tarifas e desembaraço aduaneiro | S |

### 5.14 IA e engenharia

| # | Função | O que faz | Fonte |
|---|---|---|---|
| 1 | Materials.AI | Recomenda material a partir de uma descrição em linguagem comum; também abre de dentro da configuração | S T |
| 2 | Escolha da fábrica | IA sugere o parceiro pelas capacidades comprovadas; engenheiros confirmam | S |
| 3 | Serviços de engenharia | Projeto de molde, análise por elementos finitos (FEA), consolidação da lista de materiais e avaliação de prontidão para lançamento | S |
| 4 | Consultoria de injeção | Reunião por vídeo com especialistas para projetos de moldagem | S |
| 5 | Análise de redução de custo | A equipe de suprimentos aponta onde cortar custo na lista de materiais | S |

### 5.15 Integrações

| # | Integração | O que faz | Fonte |
|---|---|---|---|
| 1 | Sistemas de compras | Punchout em cXML com SAP Ariba, Coupa, Microsoft Dynamics 365 e Zip | S A |
| 2 | Pagamento | Stripe e Google Pay | T |
| 3 | Transportadoras | Rastreio pela página da transportadora; conta DHL Express do cliente em envios internacionais | A |
| 4 | Migração do meviy | Há artigo de ajuda sobre a passagem do meviy (serviço de peças sob medida da MISUMI) para a Fictiv | S |
| 5 | API pública | Não encontrei nenhuma documentada | T |

---

## 6. Como o sistema funciona, passo a passo

### 6.1 Fluxo principal

1. O cliente cria a conta e entra na plataforma.
2. Escolhe o processo e envia os arquivos CAD, com os desenhos em PDF se houver.
3. O sistema analisa a geometria, cria a cotação e aponta problemas de fabricabilidade.
4. O cliente declara se é protótipo ou uso comercial e configura cada peça: material, acabamento, roscas, tolerâncias, inspeção e quantidade.
5. O sistema mostra o preço e as opções de prazo e região. Se alguma peça exigir revisão humana, o cliente pede a cotação e os engenheiros respondem.
6. O cliente escolhe o prazo e, se não for ele quem paga, encaminha a cotação ao comprador.
7. No fechamento, informa endereço, frete e pagamento, e confirma o pedido.
8. A Fictiv escolhe o fabricante parceiro e envia a ele o pacote técnico: modelo 3D, desenhos e folha de inspeção.
9. O parceiro fabrica e inspeciona. A qualidade da Fictiv revisa e publica fotos e relatórios no pedido.
10. As peças são embaladas e enviadas; o cliente acompanha o rastreio. Em pedidos internacionais há a etapa de alfândega.
11. O cliente recebe e confere. Havendo defeito, pede a devolução dentro do prazo (seção 7).
12. A peça entra na biblioteca, e a recompra parte da configuração já validada.

### 6.2 Estados de uma cotação `T`

| O que a página mostra | Significado | O que falta |
|---|---|---|
| "Required: Are these parts for prototype or commercial use?" | Uso ainda não declarado; preços ocultos | Escolher protótipo ou comercial |
| "Configure parts to receive lead times" | Há peça sem configuração | Configurar todas as peças |
| "Determining available lead times" | Sistema calculando | Aguardar |
| "Select regional preference" | Tudo configurado e com preço | Escolher uma das seis opções de prazo |
| "Please request a quote" e preços `$ --` | Alguma peça precisa de cotação manual | Pedir a cotação ou separar essa peça |
| Botão "Begin checkout" | Pronta para compra | Fechar o pedido |

### 6.3 Moldagem por injeção `A`

1. O cliente pede a cotação. Desde 2026 há preço instantâneo para peças simples, de extração direta; as demais são cotadas por engenheiros.
2. A Fictiv entrega, sem custo e antes da compra, um relatório preliminar de DFM: ângulo de saída, linha de fechamento, espessura e viabilidade das tolerâncias.
3. O cliente responde slide a slide, envia revisões do projeto e aprova. Se o projeto não for adequado ao processo, a Fictiv pode recusar.
4. Com o pedido feito, a Fictiv designa o parceiro e faz um segundo DFM, mais profundo: empenamento, ponto de injeção, linhas de solda, pinos extratores e gavetas.
5. Aprovado tudo, o molde é fabricado e saem as primeiras amostras (T1): a partir de 10 dias, ou cerca de 21 dias corridos em projetos mais complexos.
6. Depois da aprovação das amostras, a produção leva em média 4 a 7 dias úteis.
7. O molde fica guardado sem taxa enquanto houver pedidos a cada 2 anos. Passado esse tempo sem uso, é enviado ou destruído conforme o cliente decidir.
8. Mudanças no projeto são possíveis a qualquer momento: novo arquivo, novo DFM, nova cotação e novo lote.

### 6.4 Etapas de um pedido `T`

| Etapa | O que acontece |
|---|---|
| Production Assignment | A Fictiv escolhe o parceiro; não há leilão |
| Manufacturing | Fabricação |
| Partner Inspection | O parceiro mede e fotografa as peças |
| Quality Review | A qualidade da Fictiv revisa fotos e dados, à distância ou no local |
| Packing & Shipping | Embalagem, envio e publicação do número de rastreio |

A documentação oficial confirma o rastreador de etapas e a dupla inspeção (parceiro e Fictiv), mas não li nela os nomes das etapas.

### 6.5 Regras de prazo

- O prazo conta em dias úteis; fins de semana e feriados de produção ficam de fora. `A`
- A produção é programada uma vez por dia. Pedido feito depois do horário de corte começa no dia útil seguinte. `A`
- O horário de corte é 15h (horário do Pacífico) segundo a Central de Ajuda; a descrição de terceiros viu 20h na tela de fechamento. `A T`
- Todas as peças da cotação são enviadas juntas, pelo prazo da mais demorada. Para liberar as rápidas, mover as lentas para outra cotação. `A`
- Acabamentos, inspeções avançadas e eletroerosão somam dias. `T`
- Produção no exterior segue para os EUA em 4 dias úteis. `A`

### 6.6 Escolha do fabricante e qualidade `S` `A`

- O pedido é comparado com as capacidades comprovadas dos parceiros e confirmado por engenheiros de manufatura.
- Para entrar na rede, a fábrica passa por seleção, auditoria de certificações, auditoria de registros, auditoria no local e fabricação de uma peça de teste. Começa em status provisório, com trabalhos mais simples e acompanhados.
- Cada pedido gera uma nota de desempenho do parceiro. Quem não mantém o padrão sai da rede.
- Toda peça é inspecionada pelo parceiro e verificada pela Fictiv. A inspeção padrão confere dimensões críticas com instrumentos manuais e a aparência; máquina de medir por coordenadas, laser, inspeção de primeira peça e PPAP ficam disponíveis a pedido.
- O site cita ISO 9001:2015 no sistema da qualidade e parceiros com AS9100, ISO 13485 e IATF 16949.

### 6.7 Proteção dos arquivos do cliente `S` `A`

- Só o parceiro escolhido recebe os arquivos, sob acordo de confidencialidade repassado pela Fictiv.
- Dados de identificação são removidos dos modelos e desenhos antes do envio.
- Projetos com controle de exportação fora de EAR99 e 9E991 só entram depois de análise de vendas e conformidade, num armazenamento de arquivos em conformidade com o FedRAMP.

---

## 7. Regras de negócio

| Regra | Detalhe | Fonte |
|---|---|---|
| É preciso modelo 3D | A Fictiv não projeta peças e não cota a partir de foto, desenho 2D isolado ou peça física | A |
| Formato recomendado | STEP, uma peça por arquivo; também aceita formatos nativos de SolidWorks, Siemens, Autodesk, PTC e outros | A T |
| Malha só em impressão 3D | STL, OBJ e similares não servem para CNC, injeção nem fundição em uretano | A |
| Formatos recusados | IGES, F3D, DXF, desenhos nativos e arquivos nativos de chapa do Solid Edge | A |
| Desenho | Só em PDF e sempre junto de um modelo; não é aceito em impressão 3D | A |
| Um corpo sólido por arquivo | Arquivos com vários corpos perdem o preço instantâneo ou são recusados; em impressão 3D há exceções | A T |
| Arquivo fechado | Malha com buracos precisa ser reparada antes do envio | A |
| Tolerância padrão | ISO 2768 médio quando não há desenho | T |
| Validade da cotação | 30 dias, salvo indicação diferente na cotação | T |
| Cancelamento | Pelos Termos, pedido feito não pode ser cancelado; na prática a Fictiv tenta atender se a produção não começou | A |
| Devolução | Peça com defeito deve voltar com autorização (RMA) em até 72 horas após a entrega | A |
| Peça sem defeito | Se a análise concluir que a peça está conforme, o cliente paga os custos da inspeção | A |
| Resposta a pedido de mudança | Quando a Fictiv pede alteração no pedido, o cliente tem 1 dia útil para responder; sem resposta, o pedido é cancelado | A |
| Destinos de entrega | Estados Unidos e Canadá; outros países pelo setor de vendas | T |
| Canadá | Envio por conta do cliente (EXW), que é o importador | T |
| Pagamento por PO | Exige aprovação de crédito; prazo padrão de 30 dias | A |
| Moeda | Dólar americano | T |
| Isenção de imposto | Precisa ser habilitada na conta e marcada em cada pedido | A |
| Controle de exportação | Só EAR99 e 9E991 pelo site; ITAR nunca | A |
| Recursos por tipo de conta | Moldagem, fundição, PO e Materials.AI pedem e-mail corporativo verificado | T |
| Punchout | Só para cotações configuradas e precificadas pela plataforma; cotações sob medida ficam de fora | A |

---

## 8. Catálogo de fabricação

### 8.1 Processos

| Processo | Variações | Prazo anunciado | Volume e tolerância | Fonte |
|---|---|---|---|---|
| Usinagem CNC | Fresamento, torneamento, eletroerosão; 3 e 5 eixos | 1 a 10 dias | 1 a 10.000 peças; até ±0,0001" | A T |
| Impressão 3D | FDM, SLS, SLA, PolyJet, MJF, Carbon DLS | A partir de 1 dia | Protótipos e baixos volumes | S A |
| Chapa metálica | Corte, dobra, solda, ferragens | 5 a 15 dias | 1 a 50.000 peças; ±0,005" | A T |
| Injeção de plástico | Moldes de produção, familiares e multicavidade; sobreinjeção | Amostras a partir de 10 dias; 2 a 6 semanas | 500 a mais de 1 milhão; ±0,005" | S A T |
| Fundição em uretano | Moldes de silicone | 7 a 10 dias | Dezenas a centenas de peças | S T |
| Fundição sob pressão | Alta e baixa pressão; usinagem posterior | 10 a 15 dias | Ligas de alumínio, zinco e magnésio | S T |
| Moldagem por compressão | Borrachas e compósitos | 3 a 6 semanas | 100 a 50.000 peças; ±0,010" | A |

Serviços complementares `S` `A`: acabamentos, montagem e solda, serviços de engenharia, peças de reposição (MRO) e usinagem de peças grandes, de até 10 pés (cerca de 3 m).

### 8.2 Materiais e acabamentos `T`

Listas vistas no configurador em setembro de 2026, segundo a descrição de terceiros. As notas de versão oficiais confirmam vários desses materiais.

| Processo | Materiais |
|---|---|
| CNC, metais | Alumínio 2024, 5052, 6061, 6063, 7050, 7075, MIC-6; inox 303, 304, 316, 410, 416, 420, 440C, 15-5, 17-4, A286; aços 1018, 1045, 4130, 4140, 4340, 8620, A36, aços-ferramenta A2, D2, O1; Inconel 625 e 718; cobre, latão, bronze; titânio graus 2 e 5; magnésio, Invar, Kovar |
| CNC, plásticos | ABS, acrílico, PVC, Delrin, G-10, HDPE, nylon, PEEK, policarbonato, polipropileno, PPS, PTFE, Torlon, UHMW, ULTEM |
| Impressão 3D | SLS: nylon 12 e TPU. MJF: PA 12. SLA: linhas Accura e Somos. FDM: ABS, ASA, PETG, policarbonato, Ultem. PolyJet: linha Vero e borracha. Carbon DLS: EPU, EPX, FPU, MPU, RPU, UMA |
| Chapa | Alumínio 5052, 6061, 7075; inox 301, 303, 304, 316, 430; aço carbono e galvanizado; latão, cobre, bronze, titânio |
| Injeção | ABS, POM, PA66, PBT, PC, PC/ABS, PEEK, PEI, PMMA, PP, PPS, TPE, TPU, silicone líquido, entre outros; resinas sob medida |
| Uretano | Similares a ABS, acrílico, nylon, POM e PP; elastômeros de 20A a 90A |
| Fundição sob pressão | Alumínio ADC12, A380, A383, A390; Zamak 3 e 5; magnésio AZ91D |
| Compressão | Silicone, SBR, borracha natural, neoprene, NBR, FKM, HNBR, PU, EPDM |

| Família | Acabamentos |
|---|---|
| Alumínio | Anodização tipo II e tipo III, cromatização, níquel químico, jateamento, niquelação, pintura a pó, tamboreamento |
| Aço e inox | Oxidação negra, passivação, eletropolimento, zincagem, níquel químico, pintura a pó, tratamento térmico |
| Plásticos | Polimento manual em acrílico, polimento a vapor em policarbonato, alisamento a vapor em MJF |
| Injeção | Texturas SPI e Mold-Tech, tampografia, metalização, gravação a laser |

---

## 9. Central de Ajuda: índice dos artigos

São 6 coleções e 69 entradas, das quais 64 são artigos diferentes (alguns aparecem em mais de uma coleção). `S`

**Getting Started (14)**
- How to seamlessly transition from meviy to Fictiv
- Should I use a personal email or company email for my Fictiv account?
- How to Generate and Annotate 2D Drawings
- How to Initiate the NDA process
- What material should I choose?
- Can you design a part I need?
- How do Fictiv's lead times work?
- What are Fictiv's production holidays?
- What infill do you use for 3D printing?
- Can you deliver parts to my location?
- How do you handle IP/confidentiality?
- Optimizing part design for CNC machining
- How to get started with Fictiv
- What to expect with 3D printing

**Getting a Quote (14)**
- How to use the multi-quantity quote feature
- How to seamlessly transition from meviy to Fictiv
- How to Submit an Export-Controlled Project
- Multiple body files in 3D printing
- What happens after I request an exact CNC quote?
- How long does it take to get a quote?
- How do I view and respond to DFM feedback?
- How do I download a PDF quote?
- How do I use the Auto Thread Detection feature?
- How do I request hardware installation?
- How do I add finishing to my parts?
- How to get parts quoted with attached drawings
- How do I select a lead time for my quote?
- How do I review and approve an Injection Molding DFM report?

**Placing an Order (10)**
- How to use the multi-quantity quote feature
- How do I use Drawings Reconciliation?
- How to Submit an Export-Controlled Project
- Know the Full Cost Upfront With Built-In DDP & IoR Services
- Guide to International Shipping
- What if I'm a tax-exempt reseller?
- How do I download my order invoice or receipt?
- How do I place an order using a purchase order?
- How do I place a reorder?
- How to share a Fictiv quote

**Uploading and Organizing Parts (7)**
- How do I use Drawings Reconciliation?
- How do I choose and change units for my parts?
- What do I do if my file is not watertight?
- Why won't my file upload?
- Maximum build sizes for 3D printed and CNC machined parts
- What file formats does Fictiv support?
- How to move parts between quotes

**Production and Fulfillment (12)**
- How to seamlessly transition from meviy to Fictiv
- Tariffs 101 Q&A: A Guide for Manufacturers
- Understanding Section 232 Tariffs
- How Does Injection Molding with Fictiv Work?
- What is your return/remake policy?
- Discrepancies between 2D drawings and 3D models
- Customs clearance tips for international shipping
- Can I cancel or make changes to an existing order?
- What happens after I place an order?
- How do I track and manage my orders?
- How do I find my orders?
- Fictiv DDP Shipment Upgrade Program for International Orders

**Fictiv Teams (12)**
- Inspection reports and certificates of conformance
- How to use the Lead Time Optimizer
- What is Preferred Pricing?
- What is Team Spend Analytics?
- Sharing quotes outside of your team
- What quotes and orders are visible to me and my team?
- Managing quotes and orders in a team
- Creating and managing a team
- What are Team Workspaces?
- Setting Up Your Punchout Integration with Procure-to-Pay (P2P) Systems
- Getting started with Fictiv Teams
- What are your standard manufacturing tolerances?

**Fora das seis coleções** (encontrados por links e busca)
- How to use Fictiv's Mold Library to place reorders and request modifications
- How to Reorder Parts from Your Library
- How do I respond to an Injection Molding DFM report?
- Updates to Export Control Compliance at Fictiv

---

## 10. Linha do tempo dos recursos

Datas das notas de versão oficiais (2022 e 2023), do próprio site (2025 e 2026) e da imprensa (compra pela MISUMI). Onde está "aprox.", a data não aparece escrita e foi deduzida. `S` `A`

| Quando | Novidade |
|---|---|
| Mar/2022 | Abas "Part Status" e "Track Shipment" no pedido; miniaturas das peças |
| Abr/2022 | Cotação instantânea para titânio; aviso de bloqueio de login; texto editável no desenho gerado |
| Mai/2022 | Desenhos gerados por processo; recado ao compartilhar cotação |
| Jul/2022 | "Forward to Purchaser"; 22 novos materiais de CNC; novo DFM de injeção com anotações |
| Ago/2022 | Registro de atividade da cotação; DFM no PDF e na recompra |
| Set/2022 | Lançamento do Fictiv Premium (assinatura anual): espaços de trabalho, controles entre times, otimizador de prazo, preço preferencial; DFM de injeção em 3D; contagem de 48 h para dados alfandegários |
| Out/2022 | Busca de pedidos; conta DHL Express; botão "Close and notify" |
| Nov/2022 | Busca dentro dos times; local de produção da injeção; polimentos e eletropolimento |
| Dez/2022 | Gestão de membros da conta da empresa; botão de convite |
| Jan/2023 | CNC de até 10 pés (cerca de 3 m); mais padrões de rosca; validação de telefone; pedido de isenção de imposto; lista de espaços de trabalho |
| Fev/2023 | Team Spend Analytics |
| Mai/2023 | Certificado de material com preço automático; pedido de entrada em espaço de trabalho; envio do exterior em 4 dias úteis |
| Ago/2023 | Várias velocidades de produção em impressão 3D; 14 novos materiais 3D |
| Set/2023 | Integração com SAP Ariba, Coupa e Dynamics 365; preenchimento em FDM; estimativa de injeção; data de entrega no lugar da data de envio |
| Out/2023 | Insertos roscados e filtro de materiais em 3D; tratamento térmico em CNC |
| Nov/2023 | Carbon DLS; três níveis de inspeção e certificado de conformidade para impressão 3D |
| Dez/2023 | Cores sob medida por Pantone e RAL |
| Abr/2025 | Anúncio da compra pela MISUMI |
| 2025 (aprox.) | Serviços de gestão de tarifas, DDP e importadora |
| Dez/2025 | Vídeo da Parts Library |
| Mar/2026 | Vídeo da Drawing Annotation Tool |
| Mai/2026 | Vídeo do Materials.AI |
| 2026 (aprox.) | Cotação instantânea de injeção para peças simples; cotação com até 5 quantidades |

---

## 11. Observações técnicas e defeitos notados

### Site público `S`

- O site roda em WordPress com tema próprio (`fictiv-theme`); as imagens estão em WebP.
- Algumas páginas trazem dois menus no código: um novo, com links marcados `?src=nav&variant=navE`, e o antigo. Isso indica teste A/B ou troca de menu em andamento.
- A Central de Ajuda foi migrada de `help.fictiv.com` para `/help` dentro do site. Os endereços antigos ainda aparecem nos buscadores.
- O `robots.txt` libera o site, exceto `/admin/`, `/api/`, `/checkout/` e `/account/`. Tem regras específicas para robôs de IA e bloqueia dois deles.
- O `robots.txt` publicado começa com o título "Proposed robots.txt Configuration" e marcas de formatação. Parece um rascunho colado como estava.
- `/sitemap.xml` devolveu erro 500 na minha leitura. Não sei se a falha é do site ou do meu acesso.
- Na página inicial, três imagens do bloco "Digital Manufacturing Resources" apontam para o endereço `/Array`. Provavelmente não carregam.
- No menu antigo, "MRO Services" leva à página da plataforma; no novo, leva a `/mro-solutions`.
- Um vídeo-guia de CNC diz que o envio aceita IGES e STL, mas a Central de Ajuda diz que IGES não é aceito e que malha só serve para impressão 3D.

### Plataforma `T`

- Rotas citadas: `/home`, `/pages/quotes`, `/pages/quotes/upload`, `/pages/quotes/<id>`, `/pages/orders/quote/<id>` (fechamento), `/orders`, `/library/parts`, `/pages/my-account`.
- Os nomes de classes citados (`ant-table-row`, `ant-modal-content`) são da biblioteca de componentes Ant Design. Isso é dedução minha.
- Os campos de cartão são do Stripe, carregados em quadro separado.
- A descrição cita um serviço GraphQL interno e afirma não haver API pública documentada.

---

## 12. O que não foi verificado

- **Nenhuma tela interna foi vista por mim.** Tudo o que está marcado só com `T` depende da descrição de terceiros.
- **Campos dos formulários** de cadastro, contato, NDA e cotação de produção: sei que existem, mas não li os campos.
- **Rodapé e páginas legais**: a leitura não trouxe o rodapé. As regras dos Termos citadas aqui vêm de uma cópia de 2022 publicada em `fictivlabs.com/terms`; o texto atual pode ser diferente.
- **Páginas lidas só pelo menu**: setores, a maioria das páginas de processo, sobre a empresa, carreiras, imprensa e eventos.
- **Preços**: não existe tabela; todo preço depende da peça.
- **Custo do plano Teams hoje**: em 2022 era uma assinatura anual paga (Fictiv Premium); não confirmei a condição atual.
- **Lista completa de páginas**: sem o sitemap, o mapa da seção 3 vem do menu e dos links.

---

## 13. Glossário

| Termo | Significado |
|---|---|
| CAD | Modelo 3D da peça feito em programa de projeto |
| DFM | *Design for Manufacturability*: análise de quão fácil é fabricar a peça |
| RFQ | *Request for Quote*: pedido de cotação feito por pessoas, não pelo sistema |
| PO | *Purchase Order*: pedido de compra emitido pela empresa cliente |
| Punchout | Ligação entre o site do fornecedor e o sistema de compras do cliente |
| cXML | Formato de troca de dados usado pelo Punchout |
| P2P | *Procure-to-Pay*: sistema de compras e pagamentos da empresa |
| DDP | *Delivered Duty Paid*: entrega com impostos de importação pagos pelo vendedor |
| IoR | *Importer of Record*: quem responde pela importação perante a alfândega |
| EXW | *Ex Works*: o comprador cuida do transporte e da importação |
| ECO | *Engineering Change Order*: pedido de mudança de engenharia |
| RMA | Autorização de devolução de mercadoria |
| CoC | Certificado de conformidade |
| FAI | Inspeção de primeira peça |
| CMM | Máquina de medir por coordenadas |
| PPAP | Processo de aprovação de peça de produção, comum no setor automotivo |
| T1 | Primeiras amostras tiradas de um molde novo |
| MRO | Manutenção, reparo e operação: peças de reposição |
| NPI | Lançamento de novo produto |
| BOM | Lista de materiais de um produto |
| EAR / ITAR | Regras americanas de controle de exportação; ITAR cobre itens de defesa |
| ECCN | Código de classificação de exportação dentro do EAR |

---

## 14. Fontes

**Páginas lidas diretamente em 14/11/2026 (marca S)**
- https://www.fictiv.com/
- https://www.fictiv.com/why-choose-fictiv/our-platform
- https://www.fictiv.com/why-choose-fictiv/how-it-works
- https://www.fictiv.com/why-choose-fictiv/compare
- https://www.fictiv.com/teams
- https://www.fictiv.com/tools
- https://www.fictiv.com/help e as seis páginas de coleção em `/help/...`
- https://www.fictiv.com/articles/fictiv-release-notes
- https://www.fictiv.com/robots.txt

**Documentação oficial lida por trechos (marca A)**
- Artigos da Central de Ajuda: primeiros passos, formatos de arquivo, DFM, DFM de injeção, desenhos anexados, escolha de prazo, funcionamento dos prazos, otimizador de prazo, preço preferencial, criação e gestão de times, visibilidade de cotações, recompra pela biblioteca, pedido de compra, cancelamento e mudanças, Punchout, projetos com controle de exportação, acompanhamento de pedidos
- https://www.fictiv.com/our-network
- https://www.fictiv.com/quality-assurance
- https://www.fictiv.com/why-choose-fictiv
- https://www.fictiv.com/capabilities
- https://www.fictiv.com/capabilities/injection-molding-services
- https://www.fictiv.com/inside-the-factory
- https://www.fictiv.com/misumi
- https://www.fictiv.com/articles/premium
- https://www.fictiv.com/articles/design-validation-thats-disrupting-injection-molding
- https://www.fictivlabs.com/terms (cópia de 2022 dos Termos)

**Terceiros (marca T)**
- https://github.com/K-Dense-AI/scientific-agent-skills, pasta `skills/fictiv`, versão `2d2065f` de 09/11/2026

**Imprensa**
- https://www.freightwaves.com/news/fictiv-acquired-for-350m-by-japanese-components-supplier
