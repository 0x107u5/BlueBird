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

## ✍️ Padrão de escrita

Antes de escrever, veja o [guia de estilo](GUIA-DE-ESTILO.md): tom, termos técnicos, formato de nota, admonitions, blocos de código e como anonimizar dados. Há uma nota completa de exemplo em `templates/exemplo-nota.md`.

## ✍️ Como escrever um post no blog

1. Copie `templates/post.md` para `docs/blog/posts/`, com um nome como `2026-12-01-meu-post.md`.
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
├── index.md              # Página inicial
├── sobre.md
├── SIEM/                 # Conceitos de SIEM
│   ├── index.md
│   └── Google-SecOps/    # UDM, YARA-L, ingestão
├── Logs/                 # Windows, Linux, rede
├── Redes/                # IPv4, portas
└── blog/
    ├── index.md          # Listagem automática
    ├── .authors.yml
    └── posts/            # Um arquivo .md por post
templates/
├── post.md               # Modelo de post do blog
├── pagina.md             # Modelo de nota técnica (página de referência)
└── exemplo-nota.md       # Nota completa seguindo o guia de estilo
```

### Post ou página?

- **Página** (em `docs/SIEM/`, `docs/Logs/`, ...): conteúdo de referência que você vai atualizar com o tempo, como "Eventos de segurança do Windows".
- **Post** (em `docs/blog/posts/`): algo datado, como um write-up, um caso investigado ou uma novidade. Use as categorias `SIEM`, `Google SecOps` ou `Logs` para ligar o post ao tema.

### Adicionar uma página nova

1. Copie `templates/pagina.md` para a pasta da seção, por exemplo `docs/Logs/sysmon.md`.
2. Adicione a página no `nav` do `mkdocs.yml`, dentro da seção certa.

### Adicionar uma nova plataforma de SIEM

1. Crie uma pasta em `docs/SIEM/`, por exemplo `docs/SIEM/Splunk/`, com um `index.md`.
2. Adicione a pasta no `nav` do `mkdocs.yml` e uma linha na tabela de `docs/SIEM/index.md`.
3. Se quiser, adicione a plataforma em `categories_allowed` no `mkdocs.yml` para usar como categoria do blog.
