---
tags:
  - arquivo
---
## Mitigate ICMP Attacks

Os hackers podem usar pacotes de eco do protocolo de mensagem de controle da Internet para descobrir sub-redes e hosts em uma rede protegida e gerar ataques de inundação dos DoS. 

Hackers podem usar mensagens de redirecionamento `ICMP` para alterar as tabelas de roteamento do host. Tanto as mensagens do `ICMP` Echo e quanto as Redirect devem ser bloqueadas pela entrada do roteador.

Várias mensagens `ICMP` são recomendadas para operação adequada de rede e devem ser permitidas na rede interna:

- `Echo reply` — Permite que os usuários façam ping em hosts externos.
- `Source quench` — Solicita que o remetente diminua a taxa de tráfego das mensagens.
- `Unreachable` — Gerado para pacotes que são negados administrativamente por uma ACL.

Várias mensagens ICMP são necessárias para a operação de rede adequada e devem ser permitidas para sair da rede:

- `Echo` — Permite que os usuários façam ping em hosts externos.
- `Problem parameter` — Informa o host sobre problemas de cabeçalho de pacote.
- `Packet too big` — Habilita a descoberta da unidade máxima de transmissão do pacote — `MTU`
- `Source quench` — Reduz o tráfego quando necessário.

> *Como regra, bloqueie todos os outros tipos de mensagens ICMP de saída.*

Os ACLs são usados para bloquear o Spoofing de Endereços IP, permitem marcar seletivamente serviços específicos por meio de um firewall e permitir que somente as mensagens ICMP necessárias. 

![[mitigate_ICMP_attacks.png]]

Inbound em `S0/0/0`:

``` shell
R1(config)# access-list 112 permit icmp any any echo-reply
R1(config)# access-list 112 permit icmp any any source-quench
R1(config)# access-list 112 permit icmp any any unreachable
R1(config)# access-list 112 deny icmp any any
R1(config)# access-list 112 permit ip any any
```

Inbound em `S0/0/0`:

``` shell
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any echo
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any parameter-problem
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any packet-too-big
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any source-quench
R1(config)# access-list 114 deny icmp any any
R1(config)# permit ip any any
```

---
## Mitigate SNMP Attacks

Protocolos de gerenciamento, como `SNMP`, são úteis para monitoramento remoto e gerenciamento de dispositivos em rede. No entanto, eles ainda podem ser explorados. 

Se o `SNMP` for necessário, a exploração de vulnerabilidades `SNMP` pode ser mitigada aplicando ACLs de interface para filtrar pacotes `SNMP` de sistemas não autorizados. Uma exploração ainda pode ser possível se o pacote `SNMP` for provido de um endereço que foi falsificado e é permitido pela ACL.

Essas medidas de segurança são úteis, mas os meios mais eficazes de prevenção de exploração é desativar o servidor `SNMP` em dispositivos iOS para os quais não é necessário. Como mostrado na figura, use o comando no snmp-server para desativar os serviços SNMP nos dispositivos Cisco IOS.

``` shell
Router(config)# no snmp-server
```