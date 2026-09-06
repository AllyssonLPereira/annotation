---
tags:
  - arquivo
---
### Mensagens RS e RA

Para o GUA, um dispositivo obtém o endereço dinamicamente através de mensagens ICMPv6 (Internet Control Message Protocol version 6). Os roteadores IPv6 enviam mensagens [ICMPv6 de RA] a cada 200 segundos para todos os dispositivos habilitados para IPv6 na rede. 

Uma mensagem de RA também é enviada em resposta a um host que envie uma mensagem [ICMPv6 de RS] (Solicitação de Roteador).

- As mensagens RS são enviadas pelos hosts, a todos os roteadores IPv6, solicitando informações de endereçamento.

- Mensagens RA são enviadas para todos os nós IPv6.


As mensagens de RA estão nas interfaces Ethernet do roteador IPv6. *O roteador deve estar habilitado para roteamento IPv6, que não vem habilitado por padrão.* Para habilitar um roteador como um roteador IPv6, o comando de configuração global `ipv6 unicast-routing` deve ser usado.

*A mensagem ICMPv6 de RA é uma sugestão para um dispositivo sobre como obter um endereço IPv6 unicast global.* A decisão final é do sistema operacional do dispositivo. A mensagem ICMPv6 de RA inclui:

- [Prefixo de rede e comprimento do prefixo]

	Informa ao dispositivo a que rede ele pertence.

- [Endereço do gateway padrão]

	É um endereço LLA IPv6, o endereço IPv6 origem da mensagem de RA.

- [Endereços DNS e nome de domínio]

	Endereços de servidores DNS e um nome de domínio.


Existem três métodos para mensagens RA:

- [Método 1]: *SLAAC*

	“Eu tenho tudo o que você precisa, incluindo o prefixo, comprimento do prefixo, endereço de gateway padrão e endereço DNS.”

- [Método 2]: *SLAAC com um servidor DHCPv6 sem estado ([DHCPv6 stateless])*

	"Aqui estão as minhas informações, mas você precisa obter outras informações, como endereços DNS, de um servidor DHCPv6 sem estado".

- [Método 3]: *DHCPv6 com estado - DHCPv6 stateful (sem SLAAC)*

	“Posso dar-lhe o seu endereço de gateway padrão. Você precisa pedir a um servidor DHCPv6 com estado todas as suas outras informações.”

---
### Método 1: SLAAC


*SLAAC* é um método que permite que [um dispositivo crie seu próprio GUA sem os serviços do DHCPv6]. *Com SLAAC, os dispositivos dependem das mensagens ICMPv6 de RA (Anúncio de Roteador) do roteador local para obter as informações necessárias.

Por padrão, a mensagem de RA sugere que o dispositivo de recebimento use as informações dessa mensagem para criar seu próprio endereço IPv6 unicast global e para todas as demais informações. *Os serviços de um servidor DHCPv6 não são obrigatórios.

*SLAAC é stateless*, o que significa que não existe servidor central (por exemplo, um servidor DHCPv6 stateful) alocando endereços unicast globais e mantendo uma lista de dispositivos e seus endereços. 

Com SLAAC, o dispositivo cliente usa as informações da mensagem de RA para criar seu próprio endereço unicast global. As duas partes do endereço são criadas da seguinte forma:

- [Prefixo] - Isso é anunciado na mensagem RA.
- [ID da Interface] - Isso usa o processo EUI-64 ou gera um número aleatório de 64 bits, dependendo do sistema operacional do dispositivo.

---
### Método 2: SLAAC and DHCPv6 stateless


Uma interface de roteador pode ser configurada para enviar um anúncio de roteador (RA) usando SLAAC e DHCPv6 stateless.

Com esse método, a mensagem RA sugere que os dispositivos usem o seguinte:

- SLAAC para criar seu próprio IPv6 GUA;
- O LLA do roteador, que é o endereço IPv6 de origem RA, como o endereço de gateway padrão;
- Um servidor DHCPv6 sem estado (stateless) para obter outras informações como o endereço de um servidor DNS e um nome de domínio.


> [!NOTE]
> Um servidor DHCPv6 sem estado distribui endereços do servidor DNS e nomes de domínio. Não atribui GUAs.

---
### Método 3: DHCPv6 stateful


Uma interface de roteador pode ser configurada para enviar um RA usando apenas DHCPv6 com estado.

O DHCPv6 stateful é semelhante ao DHCP para IPv4. Um dispositivo pode receber automaticamente suas informações de endereçamento, incluindo uma GUA, tamanho do prefixo e os endereços dos servidores DNS de um servidor DHCPv6 com monitoração de estado.

Com esse método, a mensagem RA sugere que os dispositivos usam o seguinte:

- O LLA do roteador, que é o endereço IPv6 de origem RA, como o endereço de gateway padrão;
- Um servidor DHCPv6 stateful para obter o endereço unicast global, o endereço do servidor DNS, o nome do domínio e todas as demais informações.

> Um servidor DHCPv6 com estado aloca e mantém uma lista dos dispositivos que recebem endereços IPv6. DHCP para IPv4 é stateful.


> [!NOTE]
> O endereço de gateway padrão só pode ser obtido dinamicamente da mensagem de RA. O servidor DHCPv6 sem estado ou com estado não fornece o endereço de gateway padrão.

---
### Processo EUI-64 ou Gerado Aleatoriamente

Quando a mensagem de RA é SLAAC ou SLAAC com DHCPv6 sem estado, o cliente deve gerar sua própria ID da interface. O cliente conhece a parte de prefixo do endereço da mensagem de RA, mas deve criar sua própria ID da interface. 

*A ID da interface pode ser criada por meio do processo EUI-64 ou de um número de 64 bits gerado aleatoriamente.

---
### Processo EUI-64

A IEEE definiu o identificador exclusivo estendido (EUI - Extended Unique Identificator) ou processo EUI-64 modificado. Esse processo usa o endereço MAC Ethernet de 48 bits de um cliente e insere outros 16 bits no meio do endereço MAC de 48 bits para criar uma ID da interface de 64 bits.

Geralmente representados em hexadecimal, os endereços MAC de Ethernet são compostos de duas partes:

- [Organizationally unique identifier (OUI)]:

	O OUI é um código de fornecedor de 24 bits (6 dígitos hexadecimais) designado pelo IEEE.

- [Identificador de dispositivo]:

	O identificador do dispositivo é um valor exclusivo de 24 bits (6 dígitos hexadecimais) com um OUI em comum.


Um ID de interface EUI-64 é representado em binário e composto por três partes:

- OUI de 24 bits do endereço MAC do cliente, mas o sétimo bit (o bit universal/local (U/L)) é invertido. Isso significa que, se o sétimo bit for 0, ele se tornará 1, e vice-versa;

- O valor de 16 bits fffe (em hexadecimal) inserido;

- Identificador do dispositivo de 24 bits do endereço MAC do cliente.


![[processo_eui.64.png]]

- [Etapa 1]: Divida o endereço MAC entre o OUI e o identificador do dispositivo.

- [Etapa 2]: Insira o valor hexadecimal FFFE, o qual em binário: 1111 1111 1111 1110.

- [Etapa 3]: Converta os primeiros 2 valores hexadecimais do OUI em binário e inicie o bit de U/L (7 bits). Neste exemplo, o 0 do bit 7 é alterado para 1.

O resultado é um ID de interface gerado pela EUI-64 de fe99: 47ff: fe75: cee0.

> O uso do bit de U/L e os motivos para reverter o valor são discutidos em RFC 5342.


A vantagem do EUI-64 é o endereço MAC Ethernet que pode ser usado para determinar a ID da interface. Ele também permite que os administradores de rede rastreiem facilmente um endereço IPv6 para um dispositivo final usando o endereço MAC exclusivo. 

*No entanto, isso causou preocupações de privacidade entre muitos usuários que se preocupavam que seus pacotes pudessem ser rastreados para o computador físico real. 

Devido a essas preocupações, poderá ser utilizada uma ID da interface gerada de forma aleatória.

---
### Ds da Interface Geradas Aleatoriamente

Dependendo do sistema operacional, um dispositivo pode usar uma ID da interface gerada de forma aleatória em vez de usar o endereço MAC e o processo EUI-64. 

Por exemplo, do Windows Vista em diante, o Windows usa uma ID da interface gerada de forma aleatória em vez de uma criada com o EUI-64. O Windows XP e os sistemas operacionais Windows anteriores usavam o EUI-64.

Depois que a ID da interface for estabelecida, seja pelo processo de EUI-64 ou por geração aleatória, ela poderá ser combinada a um prefixo IPv6 da mensagem de RA para criar um endereço unicast global.

> [!NOTE]
> Para garantir a exclusividade de qualquer endereço IPv6 unicast, o cliente pode usar um processo conhecido como detecção de endereço duplicado (DAD). Isso equivale a uma solicitação ARP para seu próprio endereço. Se não houver resposta, significa que o endereço é exclusivo.

