---
tags:
  - arquivo
---
### Topologias Físicas e Lógicas

A camada de enlace de dados prepara os dados da rede para a camada física. Ela deve conhecer a topologia lógica de uma rede para poder determinar o que é necessário para transferir quadros de um dispositivo para outro.

A topologia de uma rede é a organização/ relacionamento dos dispositivos de rede e as interconexões entre eles.

Existem dois tipos de topologias usadas ao descrever redes LAN e WAN:

- **[Topologia física]:**

	***Identifica as conexões físicas e como os dispositivos finais e intermediários*** (ou seja, roteadores, switches e pontos de acesso sem fio) ***são interconectados***. 

	A topologia também pode incluir a localização específica do dispositivo, como o número do quarto e a localização no rack do equipamento. As topologias físicas são geralmente ponto a ponto ou estrela.

![[topologia_fisica.png]]

- **[Topologia lógica]:**

	Refere-se ao ***modo como uma rede transfere quadros de um nó para outro***. Esta topologia identifica conexões virtuais usando interfaces de dispositivo e esquemas de endereçamento IP da Camada 3.

	***Ela se concentra no fluxo de informações, inclusive no endereçamento***. Normalmente, os dispositivos do cliente não são incluídos, em vez disso, eles são representados usando um único switch Ethernet.

	*Isso ajuda a monitorar o tráfego de rede para performance e segurança, dimensionar e aprimorar a rede com dispositivos e recursos adicionais e, o mais importante, ajuda a resolver problemas mais rapidamente.

![[topologia_logica.png]]

"Em resumo, a topologia física é o "mapa" real da rede, enquanto a topologia lógica é o "mapa" do caminho que os dados percorrem dentro dessa rede" - *Perplexity*.

A camada de enlace de dados “vê” a topologia lógica da rede quando controla o acesso de dados ao meio físico. É a topologia lógica que influencia o tipo de enquadramento de rede e o controle de acesso ao meio usado.

---
### Topologias WAN


- **[Ponto a Ponto]:**

Esta é a topologia WAN mais simples e comum. Consiste em uma ligação permanente entre dois pontos finais.

Nessa organização, dois nós não têm de compartilhar o meio físico com outros hosts. 

Além disso, ao usar um [protocolo de comunicação serial como o protocolo ponto a ponto] (PPP), um nó não precisa determinar se um quadro de entrada é destinado a ele ou a outro nó. 

Portanto, os protocolos de enlace de dados podem ser muito simples, assim como todos os quadros no meio físico podem trafegar apenas para os dois nós ou a partir deles. 

> [!NOTE] Importante frisar!
> Uma conexão ponto a ponto via Ethernet não requer que o dispositivo determine se o quadro de entrada está destinado a esse nó.

Um nó de origem e destino pode ser indiretamente conectado entre si por alguma distância geográfica, usando vários dispositivos intermediários. No entanto, o uso de dispositivos físicos na rede não afeta a topologia lógica. ***Adicionar conexões físicas intermediárias pode não alterar a topologia lógica.


- **[Hub and spoke]**

Esta é uma [versão WAN da topologia em estrela] na qual um site central interconecta sites de filial através do uso de links ponto a ponto. Os sites de filiais não podem trocar dados com outros sites de filiais sem passar pelo site central.


- **[Malha]**

Essa topologia fornece [alta disponibilidade], mas requer que todos os sistemas finais estejam interconectados a todos os outros sistemas. Portanto, [os custos administrativos e físicos podem ser significativos]. Cada link é essencialmente um link ponto a ponto para outro nó.


- **[Híbrido]**

Um híbrido é uma [variação ou combinação de qualquer topologia]. Por exemplo, uma malha parcial é uma topologia híbrida em que alguns dispositivos finais, mas não todos, são interconectados.

---
### Topologia LAN


Em LANs multiacesso, os dispositivos finais (isto é, nós) são interligados usando topologias [estrela] ou [estrela estendida]. 

Na topologia [estrela], os dispositivos finais são conectados a um dispositivo intermediário central, neste caso, um switch Ethernet. Já a topologia **[estrela estendida]** interconecta vários switches Ethernet. 

As topologias em estrela e estendidas são fáceis de instalar, muito escalonáveis (fáceis de adicionar e remover dispositivos finais) e fáceis de solucionar problemas. *As primeiras topologias em estrela interconectavam dispositivos finais usando hubs Ethernet.

Às vezes, pode haver apenas dois dispositivos conectados na LAN Ethernet. Um exemplo são dois roteadores interconectados. Este seria um exemplo de Ethernet usado em uma topologia ponto a ponto.

**[Topologias LAN legadas]**

As primeiras tecnologias Ethernet e Token Ring LAN legadas incluíam dois outros tipos de topologias:

- **[Barramento]**

	Todos os sistemas finais são encadeados entre si e terminados de alguma forma em cada extremidade. Os dispositivos de infraestrutura, como switches, não são necessários para interconectar os dispositivos finais. 

	As redes Ethernet herdadas costumavam ser topologias de barramento usando cabos coaxiais, porque era barato e fácil de configurar.


- **[Anel]**

	Os sistemas finais são conectados ao seu respectivo vizinho formando um anel. O anel não precisa ser terminado, ao contrário da topologia de barramento. As redes de interface de dados distribuídos de fibra herdada (FDDI) e Token Ring usavam topologias em anel.
