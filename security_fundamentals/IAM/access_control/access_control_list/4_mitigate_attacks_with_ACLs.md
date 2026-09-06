---
tags:
  - arquivo
---
## Mitigate Spoofing Attacks

As ACLs podem ser usadas para mitigar muitas ameaças de rede, como falsificação de endereço IP e ataques de negação de serviço — `DoS`. 

A maioria dos ataques usa algum tipo de falsificação. Spoofing de endereço IP substitui o processo de criação de pacotes normais inserindo um cabeçalho IP personalizado com um endereço IP de origem diferente. Os invasores podem esconder sua identidade, falsificando o endereço IP de origem.

Existem muitas classes conhecidas de endereços IP que nunca devem ser vistas como endereços IP de origem para o tráfego que entram na rede de uma organização. Por exemplo, na figura a interface `S0/0/0` é anexada à Internet e nunca deve aceitar pacotes de entrada dos seguintes endereços:

![[Mitigate Spoofing Attacks.png]]

- Todos os endereços de zeros;
- Endereços de broadcast;
- Endereços de host local — `127.0.0.0/8`;
- Automatic Private IP Addressing Addresses — `APIPA` — `169.254.0.0/16`;
- Endereços privados reservados — `RFC 1918`;
- Intervalo de endereço IP multicast — `224.0.0.0/4`;

A rede `192.168.1.0/24` é anexada à interface `R1 G0/0`. Essa interface deve permitir apenas pacotes de entrada com um endereço de origem dessa rede. A ACL para `G0/0` mostrada na figura só permitirá pacotes de entrada da rede `192.168.1.0/24`. Todos os outros serão descartados.

Inbound em `S0/0/0`:

``` shell
R1 — config# access-list 150 deny ip host 0.0.0.0 any
R1 — config# access-list 150 deny ip 10.0.0.0 0.255.255.255 any
R1 — config# access-list 150 deny ip 127.0.0.0 0.255.255.255 any
R1 — config# access-list 150 deny ip 172.16.0.0 0.15.255.255 any
R1 — config# access-list 150 deny ip 192.168.0.0 0.0.255.255 any
R1 — config# access-list 150 deny ip 224.0.0.0 15.255.255.255 any
R1 — config# access-list 150 deny ip host 255.255.255.255 any
```

Inbound em `G0/0`:

``` shell
R1— config# access-list 105 permit ip 192.168.1.0 0.0.0.255 any
```

---
## Allow necessary traffic through a firewall

Uma estratégia eficaz para atenuar ataques é permitir explicitamente apenas alguns tipos de tráfego através de um firewall. Por exemplo, o `Domain Name System` — `DNS`, o protocolo `Simple Mail Transfer Protocol`  — `SMTP` — e o `File Transfer Protocol` — `FTP` — são os serviços que geralmente devem ser permitidos por meio de um firewall. 

> *Também é comum configurar um firewall para que permita os administradores acesso remoto através do firewall. Secure Shell — `SSH`, `Syslog` e `Simple Network Management Protocol` — `SNMP` — são exemplos de serviços que um roteador pode precisar incluir.* 

Enquanto muitos desses serviços são úteis, eles devem ser controlados e monitorados. A exploração desses serviços leva a vulnerabilidades de segurança.

A figura mostra um exemplo de topologia com configurações de ACL para permitir serviços específicos na interface serial `S0/0/0`.

![[allow_necessary_traffic_through_a_firewall.png]]

Inbound em `S0/0/0`:

``` shell
R1 — config# access-list 180 permit udp any host 192.168.20.2 eq domain
R1 — config# access-list 180 permit tcp any host 192.168.20.2 eq smtp
R1 — config# access-list 180 permit tcp any host 192.168.20.2 eq ftp
R1 — config# access-list 180 permit tcp host 200.5.5.5 host 10.0.1.1 eq 22
R1 — config# access-list 180 permit udp host 200.5.5.5 host 10.0.1.1 eq syslog
R1 — config# access-list 180 permit udp host 200.5.5.5 host 10.0.1.1 eq snmptrap
```