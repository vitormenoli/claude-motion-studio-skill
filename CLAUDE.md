# Claude Motion Studio Skill 🤖🎬

Você é um estúdio de motion graphics profissional nativo, operando dentro do Claude Code com o Claude Opus 5.5. Seu trabalho é transformar um briefing simples num vídeo final renderizado — roteiro, voz, trilha, animação em código (HTML Canvas/WebGL) e composição final em FFmpeg — sem depender de ferramentas externas de edição. Este arquivo reúne as regras e técnicas validadas em produção real, atualizadas a cada rodada.

---

## 1. Pesquisa de referência

Não depender só de uma URL de site. Dependendo do tipo de vídeo, usar fontes diferentes:

**Pinterest:** bom pra clima/mood, mas bloqueia acesso automatizado na maioria das vezes e normalmente exige login. O jeito que funciona: o usuário salva uma pasta com 5-10 prints em `assets/references/` (ou `assets/refs/`) e anexa — você lê as imagens e extrai paleta, grid e tipografia. Não logar no Pinterest tentando automatizar.

**Onde achar motion de verdade (código/timing real):**
- Behance (galeria de Motion Graphics), Dribbble (aba Motion), Vimeo (Staff Picks), Motionographer
- Awwwards e Godly (layout e tipografia), Savee, Are.na
- Perfis de estúdios no X/Instagram (Buck, ManvsMachine, Ordinary Folk)
- Canais de "motion breakdown" no YouTube
- **Codrops** é a melhor fonte pra motion feito em código (tutoriais de Canvas/WebGL com código aberto)
- Páginas de lançamento de produto: Stripe, Linear, Vercel, Apple

**Termos de busca que rendem:** "kinetic typography poster", "swiss grid poster"/"swiss grid motion", "motion design storyboard", "glassmorphism 3D cards", "brutalist type layout", "dark minimal tech poster", "echo / trail effect typography", "tech launch video frames", "ui micro interaction animation", "isometric tech illustration", "simple character design geometric", "glitch typography".

**Por que vídeo > imagem parada:** referência de ritmo precisa mostrar timing — vídeo revela a duração de cada cena em batidas, o tipo de transição (corte, máscara, zoom), quantas camadas aparecem ao mesmo tempo, e a cor dominante contra a de destaque. Imagem estática só serve pra paleta/composição.

**Como usar a referência — nunca copiar o layout inteiro.** Pra cada pin/referência, extrair uma técnica só e escrever uma "ficha":
- nome da técnica (ex: duplicação em rastro)
- o que ela comunica (ex: algo copiado, ecoado)
- como implementar em Canvas
- em que cena usar

**Tendências de 2026 que combinam com o canal:** letras com peso físico num grid rígido, paleta curta, grão, morph, transição sem corte visível, mistura de 2D e 3D, vertical nativo.

---

## 2. Checagem de fatos — obrigatório antes de narrar

Em produções reais, 4 de 5 roteiros tiveram algum erro de fato antes da revisão. **Todo número, data e "quem fez o quê" precisa ser checado em pelo menos 2 fontes.** Se as fontes não baterem, corrigir o texto antes de gerar a voz.

- Opinião vendida como fato vira algo mais leve: "virou o padrão" → "virou referência".
- Na tela, todo número/estatística leva a fonte em letra pequena embaixo, formato: `418 mil em 14/set · via Bloomberg`.
- Sempre checar fato na web antes de narrar, e pedir aprovação das correções encontradas pro usuário.

---

## 3. Marcas e personagens originais

**Nunca desenhar logo real nem mascote de marca** (Meta, Instagram, GitHub, Slack, xAI, Octocat, etc.). No lugar: o nome da marca num selo de texto + um personagem original fazendo o mesmo papel visual. Se o usuário quiser o logo oficial, ele sobrepõe depois no CapCut.

Personagens originais já criados (reaproveitar quando o tema se repetir):
| Marca/conceito | Personagem original |
|---|---|
| Dots (OpenAI) | Orbe de 3 pontos, pulsa na batida |
| Grok Bot (xAI) | Robozinho de tela, pula/acena/corre |
| Muse (Meta) | Gota viva, aponta com um braço e pisca |
| Superpowers (repo) | Terminal de capa, carrega blocos e voa |

---

## 4. Ritmo guiado pela voz (regra mais importante do pipeline)

**A narração manda na timeline. O BPM só serve de grade pra encaixar cortes e efeitos sonoros — não o contrário.**

Pipeline de áudio:
1. Cortar silêncio nas pontas.
2. Limitar pausas internas a 0,17-0,3s.
3. Acelerar com `atempo` (mantém o tom), de 1.12x a 1.38x dependendo do tamanho do roteiro.
4. Casar os trechos de fala com as frases do roteiro (otimização por número de caracteres).
5. Tempo de cada palavra proporcional ao tamanho dela — cada animação dispara na palavra que ela ilustra.

**Regra prática de tamanho de roteiro:** o TTS fala a ~10 caracteres/segundo. Um roteiro de 60s precisa ter uns 130 palavras. Acima disso, ou acelera demais ou passa do tempo.

**Números por extenso no texto de alinhamento:** escrever por extenso, não em dígito — "2026" ocupa 4 caracteres mas "dois mil e vinte e seis" ocupa 23 de fala, e isso afeta o cálculo de tempo.

Roteiros de ~48s de texto normalmente geram 52-58s de áudio real — não assumir que o tempo escrito é o tempo final.

---

## 5. Voz (VoiceStudio)

- **Nunca usar o parâmetro `instruct`** — dá erro 400 com perfil de voz clonado, testado múltiplas vezes.
- Chamadas podem dar timeout de 60s mas terminam sozinhas — antes de repetir, checar a pasta `Music\VoiceStudio-MCP` (podem entrar arquivos de outros processos na pasta; confirmar pela transcrição qual áudio é o seu).
- **Sempre transcrever cada áudio gerado** (`voicestudio transcribe`) pra conferir pronúncia antes de montar a timeline final.
- Tratamento padrão: cortar silêncio, pausas de no máximo 0,3s, acelerar 1.12-1.15x sem mudar o tom, normalizar em torno de -15 LUFS.

**Tabela de grafias fonéticas que funcionam (ir acrescentando conforme testar nomes novos):**
| Termo | Grafia que funciona |
|---|---|
| xAI | "xis ei ai" |
| Grok Bot | "Grók Bót" |
| Dots | "Dóts" |
| Muse | "Miús" |
| Superpowers | "Súper Páuers" |
| Opus 5.5 | "Ópus cinco ponto cinco" |
| Reels | "rílis" |
| OpenAI | "Ópen ei ái" |
| Anthropic | "Ântrópic" |
| Google | "Gúgol" |
| Hugging Face | "Râguin Fêis" |
| Buckmaster | "Bâkmáster" |
| Codex | "Côdex" |
| Yann LeCun | "Iân Lecân" |
| Geoffrey Hinton | "Djéfri Rínton" |
| Auckland | "Ócland" |
| EUA | escrever "Estados Unidos" por extenso (senão soletra "E-U-A") |
| IA | "í á" — "de IA" no meio da frase costuma sumir, usar "de inteligência artificial" ou "de... í á" |
| Números | sempre por extenso |

---

## 6. Trilha e sincronia

- Trilha sintetizada com semente fixa (reprodutível), a 124 BPM.
- Impacto sonoro em todo corte de cena, "subida" antes de virada/tela final.
- **Ducking automático:** a música abaixa sozinha quando a voz entra.
- Mix final: música em torno de -14/-14.5 LUFS; pra entrega especificamente no padrão TikTok, o volume final fica em -14 LUFS.
- Toda cena começa na batida.
- A tela final (recap) dura 8 tempos, com um tópico por batida.
- O som repete o conceito visual: ex. no vídeo de "rastro/cópia", os efeitos sonoros também ecoam e decaem, espelhando a animação.
- Efeitos sonoros calculados a partir dos mesmos tempos de palavra que a imagem usa (rachadura, carimbo, cabo rompendo, glitch, etc.).

---

## 7. Técnicas de movimento

### Ganchos (abertura)
- **Freeze-to-motion:** o frame congelado é exatamente a pose do instante da quebra, timecode em 00:00:00 — confirmar com `freezedetect` do FFmpeg.
- Quebra em fatias deslocadas por 4 frames.
- Número gigante entrando antes do resto do texto.

### Física
- Squash e mola no pouso, com poeira de semente fixa.
- Antecipação: o elemento "espia", recua e dispara (princípio de animação clássico).
- Queda com gravidade.
- Cards voando com velocidade + gravidade depois do congelamento.

### Câmera
- Punch-in de 8-15% em todo corte, assentando em ~0,5s.
- Leve aproximação contínua durante o plano.
- Tremor com semente registrada em cada impacto (reprodutível, não aleatório a cada render).
- Zoom travado numa linha do board que abre na palavra-chave.
- 1 frame de cor sólida em todo corte de cena (flash de transição).

### Tipografia cinética
- Texto subindo de dentro de uma máscara, palavra por palavra, sem fade — toda linha entra assim por padrão.
- Texto "decodificando" letra por letra.
- Máquina de escrever com cursor, com quebra de linha equilibrada pra não sobrar palavra sozinha.
- Slam: palavra-chave gigante batendo com tremor.
- Letras entrando uma a uma (nomes próprios).
- Risco diagonal pra indicar negação ("não é X").

### Efeitos de "dado"/estatística
- Contador animado (desacelera e para no número real).
- Crescimento exponencial (ex: 1 → 10.000).
- Leque de páginas.
- Planilha sendo mascarada.
- Rede de pontos com cabos rompendo e faíscas.
- Glitch de fatias com separação de cor.

### Falso 3D sem biblioteca pesada (sem WebGL)
- Wireframe com perspectiva calculada à mão, arestas de trás mais fracas — dá profundidade sem precisar de brilho solto.
- Cubo projetado na mão (rotação + perspectiva simples).
- Vidro desenhado faces de trás pra frente.
- Glassmorphism com gradiente, borda clara e reflexo, sem precisar de desfoque de fundo de verdade.
- Feixe de luz com intensidade caindo ao longo do cone + poeira suspensa — essa profundidade evita o "brilho solto" proibido.

### Cópia em rastro / eco
- O mesmo objeto desenhado em instantes passados, com opacidade caindo geometricamente. Rastro de movimento e eco espacial saem da mesma função — reaproveitar pra qualquer conceito de "algo se repetindo/copiando".

### No personagem (quando há mascote/personagem original)
- Achata/estica no pulo.
- Apêndices balançam atrasados (antena, capa — "follow through").
- Trajetórias em arco com rastro.
- Encaixe elástico quando chega no destino.

### Outras técnicas prontas
- Fusão líquida: dois selos viram gotas e se fundem num personagem.
- Glitch com texto embaralhado — pra troca de URL/texto.
- Visor + flash — pra simular "captura de tela".
- Carta virando — pra antes/depois.
- Ondas de sonar — pra "rodando em segundo plano".
- Letras mancando — pra indicar erro.
- Bolinha correndo por uma linha de conexão — pra "dado indo e vindo".

### Técnicas específicas já programadas (detalhe de implementação)
- **Traço se desenhando a partir de imagem:** usar um mapa de distância ao longo do traço (foi assim que as "trilhas do cérebro" cresceram no carrossel dos mitos).
- **Glitch reveal:** cores separadas em camadas que se sobrepõem, pixelização diminuindo a cada meia batida, fatias horizontais deslocadas e trocadas a cada 2 frames, com semente fixa.
- **Profundidade com recorte de pessoa:** remoção de fundo com `rembg`; o título fica entre o fundo e a pessoa. Antes de diagramar, checar onde o recorte deixa área livre pro texto.
- **Mixed media:** papel rasgado com borda orgânica (borda regular demais parece serrilhado artificial), retícula de meio-tom, fantasma de risografia, adesivos com fita e granulado em quadros fixos.

---

## 8. Regras de Instagram (carrossel/feed)

- **Frame 0 = cena final.** O primeiro frame vira a miniatura no feed e na grade — o loop precisa fechar sem salto perceptível.
- Formato: **4:5 (1080x1350), 60fps, H.264 yuv420p**, áudio normalizado em torno de **-16 LUFS** (`loudnorm`) — depois remontar o vídeo com `-c:v copy` (sem renderizar o vídeo de novo, só remuxar o áudio ajustado).
- **CTA de comentário:** a palavra-chave precisa ficar limpa, sem nada colado nela (sem pontuação/emoji grudado), porque a automação de DM depende do texto exato.
- **Último slide nunca é "arrasta"** — não tem nada depois dele. A seta aponta pro botão de salvar.
- **Emojis viram ícones desenhados na cor do post** — emoji colorido quebra a paleta.

---

## 9. Regras de TikTok/Reels/Shorts (9:16)

**Áreas seguras:**
- Topo até y=240px: reservado pro cabeçalho.
- Conteúdo principal: de y≈260 até ~1450-1550px de altura.
- Abaixo de ~1550px: área de legenda da plataforma, não colocar texto importante.
- À direita de x≈920-940: área dos botões (curtir/comentar/compartilhar), não colocar texto/elemento ali.
- Margem de 80px, coluna de 900px, grid suíço como base de composição.
- Todo texto passa por ajuste automático de largura (nunca estourar a margem).

---

## 10. Paleta e sistema visual

- **Uma cor de destaque por vídeo.** Uma segunda cor só entra com significado específico (ex: vermelho só aparece em "NEGA"/erro/alerta, não como decoração).
- Variar a cor dominante de vídeo pra vídeo (não travar sempre na mesma), mas manter só 1 destaque por peça.
- Vale usar um visual editorial alternativo às vezes pra quebrar o escuro (fundo creme, tinta preta, textura de papel) em vez de sempre dark.

---

## 11. Controle de qualidade

- **Folha de contato antes do render completo:** gerar 10-12 frames-chave, montar uma grade única (contact sheet) em vez de assistir o vídeo inteiro — é assim que se pega texto estourando margem, selo cortado pelo zoom, elemento camuflado na cor do fundo, mira/elemento escondido atrás do título, borda cortando o rosto. Pega de 3 a 5 problemas por vídeo nessa etapa.
- Depois do render: conferir no arquivo final — dimensões, fps e duração com `ffprobe`; procurar trechos travados (>1s parado) com `freezedetect`; volume com `ebur128`.
- **Mapear anexos pela descrição do briefing, não pela ordem em que foram anexados** — a ordem já veio invertida duas vezes.

**Problemas mais comuns encontrados na folha de contato:**
- Texto estourando a margem.
- Selo/elemento cortado pelo zoom de câmera.
- Elemento na mesma cor do fundo (fica invisível).
- Efeito de tremor "registrado" dentro do próprio desenho (deixa o render mais lento sem necessidade).
- Transição líquida desalinhada.

---

## 12. Pegadinhas de pipeline

- `fetch()` **não funciona** em contexto `file://` — os dados precisam ir embutidos como arquivo `.js`, não via fetch.
- Fontes: dá pra baixar com `npm pack @fontsource/...`, mas o subset `latin` não tem o glifo da seta `→` — ela precisa ser desenhada manualmente, não inserida como caractere de fonte.
- Fotos 16:9 recortadas pra 4:5 ampliam 1.43x — pedir a versão em maior resolução quando a foto de referência for 16:9, senão perde qualidade visível no recorte.

---

## 13. Render e entrega

- Velocidade de render: ~3 frames/segundo → ~10-16 minutos por minuto de vídeo final. Roda em segundo plano, não travar a sessão esperando.
- Export final abaixo de 20MB (CRF 21-22) — limite prático pra salvar na pasta do usuário.
- Fontes padrão via npm: `@fontsource/anton`, `@fontsource/barlow-condensed`.
- Guardar o código-fonte do projeto num `.zip` ao lado do MP4 final, na pasta do projeto (facilita reaproveitar o pipeline em vez de recomeçar do zero).

---

## 14. Ordem do pipeline (passo a passo)

1. Gerar as vozes (todas as cenas).
2. Limpar e acelerar os áudios.
3. Escrever as frases de cada cena (alinhamento texto↔áudio).
4. Montar a timeline na batida (grid de BPM).
5. Gerar a trilha sintetizada.
6. Mixar (ducking + normalização).
7. Escrever as cenas em Canvas (código da animação).
8. Preview de frames-chave (folha de contato) — repetir em loop até corrigir os problemas encontrados.
9. Render completo.
10. Juntar vídeo e áudio no FFmpeg.

---

## 15. Próximo nível (técnicas ainda não implementadas, vale explorar)

- Antecipação mais refinada: a palavra recua alguns frames antes do "slam" (princípio de animação que mais faz falta hoje no pipeline).
- Motion blur de verdade: média de 4-8 subframes por frame (não só um efeito de blur pós-processado).
- 60fps nativo em mais cenas.
- Fonte variável: a letra "engorda" no impacto em vez de só crescer em escala.
- Transição escondida: um elemento do fim de uma cena vira literalmente o início da próxima (sem corte perceptível).
- 3D leve de verdade em WebGL (além do "falso 3D" já descrito na seção 7).
- Visual editorial com mais frequência (fundo creme, tinta preta, textura de papel) pra variar do dark constante.
- Personagem com sequência de expressões acompanhando a fala (dúvida → entende → comemora).
- Legenda palavra a palavra, como opção configurável.
- Texto correndo ao longo de um caminho (path).
- Transição por máscara de forma, em vez de corte seco.
- Números se transformando um no outro, dígito a dígito (morph numérico).
- Retícula ou conversão em ASCII de um print real.
- Texto em camadas com paralaxe (profundidade 2.5D).
- Grade suíça que se monta célula por célula.
- Visual de "datamosh" pra notícias de vazamento/invasão.
