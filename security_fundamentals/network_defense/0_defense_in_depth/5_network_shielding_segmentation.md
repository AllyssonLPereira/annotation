---
tags:
  - arquivo
---
## Virtual Local Area Networks — VLANs

As VLANs fornecem uma forma de agrupar dispositivos em uma LAN e em switches individuais. VLANs não são iguais a LANs: LANs virtuais são baseadas em conexões lógicas, enquanto LANs são baseadas em conexões físicas. 

Portas individuais de um switch podem ser atribuídas a uma VLAN específica. Outras portas podem ser usadas para interconectar fisicamente os switches e permitir o tráfego de várias VLANs entre os switches. Essas portas são chamadas *`Trunks`* — troncos.

![[vlan.png]]

Os administradores usam VLANs para segmentar redes com base em fatores como função, equipe ou aplicativo. Os dispositivos em uma VLAN atuam como se estivessem em sua própria rede independente, mesmo que compartilhem uma infraestrutura comum com outras VLANs.

Uma VLAN pode separar grupos que têm dados confidenciais do resto da rede, diminuindo as chances de violações de informações confidenciais. *`Trunks`* permitem que indivíduos na VLAN do RH estejam conectados fisicamente a vários switches diferentes.

As VLANs oferecem uma maneira de limitar o tráfego de transmissão em uma rede comutada. Os hackers podem atacar também a disponibilidade e o desempenho da VLAN. Para proteger a VLAN, monitorar seu desempenho, usar configurações avançadas e instalar regularmente patches e atualizações.

Redes locais virtuais (VLANs) permitem que administradores de rede utilizem switches para criar segmentos de LAN baseados em software, que podem segregar ou consolidar o tráfego entre várias portas de switch. Dispositivos que compartilham uma VLAN se comunicam por meio de switches como se estivessem na mesma rede de Camada 2. 

A imagem abaixo mostra diferentes VLANs — vermelha, verde e azul — conectando conjuntos separados de porções, enquanto compartilham o mesmo segmento de rede composto pelos dois switches e suas conexões. 

![[vlan 1.png]]

Como as VLANs atuam como redes discretas, as comunicações entre VLANs devem ser habilitadas. O tráfego de broadcast é limitado à VLAN, reduzindo o congestionamento e a eficácia de alguns ataques.

A administração do ambiente é simplificada, pois as VLANs podem ser reconfiguradas quando os indivíduos mudam de localização física ou precisam de acesso a diferentes serviços. 

As VLANs podem ser configuradas com base na porta do switch, sub-rede IP, endereço MAC e protocolos. As VLANs não garantem a segurança de uma rede. À primeira vista, pode parecer que o tráfego não pode ser interceptado porque a comunicação dentro de uma VLAN é restrita aos dispositivos membros. 

No entanto, existem ataques que permitem que um usuário mal-intencionado veja o tráfego de outras VLANs (o chamado "salto de VLAN"). A tecnologia VLAN é apenas uma ferramenta que pode melhorar a segurança geral do ambiente de rede.

---
## Demilitarized Zone — DMZ

Uma zona desmilitarizada — *`DMZ`* — é uma pequena rede entre uma rede privada confiável e a Internet. Elas são uma parte da rede que *interage diretamente com o mundo externo* e *tem mais controles e restrições de segurança* do que seu ambiente de TI mais amplo.

![[demilitarized_zone.png]]


- *Acesso a redes não confiáveis*

	Os servidores Web e de correio geralmente são colocados na DMZ para permitir que os usuários acessem uma rede não confiável, como a Internet, sem comprometer a rede interna.

- *Zonas de risco*

	A maioria das redes tem de duas a quatro zonas de risco: a LAN privada confiável, a DMZ, a Internet e uma extranet.

	- Na zona de LAN, o nível de risco é baixo e o nível de confiança é alto. 
	- Na zona da extranet, o nível de risco é médio-baixo e o nível de confiança médio-alto.
	- Na DMZ, o nível de risco é médio-alto e o nível de confiança é médio-baixo.
	- Na zona da Internet, o nível de risco é alto e o nível de confiança é baixo. 

- *Modelo `zero-trust`*

	Os firewalls gerenciam o tráfego de ponta a ponta (tráfego que vai entre os servidores no data center da empresa) e o tráfego de ponta a ponta (dados que entram e saem da rede da empresa).

	Para proteger sua rede, uma empresa pode implementar um modelo de confiança zero. Confiar em usuários e endpoints automaticamente na empresa pode colocar qualquer rede em risco, já que usuários confiáveis podem se mover por toda a rede para acessar dados. A rede *`Zero Trust`* monitora constantemente todos os usuários na rede, independentemente de status ou função.

---
## Microsegmentation

A microssegmentação divide uma rede em seções pequenas e distintas, cada uma das quais tem suas próprias políticas de segurança e é acessada separadamente. O objetivo da microssegmentação é aumentar a segurança da rede confinando as ameaças e as violações ao segmento comprometido, sem afetar o resto da rede.

Os conjuntos de ferramentas dos atuais adversários são polimórficos por natureza e permitem que as ameaças contornem os controles de segurança estáticos.

Os ataques cibernéticos modernos aproveitam os modelos de segurança tradicionais para se moverem facilmente entre sistemas dentro de um data center. A *microssegmentação* auxilia na proteção contra essas ameaças.

> *Um requisito fundamental de design da microssegmentação é entender os `requisitos de proteção` para o tráfego dentro de um data center e o tráfego de e para os fluxos de tráfego da internet.*

A microssegmentação é um componente chave de uma arquitetura *`Zero Trust`* . Essa arquitetura pressupõe que qualquer tráfego entrando, saindo ou que esteja dentro de uma rede pode ser uma ameaça. A microssegmentação torna possível isolar essas ameaças antes que se espalhem, impedindo o *movimento lateral*.

A microssegmentação pode ocorrer em níveis extremamente granulares em uma rede, até o isolamento de *cargas de trabalho individuais* — ao contrário de isolar aplicações, dispositivos ou redes, com uma "carga de trabalho" sendo qualquer programa ou aplicação que utilize alguma quantidade de memória e CPU.

Em outras palavras, a microssegmentação permite restrições granulares dentro do ambiente de TI, a ponto de *regras poderem ser aplicadas a máquinas e/ou usuários individuais*, e essas regras podem ser tão detalhadas e complexas quanto desejado. Por exemplo, ele pode limitar quais endereços IP podem se comunicar com uma determinada máquina, em que horário do dia, com quais credenciais e quais serviços essas conexões podem usar.

A microssegmentação, portanto, permite que a organização limite quais funções, unidades, escritórios ou departamentos de negócios podem se comunicar com outros, para aplicar o conceito de *privilégio mínimo*.

#### How does microsegmentation work?

As técnicas de microssegmentação de uma rede variam ligeiramente. Mas alguns princípios-chave quase sempre se aplicam:

- *`Application layer visibility`*

	As soluções de microssegmentação estão cientes dos aplicativos que estão enviando tráfego na rede. A microssegmentação fornece o contexto no qual os aplicativos estão se comunicando e como o tráfego de rede flui entre eles.

	Esse é um dos aspectos que diferencia a microssegmentação da divisão de uma rede usando redes locais virtuais ou outro método de camada de rede.

- *`Software-based, not hardware-based`*

	A microssegmentação é configurada através de software. A segmentação é virtual, portanto os administradores não precisam ajustar roteadores, switches, ou outros equipamentos de rede a fim de implementá-la.

- *`Uses next-generation firewalls — NGFWs`*

	A maioria das soluções de microssegmentação usa firewalls de próxima geração para separar seus segmentos.

	Os NGFWs, ao contrário dos firewalls tradicionais, têm consciência do aplicativo, permitindo-lhes analisar o tráfego da rede na camada de aplicação, não apenas nas camadas de rede e transporte.

	Além disso, os firewalls baseados em nuvens podem ser usados para microssegmentar implantações de computação em nuvem. Alguns provedores de hospedagem em nuvem oferecem essa capacidade usando seus serviços de firewall integrados.

- *`Security policies differ between segments`*

	Os administradores podem personalizar as políticas de segurança para cada carga de trabalho, se quiserem. 

	Uma carga de trabalho pode permitir amplo acesso, enquanto outra pode ser altamente restrita, dependendo da importância da carga de trabalho em questão e dos dados que ela processa. 

	Uma carga de trabalho pode aceitar consultas de API a partir de uma gama de endpoints; outra pode se comunicar apenas com um servidor específico.

- *`Visibility into all network traffic`*

	O log de rede típico fornece informações da camada de rede e de transporte, como portas e endereços de IP. A microssegmentação também fornece contexto de aplicativos e carga de trabalho. 

	Ao monitorar todo o tráfego de rede e adicionar contexto de aplicativo, as organizações podem aplicar segmentação e políticas de segurança de forma consistente em suas redes. Isso também fornece as informações necessárias para ajustar as políticas de segurança conforme necessário.

---
## Conexão via VPN

Uma rede virtual privada (VPN) nos permite conectar a uma rede privada (interna) e acessar hosts e recursos como se estivéssemos conectados diretamente à rede privada de destino.

É um canal de comunicação seguro por meio de redes públicas compartilhadas para se conectar a uma rede privada (ou seja, um funcionário se conectando remotamente à rede corporativa de sua empresa a partir de sua casa).

As VPNs oferecem um certo grau de privacidade e segurança ao criptografar as comunicações pelo canal para impedir a espionagem e o acesso aos dados que passam pelo canal.

![[vpn.png]]

Em um nível mais amplo, *a VPN funciona roteando a conexão de internet do nosso dispositivo conectado por meio do servidor privado da VPN de destino, em vez do nosso provedor de serviços de internet (ISP)*.

Então, em vez de acessar as coisas pelo provedor, acessamos por um provedor VPN. O que muda é o COMO ACESSAMOS. 

Quando conectado a uma VPN, os dados se originam do servidor VPN em vez do nosso computador e parecem se originar de um endereço IP público diferente do nosso.

Existem dois tipos principais de VPNs de acesso remoto: `VPN baseada em cliente` e `VPN SSL`.

*A VPN SSL usa o navegador da web como cliente VPN*. A conexão é estabelecida entre o navegador e um gateway SSL VPN, que pode ser configurado para permitir acesso apenas a aplicativos baseados na web, como e-mails e sites de intranet, ou mesmo à rede interna, sem a necessidade de o usuário final instalar ou usar qualquer software especializado.

A VPN baseada em cliente requer o uso de um software cliente para estabelecer a conexão VPN. Uma vez conectado, o host do usuário funcionará basicamente como se estivesse conectado diretamente à rede da empresa e poderá acessar quaisquer recursos (aplicativos, hosts, sub-redes, etc.) permitidos pela configuração do servidor.

Algumas VPNs corporativas fornecerão aos funcionários acesso total à rede corporativa interna, enquanto outras colocarão os usuários em um segmento específico reservado para trabalhadores remotos.

---
## Por que usar uma VPN?

Podemos usar um serviço de VPN como `NordVPN` ou `Private Internet Access` e nos conectar a um servidor VPN em outra parte do nosso país ou região do mundo para *ocultar nosso tráfego de navegação ou disfarçar nosso endereço IP público*.

Isso pode nos proporcionar algum nível de segurança e privacidade. Ainda assim, como estamos nos conectando ao servidor de uma empresa, sempre existe a possibilidade de que dados estejam sendo registrados ou que o serviço de VPN não esteja seguindo as práticas recomendadas de segurança ou os recursos de segurança anunciados.

*Usar um serviço de VPN traz o risco de o provedor não estar fazendo o que promete e estar registrando todos os dados.

O uso de um serviço de VPN ***[NÃO GARANTE ANONIMATO OU PRIVACIDADE]***, *mas é útil para contornar certas restrições de rede/firewall ou quando conectado a uma possível rede hostil (por exemplo, uma rede sem fio pública de aeroporto)*.

Um serviço de VPN nunca deve ser usado com a ideia de que nos protegerá das consequências de atividades nefastas.

---

- Caixa de salto
- bastion host