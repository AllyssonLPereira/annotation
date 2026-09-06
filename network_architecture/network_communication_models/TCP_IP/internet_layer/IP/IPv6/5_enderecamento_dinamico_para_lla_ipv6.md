---
tags:
  - arquivo
---
### LLAs dinâmicos


Todos os dispositivos IPv6 devem ter um IPv6 LLA. Assim como IPv6 GUAs, você também pode criar LLAs dinamicamente. Independentemente de como você cria seus LLAS (e seus GUAs), é importante que você verifique toda a configuração de endereço IPv6.

---
### LLAs dinâmicos no Windows


Sistemas operacionais, como o Windows, normalmente usarão o mesmo método para um GUA criado pelo SLAAC e um LLA atribuído dinamicamente.

---
### LLAs dinâmicos em Roteadores Cisco


Os roteadores Cisco criam automaticamente um endereço IPv6 de link local sempre que um endereço unicast global é atribuído à interface. 

Por padrão, os roteadores Cisco IOS usam o EUI-64 para gerar a ID da interface de todos os endereços de link local em interfaces IPv6. Em interfaces seriais, o roteador usará o endereço MAC de uma interface Ethernet. Lembre-se de que um endereço de link local deve ser exclusivo somente nesse link ou rede. 

No entanto, uma desvantagem ao usar o endereço link local atribuído dinamicamente é sua longa ID de interface, o que faz com que seja um desafio identificar e lembrar os endereços atribuídos. A Figura 3 mostra o endereço MAC da interface Gigabit Ethernet 0/0 de R1. 

Esse endereço é usado para criar dinamicamente o LLA na mesma interface e também para a interface Serial 0/1/0.

Para tornar mais fácil reconhecer esses endereços em roteadores e lembrar deles, é comum configurar estaticamente endereços IPv6 de link local nos roteadores.

``` shell
R1# show interface gigabitEthernet 0/0/0

GigabitEthernet0/0/0 is up, line protocol is up
  Hardware is ISR4221-2x1GE, address is 7079.b392.3640 (bia 7079.b392.3640)
  
(Output omitted)

R1# show ipv6 interface brief

GigabitEthernet0/0/0   [up/up]
    fe80::7279:b3ff:fe92:3640
    2001:db8:acad:1::1
  
GigabitEthernet0/0/1   [up/up]
    fe80::7279:b3ff:fe92:3641
    2001:db8:acad:2::1

Serial0/1/0            [up/up]
    fe80::7279:b3ff:fe92:3640
    2001:db8:acad:3::1

Serial0/1/1            [down/down]
    unassigned
  
R1#
```