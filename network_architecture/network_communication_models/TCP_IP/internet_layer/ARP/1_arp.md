---
tags:
  - arquivo
---
##### O que é ARP?

O Protocolo de Resolução de Endereços (Address Resolution Protocol - ARP) é usado para determinar o endereço MAC de um dispositivo com um endereço IPv4 de destino conhecido. 

---
##### Solicitação ARP

Uma solicitação ARP é enviada quando um dispositivo precisa determinar o endereço MAC associado a um endereço IPv4 e não possui uma entrada para o endereço IPv4 em sua tabela ARP.

As mensagens do ARP são encapsuladas diretamente em um quadro Ethernet. Não há cabeçalho IPv4. A requisição ARP é encapsulada em um quadro Ethernet usando as seguintes informações de cabeçalho:

- **[Endereço MAC de destino]** – Este é um endereço de broadcast FF-FF-FF-FF-FF-FF que requer todos os NICs Ethernet na LAN para aceitar e processar a solicitação ARP.

- **[Endereço MAC de origem]** - Este é o endereço MAC do remetente da solicitação ARP.

- **[Tipo]** - As mensagens ARP têm um campo de tipo de 0x806. Ele informa à NIC de recebimento que a parte de dados do quadro precisa ser transferida para o processo ARP.

Como as solicitações de ARP são transmissões, elas são inundadas em todas as portas pelo switch, exceto a porta de recebimento. Todas as NICs Ethernet no processo de LAN devem entregar a solicitação ARP ao seu sistema operacional para processamento. 

Cada dispositivo deve processar a requisição ARP para ver se o endereço IPv4 destino corresponde ao seu. *Um roteador não encaminhará broadcasts pelas outras interfaces.

Somente um dispositivo na LAN terá um endereço IPv4 correspondente ao endereço IPv4 na requisição ARP. Nenhum outro dispositivo responderá.

---
##### Respostas ARP

Somente o dispositivo com o endereço IPv4 de destino associado à solicitação ARP responderá com uma resposta ARP. A resposta de ARP é encapsulada em um quadro Ethernet com as seguintes informações de cabeçalho:

- **[Endereço MAC de destino]** - Este é o endereço MAC do remetente da solicitação ARP.

- **[Endereço MAC de origem]** - Este é o endereço MAC do remetente da resposta ARP.

- **[Tipo]** - As mensagens ARP têm um campo de tipo de 0x806. Ele informa à NIC de recebimento que a parte de dados do quadro precisa ser transferida para o processo ARP.

Apenas o dispositivo que enviou originalmente uma requisição ARP receberá a resposta ARP unicast. Depois que a resposta do ARP é recebida, o dispositivo adiciona o endereço IPv4 e o endereço MAC correspondente à sua tabela ARP. 

Agora os pacotes destinados a esse endereço IPv4 podem ser encapsulados em quadros com o endereço MAC correspondente. Se nenhum dispositivo responder à requisição ARP, o pacote será descartado porque não será possível criar um quadro.

As entradas na tabela ARP têm carimbo de data/hora (timestamp). Se um dispositivo não receber um quadro de um dispositivo específico antes que o carimbo de data/hora expire, a entrada desse dispositivo será removida da tabela ARP.

Além disso, entradas de mapa estáticas podem ser inseridas em uma tabela ARP, mas isso é raro. As entradas estáticas na tabela ARP não expiram com o tempo e devem ser removidas manualmente.

> [!NOTE]
> O IPv6 usa um processo semelhante ao ARP para IPv4, conhecido como ICMPv6 Neighbour Discovery (ND). O IPv6 usa mensagens de requisição e de anúncio de vizinho, semelhantes a solicitações ARP e respostas ARP no IPv4.

---
##### Detalhes

Quando um pacote é enviado à camada de enlace de dados para ser encapsulado em um quadro Ethernet, o dispositivo consulta uma tabela em sua memória para encontrar o endereço MAC que é mapeado para o endereço IPv4. 

Esta tabela é armazenada temporariamente na memória RAM e denominada [tabela ARP] ou [cache ARP].

O dispositivo emissor pesquisará em sua tabela ARP um endereço IPv4 destino correspondente a um endereço MAC.

- Se o endereço IPv4 destino do pacote estiver na mesma rede que o endereço IPv4 origem, o dispositivo pesquisará o endereço IPv4 destino na tabela ARP.

- Se o endereço IPv4 destino do pacote estiver em uma rede diferente do endereço IPv4 origem, o dispositivo pesquisará o endereço IPv4 do gateway padrão na tabela ARP.


> [!NOTE]
> Quando um host cria um pacote para um destino, ele compara o endereço IPv4 destino e seu próprio endereço IPv4 para determinar se os dois endereços IPv4 estão localizados na mesma rede de Camada 3.

Nos dois casos, a pesquisa é por um endereço IPv4 e um endereço MAC correspondente para o dispositivo.

Cada entrada (linha) da tabela ARP vincula um endereço IPv4 a um endereço MAC. Chamamos a relação entre os dois valores de um mapa. Isso significa simplesmente que você pode localizar um endereço IPv4 na tabela e descobrir o endereço MAC correspondente. 

A tabela ARP salva (armazena em cache) temporariamente o mapeamento dos dispositivos da LAN.

---
##### Remoção de Entradas de uma Tabela ARP

Em cada dispositivo, um temporizador da cache ARP remove entradas ARP que não tenham sido usadas durante um determinado período. 

Os horários diferem dependendo do sistema operacional do dispositivo. Por exemplo, os sistemas operacionais Windows mais recentes armazenam entradas da tabela ARP entre 15 e 45 segundos

---
##### Segurança

Em alguns casos, o uso do ARP pode levar a um [risco potencial à segurança]. Um ator de ameaça pode usar [falsificação ARP para realizar um ataque de envenenamento por ARP]. 

Esta é uma técnica usada por um ator de ameaça para responder a uma solicitação ARP de um endereço IPv4 que pertence a outro dispositivo, como o gateway padrão.

O agente da ameaça envia uma resposta ARP com seu próprio endereço MAC. O destinatário da resposta ARP adicionará o endereço MAC errado à sua tabela ARP e enviará esses pacotes ao agente de ameaça.  

***Switches de nível corporativo incluem técnicas de mitigação conhecidas como inspeção dinâmica ARP (DAI).
