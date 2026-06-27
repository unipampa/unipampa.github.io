source "https://rubygems.org"

# Build com Jekyll 4 (toolchain moderno, compatível com Ruby 3.x).
# O deploy usa GitHub Actions (.github/workflows/jekyll.yml), e não o
# builder nativo do GitHub Pages, então não dependemos da gem github-pages.
gem "jekyll", "~> 4.3"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.17"
end

# Dependências de runtime que saíram da biblioteca padrão do Ruby 3.x.
gem "webrick", "~> 1.8"
