# 📌 O que são portas de rede?

Portas de rede são identificadores numéricos usados para direcionar a comunicação entre dispositivos em uma rede. Elas funcionam como "portas de entrada e saída" lógicas que permitem que um único endereço IP suporte múltiplos serviços ao mesmo tempo — como navegação web, e-mail, acesso remoto, entre outros.

No modelo TCP/IP, cada conexãooaneamente.

# 📌 Como funcionam?

Quando você acessa um site, por exemplo, seu navegador se conecta ao IP do servidor na porta 80 (HTTP) ou 443 (HTTPS). O sistema operacional do servidor sabe que deve entregar esse tráfego ao serviço web porque está escutando naquela porta.

# 📌 Faixas de portas

As portas vão de 0 a 65535 e são divididas em três categorias:

 -   **0–1023** — Portas bem conhecidas (Well-known ports):
    Reservadas para serviços padrão como HTTP (80), SSH (22), DNS (53), etc.

 -   **1024–49151** — Portas registradas (Registered ports):
    Usadas por softwares e aplicações específicas que não fazem parte do núcleo do sistema.

 -   **49152–65535** — Portas dinâmicas/privadas (Dynamic/Private ports):
    Usadas temporariamente por clientes durante conexões (também chamadas de portas efêmeras).


# 📌 Tabela de portas x Serviços

| Porta Padrão | Serviço         | Finalidade                                           | Portas Alternativas/Notas |
| ------------ | --------------- | ---------------------------------------------------- | ------------------------- |
| 21           | FTP             | Transferência de arquivos (sem criptografia)         | 2121                      |
| 22           | SSH / SFTP      | Acesso remoto seguro / FTP sobre SSH (criptografado) | 2222                      |
| 23           | Telnet          | Acesso remoto (sem criptografia)                     |                           |
| 25           | SMTP            | Envio de e-mails                                     | 587 (STARTTLS), 465 (SSL) |
| 53 (TCP/UDP) | DNS             | Resolução de nomes de domínio                        |                           |
| 80           | HTTP            | Comunicação web sem criptografia                     | 8080, 8000, 8888          |
| 88           | Kerberos        | Autenticação segura em redes corporativas            |                           |
| 110          | POP3            | Recebimento de e-mails (simples)                     | 995 (com SSL)             |
| 123 (UDP)    | NTP             | Sincronização de tempo entre dispositivos            |                           |
| 143          | IMAP            | Recebimento de e-mails (sincronização)               | 993 (com SSL)             |
| 161 (UDP)    | SNMP            | Monitoramento de dispositivos de rede                | 162 (trap)                |
| 389          | LDAP            | Diretório de autenticação e informações              | 636 (LDAPS)               |
| 443          | HTTPS           | Comunicação web com criptografia (TLS/SSL)           | 8443                      |
| 445          | SMB/CIFS        | Compartilhamento de arquivos e impressoras (Windows) | 139 (NetBIOS)             |
| 465          | SMTP (SSL)      | Envio de e-mails com criptografia                    |                           |
| 993          | IMAP (SSL)      | Recebimento de e-mails com criptografia              |                           |
| 995          | POP3 (SSL)      | Recebimento de e-mails com criptografia              |                           |
| 990          | FTPS            | FTP com criptografia (SSL/TLS)                       |                           |
| 3306         | MySQL           | Banco de dados relacional                            |                           |
| 3389         | RDP             | Acesso remoto a desktops Windows                     | 3390                      |
| 5432         | PostgreSQL      | Banco de dados relacional                            |                           |
| 6379         | Redis           | Armazenamento em memória (chave-valor)               |                           |
| 27017        | MongoDB         | Banco de dados NoSQL                                 |                           |
