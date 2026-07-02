# Site trilíngue (PT / ES / EN) — design

Data: 2026-07-01
Projeto: `unipampa.github.io` (proposta de redesign, Jekyll)

## Objetivo

Tornar o site institucional trilíngue: português (padrão), espanhol e inglês,
com interface, dados estruturados e notícias 100% traduzidos nos três idiomas.

## Decisões

- **Abordagem: i18n nativo, sem plugin.** Liquid puro + dicionário em `_data/`.
  Motivo: o build local é Jekyll 3.9 (Ruby 2.6) e o CI é Jekyll 4.3; um plugin
  (ex.: `jekyll-polyglot`) arriscaria divergência entre os dois ambientes e
  contraria o espírito minimalista do projeto (sem tema, sem plugins externos).
- **Escopo: completo.** UI, dados (menu, campi, acesso rápido) e as 6 notícias.

## Arquitetura

### URLs
- PT (idioma padrão) na raiz: `/`, `/noticias/`, `/campi/`. Nenhum link atual quebra.
- ES em `/es/` e EN em `/en/`: `/es/`, `/es/noticias/`, `/es/campi/` (idem `/en/`).

### Configuração (`_config.yml`)
- `languages: ["pt", "es", "en"]` e `default_lang: "pt"`.

### Dicionário de interface (`_data/i18n.yml`)
- Uma chave por string de UI, um bloco por idioma, incluindo `bcp47` (mapa para o
  atributo `lang`/`hreflang`) e `site_title`.
- Uso nos templates: `{{ site.data.i18n[lang].chave }}`, com
  `lang = page.lang | default: site.default_lang`.

### Dados por idioma (`_data/{pt,es,en}/`)
- `navigation.yml`, `quicklinks.yml`, `campi.yml` em subpastas por idioma.
- Acesso: `site.data[lang].navigation` etc. Nos campi, só a descrição (`destaque`)
  é traduzida; o nome da cidade é mantido.

### Idioma da página
- Cada página e cada post declara `lang:` no front matter.
- Layouts e includes derivam `lang` de `page.lang` diretamente (robusto entre
  Jekyll 3.9 e 4.3, sem depender de escopo de variáveis herdado em includes).

### Páginas
- Home, Notícias e Campi têm uma versão por idioma. Os corpos de Notícias e Campi
  vivem em includes compartilhados (`noticias-list.html`, `campi-page.html`), então
  os arquivos por idioma só definem front matter (`lang`, `ref`, `permalink`).

### Notícias (posts)
- Cada post recebe `lang:` e `ref:` (id compartilhado entre as três traduções).
- PT usa o permalink global; ES/EN definem `permalink` explícito sob `/es/` e `/en/`.
- Listagens filtram por idioma: `site.posts | where: "lang", lang`.

### Seletor de idioma e alternativas (`ref`)
- `lang-switcher.html` encontra as versões irmãs pelo `ref`, procurando em
  `site.pages` e `site.posts`. Idioma sem tradução fica desativado.
- `default.html` emite `<link rel="alternate" hreflang>` para cada versão irmã e
  define `<html lang>` a partir do `bcp47` do idioma.

## Acessibilidade / SEO
- `<html lang>` por página; `hreflang` para cada versão; skip-link, labels de busca,
  menu e breadcrumb traduzidos.

## Verificação
- Build local (Jekyll 3.9): 27 páginas geradas (3 homes + 3 listagens + 3 campi + 18
  posts). Seletor, hreflang, `<html lang>`, filtro de posts por idioma e menus
  conferidos no HTML de saída.
