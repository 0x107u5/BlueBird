# 🛡️ BlueBird

Um site dedicado ao compartilhamento de conhecimentos, ferramentas, boas práticas e recursos voltados à defesa cibernética (Blue Team). Ideal para profissionais de segurança da informação, SOC analysts, e entusiastas que desejam fortalecer sua postura defensiva.  
Para acessar https://0x107u5.github.io/BlueBird/
O site é gerado com [Zensical](https://zensical.org), a partir do `mkdocs.yml` e dos arquivos em `docs/`.

## 🔍 Sobre o Projeto

Este projeto tem como objetivo centralizar e organizar conteúdos relevantes para o dia a dia de profissionais de defesa cibernética. O site traz tutoriais, checklists, ferramentas, indicadores de compromisso (IOCs), referências de hardening, scripts úteis e muito mais.

## 🚀 Como Rodar o Projeto Localmente

### Pré-requisitos

- Git
- Python
### Passos

1. Clone o repositório:

```bash
git clone https://github.com/0x107u5/BlueBird.git
cd BlueBird
```
2. Baixar dependências 
```bash
pip install -r requirements.txt
```

3. Rodar o projeto

```bash
zensical serve
```

## ✍️ Como escrever um post no blog

1. Crie um arquivo em `docs/blog/posts/`, por exemplo `2026-12-01-meu-post.md`.
2. Comece com o cabeçalho (front matter):

```markdown
---
date: 2026-12-01
authors:
  - 0x107u5
categories:
  - Write-ups
tags:
  - soc
slug: meu-post
draft: true   # remova quando quiser publicar
---

# Título do post

Resumo que aparece na listagem do blog.

<!-- more -->

Resto do conteúdo...
```

3. Rode `zensical serve` para ver o post (rascunhos aparecem localmente, mas não no site publicado).
4. Faça o push para `main`: o GitHub Actions publica o site automaticamente.

A listagem, o arquivo por data e as páginas de categorias são gerados sozinhos. Autores ficam em `docs/blog/.authors.yml`.

## 📁 Estrutura

```
docs/
├── index.md            # Página inicial
├── sobre.md
├── Redes/              # Páginas de referência
└── blog/
    ├── index.md        # Página do blog (listagem automática)
    ├── .authors.yml    # Autores
    └── posts/          # Um arquivo .md por post
```
