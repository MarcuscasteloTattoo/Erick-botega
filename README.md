# Erick Bottega | Bottega Ink

Site do tatuador Erick Bottega, da Bottega Ink, em Florianópolis: tatuagens fineline, sketch, blackwork e composições em preto e vermelho. A página tem o banner, os projetos recentes em carrossel, o portfólio, o "Quem sou", as avaliações do Google, o valor das tatuagens e o formulário de orçamento.

É um site estático: um `index.html`, os ícones e a pasta `assets/` com as fotos. Não precisa de build nem de instalação. As fontes vêm do Google Fonts.

## Testar no computador

Abra o `index.html` no navegador (dois cliques no arquivo).

## Publicar

Funciona em qualquer hospedagem de site estático. Envie o `index.html`, os ícones (`favicon-bottega-ink.png`, `apple-touch-icon-bottega-ink.png`, `favicon.png` e `apple-touch-icon.png`) e a pasta `assets/` juntos, mantendo a estrutura.

- **Hostinger (deploy pelo Git):** cada envio ao branch `main` é publicado na pasta do site, se a integração com este repositório estiver ativa no hPanel.
- **GitHub Pages:** Settings → Pages → *Deploy from a branch* → `main` / `(root)`.

## Formulário de orçamento

O visitante preenche nome e WhatsApp, com máscara `(DD) 9 0000-0000`. Ao enviar:

1. Os dados vão para o webhook do Make (`webhookMake` no objeto `site`), com data e hora de Brasília, telefone no padrão brasileiro, dispositivo, sistema, navegador e página de origem.
2. O Meta Pixel registra o evento `Lead`, sem dados pessoais.
3. O visitante vai direto para o WhatsApp (`whatsappBase`), com a mensagem `mensagemWhatsApp`.

## Meta Pixel

Pixel `1784247566187393`, com o código oficial da Meta no `<head>`. `PageView` dispara ao abrir a página. `Lead` dispara uma única vez por visita, só depois de um envio válido do formulário.

## Idiomas

O site abre sempre em português. Os botões no canto superior direito (PT, EN, ES) traduzem a página inteira, inclusive a mensagem do WhatsApp. Um link terminado em `?lang=en` ou `?lang=es` já abre em inglês ou espanhol.

Os textos em inglês e espanhol ficam no objeto `I18N`, no fim do `index.html`. Ao mudar um texto em português, mude também nas duas traduções.

## Onde editar

No fim do `index.html`, dentro do `<script>`, o objeto `site` guarda o conteúdo que muda com frequência:

- `estilos`: os cards do carrossel "Projetos recentes" (título, texto, foto, foto grande e descrição da foto).
- `portfolio`: as fotos do portfólio, na ordem em que aparecem. Mantenha um múltiplo de 6 fotos (hoje são 12): a grade tem 2 colunas no celular e 3 no computador, e assim nunca termina com uma foto sozinha. `PF_VISIVEIS` define quantas aparecem antes do botão "Ver portfólio completo".
- `avaliacoes`: avaliações do Google (nome, foto do perfil, tempo, texto e fotos). As fotos abrem ampliadas ao toque.
- `whatsappBase`, `mensagemWhatsApp` e `webhookMake`: WhatsApp, mensagem inicial e webhook do formulário.

Ficam direto no HTML: textos do banner, do "Quem sou" e dos preços, e o link do Instagram (@bottegaink).

## Fotos

- `assets/erick-bottega-tatuador-bottega-ink-banner-*.webp`: banner (um recorte para celular e outro para computador)
- `assets/erick-bottega-paris-opera-bottega-ink-quem-sou*.webp`: foto do "Quem sou"
- `assets/tatuagem-*-florianopolis.webp`: fotos do carrossel e do portfólio, com versões `-480` e `-360` para celular e `-grande` para a foto ampliada
- `assets/avaliacao-*.webp`: fotos de perfil das avaliações
- `assets/logo-*.webp|png` e `assets/monograma-*.webp`: logo da Erick Bottega Ink

Ao trocar uma foto, use um nome de arquivo novo e mantenha o padrão descritivo terminado em `-florianopolis`.

## SEO

No `<head>` ficam o título, a descrição, as palavras-chave, os dados para redes sociais (`og:`) e um bloco `application/ld+json` com os dados da Bottega Ink: endereço, horário, telefone, Instagram, Google e logo. Quando o domínio estiver definido, troque os caminhos das imagens nesse bloco e em `og:image` por endereços completos.

## Desempenho

`_headers` (Netlify e Cloudflare Pages) e `vercel.json` (Vercel) mandam o navegador guardar as fotos em cache por 1 ano. Na Hostinger, o mesmo pode ser feito no `.htaccess`.
