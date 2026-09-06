---
tags:
  - arquivo
---
## Overview

Nos últimos anos, muitas redes começaram a transição para um ambiente IPv6. Parte da necessidade da transição para IPv6 é por causa das fraquezas inerentes no IPv4.

Infelizmente, como a migração para o IPv6 continua, os ataques IPv6 estão se tornando mais difundidos. IPv4 não desaparecerá durante a noite. O IPv4 coexistirá com o IPv6 e, em seguida, será gradualmente substituído pelo IPv6. Isso cria potenciais furos de segurança. 

Um exemplo de uma preocupação de segurança é que os atores de ameaça que alavancam o IPv4 para explorar o IPv6 em ambientes de pilha dupla. `Dual Stack` é um método de integração no qual um dispositivo tem conectividade para as redes IPv4 e IPv6. Em dispositivos de ambiente de pilha dupla operam com duas pilhas de protocolo IP.

O ator de ameaças pode realizar ataques furtivos que resultam na exploração da confiança usando anfitriões empilhados duplos, as mensagens do `NDP` do vizinho desonesto e técnicas de tunelamento. 

O Teredo Tunneling, por exemplo, é uma tecnologia de transição IPv6 que fornece atribuição automática de endereços IPv6 quando os hosts IPv4/IPv6 estão localizados por trás dos dispositivos Tradução de Endereços de Rede IPv4 — `NAT`. Isso realiza isso incorporando os pacotes IPv6 dentro dos pacotes IPv4 UDP. 

O ator de ameaça ganha uma posição na rede IPv4. O host comprometido envia anúncios de rogue roteador — `RAS`, que acionam hosts duplos empilhados para obter um endereço IPv6. 

O ator de ameaças pode então usar essa posição para se movimentar ou pivô, dentro da rede. O ator de ameaças pode comprometer anfitriões adicionais antes de enviar o tráfego de volta da rede, conforme mostrado na figura.

![[ipv6_exploit_acls.png]]

É necessário desenvolver e implementar uma estratégia para mitigar ataques contra infraestruturas e protocolos IPv6. Esta estratégia de mitigação deve incluir filtrar na borda usando várias técnicas, como ACLs IPv6.

---
## IPv6 ACL Syntax

A funcionalidade do ACL no IPv6 é semelhante às ACLs no IPv4. No entanto, não há equivalente a ACLs padrão IPv4. Além disso, todos os ACLs IPv6 devem ser configurados com um nome. A ACLs IPv6 permitem filtrar com base nos endereços de origem e de destino que estão viajando de entrada e saída para uma interface específica. 

Eles também suportam a filtragem de tráfego com base em cabeçalhos de opção IPv6 e informações opcionais do tipo de protocolo de camada superior para a granularidade mais fina de controle, semelhante a ACLs estendidas no IPv4. 

Para configurar uma ACL IPv6, use o comando ipv6 access-list para entrar no modo de configuração da ACL IPv6. Em seguida, use a sintaxe mostrada na figura para configurar cada entrada da lista de acesso para permitir ou negar especificamente o tráfego. 

A sintaxe mostrada é uma versão simplificada da sintaxe do IPv6 ACE. Existem opções adicionais. Deve ser claro a partir da sintaxe fornecida que os ACLs IPv6 são consideravelmente mais flexíveis que os ACLs IPv4.

Aplique uma ACL IPv6 a uma interface com o comando ipv6 traffic-filter.

``` shell
Router(config)# ipv6 access-list access-list-name
Router(config-ipv6-acl)# deny | permit protocol {source-ipv6-prefix / prefix-length | any | host source-ipv6-address} [ operator [ port-number ]] { destination-ipv6-prefix / prefix-length | any | host destination-ipv6-address } [ operator [ port-number ]] [ dscp value ] [ fragments ] [ log ] [ log-input ] [ sequence value ] [ time-range name ]
```

---
## Configure IPv6 ACLs

Uma ACL do IPv6 contém uma negação implícita no deny ipv6 any any. Cada IPv6 ACL também contém regras de licença implícitas para permitir a descoberta vizinha do IPv6. 

O IPv6 `Neighbor Discovery Protocol` — `NDP` — requer o uso da camada de rede IPv6 para enviar anúncios vizinhos — `NAS` — e solicitações vizinhas — `NSS`. Se um administrador configurar o comando deny ipv6 any Sem permitir explicitamente permitir o neighbor discovery, o NDP será desativado.

Na figura, R1 está permitindo o tráfego de entrada em `G0/0` a partir de `2001:DB8:1:1::/64` rede. Os pacotes Na e NS são explicitamente permitidos. O tráfego proveniente de qualquer outro endereço IPv6 é explicitamente negado. 

Se o administrador configurasse apenas a primeira instrução de permissão, a ACL teria o mesmo efeito. No entanto, é uma boa prática documentar as declarações implícitas explicitamente configurando-as.

![[configure_IPv6_ACLs.png]]

``` shell
R1(config)# ipv6 access-list LAN_ONLY
R1(config-ipv6-acl)# permit 2001:db8:1:1::/64 any
R1(config-ipv6-acl)# permit icmp any any nd-na
R1(config-ipv6-acl)# permit icmp any any nd-ns
R1(config-ipv6-acl)# deny ipv6 any any
R1(config-ipv6-acl)# end
R1# show ipv6 access-list
IPv6 access list LAN_ONLY
    permit ipv6 2001:DB8:1:1::/64 any sequence 10
    permit icmp any any nd-na sequence 20
    permit icmp any any nd-ns sequence 30
    deny ipv6 any any sequence 40
R1#
```
