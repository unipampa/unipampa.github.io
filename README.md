# unipampa.github.io

Proposta de **redesign** do portal institucional da Universidade Federal do Pampa
(UNIPAMPA), construída como site estático em **Jekyll** e publicada via **GitHub Pages**.

> Site demonstrativo. Reaproveita a identidade visual da UNIPAMPA (cor institucional
> verde, logo e estrutura de menu), com layout e arquitetura repensados. Não é o portal
> oficial.

## Stack

- Jekyll (build nativo do GitHub Pages, sem plugins externos)
- Layouts e CSS próprios (Sass), sem framework
- Conteúdo de notícias em Markdown (`_posts/`) e dados estruturados em `_data/`

## Estrutura

```
_config.yml          configuração do site
index.html           home
_layouts/            default, home, post, page
_includes/           header, footer, hero, news-card, quick-links, campi
_posts/              notícias em Markdown
_data/               navigation.yml, campi.yml, quicklinks.yml
noticias/, campi/    páginas de listagem
assets/css/main.scss estilos
assets/img/          logo
docs/                spec do projeto
```

## Rodar localmente

```bash
bundle install
bundle exec jekyll serve
# abre http://localhost:4000
```

## Publicação

Site de organização (`*.github.io`): basta `git push` para a branch `main`. Em
**Settings → Pages**, defina a fonte como branch `main` / pasta raiz. O GitHub Pages
compila o Jekyll automaticamente.
