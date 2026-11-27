# 📌 O que é um Endereço IP?

Um **IP (Internet Protocol)** é um identificador único atribuído a cada dispositivo conectado a uma rede que utiliza o protocolo IP para comunicação. Ele funciona como o "endereço" de uma casa na internet — sem ele, os dispositivos não conseguem se localizar ou se comunicar.
O protocolo IP é **sem conexão** e **não confiável**, isso significa que ele entrega pacotes ("datagramas") **sem garantia de entrega, ordem ou integridade**.
---

# 📌 Classificação dos Endereços IPv4

Os endereços IPv4 são classificados em **classes** com base no primeiro octeto:

| Classe | Intervalo de IPs      | Uso Principal           |
|--------|------------------------|--------------------------|
| A      | 1.0.0.0 – 126.255.255.255 | Redes muito grandes       |
| B      | 128.0.0.0 – 191.255.255.255 | Redes médias              |
| C      | 192.0.0.0 – 223.255.255.255 | Pequenas redes            |
| D      | 224.0.0.0 – 239.255.255.255 | Multicast                 |
| E      | 240.0.0.0 – 255.255.255.255 | Reservado para testes     |

> ⚠️ O range de ip `127.0.0.0/8` é reservado para **loopback** (localhost).

---

# 📌 Endereços IP Privados

Certos intervalos são reservados para redes **privadas**, ou seja, não roteáveis diretamente na Internet:

- **Classe A**: `10.0.0.0/8`
- **Classe B**: `172.16.0.0/12`
- **Classe C**: `192.168.0.0/16`

Esses IPs são usados dentro de redes locais (LANs) e requerem NAT para acessar a Internet pública.

---

# 📌 O que é um IP APIPA?

**APIPA** significa **Automatic Private IP Addressing**. Ele é um mecanismo que permite a atribuição **automática** de um IP **caso o DHCP não esteja disponível**.

## Características do IP APIPA:

- Intervalo: `169.254.0.1` até `169.254.255.254`
- Máscara de sub-rede: `255.255.0.0` `/16`
- Atribuído **automaticamente** quando o computador não consegue contato com um servidor DHCP.
- **Não permite acesso à Internet**, apenas comunicação ponto a ponto entre máquinas na mesma sub-rede APIPA.

### Situação de uso:
📌 Um computador tenta obter um IP via DHCP, mas o servidor está fora do ar. O sistema, então, atribui um IP APIPA automaticamente para permitir alguma forma de conectividade básica.

---