# PLANO — inemaSEO 1 · Fundação: o raio-x e o alicerce do seu site (v7.2)

Curso 1 de 6 (piloto) da Formação inemaSEO. Público: dono de site ou pequeno negócio, sem experiência em SEO. Ordem da formação: 1 → 2 → 3 → 4 → 5 → 6.

Fontes (não alteradas): `~/projetos/inemaseo-metodo` (docs/METODO.md, docs/CHECKLIST.md, tools/, templates/), `~/projetos/inemaseo` (FALHAS.md, reports/ — números só da lista "Casos reais" do BRIEF), `~/projetos/inemaseo-pratica` (vídeo), e a pesquisa `wifi/longrun/2026-10-19-formacao-inemaseo-v72/TENDENCIAS-SEO-GEO-2026-10.md` (régua de 2026).

## As 8 aulas

| # | slug | aula | objetivo (≤ 160) | diagrama | prática ("pronto quando") | fonte |
|---|---|---|---|---|---|---|
| 1 | `como-acham` | Como Google, Bing e as IAs acham um site | explicar o caminho rastrear → indexar → mostrar → citar e escolher o que fazer primeiro no seu site | rastrear → indexar → mostrar (Google/Bing) → citar (IAs) | 1) escrever as 3 perguntas-teste do seu assunto e rodar em 2 assistentes; 2) anotar em 3 linhas o que o seu site tem que só você pode dizer | METODO intro e 3 princípios; TENDENCIAS §1.4; vídeo |
| 2 | `raio-x` | Raio-x só de leitura | rodar o auditoria.sh no seu site e ler cada linha da saída como o buscador lê | site → curl (sem JS) → redirecionamentos / robots / sitemaps / páginas → achados | 1) rodar a auditoria na home + 2 páginas e salvar em `raio-x.txt`; 2) lista de 3 achados com a linha da saída | `tools/auditoria.sh`; METODO etapa 1; §2.4 |
| 3 | `search-console-bing` | Search Console e Bing Webmaster | conferir se o site já está verificado e verificar no Search Console e no Bing Webmaster | DNS TXT → propriedade de domínio → Bing importa do GSC → sitemap enviado | 1) `dig TXT` anotado; 2) as duas contas mostram o site verificado e o sitemap com status "sucesso" | METODO etapa 1/10; `inemaseo/FALHAS.md` 23/09 |
| 4 | `canonico` | Um canônico só | escolher www ou sem www e fazer canonical, sitemap, JSON-LD e links usarem o mesmo endereço | versões do endereço → 301 → canônico escolhido → conferir em 4 lugares | 1) as 3 variações levam à mesma URL (saída do raio-x); 2) tabela dos 4 lugares sem divergência | METODO etapa 2; §2.4 (`/conhecimento/`) |
| 5 | `sitemaps-hreflang` | Sitemaps e hreflang | gerar o sitemap do mesmo dado das páginas, com data real e hreflang recíproco quando houver tradução | dado → páginas + sitemap → lastmod real → hreflang em cada página | 1) 3 URLs do sitemap com `lastmod` igual à data da última mudança; 2) se houver tradução, ida e volta do hreflang conferidas | METODO etapa 2 e "Multilíngue" |
| 6 | `robots-por-finalidade` | robots.txt por finalidade | decidir no robots.txt e no painel da CDN o que liberar para busca, para ação do usuário e para treino | robôs → busca / ação do usuário / treino → robots.txt (pedido) → CDN (imposição) | 1) robots.txt com os 3 grupos e o motivo de cada decisão; 2) painel da CDN conferido e anotado | `templates/robots.txt`, `templates/llms.txt`; TENDENCIAS §2.2–2.5, §4.1, §4.2 |
| 7 | `pagina-rasa` | Página rasa sai do índice | identificar páginas rasas e tirá-las do índice e do sitemap até terem corpo próprio | lote de páginas → teste (palavras, repetição, link) → noindex + fora do sitemap → volta com corpo | 1) lista das 5 páginas mais finas com nº de palavras; 2) as que ficaram: `noindex` e fora do sitemap, conferido no raio-x | METODO etapa 2 e Plano B; §2.3 |
| 8 | `avisar-conferir` | Avisar os buscadores e conferir | avisar IndexNow e Bing só com URLs 200 e conferir a indexação na inspeção de URL | publicar → conferir 200 → IndexNow/Bing → inspeção de URL → plano da semana | 1) chave IndexNow publicada e primeiro envio com HTTP 200/202; 2) 5 URLs-chave inspecionadas com o estado anotado; plano datado pelo gerador | `tools/avisar_buscadores.sh`, `tools/gsc_inspecionar.py` (só modelo); §2.5; `inemaseo/FALHAS.md` 02/10 |

Aula 8 fecha com `mapa` (4 degraus: raio-x, painéis, alicerce, avisar) + `gerador` (as 8 aulas).

## Simconversa da aula 6 — "o dono da pousada quer bloquear todas as IAs"

Personagem: dono de pousada, site pequeno, reservas vindas de busca. Ficção rotulada; o que ensina vem de TENDENCIAS §2.2–2.5, §4.1, §4.2.

| fala | cliente | opções (nota → destino) |
|---|---|---|
| `abre` | "quero bloquear todas as IAs no robots.txt" | bloquear tudo agora (0 → `fim-sumiu`) · perguntar o que incomoda: treino ou ser recomendado (2 → `finalidade`) · "robots é só pedido, não adianta" (1 → `pedido`) |
| `pedido` (desvio) | "então faço o quê?" | separar por finalidade (1 → `finalidade`) · bloquear todo robô na CDN (0 → `fim-sumiu`) |
| `finalidade` | treino incomoda; reservas vêm de gente perguntando ao celular | bloquear treino, liberar busca e ação do usuário (2 → `cdn`) · bloquear o Googlebot também (0 → `fim-sumiu`) · bloquear só o GPTBot (1 → `cdn`) |
| `cdn` | "o site está no Cloudflare gratuito, muda algo?" | conferir no painel o bloqueio padrão de 15/09/2026 (2 → `llms`) · "robots manda em tudo" (0 → `fim-cego`) |
| `llms` | "me ofereceram um llms.txt que garante o ChatGPT" | opcional e barato, sem evidência de citação (2 → `fim-bom`) · comprar (0 → `fim-llms`) · "nunca faça" (1 → `fim-bom`) |

Somas à mão: melhor caminho direto 2+2+2+2 = 8; pelo desvio 1+1+2+2+2 = 8 (não passa do direto). Máximo = 8.

## Decisões tomadas sozinho
- Vídeo da aula 1 = o publicado (411 s). Ele repete três falas que a régua de 2026 corrige (llms.txt como "mapa para as IAs", robots "senão a IA não cita", 40–60 palavras "formato que a IA cita"); a aula 1 tem um bloco "o que mudou desde o vídeo".
- `templates/robots.txt` põe ClaudeBot no grupo de busca; ele é de treino (Anthropic). A aula 6 mostra o modelo reorganizado por finalidade e explica a diferença; o repo de origem não muda.
- FAQPage não aparece neste curso (fica para o curso 2, dizendo que o rich result acabou em 07/05/2026).
- Saída do `auditoria.sh` contra www.inema.club capturada em 19/10/2026 entra só dentro do bloco `saida` (selo "real"), não como número de caso no texto.
- Ligação ChatGPT–Bing sempre como "estudo da Seer, não declaração da OpenAI".
- Cloudflare 15/09/2026: TENDENCIAS só leu cobertura; a aula diz "confira no painel do seu site".

## Convenções para os cursos 2–6 (piloto)
- `curso.json`: `icone` **"lupa"** em toda a formação; `nome` "inemaSEO N — <Tema>: <promessa>"; `sub` "Formação inemaSEO · curso N de 6"; `volta` área inemaSEO; `lado_card` aponta o próximo curso; `inicio.kicker` "Formação inemaSEO · curso N de 6 · 8 aulas"; `inicio.cursos` NÃO usado no piloto (os irmãos ainda não existem).
- `inicio.blocos`: "Para quem é" / "O que você sai fazendo" / "Onde este curso entra na Formação inemaSEO" (lista os 6 cursos em uma linha cada).
- Aula: diagrama → passos → codigo (comando real com `saida`) → [simconversa] → pratica (2 exercícios, ids `e1`/`e2`) → quiz (4 perguntas) → resumo → links.
- Cada aula termina o `resumo` com uma linha "Régua de 2026" quando o tema tem moda (llms.txt, FAQ, 40–60 palavras, Bing/ChatGPT).
- Glossário `i18n/glossario.json` deste repo serve de base para os 5 seguintes.
- Vídeo só no curso 1 (EN/ES tocam o áudio PT; pendente motor aceitar `mp4_en`/`vtt_en`).

## Resultado do piloto (19/10/2026)
- Publicado: https://inematds.github.io/formacao-inemaseo-fundacao-v72/ (+ `en/`, `es/`), todos 200.
- Portão: `validar.py` OK em PT/EN/ES (único link falho: curso 2, ainda não publicado); `conferir-tela.cjs` 27 páginas × 2 larguras OK, simconversa percorrida (máx. 8).
- Imagens: 10/10 pelo Codex na 1ª tentativa (script sequencial em segundo plano enquanto o conteúdo era escrito); nenhuma reserva flux.
- Motor 7.5.6: `validar.py` acusava "sobra TODO" em links para `METODO.md`; agora só palavra inteira.

## Lições para os cursos 2–6
- Rode o script de imagens em segundo plano logo depois do PLANO.md: 10 imagens levam ~40 min e não bloqueiam a escrita.
- `i18n/glossario.json`: copie este e acrescente os termos do curso. "alicerce" = groundwork (foundation já é "Fundação" e repetia no título EN).
- Varredura de sobras PT no ES: "página" e "buscador" são espanhol válido; procure "você", "não", "aula", "também".
- Ao citar ferramenta/fonte com caso do INEMA: número no texto só da lista "Casos reais"; saída capturada de script fica dentro de `saida` (selo real, com data).
- Templates do inemaseo-metodo divergentes da régua (robots.txt com ClaudeBot em "busca", llms.txt como etapa, "40–60 palavras" como técnica de IA): mostre adaptado e diga por quê, sem alterar o repo de origem.
- `<details>` e outros nomes de tag em texto de quiz/passos viram tag; escreva por extenso ou `&lt;details&gt;` só dentro de `saida.html`.
