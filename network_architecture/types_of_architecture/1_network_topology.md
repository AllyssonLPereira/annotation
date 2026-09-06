---
tags:
  - arquivo
---
## Half and Full Duplex Communication

Compreender a comunicação duplex é importante ao discutir topologias de LAN porque esta se refere à direção da transmissão de dados entre dois dispositivos. Existem dois modos comuns de duplex.

- *`Half duplex communication`*

	Ambos os dispositivos podem transmitir e receber no meio físico, mas não podem fazer isso simultaneamente. WLANs e topologias de barramento herdadas com hubs Ethernet usam o modo meio duplex.

	O meio duplex permite que apenas um dispositivo envie ou receba por vez na mídia compartilhada. 


- *`Full duplex communication`*

	Ambos os dispositivos podem transmitir e receber simultaneamente na mídia compartilhada. A camada de enlace de dados supõe que o meio físico está disponível para transmissão para ambos os nós a qualquer momento.

	Os comutadores Ethernet (switches) operam no modo duplex completo por padrão, mas podem operar no modo meio duplex se estiverem conectados a um dispositivo como um hub Ethernet.

*É importante que as duas interfaces interconectadas, como uma NIC de host e uma interface em um comutador Ethernet, operem usando o mesmo modo duplex. Caso contrário, haverá uma incompatibilidade de duplex que criará ineficiência e latência no link.

---
## Access control methods

LANs Ethernet e WLANs são exemplos de redes multiacesso. *Uma rede multiacesso é uma rede que pode ter dois ou mais dispositivos finais tentando acessar a rede simultaneamente.

Algumas redes multiacesso requerem regras para controlar como os dispositivos compartilham a mídia física. Existem dois métodos básicos de controle de acesso para meio físico compartilhado.

- *Contention-based access*:

	Em redes multiacesso baseadas em contenção, todos os nós estão operando em half duplex, competindo pelo uso do meio. No entanto, apenas um dispositivo pode enviar por vez. 

	Portanto, há um processo se mais de um dispositivo transmitir ao mesmo tempo. Exemplos de métodos de acesso baseados em contenção incluem o seguinte:

	- Acesso múltiplo com detecção de colisão — CSMA/CD — usado em LANs Ethernet de topologia de barramento herdada;
	
	- Acesso múltiplo por operadora com prevenção de colisão — CSMA/CA — usado em LANs sem fio.

- *Controlled access*

	Em uma rede multiacesso controlada, cada nó tem seu próprio tempo para usar o meio. Esses tipos determinísticos de redes herdadas são ineficientes porque um dispositivo deve aguardar sua vez para acessar o meio.

	Exemplos de redes multiacesso que usam acesso controlado incluem o seguinte:

	- Token Ring legada;
	- ARCNET legada.

> [!NOTE]
> Atualmente, as redes Ethernet operam em duplex completo e não exigem um método de acesso.

---
## Acesso baseado em contenção — CSMA/CD

Exemplos de redes de acesso baseadas em contenção incluem o seguinte:

- LAN sem fio;
- LAN Ethernet de topologia de barramento legado;
- LAN Ethernet herdada usando um hub.

Essas redes operam no modo half duplex, o que significa que apenas um dispositivo pode enviar ou receber de cada vez. ***Isso requer um processo que determine quando um dispositivo pode enviar e o que acontece quando vários dispositivos enviam ao mesmo tempo.

Se dois dispositivos transmitirem simultaneamente, ocorre uma colisão. Para LANs Ethernet herdadas, ambos os dispositivos detectam a colisão na rede. Esta é a parte de detecção de colisão — CD — do CSMA/CD. 

A NIC compara os dados transmitidos com os dados recebidos ou reconhecendo que a amplitude do sinal é maior que o normal na mídia. Os dados enviados por ambos os dispositivos serão corrompidos e precisarão ser reenviados.

- Por exemplo:

	O PC1 tem um quadro Ethernet para enviar ao PC3. A placa de rede PC1 precisa determinar se algum dispositivo está transmitindo na mídia. 

	Se ele não detectar um sinal de operadora (em outras palavras, não estiver recebendo transmissões de outro dispositivo), ele assumirá que a rede está disponível para envio.

	O hub Ethernet recebe e envia o quadro. Um hub Ethernet também é conhecido como repetidor multiporta. Quaisquer bits recebidos em uma porta de entrada são regenerados e enviados para todas as outras portas.

	Se outro dispositivo, como o PC2, quiser transmitir, mas estiver recebendo um quadro no momento, deverá aguardar até que o canal esteja limpo.

	Todos os outros dispositivos conectados ao hub receberão o quadro. No entanto, como o quadro possui um endereço de link de dados de destino para PC3, somente esse dispositivo aceitará e copiará o quadro inteiro. Todas as outras NICs do dispositivo ignoram o quadro.

---
## Acesso Baseado em Contenção – CSMA/CA

Outra forma de CSMA usada pelas WLANs IEEE 802.11 é o acesso múltiplo por detecção de portadora/prevenção de colisão — CSMA/CA.

O CMSA/CA usa um método semelhante ao CSMA/CD para detectar se a mídia está livre, mas com umas técnicas adicionais. 

Em ambientes sem fio pode não ser possível para um dispositivo detectar uma colisão. 

O CMSA/CA não detecta colisões, mas tenta evitá-las esperando antes de transmitir. Cada dispositivo que transmite inclui o tempo necessário para a transmissão. Todos os outros dispositivos sem fio recebem essas informações e sabem quanto tempo a mídia ficará indisponível.

Depois que um dispositivo sem fio enviar um quadro 802.11, o receptor retornará uma confirmação para que o remetente saiba que o quadro chegou.

Quer se trate de uma LAN Ethernet que use hubs, ou uma WLAN, os sistemas baseados em contenção não escalam bem sob uso intenso.

> [!NOTE]
> As LANs Ethernet que usam switches não utilizam um sistema baseado em contenção porque o switch e a NIC do host operam no modo duplex completo.
> 

---
### Alcance da rede


- PAN:

	Uma rede de área pessoal (PAN) conecta dispositivos (como mouses, teclados, impressoras, smartphone e tablets) que ***se encontram dentro do alcance de um indivíduo***. Esses dispositivos são, geralmente, conectados com a tecnologia Bluetooth.

- LAN:

	Tradicionalmente, uma rede de área local (LAN) é definida como uma rede que conecta dispositivos usando cabos com fio em uma área geográfica pequena. 

	Entretanto, a característica que distingue as LANs hoje em dia é que normalmente elas são usadas por um indivíduo (em casa ou em uma empresa pequena) ou completamente gerenciadas por um departamento de TI, como em uma escola ou uma corporação.

- VLAN:

	As LANs virtuais (VLANs) permitem que um administrador segmente as portas em um único switch, como se fossem vários switches. Isso proporciona um encaminhamento mais eficiente de dados, isolando o tráfego para apenas essas portas, onde é necessário. 

	As VLANs também permitem que os dispositivos finais sejam agrupados em conjunto para fins administrativos.

- WLAN:

	Uma LAN sem fio (WLAN) é semelhante a uma LAN, mas conecta, via conexão sem fio, usuários e dispositivos em uma área geográfica pequena, ao invés de usar uma conexão com fio.

- WMN:

	Uma rede de malha sem fio (WMN) usa vários pontos de acesso para estender a WLAN.

- CAN:

	Uma rede de área de campus (CAN) é um grupo de LANs interconectadas, pertencentes à mesma organização e operando em uma área geográfica limitada. Estes podem ser campi acadêmicos e campi empresariais ou corporativos. 

	As redes da área do campus geralmente consistem em vários prédios interconectados por links Ethernet de alta velocidade usando cabeamento de fibra óptica.

- MAN:

	Uma rede de área metropolitana (MAN) é uma rede que abrange uma cidade ou um grande campus. A rede consiste em vários prédios interconectados por backbones de fibra ótica ou sem fio.

- WAN:

	Uma rede de longa distância (WAN) conecta várias redes que estão em locais separados geograficamente. Indivíduos e empresas contratam serviços de WAN. Seu provedor de serviços para sua casa ou dispositivo móvel conecta você à rede de longa distância, Internet.

- VPN:

	Uma rede privada virtual (VPN) é usada para se conectar com segurança a outra rede usando uma rede não segura, como a Internet. 

	O tipo mais comum de VPN é usado pelos trabalhadores remotos para acessar uma rede privada corporativa. 

	Colegas de trabalho são usuários de rede que são externos ou remotos.
