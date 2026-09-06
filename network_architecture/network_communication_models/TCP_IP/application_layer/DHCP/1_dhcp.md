---
tags:
  - arquivo
---
##### Atribuição estática 

O administrador de rede deve configurar manualmente as informações da rede para um host. No mínimo, isso inclui o seguinte:

- **[Endereço IP]** – Identifica o computador na rede.
- **[Máscara de Sub-rede]** – Identifica a rede à qual o host está conectado
- **[Gateway padrão]** – Identifica o dispositivo de rede que o host usa para acessar a Internet ou outra rede remota.

Os endereços estáticos têm algumas vantagens:

- São úteis para impressoras, servidores e outros dispositivos de rede que precisam estar acessíveis para clientes na rede. 

- Se os hosts normalmente acessam um servidor em um determinado endereço IPv4, não seria bom que esse endereço mudasse.

Embora a atribuição estática de informações de endereçamento possa proporcionar um controle maior dos recursos de rede, a digitação de informações em cada host pode ficar demorada. Quando os endereços IPv4 são inseridos estaticamente, o host executa apenas verificações básicas de erro no endereço IPv4. Isso aumenta a probabilidade de que ocorram erros.

Ao usar endereçamento IPv4 estático, é importante manter uma lista precisa de quais endereços IPv4 estão atribuídos a quais dispositivos. Além disso, como são endereços permanentes, normalmente eles não são reutilizados.

---
##### Atribuição dinâmica

Nas redes locais, geralmente, a população de usuários muda com frequência. Novos usuários chegam com notebooks e precisam de uma conexão. Outros têm novas estações de trabalho que precisam ser conectadas. 

Em vez de fazer com que o administrador de rede atribua endereços IPv4 em cada estação de trabalho, é mais eficiente ter endereços IPv4 atribuídos automaticamente. Isso é feito com um protocolo conhecido como [Dynamic Host Configuration Protocol] (DHCP).

O DHCP fornece um mecanismo para atribuição automática de informações de endereçamento, como endereço IPv4, máscara de sub-rede, gateway padrão e outras informações de configuração.

O DHCP em geral é o método preferido de designação de endereços IPv4 para hosts em redes grandes porque reduz a carga sobre a equipe de suporte da rede e praticamente elimina erros de entrada.

Outro benefício do DHCP é que o endereço não é permanentemente atribuído a um host, mas é só “alugado” por um período. Se o host é desligado ou retirado da rede, o endereço retorna ao pool para ser reutilizado. Isso é especialmente útil com usuários móveis que vêm e vão em uma rede.

> [!NOTE] 
> O DHCP para IPv6 (DHCPv6) fornece serviços semelhantes para clientes IPv6. Uma diferença importante é que o DHCPv6 não fornece o endereço do gateway padrão. Isso só pode ser obtido dinamicamente a partir da mensagem Anúncio do roteador do roteador.

---
##### Período de concessão

O DHCP pode alocar endereços IP por um período de [tempo configurável], chamado [período de concessão]. 

O período de concessão é uma configuração DHCP importante, quando o período de concessão expira ou o servidor DHCP recebe uma mensagem DHCP RELEASE, o endereço é retornado ao pool DHCP para reutilização. 

Os usuários podem se mover livremente de um local para outro e restabelecer com facilidade conexões de rede com o DHCP.

---
##### Mensagens DHCP

Quando um dispositivo IPv4 configurado com DHCP inicia ou se conecta à rede, o cliente transmite uma mensagem de descoberta DHCP (DHCP DISCOVER) para identificar qualquer servidor DHCP disponível na rede. Um servidor DHCP responde com uma mensagem de oferta DHCP (DHCP OFFER), que oferece uma locação ao cliente. 

A mensagem de oferta contém o endereço IPv4 e a máscara de sub-rede a serem atribuídos, o endereço IPv4 do servidor DNS e o endereço IPv4 do gateway padrão. *A oferta de locação também inclui a duração da locação.

*O cliente pode receber várias mensagens DHCP OFFER, caso exista mais de um servidor DHCP na rede local*. Portanto, deve escolher entre eles e transmitir uma mensagem de requisição de DHCP (DHCP REQUEST) que identifique o servidor explícito e a oferta de locação que o cliente está aceitando. 

***Um cliente também pode decidir requisitar um endereço que já havia sido alocado pelo servidor.

Presumindo que o endereço IPv4 requisitado pelo cliente, ou oferecido pelo servidor, ainda seja válido, o servidor retornará uma mensagem de confirmação DHCP (DHCP ACK) que confirma para o cliente que a locação foi finalizada. 

Se a oferta não é mais válida, o servidor selecionado responde com uma mensagem de confirmação negativa DHCP (DHCP NAK). Se uma mensagem DHCP NAK for retornada, o processo de seleção deverá recomeçar com a transmissão de uma nova mensagem DHCP DISCOVER. 

Quando o cliente tiver a locação, ela deverá ser renovada por outra mensagem DHCP REQUEST antes do vencimento.


> [!NOTE] 
> O DHCPv6 possui um conjunto de mensagens semelhantes às do DHCPv4. As mensagens DHCPv6 são SOLICIT, ADVERTISE, INFORMATION REQUEST, e REPLY.


1) Um cliente inicia uma mensagem para encontrar um servidor DHCP (DHCP DISCOVER) - pacote broadcast (255.255.255.255) e mac (FF-FF-FF-FF-FF-FF)

2) Um servidor DHCP responde à solicitação inicial de um cliente (DHCP OFFER)

3) O cliente aceita o endereço IP fornecido pelo servidor DHCP (DHCP REQUEST)

4) O servidor DHCP confirma que a concessão de endereço foi aceita (DHCP ACK)
