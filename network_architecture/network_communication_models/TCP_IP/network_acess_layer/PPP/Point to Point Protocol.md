
### O que é o PPP?

O protocolos **PPP (Point-to-Point Protocol)**, ou **Protocolo Ponto a Ponto**, é um **protocolo da camada de enlace** (camada 2 do modelo OSI) usado para estabelecer uma conexão direta entre **dois dispositivos**.

Ele é muito usado em conexões de **redes metropolitanas e de longa distância (WAN)**, como ligações via linhas telefônicas, links seriais entre roteadores, conexões DSL e até em algumas tecnologias de banda larga.

***

### Por que o PPP foi criado?

Antes do PPP, existiam protocolos como o **SLIP (Serial Line Internet Protocol)**, que eram muito básicos e tinham limitações sérias, por exemplo:

- Não tinham **autenticação**;
- Não negociavam parâmetros de forma dinâmica;
- Não detectavam erros de ligação de forma eficiente;
- Não suportavam bem múltiplos protocolos de rede ao mesmo tempo.

Sendo assim, o PPP foi desenvolvido para superar essas limitações, oferecendo:

1. **Autenticação de identidade**;
2. **Transmissão confiável** (detecção de erros e controle de qualidade).
3. **Escalabilidade forte** (suporta múltiplos protocolos de rede, como IP, IPX, AppleTalk, etc.).

Essas três capacidades são consideradas os **três pilares do PPP**, segundo a Huawei:  

✔️ Verificação de identidade;
✔️ Transmissão confiável;
✔️ Forte escalabilidade.


Logo, vemos que o Protocolo Ponto a Ponto (PPP) foi originalmente projetado para acesso discado à Internet por linhas telefônicas ou linhas seriais.

Desde então, tem sido amplamente aplicado a outros tipos de conexões ponto a ponto, como Ethernet e fibras ópticas. 

As principais funções fornecidas pelo PPP incluem encapsulamento de dados, controle de links, controle de camada de rede, rede autenticação, detecção de erros e agrupamento de vários links.

- **Encapsulamento de dados**: PPP encapsula dados de protocolo da camada superior (como pacotes IP) em um formato adequado para transmissão através de links ponto a ponto. Este modo de encapsulamento se aplica a vários protocolos de camada de rede, sendo o mais comum o IP.

- **Controle de link**: O PPP pode estabelecer, configurar, manter e encerrar conexões ponto a ponto por meio do Link Control Protocol (LCP). O LCP negocia parâmetros de configuração do link, como o modo de autenticação e a unidade máxima de transmissão (MTU), para garantir que os dispositivos em ambas as extremidades possam se comunicar adequadamente entre si.

- **Controle da camada de rede**: O PPP também oferece suporte a Protocolos de Controle de Rede (NCPs), que são usados para configurar e gerenciar protocolos da camada de rede. Por exemplo, o Internet Protocol Control Protocol (IPCP) é usado para configurar parâmetros como endereços IP.

- **Autenticação de rede**: O PPP fornece vários mecanismos de autenticação, como o Password Authentication Protocol (PAP) e o Challenge-Handshake Authentication Protocol (CHAP), para verificar as identidades de ambas as partes comunicantes e garantir a segurança da comunicação.

- **Detecção de erros**: O PPP pode detectar e lidar com erros que ocorrem durante a transmissão para garantir a integridade e a confiabilidade dos dados.

- **Agrupamento multi-link**: Por meio do Protocolo Multilink (MP), o PPP permite que vários links físicos sejam agrupados em um link lógico para melhorar a largura de banda e a confiabilidade da conexão.


***

### Como o PPP funciona?

O estabelecimento de uma conexão PPP ocorre em **fases bem definidas**, cinco fases, antes de começar a trocar dados reais. Essas fases são:

#### 1. Dead phase

O link físico ainda não está estabelecido, ou seja, não há conexão física ou o meio está inativo. Assim que isso muda, eles passam para a próxima fase.

#### 2. Establish phase

 Aqui, os dispositivos negociam entre si alguns parâmetros para a comunição acontecer, ser viável, e estabelecem o link de enlace usando o **LCP (Link Control Protocol)**.

- O LCP é responsável por:

	- Configurar o link.
	- Testar a qualidade da conexão.
	- Detectar erros de ligação.
	- Negociar opções como tamanho máximo da trama, autenticação, etc.


Então, repetindo para firmar o entendimento. Quando o link físico ainda não está disponível, o LCP fica no estado Inicial. Assim que a camada física detecta que o link está ativo, ela envia um evento “up” para a camada de enlace, que muda o estado do LCP para Request-Sent e ambos os dispositivos enviam pacotes Configure-Request para negociar parâmetros como tamanho da trama (MTU) e autenticação.

Depois disso, o processo segue por dois caminhos possíveis, dependendo de quem recebe primeiro a confirmação do outro lado. 

- Se o dispositivo local receber primeiro um Configure-Ack do peer, o estado muda de Request-Sent para Ack-Received; ao enviar seu próprio Configure-Ack, o estado vai para Opened.

- Se o dispositivo local enviar primeiro o Configure-Ack, o estado muda para Ack-Sent e, ao receber o Configure-Ack do peer, também vai para Opened. 

Em ambos os casos, o estado final é Opened, indicando que o link de enlace está totalmente estabelecido e os parâmetros foram concordados.

Após o LCP atingir o estado Opened, o PPP avança para a próxima fase. Se autenticação for necessária, os dispositivos entram na fase de Autenticação, usando PAP (menos seguro, com senha em texto claro) ou CHAP (mais seguro, com desafio criptográfico).

Se essa fase falhar, o link vai diretamente para a fase **Terminate**.

#### 3. Authenticate phase – opcional, mas comum

Aqui, os dispositivos podem se autenticar mutuamente usando um dos dois protocolos principais:

- **PAP (Password Authentication Protocol)**:  

	- O peer local envia usuário e senha em texto claro para o autenticador;
	- Se tudo estiver OK, o autenticador libera; se não, não libera.

- **CHAP (Challenge-Handshake Authentication Protocol)**:  
	  
	- O processo do CHAP ocorre em três etapas. Primeiro, após o link PPP ser estabelecido pela negociação LCP, o autenticador (servidor) envia uma mensagem de desafio (challenge) ao dispositivo remoto (peer). Esse desafio contém um valor aleatório gerado no momento, que muda a cada autenticação, o que impede ataques de replay.
	
	- Em seguida, o peer calcula um valor de resposta usando uma função de hash (como MD5) que combina o valor do desafio com uma senha compartilhada, conhecida apenas pelo autenticador e pelo peer, e envia essa resposta de volta. 
	
	- Por fim, o autenticador calcula seu próprio valor de hash usando o mesmo desafio e a senha que tem registrada, compara com a resposta recebida e, se os valores forem iguais, a autenticação é bem-sucedida; caso contrário, a conexão é encerrada.

Além disso, o CHAP oferece uma vantagem importante de segurança: ele pode refazer a autenticação periodicamente durante a sessão, não apenas no início do link.

Isso significa que o autenticador pode enviar novos desafios ao longo do tempo para garantir que o peer continua sendo quem diz ser, tornando o CHAP mais robusto contra invasões mesmo após o link estar estabelecido

Se a autenticação falhar, o link vai para a fase **Terminate**.

#### 4. Network phase

Nessa fase, o PPP usa os **NCP (Network Control Protocols)** para negociar os **parâmetros da camada de rede**. Exemplo mais comum: **IPCP (IP Control Protocol)**, que negesocia:

- Endereços IP dos dispositivos.
- DNS.
- Rotas padrão, entre outros.

É nessa fase que, por exemplo, um roteador pode tentar **obter um IP automaticamente** do outro lado da conexão, usando negociação de endereço.

Se tudo der certo, o link estará **estabelecido e pronto para transmitir dados**.

#### 5. Terminate phase

Quando a comunicação termina (pelo usuário, por falha, por timeout, etc.), o link é encerrado de forma controlada, então, o PPP libera os recursos e volta à fase **Dead**.

***

### A estrutura da trama PPP

O PPP define seu próprio formato de **envelope** para os dados, chamado **trama PPP**. Essa estrutura é similar à de outras tramas de camada de enlace, mas com características próprias.

![[download.png]]


A **trama PPP (Point-to-Point Protocol Frame)**, também chamada de **frame PPP**, é o “envelope” que carrega os dados entre dois dispositivos em uma conexão ponto a ponto. Sua estrutura é composta por **seis campos** principais, organizados de forma sequencial para garantir a identificação, entrega e integridade dos dados.

O primeiro campo é a **Flag**, de **1 byte**, com o valor binário fixo `01111110`. Ele marca o **início e o fim** da trama, funcionando como um delimitador claro que diz ao receptor onde o quadro começa e onde termina. Em tramas PPP contíguas, apenas uma Flag é usada entre elas, pois o fim de uma é o início da próxima.

Em seguida vem o campo **Endereço**, também de **1 byte**, com valor fixo `11111111`. Como o PPP é ponto a ponto, não há necessidade de endereçar dispositivos específicos, então esse campo é **fixo e não usado para endereçamento real**, mas deve estar presente na estrutura.

Depois, o campo **Controle**, de **1 byte** e valor fixo `00000011`, indica que se trata de uma **trama não sequenciada** (sem numeração de sequência), já que o PPP, em sua configuração padrão, não usa controle de fluxo baseado em sequência como outros protocolos de enlace.

O campo **Protocolo** tem **2 bytes** e identifica qual protocolo da camada de rede está sendo carregado no payload (por exemplo, IP, IPX, LCP, NCP). Se os dois lados negociarem **compressão do campo de protocolo** durante a fase LCP, esse campo pode ser reduzido para **1 byte**, mas o padrão é 2 bytes. Os valores do campo Protocolo são definidos nas RFCs de Assigned Numbers e permitem que o PPP carregue múltiplos protocolos de rede simultaneamente.

O campo **Informação** (ou **Payload**) é a parte variável da trama e carrega os **dados reais** encapsulados, como pacotes IP. Seu tamanho pode variar, mas o **tamanho máximo padrão** é de **1500 bytes**, igual ao MTU comum da Ethernet. Esse valor pode ser negociado durante a fase LCP, permitindo frames maiores ou menores conforme necessário.

Por fim, o campo **CRC** (também chamado de **FCS – Frame Check Sequence**) tem **2 bytes** e contém um valor de verificação de erro calculado pelo emissor. O receptor usa esse valor para detectar se a trama chegou **corrompida** durante a transmissão. Se o cálculo no receptor não bater com o valor do FCS, a trama é descartada, garantindo a **integridade dos dados**.

***

### Principais características do PPP

| Característica                     | Descrição                                                |
| ---------------------------------- | -------------------------------------------------------- |
| **Camada**                         | Camada de enlace                                         |
| **Tipo de conexão**                | Ponto a ponto                                            |
| **Meios suportados**               | Linhas seriais, telefônicas, DSL, fibra, links WAN, etc. |
| **Autenticação**                   | PAP e CHAP                                               |
| **Negociação de link**             | LCP (Link Control Protocol)                              |
| **Negociação de rede**             | NCP (Network Control Protocol), como IPCP para IP        |
| **Suporte a múltiplos protocolos** | IP, IPX, AppleTalk, entre outros                         |
| **Detecção de erro**               | FCS/CRC na trama PPP                                     |
| **Tamanho máximo da trama**        | 1500 bytes (padrão)                                      |

***

### Onde o PPP é usado na prática?

O PPP é amplamente utilizado em:

- **Conexões seriais entre roteadores** em redes WAN.
- **Acesso discado (dial-up)** via linha telefônica (antigamente muito comum).
- **DSL (Digital Subscriber Line)**, muitas vezes usando uma variação chamada **PPPoE** (PPP over Ethernet).
- **Links ponto a ponto dedicados** entre filiais de empresas.

***

### PPPoE


O **PPPoE (Point-to-Point Protocol over Ethernet)** é um protocolo que **combina o PPP com a Ethernet**, permitindo que conexões PPP (que originalmente foram feitas para linhas seriais e discadas) funcionem sobre redes **Ethernet**, que são a base das redes locais e de muitas conexões de banda larga. 

Em termos simples, o PPPoE **encapsula quadros PPP dentro de quadros Ethernet**, de modo que os recursos de autenticação, controle de sessão e múltiplos protocolos do PPP possam ser usados em uma infraestrutura Ethernet.

O PPPoE é **amplamente usado por provedores de internet (ISPs)**, especialmente em conexões **DSL (linha telefônica digital)** e em algumas redes de **fibra óptica**, porque permite que múltiplos usuários compartilhem a mesma infraestrutura física, mas tenham **sessões individuais autenticadas** com nome de usuário e senha.

Sem o PPPoE, a autenticação individualizada sobre Ethernet seria muito mais difícil, já que a Ethernet em si não tem mecanismos nativos de autenticação de usuário como o PPP tem.

O funcionamento do PPPoE ocorre em **duas fases principais**: a **fase de descoberta** e a **fase de sessão**. Na **fase de descoberta**, o cliente (por exemplo, o roteador do usuário) precisa **localizar um servidor PPPoE** disponível na rede. Esse processo usa quatro tipos de pacotes:

1. **PADI (PPPoE Active Discovery Initiation)**: o cliente envia um pacote de iniciação de descoberta em **broadcast**, procurando qualquer servidor PPPoE na rede.

2. **PADO (PPPoE Active Discovery Offer)**: o servidor PPPoE que receber o PADI responde com uma oferta, indicando que está disponível para estabelecer a sessão.

3. **PADR (PPPoE Active Discovery Request)**: o cliente escolhe um servidor e envia um pedido de conexão a ele.

4. **PADS (PPPoE Active Discovery Session-confirmation)**: o servidor confirma a solicitação e **atribui um ID de sessão único**; a partir desse momento, a sessão PPPoE está estabelecida.

Na **fase de descoberta**, o cliente ainda não está enviando dados de verdade, apenas está **descobrindo o servidor e criando uma sessão lógica**. Uma vez que a sessão é estabelecida (com o ID de sessão único), o PPPoE entra na **fase de sessão**, onde a **autenticação PPP real** ocorre.

Durante a fase de sessão, o PPPoE usa os **mesmos mecanismos de autenticação do PPP tradicional**: **PAP** ou **CHAP**. Após a autenticação bem-sucedida, os **dados do usuário** (pacotes IP, por exemplo) são **encapsulados em quadros PPP** e, em seguida, **encapsulados novamente em quadros PPPoE**, que são transmitidos pela rede Ethernet.

Cada quadro PPPoE contém:

- Cabeçalho Ethernet (com endereços MAC de origem e destino).
- Tipo de protocolo (que indica que se trata de PPPoE).
- Cabeçalho PPPoE (com versão, tipo, código, ID de sessão e tamanho).
- Payload PPP (que contém o próprio quadro PPP com o campo Protocolo, dados e FCS).

![[pppoe-basic-principle.webp]]

Esse “duplo encapsulamento” (PPP dentro de PPPoE dentro de Ethernet) é o que permite que o PPP “viaje” sobre Ethernet.

Uma vez estabelecida a sessão e autenticado o usuário, os dados trafegam até que a sessão seja encerrada. O encerramento pode ser feito pelo cliente ou pelo servidor usando o pacote **PADT (PPPoE Active Discovery Terminate)**, que finaliza a sessão PPPoE imediatamente.

A principal **vantagem do PPPoE** é que ele **combina a simplicidade e o baixo custo da Ethernet** com os recursos de **autenticação, controle de sessão e segurança do PPP**, permitindo que ISPs gerenciem **muitos usuários individuais** sobre uma mesma infraestrutura compartilhada, com **controle de acesso**, **atribuição dinâmica de IP** e **possibilidade de criptografia**.

Além disso, o PPPoE permite que o provedor **identifique cada usuário** de forma única, aplicando políticas de banda, bloqueios ou perfil de serviço individualmente.


