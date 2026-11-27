---
description: Uma frase que resume a página.
tags:
  - tag-1
  - tag-2
---

# Título da nota

Resumo de 1 a 2 frases: o que é e por que importa para a defesa.

<!-- Opcional, para notas longas. Apague se não usar. -->
!!! abstract "Resumo rápido"
    - Fato-chave 1
    - Fato-chave 2

## Conceito

O que é, explicado sem depender de uma ferramenta específica.

## Onde aparece

<!-- Opcional. Fonte de log, canal, campos importantes. -->

| Campo | O que significa |
|-------|-----------------|
| `campo` | Descrição |

## Exemplo

Um log, evento ou saída real, com os dados anonimizados.

```text title="Exemplo"
cole aqui o log ou evento
```

## Detecção e busca

<!-- Opcional. Uma aba por ferramenta. -->

=== "Google SecOps"

    ```text title="Busca UDM"
    metadata.event_type = "EXEMPLO"
    ```

=== "Outra ferramenta"

    ```text
    consulta equivalente
    ```

## O que olhar numa investigação

- [ ] Primeira coisa a checar
- [ ] Segunda coisa a checar

## Armadilhas e falsos positivos

<!-- Opcional. -->

## Referências

- [Documentação oficial](https://example.com)
