# Guia de estilo do BlueBird

Regras para escrever páginas e posts no BlueBird. O objetivo é que qualquer nota possa ser lida com pressa, no meio de uma investigação, e ainda assim ser útil.

Modelos prontos ficam em `templates/`:

| Arquivo | Para quê |
|---------|----------|
| `templates/pagina.md` | Nota técnica de referência (SIEM, Logs, Redes) |
| `templates/post.md` | Post datado do blog (write-up, caso, novidade) |
| `templates/exemplo-nota.md` | Uma nota completa seguindo este guia, para consulta |

## 1. Tom e voz

- **Português do Brasil**, direto e prático. Escreva como quem explica para um colega de SOC.
- Fale com o leitor por **"você"** ("filtre pelo campo...", "você vai ver..."). Em write-ups, a primeira pessoa é bem-vinda ("eu encontrei...").
- **Frases curtas e voz ativa.** "O parser mapeia o campo" em vez de "o campo é mapeado pelo parser".
- **Comece pelo que importa.** O primeiro parágrafo diz o que é e por que o defensor deve se importar. História e detalhes vêm depois.
- Diga quando algo **não foi testado** ou depende do ambiente, com um aviso `!!! warning`.
- Sem emojis em títulos. Use admonitions (seção 5) para chamar atenção.

## 2. Termos técnicos

- Mantenha em inglês os termos que o mercado usa em inglês: *log*, *parser*, *query*, *dashboard*, *threat hunting*, *brute force*. Não force traduções como "analisador sintático".
- Use o termo em português quando ele é o comum: "regra de detecção", "falso positivo", "consulta" (também vale *query*), "evento".
- **Siglas:** escreva por extenso na primeira vez que aparecem na página. Ex.: "UDM (Unified Data Model)". Depois, só a sigla.
- **Sempre em `código`:** nomes de campos (`target.user.userid`), IDs de evento (`4625`), comandos, caminhos de arquivo, valores literais, nomes de log type (`WINEVTLOG`).
- **Negrito** só para o termo sendo definido ou para o que não pode passar batido. Uma ou duas vezes por seção, no máximo.

## 3. Títulos e estrutura

- Um único `#` por arquivo: o título da página.
- `##` para seções e `###` para subseções. Evite `####`.
- Títulos com **só a primeira letra maiúscula** (exceto nomes próprios e siglas): "Campos mais usados", não "Campos Mais Usados".
- Seções curtas. Se uma seção passa de uma tela, divida em subseções ou mova para outra página.
- Use **listas** para passos e itens soltos, **tabelas** para comparações e mapeamentos (ID → significado, campo → descrição).

## 4. Formato de nota técnica (página de referência)

Toda página de referência segue esta ordem. Seções marcadas como *opcional* podem sair quando não fizerem sentido; as outras devem existir.

```markdown
---
description: Uma frase que resume a página (aparece na busca e no Google).
tags:
  - windows
  - autenticacao
---

# Título da nota

Resumo de 1 a 2 frases: o que é e por que importa para a defesa.

!!! abstract "Resumo rápido"        # opcional, para notas longas
    - Fato-chave 1
    - Fato-chave 2

## Conceito                          # o que é, sem depender de ferramenta
## Onde aparece                      # fonte de log, canal, campos (opcional)
## Exemplo                           # log/evento real, anonimizado
## Detecção e busca                  # queries e regras, uma aba por ferramenta (opcional)
## O que olhar numa investigação     # checklist prático
## Armadilhas e falsos positivos     # opcional
## Referências
```

Regras do formato:

- **Front matter:** `description` (uma frase) e `tags` (2 a 5, em minúsculas, sem acento, com hífen: `google-secops`, `autenticacao`). Tags ligam páginas e posts sobre o mesmo assunto.
- **Exemplo** sempre com um dado concreto: um log, um evento, uma saída de comando. Explicação sem exemplo não é nota.
- **Detecção e busca** usa abas quando há mais de uma ferramenta (`=== "Google SecOps"`, `=== "Splunk"`, `=== "PowerShell"`).
- **O que olhar numa investigação** é uma lista de verificação: perguntas ou campos para checar, na ordem em que você faria.
- **Referências** sempre no fim, com fontes primárias primeiro (documentação oficial, RFC, MITRE ATT&CK).
- Página ainda incompleta leva, logo abaixo do título:

  ```markdown
  !!! info "Em construção"
      Esta página ainda está sendo escrita.
  ```

## 5. Admonitions

Use no máximo 3 por página, cada tipo com um papel fixo:

| Tipo | Quando usar | Título padrão |
|------|-------------|---------------|
| `abstract` | Resumo rápido no topo de notas longas | "Resumo rápido" |
| `tip` | Atalho ou dica prática | "Dica" |
| `note` | Complemento que não cabe no texto | "Observação" |
| `warning` | Armadilha, falso positivo, algo não testado | "Atenção" |
| `danger` | Ação que pode quebrar algo ou apagar dados | "Cuidado" |
| `info` | Página em construção | "Em construção" |
| `example` | Exemplo longo que pode ficar recolhido (`??? example`) | "Exemplo" |

Use `???` em vez de `!!!` para deixar o bloco recolhido (bom para logs grandes).

## 6. Blocos de código

- **Sempre** indique a linguagem e, quando ajudar, um título:

  ````markdown
  ```json title="Evento UDM"
  ```
  ````

- Linguagens padrão:

  | Conteúdo | Linguagem |
  |----------|-----------|
  | Regra YARA-L, busca UDM | `text` (não há destaque para YARA-L) |
  | Evento do Windows | `xml` |
  | Evento UDM, log JSON | `json` |
  | Linha de syslog, log de texto | `text` |
  | Comandos Linux | `bash` |
  | Comandos Windows | `powershell` |
  | Splunk SPL, KQL | `text` |

- Um bloco por ideia. Explique o que o código faz **antes** do bloco, não depois.
- Para destacar linhas: `hl_lines="3 4"`.

## 7. Dados de exemplo

Nunca publique dados reais de clientes ou do trabalho. Antes de colar um log, troque:

| Dado | Use |
|------|-----|
| IPs | `192.0.2.x`, `198.51.100.x`, `203.0.113.x` (reservados para documentação, RFC 5737) |
| Domínios | `example.com`, `exemplo.local` |
| Usuários | `joao.silva`, `maria.souza`, `svc-backup` |
| Hosts | `WS-FIN-01`, `SRV-DC-01` |
| Hashes, IDs de cliente, tokens | Valores obviamente falsos ou truncados |

## 8. Arquivos, links e datas

- **Nomes de arquivo** em minúsculas, sem acento, com hífen: `eventos-de-logon.md`. Posts: `AAAA-MM-DD-slug.md`.
- **Links internos** sempre relativos ao arquivo `.md`: `[UDM](../SIEM/Google-SecOps/udm.md)`. O Zensical avisa no build se o link quebrar.
- **Links externos** com texto descritivo: `[Documentação do evento 4625](https://...)`, nunca "clique aqui".
- **Datas** no front matter como `AAAA-MM-DD`. No texto, por extenso: "27 de novembro de 2026".

## 9. Checklist antes de publicar

- [ ] Título claro e resumo de 1 a 2 frases no topo
- [ ] Front matter com `description` e `tags`
- [ ] Pelo menos um exemplo concreto
- [ ] Campos, IDs e comandos em `código`
- [ ] Blocos de código com linguagem
- [ ] Dados anonimizados (seção 7)
- [ ] Referências no fim
- [ ] `zensical serve` sem avisos de link quebrado
