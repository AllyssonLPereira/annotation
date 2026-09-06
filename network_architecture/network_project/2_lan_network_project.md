---
tags:
  - arquivo
---
## Cisco Three-Tier Network Design Model

O tráfego IP é gerenciado de acordo com as características e os dispositivos associados a cada uma das três camadas do modelo de design hierárquico na rede: acesso, distribuição e núcleo.

#### Access Layer

A camada de acesso provê *`Network Admission Control`* — *`NAC`*. *`NAC`* é um recurso da Cisco que previne hosts de acessarem a rede se elas não estiverem de acordo com os requerimentos da organização, como a atualização de arquivo de definição de antivírus.

O criador de perfil *`NAC`* automatiza o *`NAC`* descobrindo e inventariando automaticamente os dispositivos conectados à LAN.

Por ela fornecer acesso à rede, ela é o lugar ideal para executar *autenticação de usuários* e *segurança de porta*.

A *`Access Layer`* fornece um ponto de conexão à rede para dispositivos de usuário final e permite que vários hosts se conectem a outros hosts por um dispositivo de rede, geralmente um *switch* ou um *access point*. 

Normalmente, todos os dispositivos dentro de uma única *`Access Layer`* terão a mesma porção de rede do endereço IP.

Se uma mensagem é destinada a um host local, com base na porção de rede do endereço IP, a mensagem permanece local. Caso ela seja destinada a uma rede diferente, será passada para a *`Distribution Layer`*. 

Os switches fornecem a conexão para os dispositivos da *`Distribution Layer`*, geralmente um dispositivo layer 3 tal como um roteador ou um switch layer 3.

Essa camada fornece/garante:

- *Authentication and Access Control*:

	A *`Access Layer`* implementa mecanismos para garantir que apenas dispositivos autorizados possam se conectar à rede. Isso pode incluir autenticação via protocolos como 802.1X, onde dispositivos precisam fornecer credenciais antes de serem permitidos na rede.

- *Traffic Segmentation*:

	Switches na *`Access Layer`* segmentam o tráfego dentro da rede local, permitindo que os dados sejam enviados apenas aos dispositivos relevantes. Isso reduz a quantidade de tráfego desnecessário e melhora a eficiência da comunicação.

- *Local Traffic Management:*

	A *`Access Layer`* também gerencia o tráfego local entre dispositivos conectados à mesma rede. Isso inclui a utilização de técnicas, como VLANs para separar diferentes tipos de tráfego e melhorar a segurança e o desempenho.

#### Distribution Layer

A *`Distribution Layer`*, que às vezes é chamada de *`Aggregation layer`*, prove *filtragem de rota* entre roteamento de VLAN. 

O gerenciamento de ACLs e filtragem de IPS são tipicamente implementados na *`Distribution Layer`*.

Por essa camada ser a intermediaria entre a *`Access Layer`* e a *`Core Layer`*, ela se torna o lugar ideal para aplicar *políticas de segurança* e para realizar tarefas que envolve a *manipulação de pacotes*, tais como roteamento, sumarização e redundância do próximo salto.

A *`Distribution Layer`* fornece um ponto de conexão para redes separadas e controla o fluxo de informações entre as redes. Normalmente, ela contém switches mais eficientes do que a *`Access Layer`*, além de roteadores para fazer o roteamento entre redes. 

Os dispositivos da *`Distribution Layer`* controlam o tipo e a quantidade de tráfego que flui da camada de acesso para a camada do núcleo.

#### Core Layer

A *`Core Layer`* prove um caminho de comutação super rápido na rede. Ela é a espinha dorsal da rede — backbone, ou seja, lugar onde mais haverá tráfego. Ela está associada com *baixa latência* e *alta confiabilidade*.

Os dispositivos da *`Core Layer`* normalmente incluem roteadores e switches de alta velocidade e muito eficientes, tais como um Cisco Catalyst 9600. O objetivo principal da *`Core Layer`* é transportar dados rapidamente.


![[cisco_three-tier_network_design_model.png]]
*Fonte: Cisco*

![[cisco_three-tier_network_design_model(1).png]]
*Fonte: Cisco*

---
## Cisco Two-Tier Network Design Model

*O projeto hierárquico de três camadas maximiza o desempenho, a disponibilidade da rede e a
capacidade de escalar o projeto de rede. 

A maioria dos campi de pequenas empresas não cresce significativamente ao longo do tempo, e *a maioria dos campi de pequenas empresas é pequena o suficiente para ser bem atendida por um projeto hierárquico de duas camadas*, onde as camadas de núcleo e distribuição são
colapsadas em uma única camada. 

A principal motivação para o projeto de núcleo colapsado é reduzir o custo da rede, mantendo a maioria dos benefícios do modelo hierárquico de três camadas.

A implantação de uma rede de núcleo colapsada resulta na implementação das funções da camada de distribuição e da camada de núcleo em um único dispositivo. 

O núcleo/dispositivo de distribuição colapsado deve fornecer o seguinte:

• Caminhos físicos e lógicos de alta velocidade que se conectam à rede;
• Ponto de agregação e demarcação da Camada 2;
• Definir políticas de roteamento e acesso à rede;
• Serviços de rede inteligentes — QoS, virtualização de rede, etc.

> *Observação*: se o site principal ou um campus remoto tiver vários prédios e houver previsão de crescimento ao longo do tempo, implementar o modelo hierárquico de três camadas é uma escolha melhor.

![[cisco_two-tier_network_model.png]]