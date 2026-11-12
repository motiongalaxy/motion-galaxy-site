# Motion Galaxy — Histórico do projeto do novo site

Backup da conversa com o Claude (Claude Code na nuvem) em **6 de novembro de 2026**, que analisou o site antigo, montou a skill de design e criou o novo site. Use este arquivo para retomar o trabalho numa conversa futura.

---

## 1. Links e dados principais

| Item | Valor |
|---|---|
| Site | https://motion-galaxy.com/ |
| Repositório | https://github.com/motiongalaxy/motion-galaxy-site (branch `main`) |
| Prévia no Claude (privada) | https://claude.ai/artifact/N9X17vwPxbZZeyGierofrX |
| Canal no YouTube | https://www.youtube.com/@motion-galaxy |
| E-mail de contato | motiongalaxy.templates@gmail.com |
| Todos os produtos na FxFactory | https://fxfactory.com/search/?keywords=galaxy |
| Diretor criativo | Tiago Pacianotto |
| Hospedagem | Hostinger (o site antigo era WordPress 7.1 + Elementor + Slider Revolution) |

### Os 8 produtos

| # | Produto | Descrição (site antigo) | FxFactory | Vídeo no YouTube |
|---|---|---|---|---|
| 08 | Wedding Tools | Slides, efeitos, títulos e convites para vídeos de casamento | https://fxfactory.com/info/weddingtools/ | https://www.youtube.com/watch?v=9xyAmz59ziU |
| 07 | Essential Callouts | Destacar informações de forma dinâmica | https://fxfactory.com/info/essentialcallouts/ | https://www.youtube.com/watch?v=dbORt3hlm7U (vídeo do canal da FxFactory) |
| 06 | Soccer Tools | A energia do futebol | https://fxfactory.com/info/soccertools/ | https://www.youtube.com/watch?v=oX5Egbn9Yp0 |
| 05 | Galactic Backdrops | Títulos, fundos e efeitos sci-fi | https://fxfactory.com/info/galacticbackdrops/ | https://www.youtube.com/watch?v=964xpDUzNmA |
| 04 | Colorful Transitions | Transições com estilo lúdico | https://fxfactory.com/info/colorfultransitions/ | https://www.youtube.com/watch?v=yzL_EV8RrfQ |
| 03 | Universal Titles | 100 títulos animados | https://fxfactory.com/info/universaltitles/ | https://www.youtube.com/watch?v=ph8VJp3widI |
| 02 | Whiteboard Universe | Animações estilo quadro branco | https://fxfactory.com/info/whiteboarduniverse/ | https://www.youtube.com/watch?v=Rxf9ALdB6ao |
| 01 | Cosmo Slice | Layouts de tela dividida | https://fxfactory.com/info/cosmoslice/ | https://www.youtube.com/watch?v=sqa3TqQFWWQ |

---

## 2. O que foi feito, em ordem

### 2.1 Análise do site antigo
- O site antigo tinha **uma página só**; os links do menu (Products, Downloads, Explore, Purchase, Subscribe, `/shop`, `/contacts`) não levavam a lugar nenhum ou davam erro 404.
- Sobras do tema: e-mail `info@website.com`, "Have a Startup Project? Send Brief", "Transform your business with AI startup", depoimento de "Piter Bowman".
- Erros: "Essencial Callouts", contador "8 / 0", rodapé © 2024, inglês e português misturados, sem link para o canal do YouTube.
- Uma cópia da página antiga está em `docs/old-site/motion-galaxy-wordpress-homepage.html`, com o logo e o ícone originais.

### 2.2 Skills
- Plugins sugeridos no catálogo do claude.ai (não instalados): **frontend-design** (Anthropic), **Website Design** (UXKIN), **Ullbek**.
- Instalada a skill **apple-design** de https://github.com/emilkowalski/skills (licença MIT), e depois mais 13 skills do mesmo repositório úteis para sites: animate, animation-performance, animation-vocabulary, break-ui, choreograph, emil-design-eng, find-animation-opportunities, improve-animations, mobile-native, pick-ui-library, prototype, remove-animations, review-animations. Ficaram de fora animate-expo, write-swift e ask-sonner.
- As 14 foram juntadas numa skill só, **motion-galaxy-web-design**: um `SKILL.md` que indica qual guia usar em cada situação, mais `guides/<nome>/GUIDE.md`. Ela está neste repositório em `.claude/skills/motion-galaxy-web-design/` e o Claude a carrega sozinho quando abre o repositório.
- Para usar a skill em qualquer conversa do claude.ai: compacte a pasta `motion-galaxy-web-design` em zip e envie em Settings → Capabilities → Skills.
- **11/11/2026:** foi adicionado o plugin **modern-web-guidance** (do time do Google Chrome, catálogo `anthropics/claude-plugins-official`), com boas práticas atuais de HTML, CSS e JavaScript. Ele está ativado no repositório em `.claude/settings.json`, então toda sessão do Claude aberta com este repositório já vem com ele. No computador: `claude plugin marketplace update claude-plugins-official` e depois `claude plugin install modern-web-guidance@claude-plugins-official`.
- **12/11/2026:** foi adicionado o plugin **frontend-design** da Anthropic (mesmo catálogo), com orientações de qualidade visual para interfaces. Ele também está ativado em `.claude/settings.json`. No computador: `claude plugin install frontend-design@claude-plugins-official`.
- **12/11/2026:** foi adicionada a skill **web-design-guidelines** da Vercel (`vercel-labs/agent-skills`, licença MIT), que revisa o código segundo as Web Interface Guidelines da Vercel. A original busca as regras na internet a cada uso; aqui elas ficaram guardadas em `.claude/skills/web-design-guidelines/guidelines.md` (versão de 05/10/2026), para não dependerem de conteúdo remoto.

### 2.3 O novo site
Feito no estilo do site da Apple, com a skill acima:
- **Menu:** fixo e translúcido, com logo, links (Products, Videos, Why us, YouTube, Contact), menu de idiomas e botão "Buy".
- **Abertura:** fundo escuro com estrelas (desenhadas uma vez, sem movimento) e brilho roxo. Título "Your videos, in another orbit.", botões para os produtos e as demos, e três números (8 packs, 100 títulos, FxFactory).
- **Produtos:** Galactic Backdrops e Universal Titles ocupam a largura toda; os outros seis ficam em pares. Cada card tem nome, frase, descrição, **"Buy on FxFactory"**, **"Watch the video"** e a miniatura do vídeo, que também abre o YouTube.
- **"See them in action":** faixa com as 8 demos que rola para o lado, com setas e link para o canal.
- **"Why Motion Galaxy":** os 4 benefícios do site antigo, reescritos.
- **Fechamento (#contato):** botões "See all on FxFactory" e "Follow on YouTube", e o e-mail com botão Copiar.
- **Rodapé:** logo, e-mail, os 8 links de compra, link do canal mais os 8 vídeos, crédito e aviso de marca registrada da Apple.
- **Temas e acessibilidade:** tema escuro e claro conforme o sistema do visitante. Respeita quem pede menos movimento, menos transparência ou mais contraste.
- **Idiomas:** 7 (inglês, português, espanhol, francês, alemão, italiano, japonês), com **inglês como padrão**. O menu do topo mostra a sigla do idioma atual, e a escolha do visitante fica salva no navegador.

As imagens dos produtos são as miniaturas dos vídeos do YouTube, convertidas para WebP 1280×720.

### 2.4 Ajustes pedidos depois
1. Link do canal do YouTube colocado no menu, na seção de vídeos, no fechamento e no rodapé.
2. E-mail de contato colocado no fechamento (com botão Copiar) e no rodapé.
3. Botão de idioma corrigido para mostrar o idioma atual (antes mostrava o outro).
4. Mais 5 idiomas, com menu de escolha.
5. Inglês passou a ser o idioma padrão.
6. O site foi enviado para o GitHub; foi preciso instalar o Claude GitHub App na conta `motiongalaxy`.

### 2.5 Ambiente da nuvem
Na rede do ambiente "Default" do Claude na nuvem foram liberados: `motion-galaxy.com`, `www.motion-galaxy.com`, `www.youtube.com` e `i.ytimg.com`. Eles servem para ler o site e baixar miniaturas de vídeos.

---

### 2.6 Melhorias com o material do Google Drive (12/11/2026)
Material lido da pasta **Motion Galaxy - Backup** (Drive da conta motiongalaxy.templates, compartilhada com a conta pessoal):
- **Logo vetorial:** convertido de `_LOGO/PNG/Motion Galaxy.ai` para SVG, embutido no `index.html`. Fica nítido em qualquer tela e muda de cor conforme o tema, sem o filtro de inversão de antes.
- **Abertura com galáxia real:** `Site/galaxy1.jpg` (NGC 2336, Hubble, ESA/Hubble & NASA, CC BY 4.0), clareada e otimizada em WebP de 960 e 1920 px, no lugar das estrelas desenhadas. A abertura fica sempre escura, nos dois temas. O crédito está no rodapé, nos 7 idiomas.
- **Textos mais completos** do Whiteboard Universe e do Cosmo Slice, a partir dos roteiros "First Look" da FxFactory.
- **Favicon** com o "G" da marca.
- **Fontes da marca (Nasalization e Ethnocentric):** não foram usadas no site, porque a licença Typodermic não permite distribuir os arquivos de fonte, e uma fonte de site é baixada por cada visitante.
- **Vídeos em loop nos produtos:** ainda não feitos. O conector do Drive só baixa arquivos de até 10 MB, e os vídeos têm de 27 a 658 MB.

### 2.7 Recriação com galáxia animada e efeitos de rolagem (12/11/2026)
A pedido, o site foi recriado com:
- **Fundo fixo de galáxia em movimento**, desenhado em canvas com pontos (espiral de dois braços, núcleo brilhante), linhas de órbita com pontos que circulam, estrelas que piscam e estrelas cadentes. O conteúdo rola por cima. A rolagem gira, aproxima e escurece a galáxia. Tem botão de pausa no canto inferior esquerdo e começa parada para quem pede menos movimento. O site passou a ter só tema escuro. A foto do Hubble e o crédito dela saíram.
- **Efeitos de rolagem no estilo da página do iPhone Duo da Apple** (https://www.apple.com/br/iphone-duo/), recriados com código próprio: menu que ganha fundo ao rolar, abertura que encolhe e some, frase grande que acende palavra por palavra, galeria de destaques que avança sozinha com pontos de progresso e botão de pausa, cards que sobem ao entrar na tela, vídeos dos cards que crescem, números que contam na abertura.
- A seção de vídeos virou a galeria de destaques e subiu para antes dos produtos.
- Os efeitos de rolagem usam um recurso recente dos navegadores (animações ligadas à rolagem em CSS). Em navegadores antigos o site aparece completo, só sem esses efeitos.

### 2.8 Vídeos incorporados (12/11/2026)
Os vídeos agora tocam no próprio site, num player em tela cheia por cima da página (no estilo dos filmes da Apple), em vez de abrir o YouTube. Ele abre ao clicar nos cards da galeria, nas imagens dos produtos e nos botões "Assistir ao vídeo". Usa o modo de privacidade do YouTube (`youtube-nocookie.com`) e só carrega o vídeo quando a pessoa clica. Fecha com Esc, com o botão ou clicando fora. Tem link "Abrir no YouTube" (no computador), e Ctrl/Cmd+clique continua abrindo o YouTube numa aba nova. Os 8 vídeos permitem incorporação (conferido). Na prévia do Claude o player fica em branco, porque ela bloqueia vídeos incorporados; no site publicado funciona.

### 2.9 Prévias em vídeo, nova ordem e setas (12/11/2026)
- **Prévias em vídeo:** os vídeos `head-…` de 15 segundos da pasta Demo Videos foram comprimidos para a web (0,7 a 2,2 MB cada, sem áudio) e ficam em `video/`. O card do centro da galeria toca a sua prévia, e a galeria avança quando ela termina. Nos produtos, a prévia toca enquanto o card está visível. Os vídeos só baixam quando vão tocar. O botão do canto inferior esquerdo pausa tudo (galáxia, galeria e prévias). Não tocam para quem pede menos movimento nem com economia de dados ligada.
- **Nova ordem dos produtos:** Soccer Tools, Wedding Tools, Whiteboard Universe, Essential Callouts, Universal Titles, Galactic Backdrops, Colorful Transitions, Cosmo Slice. Soccer Tools e Essential Callouts ocupam a largura toda.
- **Setas laterais no carrossel** de destaques, que dão a volta do último para o primeiro.
- **Sombra no título da abertura** (e mais leve no texto abaixo dele), para melhorar a leitura sobre a galáxia.

### 2.10 Sombras sobre o fundo (12/11/2026)
Todos os elementos que ficam sobre a galáxia ganharam sombra. Os textos direto sobre o fundo (títulos de seção, frase grande, números da abertura, contato, links) receberam sombra de texto. Os cards de produto e da galeria têm a sombra mais funda, os cards de benefícios uma média, e os botões, seletor de idioma, controles da galeria, setas e o botão de pausa uma leve. Os valores ficam em tokens (`--sh-text`, `--sh-lg`, `--sh-md`, `--sh-sm`).

### 2.11 Correção do carrossel (12/11/2026)
No computador (provavelmente no Safari do Mac), o último vídeo do carrossel não chegava ao centro e ficava cortado na lateral. O Safari ignora o espaço extra no fim de listas roláveis, que era o que permitia centralizar o último card. Esse espaço passou a vir de elementos espaçadores reais, que funcionam igual em todos os navegadores. O carrossel também passou a calcular a posição de cada card pelo layout, então todos centralizam exatamente pelas setas, pelos pontinhos ou arrastando.

## 3. Pendências

- [x] **Hostinger:** site novo publicado em motion-galaxy.com (conferido em 12/11/2026). Atualização automática ligada: cada envio ao branch `main` de `motiongalaxy/motion-galaxy-site` vai para o `public_html`. SSL ativo com redirecionamento para HTTPS, CDN e cache ligados. O `.htaccess` esconde `docs/`, `.claude/` e os `.md` (respondem 404).
- [ ] Revisão das traduções por falantes nativos, principalmente o japonês.
- [ ] Instagram e outras redes sociais: ainda não informados.
- [ ] Opcional: preços dos produtos (não estavam no site antigo).

---

## 4. Como pedir uma alteração no futuro

Abra uma conversa no Claude Code (claude.ai/code) com o repositório `motiongalaxy/motion-galaxy-site` selecionado e peça, por exemplo:

> "Adicione o produto X com o vídeo Y e o link Z da FxFactory, nos 7 idiomas."

O Claude lê o `CLAUDE.md` e a skill deste repositório, altera o `index.html`, confere e envia para o GitHub. Com o Auto Deployment ativo, a Hostinger publica sozinha.

Se o envio para o GitHub falhar, instale ou reconecte o Claude GitHub App em https://github.com/apps/claude/installations/select_target, liberando o repositório `motion-galaxy-site`.
