---
tags:
  - arquivo
---
### O que é ND?

Neighbor Discovery (ND) é usado para determinar o endereço MAC de um dispositivo com um endereço IPv6 de destino conhecido.

---
### Comunicação na camada de Acesso

Em uma rede Ethernet local, uma NIC só aceitará um quadro se o endereço de destino for o endereço MAC de broadcast ou corresponder ao endereço MAC da NIC.

A maioria dos aplicativos de rede, entretanto, baseiam-se no endereço IP lógico de destino para identificar a localização de servidores e clientes.

---
### Mensagens de descoberta de vizinhos IPv6

O protocolo de descoberta de vizinhos IPv6 às vezes é chamado de ND ou NDP. *O ND fornece serviços de resolução de endereço, descoberta de roteador e redirecionamento para IPv6 usando ICMPv6.* O ICMPv6 ND usa cinco mensagens ICMPv6 para executar estes serviços:

- Mensagens de solicitação de vizinho
- Mensagens de anúncio vizinho
- Mensagens de solicitação de roteador
- Mensagens de anúncio do roteador
- Redirecionar mensagem (usada para uma melhor seleção do próximo salto.).

As mensagens de solicitação de vizinho e anúncio de vizinho são usadas para mensagens de dispositivo a dispositivo, como resolução de endereço (semelhante ao ARP para IPv4). Os dispositivos incluem computadores host e roteadores.

---
### Descoberta de Vizinhos IPv6 - Resolução de Endereço

Assim como ARP para IPv4, os dispositivos IPv6 usam IPv6 ND para determinar o endereço MAC de um dispositivo que tem um endereço IPv6 conhecido.

As mensagens de solicitação de vizinho ICMPv6 e de anúncio de vizinho são usadas para resolução de endereço MAC. Isso é semelhante às Solicitações ARP e Respostas ARP usadas pelo ARP para IPv4. 

> Por exemplo, suponha que PC1 queira fazer ping em PC2 no endereço IPv6 2001:db8:acad: :11. Para determinar o endereço MAC para o endereço IPv6 conhecido, o PC1 envia uma mensagem de solicitação de vizinho ICMPv6


*As mensagens de solicitação de vizinho ICMPv6 são enviadas usando endereços multicast Ethernet e IPv6 especiais.* Isso permite que o NIC Ethernet do dispositivo receptor determine se a mensagem de solicitação de vizinho é para si mesmo sem precisar enviá-la ao sistema operacional para processamento.


> O PC2 responde à solicitação com uma mensagem de anúncio de vizinho ICMPv6 que inclui seu endereço MAC.





