---
tags:
  - arquivo
---
##### Domain broadcast and segmentation:

Um domínio de broadcast define um conjunto de hosts que pertencem a uma mesma rede. 

É interessante observar que os switchs propagam broadcasts por todas as interfaces, exceto a interface em que foram recebidos. Já os routers não propagam, eles não propagam por outras interfaces.

Cada domínio de broadcast é segmentado/separado por um router, isto é, cada uma de suas interfaces se conectam a um domínio.

---

##### Problems with Large Broadcast Domains:

Um grande problema de domínio de broadcast é um domínio com vários hosts. Pois, nesse cenário, pode haver uma quantidade excessiva de tráfego broadcast. Isso pode gerar [operações de rede lentas] e [operações de dispositivo lentos] (pois cada host deve processar os broadcasts).

Se muitos hosts estiverem conectados ao mesmo domínio de broadcast, o tráfego de broadcast poderá ficar excessivo. O número de hosts e a quantidade de tráfego de rede que pode ser suportada na rede local são [limitados pelos recursos dos switches] usados para conectá-los.

A solução é transformar a rede em redes menores (processo denominado de [divisão em sub-redes]).

Por exemplo, uma rede chamada LAN1 (172.16.0.0/16) com 400 usuários é dividido em duas sub-redes: LAN1(172.16.0.0/24) e LAN2(172.16.1.0/24), cada uma com 200 usuários.


> [!NOTE] Title
> Observe como o comprimento do prefixo mudou de /16 para /24. Esta é a base da divisão em sub-redes: usar bits de host para criar sub-redes adicionais.


