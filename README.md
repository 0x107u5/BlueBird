# 🛡️ BlueBird

Blog sobre defesa cibernética (Blue Team) em português: hardening, análise de logs, redes, resposta a incidentes, threat hunting e muito mais.

Acesse: https://0x107u5.github.io/BlueBird/

O site é feito com [Jekyll](https://jekyllrb.com) e o tema [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy), e é publicado no GitHub Pages pelo GitHub Actions a cada push na `main`.

## 🚀 Rodar localmente

Pré-requisitos: Git e Ruby 3.x com Bundler.

```bash
git clone https://github.com/0x107u5/BlueBird.git
cd BlueBird
bundle install
bundle exec jekyll serve
```

O site abre em http://127.0.0.1:4000/BlueBird/.

## ✍️ Escrever um post

Crie um arquivo em `_posts/` com o nome `AAAA-MM-DD-titulo.md`, por exemplo `_posts/2026-12-01-analise-de-logs.md`:

```markdown
---
title: "Análise de logs no Windows"
date: 2026-12-01 10:00:00 -0300
categories: [SOC, Logs]        # até 2 níveis: categoria e subcategoria
tags: [windows, eventos, soc]  # sempre em minúsculas
description: Resumo que aparece na listagem e no Google.
# pin: true                    # fixa o post no topo da home
# image:
#   path: /assets/img/posts/analise-logs.png
#   alt: Descrição da imagem
---

Conteúdo do post em Markdown...
```

Rascunhos podem ficar em `_drafts/` (sem data no nome) e aparecem só com `bundle exec jekyll serve --drafts`.

Caixas de destaque do Chirpy:

```markdown
> Dica útil.
{: .prompt-tip }

> Atenção a isso.
{: .prompt-warning }
```

As abas **Categorias**, **Tags** e **Arquivo** são geradas automaticamente a partir dos posts.

## 📁 Estrutura

```
_config.yml      # Título, idioma, URL, redes sociais, tema escuro
_posts/          # Um arquivo .md por post
_tabs/           # Páginas do menu lateral (Sobre, Categorias, Tags, Arquivo)
_data/           # Links de contato e compartilhamento
assets/img/      # Imagens (crie quando precisar)
.github/workflows/pages-deploy.yml  # Build e deploy no GitHub Pages
```

## 📄 Licença

Veja [LICENSE](LICENSE).
