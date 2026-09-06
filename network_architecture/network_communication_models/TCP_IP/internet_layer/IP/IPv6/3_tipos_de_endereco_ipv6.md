---
tags:
  - arquivo
---
### Unicast, Multicast, Anycast


Tal como acontece com o IPv4, existem diferentes tipos de endereços IPv6. Na verdade, existem três grandes categorias de endereços IPv6:

- [Unicast] – Um endereço IPv6 unicast identifica exclusivamente uma interface em um dispositivo habilitado para IPv6.

- [Multicast] – Um endereço IPv6 multicast é usado para enviar um único pacote IPv6 para vários destinos.

- [Anycast] – Um endereço IPv6 anycast é qualquer endereço IPv6 unicast que possa ser atribuído a vários dispositivos. Um pacote enviado a um endereço de anycast é roteado para o dispositivo mais próximo que tenha esse endereço.

*Ao contrário do IPv4, o IPv6 não possui um endereço de broadcast. No entanto, há um endereço multicast para todos os nós IPv6 que fornece basicamente o mesmo resultado.*

---
### Comprimento do prefixo IPv6


Lembre-se de que o prefixo (a parte de rede) de um endereço IPv4 pode ser identificado pelo comprimento do prefixo (notação em barra) ou por uma máscara de sub-rede decimal com pontos. 

Por exemplo, o endereço IPv4 192.168.1.10 com máscara de sub-rede decimal com pontos 255.255.255.0 é equivalente a 192.168.1.10/24.

*No IPv6 é chamado de comprimento do prefixo*. [O IPv6 não usa a notação decimal com pontos da máscara de sub-rede]. Como o IPv4, o comprimento do prefixo é representado na notação de barra e é usado para indicar a parte da rede de um endereço IPv6.

*O comprimento do prefixo pode variar de 0 a 128. O comprimento do prefixo IPv6 recomendado para LANs e a maioria dos outros tipos de redes é /64.*


> [!NOTE] 
> É altamente recomendável usar um ID de interface de 64 bits para a maioria das redes. Isso ocorre porque a configuração automática de endereço sem estado (SLAAC) usa 64 bits para o ID de interface. Também facilita a criação e o gerenciamento de sub-redes.

---
### Endereços IPv6 unicast

![[enderecos_ipv6_unicast.png]]


Ao contrário dos dispositivos IPv4 que têm apenas um único endereço, os endereços IPv6 normalmente têm dois endereços unicast:

- [Um endereço unicast global (GUA)]:

	E semelhante a um endereço IPv4 público. São endereços de Internet roteáveis e globalmente exclusivos. GUAs podem ser configurados estaticamente ou dinamicamente distribuídos.

- [Endereço de Link-Local (LLA)]:

	Isso é necessário para cada dispositivo habilitado para IPv6. *Os LLAs são usados para se comunicar com outros dispositivos no mesmo link local.* [No IPv6, o termo link se refere a uma sub-rede.]

	LLAs são limitados a um único enlace. Sua exclusividade só deve ser confirmada nesse link, porque eles não são roteáveis além do link. Em outras palavras, os roteadores não encaminham pacotes com um endereço de link local origem ou destino.

---
### Endereço local exclusivo


Endereços locais exclusivos (intervalo fc00::/7 a fdff::/7) ainda não são comumente implementados. No entanto, endereços locais exclusivos podem eventualmente ser usados para endereçar dispositivos que não devem ser acessíveis de fora, como servidores internos e impressoras.

Os endereços IPv6 unique local têm alguma semelhança com endereços privados do RFC 1918 para o IPv4, mas há diferenças significativas:

- Os endereços unique local são utilizados para endereçamento local dentro de um site ou entre um número limitado de sites.

- Os endereços unique local podem ser usados para dispositivos que nunca precisarão ou terão acesso por outra rede.

- Endereços locais exclusivos não são globalmente roteados ou traduzidos para um endereço IPv6 global.

---
### IPv6 GUA


O endereço IPv6 unicast global (GUA) é globalmente exclusivo e roteável na Internet IPv6. *Esses endereços são equivalentes aos endereços públicos do IPv4.* O Internet Committee for Assigned Names and Numbers (ICANN), o operador de Internet Assigned Numbers Authority (IANA), aloca os blocos de endereço IPv6 para os cinco RIRs. 

*[No momento, somente endereços unicast globais com os primeiros três bits de 001 ou 2000::/3 estão sendo atribuídos.]*

	A figura mostra o intervalo de valores para o primeiro hexteto, na qual o primeiro dígito hexadecimal para GUAs atualmente disponíveis começa com um 2 ou um 3. Isso é apenas um oitavo do espaço de endereço IPv6 total disponível, excluindo uma parte muito pequena de outros tipos de endereços unicast e multicast.

> [!NOTE]
> O endereço 2001:0DB8::/32 foi reservado para fins de documentação.

![[ipv6_gua.png]]

Um GUA tem três partes:

- Prefixo global de roteamento
- ID da Sub-Rede
- ID da interface

---
### Estrutura IPv6 GUA

![[endereço_ipv6_com_prefixo_de_roteamento_global_.48_e_prefixo_.64.png]]

- [Prefixo Global de Roteamento]:

	O prefixo global de roteamento é o prefixo (parte de rede) do endereço que é atribuído pelo provedor (como um ISP) a um cliente ou um site. Por exemplo, é comum que os ISPs atribuam um prefixo de roteamento global /48 a seus clientes. 

	O prefixo de roteamento global geralmente varia dependendo das políticas do ISP.

	A figura anterior mostra um GUA usando um prefixo de roteamento global /48. Os prefixos /48 são os prefixos de roteamento global mais comuns atribuídos.

	Por exemplo, o endereço IPv6 2001:db8:acad::/ 48 possui um prefixo de roteamento global que indica que os primeiros 48 bits (3 hextets) (2001:db8:acad) são como o ISP conhece esse prefixo (rede). 

	Dois-pontos duplo (::) antes do comprimento de prefixo /48 significa que o restante do endereço contém apenas 0s. O tamanho do prefixo de roteamento global determina o tamanho da ID da sub-rede.


- [ID da Sub-Rede]:

	O campo ID da sub-rede é a área entre o Prefixo de Roteamento Global e o ID da interface. Ao contrário do IPv4, onde você deve pedir bits emprestados da parte do host para criar sub-redes, o IPv6 foi projetado tendo em mente a sub-rede. 

	O ID da sub-rede é usado por uma organização para identificar sub-redes dentro da sua localização. Quanto maior a ID da sub-rede, mais sub-redes disponíveis.

	*Muitas organizações estão recebendo um prefixo de roteamento global /32. Usando o prefixo /64 recomendado para criar um ID de interface de 64 bits, deixa um ID de sub-rede de 32 bits. 

	Isso significa que uma organização com um prefixo de roteamento global /32 e um ID de sub-rede de 32 bits terá 4,3 bilhões de sub-redes, cada uma com 18 quintilhões de dispositivos por sub-rede. Isso equivale a tantas sub-redes quantos endereços IPv4 públicos

	O endereço IPv6 na figura anterior tem um prefixo de roteamento global /48, que é comum entre muitas redes corporativas. Isso torna especialmente fácil examinar as diferentes partes do endereço. 

	Usando um tamanho típico de prefixo /64, os quatro primeiros hextetos são para a parte da rede do endereço, com o quarto hexteto indicando o ID da sub-rede. Os quatro hextetos restantes são para o ID da interface.


- [ID da interface]:

	A ID da interface IPv6 equivale à parte de host de um endereço IPv4. O termo ID da interface é usado porque um único host pode ter várias interfaces, cada uma com um ou mais endereços IPv6. 

	A figura mostra um exemplo da estrutura de um GUA IPv6. É altamente recomendável que as sub-redes /64 sejam usadas na maioria dos casos. Um ID de interface de 64 bits permite 18 quintilhões de dispositivos ou hosts por sub-rede.

	Uma sub-rede /64 ou prefixo (Global Routing Prefix + Subnet ID) deixa 64 bits para o ID da interface. Isso é recomendado para permitir que dispositivos habilitados para SLAAC criem seu próprio ID de interface de 64 bits. 

	Também torna o desenvolvimento de um plano de endereçamento IPv6 simples e eficaz.

	*Ao contrário do IPv4, no IPv6, todos os endereços de host de all-0s e de all-1s podem ser atribuídos a um dispositivo. O endereço todos-1s pode ser usado porque os endereços de broadcast não são usados dentro do IPv6. 

	*O endereço de all-0s também pode ser usado, mas é reservado como endereço de anycast de subnet-router, e deve ser atribuído somente aos roteadores.


![[ipv6_gua 1.png]]

---
### LLA IPv6

Um endereço IPv6 de link-local permite que um dispositivo se comunique com outros dispositivos habilitados para IPv6 no mesmo link e somente nesse link (sub-rede). Os pacotes com endereço de link local origem ou destino não podem ser roteados além do link de onde o pacote foi originado.

O GUA não é um requisito. No entanto, cada interface de rede habilitada para IPv6 deve ter um LLA.

Se um LLA não estiver configurado manualmente em uma interface, o dispositivo criará automaticamente um próprio, sem se comunicar com um servidor DHCP. 

Os hosts habilitados para LLA IPv6 criarão um endereço IPv6 mesmo que não tenha sido atribuído um endereço IPv6 unicast global ao dispositivo. 

Isso permite que dispositivos habilitados para IPv6 se comuniquem com outros dispositivos semelhantes na mesma sub-rede. Isso inclui a comunicação com o gateway padrão (roteador).

Os LLAs IPv6 estão no intervalo fe80: :/10. O /10 Indica que os primeiros 10 bits são 1111 1110 10xx xxxx. O primeiro hexteto tem um intervalo de 1111 1110 1000 0000 (fe80) a 1111 1110 1011 1111 (febf).

A Figura mostra um exemplo de comunicação usando endereços LLA IPv6. O PC é capaz de se comunicar diretamente com a impressora usando os LLAs.

![[ipv6_lla.png]] 

> Os roteadores usam o LLA de roteadores vizinhos para enviar atualizações de roteamento. Os hosts usam o LLA de um roteador local como gateway padrão.

> [!NOTE]
> Geralmente, é o endereço de link local do roteador, e não o endereço unicast global, que é usado como gateway padrão para outros dispositivos no link.
> 

Há duas maneiras pelas quais um dispositivo pode obter um LLA:

- [Estaticamente]

	Isso significa que o dispositivo foi configurado manualmente.

- [Dinamicamente]

	Isso significa que o dispositivo cria seu próprio ID de interface usando valores gerados aleatoriamente ou usando o método de Identificador Único Extended (EUI), que usa o endereço MAC do cliente juntamente com bits adicionais.