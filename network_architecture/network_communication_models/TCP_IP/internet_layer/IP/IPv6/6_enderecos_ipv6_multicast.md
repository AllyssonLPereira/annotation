---
tags:
  - arquivo
---
### Endereços multicast IPv6 atribuídos


Você aprendeu que existem três grandes categorias de endereços IPv6: unicast, anycast e multicast. Este tópico entra em mais detalhes sobre endereços multicast.

Os endereços IPv6 multicast são semelhantes aos endereços IPv4 multicast. Lembre-se de que um endereço multicast é usado para enviar um único pacote a um ou mais destinos (grupo multicast). Os endereços multicast IPv6 têm o prefixo ff00::/8.

> [!NOTE]
> Os endereços multicast só podem ser endereços destino e não endereços origem.

Há dois tipos de endereços IPv6 multicast:

- Endereços multicast conhecidos
- Endereços multicast de nó solicitado.

---
### Endereços Multicast IPv6 bem conhecidos


*Endereços multicast IPv6 bem conhecidos são atribuídos. 

Os endereços multicast atribuídos são endereços multicast reservados para grupos predefinidos de dispositivos. Um endereço multicast atribuído é um único endereço usado para acessar um grupo de dispositivos que executam um serviço ou um protocolo comum. 

Os endereços multicast atribuídos são usados no contexto com protocolos específicos, como o DHCPv6.

Estes são dois grupos multicast atribuídos ao IPv6 comuns:

- `ff02::1` [Grupo multicast de todos os nós]:

	Esse é um grupo de multicast que todos os dispositivos com IPv6 habilitado participam. *Um pacote enviado para esse grupo é recebido e processado por todas as interfaces IPv6 no link ou rede.* Isso tem o mesmo efeito que um endereço de broadcast em IPv4. 

- `ff02::2` [Grupo multicast de todos os roteadores]:

	Esse é um grupo multicast que todos os roteadores IPv6 participam. Um roteador se torna um membro desse grupo quando é habilitado com um roteador IPv6 com o comando de configuração global `ipv6 unicast-routing`. 

	Um pacote enviado para esse grupo é recebido e processado por todos os roteadores IPv6 no link ou rede.
	

> Os dispositivos habilitados para IPv6 enviam mensagens ICMPv6 RS para o endereço multicast de todos os roteadores. A mensagem de RS solicita uma mensagem de RA do roteador IPv6 para ajudar o dispositivo em sua configuração de endereço. O roteador IPv6 responde com uma mensagem RA.

---
### Endereços multicast IPv6 de nó solicitado
Um endereço multicast de nó solicitado é semelhante ao endereço multicast all-nodes(todos os nós). A vantagem do endereço multicast nó solicitado é que ele é mapeado para um endereço multicast Ethernet especial. Isso permite que a placa de rede Ethernet filtre o quadro, examinando o endereço MAC de destino sem enviá-lo ao processo IPv6 para ver se o dispositivo é o alvo pretendido do pacote IPv6.