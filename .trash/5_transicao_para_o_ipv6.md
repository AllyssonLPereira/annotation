---
tags:
  - arquivo
---
##### Problems with IPv4

O IPv4 tem ficado sem endereços, por isso a necessidade de migrar para o IPv6. Esse possui um espaço de endereço muito maior, de 128 bits, fornecendo $34 * 10^{37}$ espaços de endereços possíveis.

Assim, o IPv6 vem para suprir essa necessidade de endereços. Mas a sua criação também buscou resolver alguns problemas/limitações do IPv4.

Então, apesar dos endereços privados e do NAT terem sido fundamentais para retardar o esgotamento de espaços de endereço, o NAT é problemático para muitos aplicativos, ele cria latência e possui limitações que impedem as comunicações ponto a ponto.

Vemos que os provedores móveis tem liderado o caminho para a transição do IPv6, mas não somente eles, os ISP's também tem feito essa migração.

Temos ainda a IoT (Internet of Things) que tem crescido bastante e, com isso, a necessidade de espaço de endereços se torna crucial com essa evolução de dispositivos conectados à internet.

---

##### Coexistence of IPv4 and IPv6

A transição da versão 4 para a versão 6 não é algo imediato, isso levará anos para acontecer. Agora, a IETF criou vários protocolos e ferramentas para que ocorra essa migração. Para tal, existem 3 categorias:

- [Pilha dupla]:

	A pilha dupla permite que IPv4 e IPv6 coexistam no mesmo segmento de rede. Esses dispositivos de pilha dupla conseguem executar os dois protocolos simultaneamente.

- [Tunelamento]:

	Tunelamento é um método de transporte de pacote IPv6 através de uma rede IPv4. O pacote IPv6 é encapsulado dentro de um pacote IPv4, de forma semelhante a outros tipos de dados.

- [Conversão]:

	O NAT64 permite a comunicação de dispositivos habilitados com IPv6 com dispositivos habilitados com IPv4, fazendo a conversão de um pacote para outro.