# Site institucional UNIPAMPA — proposta de redesign (Jekyll / GitHub Pages)

Data: 2026-06-26

## Objetivo

Site institucional **estático** para `unipampa.github.io`, como **proposta de redesign**
moderno do portal atual da UNIPAMPA. Reaproveita a identidade visual (verde institucional,
logo, estrutura de menu), mas com layout e arquitetura repensados. Não é réplica fiel nem
clone do Drupal atual.

## Decisões fechadas (brainstorming)

1. Natureza: proposta de redesign moderno e estático.
2. Escopo: home institucional + sistema de notícias (posts em Markdown) + página de campi.
3. Conteúdo: textos reais extraídos do portal atual como exemplo.
4. Stack: layouts e CSS 100% próprios, **build nativo do GitHub Pages** (sem tema externo,
   sem plugins fora da allowlist, sem GitHub Actions).

## Design system

| Token | Valor | Uso |
|---|---|---|
| `--verde` | `#019b43` | cor institucional (logo), botões, links, faixas |
| `--verde-escuro` | `#017a35` | hover, estados ativos |
| `--preto` | `#1a1a1a` | texto principal |
| `--cinza` | `#5c5c5c` | texto secundário |
| `--cinza-claro` | `#ededed` | fundos, divisórias |
| `--branco` | `#ffffff` | fundo base |

- Tipografia: Raleway (títulos) + stack de sistema como fallback; corpo em sans neutra.
- Logo oficial em `assets/img/logo-unipampa.png`.
- Acessibilidade: contraste AA, skip-link, foco visível, HTML semântico, `alt` em imagens.
- Responsivo, mobile-first. Hero com gradiente/padrão CSS (sem fotos de terceiros, evita
  questões de licença).

## Arquitetura de arquivos

```
_config.yml                 configuração do site
Gemfile                     gem github-pages (referência; build é nativo)
index.html                  home (layout: home)
_layouts/
  default.html              <head>, header, footer, skip-link
  home.html                 monta as seções da home
  post.html                 notícia individual
  page.html                 página de conteúdo genérica
_includes/
  header.html               logo + navegação principal + busca (visual)
  footer.html               campi, contatos, horários, copyright
  hero.html                 destaque principal
  news-card.html            card de notícia reutilizável
  quick-links.html          acesso rápido (Ingresso/Ensino/Pesquisa/Extensão)
  campi.html                grade dos 10 campi
_data/
  navigation.yml            itens do menu principal
  campi.yml                 os 10 campi (nome, cidade)
  quicklinks.yml            blocos de acesso rápido
_posts/                     ~6 notícias reais em Markdown
noticias/index.html         listagem paginada de notícias
campi/index.html            página dedicada aos campi
assets/
  css/main.scss             estilos (Jekyll Sass)
  img/logo-unipampa.png     logo oficial
```

## Seções da home

1. Header: logo + menu (Institucional, Ingresso, Ensino, Pesquisa, Extensão, Estudantes,
   Servidores, Acesso à Informação) + campo de busca (visual).
2. Hero: destaque "20 anos da Unipampa" com CTA.
3. Notícias recentes: grade de cards (data, categoria, título, resumo) a partir de `_posts`.
4. Acesso rápido: Ingresso, Ensino, Pesquisa, Extensão (cards com ícone).
5. Nossos 10 campi: grade a partir de `_data/campi.yml`.
6. Footer: campi, contatos, horários (08–12h / 13:30–17:30h), copyright.

## Conteúdo inicial (notícias reais)

- 20 anos da Unipampa: inauguração de prédio e shows em Bagé.
- Curso de Música fica em 4º lugar nacional no ENADE.
- Engenharia de Energia abre primeira turma noturna em 2026/2.
- Campus Jaguarão e Campus São Gabriel recebem novas docentes.
- Edward Pessano eleito vice-presidente da Unifronteiras.
- Carta de Serviços ao Cidadão.

## Build e publicação

- Site de usuário/organização (`*.github.io`): `baseurl: ""`, `url: https://unipampa.github.io`.
- Publicação pelo build nativo do GitHub Pages: `git push` para `main`, Pages servindo da
  branch `main` na raiz. Sem workflow de Actions.

## Fora de escopo (YAGNI por agora)

- Páginas internas de cada item de menu (Institucional, Ensino etc.) além de links.
- Busca funcional (campo é apenas visual nesta entrega).
- Conteúdo dinâmico/CMS, formulários, autenticação.
