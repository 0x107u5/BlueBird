---
description: Como ler o evento 4625 (falha de logon) do Windows e usá-lo para detectar brute force e password spraying.
tags:
  - windows
  - autenticacao
  - google-secops
---

# Evento 4625: falha de logon no Windows

O evento `4625` é gerado sempre que uma tentativa de logon falha no Windows. É a principal fonte para detectar **brute force**, **password spraying** e uso de contas desativadas.

!!! abstract "Resumo rápido"
    - Canal: `Security`. Exige a auditoria de **Logon** com falha ativada.
    - Os campos que mais importam são `TargetUserName`, `IpAddress`, `LogonType` e `SubStatus`.
    - Muitas falhas de **um IP para vários usuários** sugere password spraying. Muitas falhas de **um IP para um usuário** sugere brute force.

## Conceito

Toda vez que alguém tenta se autenticar numa máquina Windows (no teclado, pela rede, por RDP) e a autenticação falha, o sistema registra um `4625` na máquina onde o logon foi tentado. O par de sucesso é o evento `4624`.

Sozinho, um `4625` quase sempre é alguém que errou a senha. O valor está no **volume e no padrão**: muitas falhas em pouco tempo, a partir da mesma origem, ou contra contas que não existem.

## Onde aparece

| Campo | O que significa |
|-------|-----------------|
| `TargetUserName` | Conta que tentou logar |
| `TargetDomainName` | Domínio da conta |
| `IpAddress` / `WorkstationName` | Origem da tentativa |
| `LogonType` | Como o logon foi tentado (tabela abaixo) |
| `Status` / `SubStatus` | Motivo da falha (tabela abaixo) |
| `ProcessName` | Processo que pediu o logon |

Tipos de logon mais comuns:

| `LogonType` | Significado |
|-------------|-------------|
| `2` | Interativo (no teclado) |
| `3` | Rede (compartilhamento SMB, por exemplo) |
| `4` | Batch (tarefa agendada) |
| `5` | Serviço |
| `7` | Desbloqueio de tela |
| `8` | Rede com senha em texto claro |
| `10` | Remoto interativo (RDP) |
| `11` | Credencial em cache |

Códigos de `SubStatus` que ajudam a separar erro comum de ataque:

| `SubStatus` | Motivo |
|-------------|--------|
| `0xC000006A` | Senha errada para um usuário que existe |
| `0xC0000064` | Usuário não existe |
| `0xC0000234` | Conta bloqueada |
| `0xC0000072` | Conta desativada |
| `0xC000006F` | Fora do horário permitido |
| `0xC0000071` | Senha expirada |
| `0xC0000193` | Conta expirada |

## Exemplo

Falha de logon por RDP com senha errada, vista no controlador de domínio:

```xml title="Evento 4625 (trecho)" hl_lines="2 5 6 7"
<EventData>
  <Data Name="TargetUserName">joao.silva</Data>
  <Data Name="TargetDomainName">EXEMPLO</Data>
  <Data Name="Status">0xc000006d</Data>
  <Data Name="SubStatus">0xc000006a</Data>
  <Data Name="LogonType">10</Data>
  <Data Name="IpAddress">203.0.113.45</Data>
  <Data Name="WorkstationName">-</Data>
  <Data Name="ProcessName">C:\Windows\System32\svchost.exe</Data>
</EventData>
```

## Detecção e busca

No Google SecOps, os eventos do Windows chegam pelo log type `WINEVTLOG` e o `4625` vira um evento UDM do tipo `USER_LOGIN` com a ação `BLOCK`.

!!! warning "Atenção"
    O mapeamento de campos depende da versão do parser. Confira um evento real na sua instância antes de usar as regras abaixo.

=== "Busca UDM"

    ```text title="Todas as falhas de logon do Windows"
    metadata.product_event_type = "4625"
    AND metadata.event_type = "USER_LOGIN"
    AND security_result.action = "BLOCK"
    ```

=== "Regra YARA-L"

    Dispara quando o mesmo IP falha 10 vezes ou mais contra o mesmo usuário em 10 minutos.

    ```text title="windows_brute_force.yaral"
    rule windows_brute_force {
      meta:
        author = "0x107u5"
        description = "10 ou mais falhas de logon (4625) do mesmo IP para o mesmo usuário em 10 minutos"
        severity = "Medium"

      events:
        $e.metadata.event_type = "USER_LOGIN"
        $e.metadata.product_event_type = "4625"
        $e.security_result.action = "BLOCK"
        $e.target.user.userid = $user
        $e.principal.ip = $ip

      match:
        $user, $ip over 10m

      outcome:
        $tentativas = count($e.metadata.id)

      condition:
        #e >= 10
    }
    ```

=== "PowerShell"

    Últimas 50 falhas de logon na máquina local:

    ```powershell
    Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 50 |
      Select-Object TimeCreated, @{n='Usuario';e={$_.Properties[5].Value}},
                                 @{n='IP';e={$_.Properties[19].Value}}
    ```

## O que olhar numa investigação

- [ ] Qual é a origem (`IpAddress`)? É interna, de VPN ou da internet?
- [ ] Um usuário ou muitos? Muitos usuários com poucas tentativas cada sugere password spraying.
- [ ] O `SubStatus` é `0xC0000064` (usuário não existe)? Indica enumeração ou lista de usuários adivinhada.
- [ ] O `LogonType` faz sentido? RDP (`10`) vindo da internet merece atenção imediata.
- [ ] Houve um `4624` (sucesso) da mesma origem logo depois das falhas?
- [ ] A conta foi bloqueada (`4740`) em seguida?

## Armadilhas e falsos positivos

- **Senha antiga salva:** um celular ou um serviço com a senha antiga gera falhas constantes da mesma origem, sempre para o mesmo usuário, por dias. Volume alto, mas padrão regular.
- **`IpAddress` vazio ou `-`:** logons locais e alguns logons de rede não trazem IP. Use `WorkstationName` como origem.
- **Contas de serviço:** senha trocada sem atualizar o serviço gera rajadas de `4625` com `LogonType` `5`.

## Referências

- [Microsoft: evento 4625](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4625)
- [Google SecOps: sintaxe YARA-L 2.0](https://cloud.google.com/chronicle/docs/detection/yara-l-2-0-syntax)
- [Google SecOps: lista de campos UDM](https://cloud.google.com/chronicle/docs/reference/udm-field-list)
- [MITRE ATT&CK T1110: Brute Force](https://attack.mitre.org/techniques/T1110/)
