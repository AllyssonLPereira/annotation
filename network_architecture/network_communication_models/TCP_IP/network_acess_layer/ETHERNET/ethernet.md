---
tags:
  - arquivo
---
## Origem

A Ethernet foi concebida originalmente no início da década de 1970 por Robert Metcalfe nos laboratórios da Xerox PARC. O objetivo inicial era interconectar computadores e impressoras, utilizando um meio compartilhado para a transmissão de dados.

O conceito fundamental baseava-se no Sistema Aloha, desenvolvido na Universidade do Havaí, que permitia que múltiplos dispositivos utilizassem o mesmo canal de comunicação. Naquela fase experimental, a Ethernet operava a uma taxa de transmissão de aproximadamente 2,94 Mbps, utilizando cabos coaxiais espessos como meio físico.

A transição de uma tecnologia proprietária para um padrão de mercado ocorreu em 1980, com o consórcio formado por Digital Equipment Corporation (DEC), Intel e Xerox, conhecido como o padrão DIX. Esse consórcio estabeleceu as bases para que a tecnologia pudesse ser adotada em larga escala pela indústria de computação. 

A evolução subsequente foi marcada pelo aumento exponencial das velocidades de transmissão, passando pela Fast Ethernet (100 Mbps) nos anos 90, seguida pela Gigabit Ethernet (1 Gbps) e as atuais implementações de alta performance, como 100 Gbps e 400 Gbps, utilizadas em centros de dados e infraestruturas de provedores de serviço.

## Padronização IEEE 802.3

Com o crescimento da adoção da tecnologia, o Institute of Electrical and Electronics Engineers (IEEE) assumiu a responsabilidade de formalizar e manter as especificações da Ethernet através do grupo de trabalho 802.3.

Essa padronização garantiu a interoperabilidade entre equipamentos de diferentes fabricantes, permitindo que placas de rede, switches e cabos funcionassem de forma coesa. Embora os termos "Ethernet" e "IEEE 802.3" sejam frequentemente utilizados como sinônimos, tecnicamente a Ethernet refere-se ao padrão original da indústria, enquanto o 802.3 define as variantes oficiais regulamentadas pelo instituto.

A manutenção deste padrão é contínua, incorporando novas mídias físicas, como diferentes categorias de cabos de par trançado e tipos de fibras ópticas, para suportar as demandas modernas de largura de banda.

## Ethernet no modelo OSI

No âmbito da arquitetura de redes, a Ethernet opera especificamente nas duas camadas inferiores do modelo de referência OSI: a Camada física (Camada 1) e a Camada de enlace (Camada 2). 

Na Camada física, a Ethernet define as especificações de hardware, o que inclui as propriedades elétricas, os tipos de conectores (como o RJ45) e os meios de transmissão. Esta camada é responsável pela sinalização, convertendo os dados binários em sinais elétricos ou pulsos de luz que percorrem o cabeamento. 

Diferentes padrões físicos, como 10BASE-T ou 1000BASE-SX, determinam como esses sinais são propagados e a distância máxima que podem atingir sem degradação.

Na Camada de Enlace, a Ethernet desempenha um papel na organização lógica dos dados antes de serem enviados ao meio físico. Esta camada é subdividida em duas subcamadas: Logical Link Control (LLC) e Media Access Control (MAC).

- A subcamada Logical-Link Control é responsável por receber o pacote IP e encapsulá-lo em um quadro Ethernet, incluindo todas as informações necessárias, como cabeçalho e trailer. Em seguida, o quadro é passado para a Camada de Controle de Acesso à Mídia.

- A camada MAC sabe para qual mídia o quadro deve ser enviado e como converter o quadro para 1s e 0s com base no padrão de mídia 802.3 usado. Se o link for IEEE802.3u FastEthernet, por exemplo, os 1s e 0s são representados como sinais elétricos; se, por exemplo, for usado um link de fibra óptica, os 1s e 0s são enviados como pulsos de luz.

---
## Estrutura do Ethernet frame

O processo de comunicação em uma rede Ethernet exige que os dados originados em camadas superiores sejam encapsulados em uma unidade lógica denominada quadro (ou _frame_). 

- A sequência inicia-se com o Preâmbulo e o _Start Frame Delimiter_ (SFD), que são padrões de bits destinados à sincronização do relógio entre o emissor e o recetor.

	- O Preamble tem o comprimento de 7 bytes (56 bits) que ficam alterando entre 1 e 0 (10101010 × 7), permitindo aos dispositivos sincronizarem seus relógios receptores;
	
	- O SFD tem 1 byte de comprimento (10101011) que marca o fim do Preamble e o início do restante do frame.

- Após a sincronização, seguem-se os campos de endereço MAC de destino e de origem, cada um com 6 bytes, fundamentais para o encaminhamento na Camada 2.

- O campo seguinte, denominado _Type_ ou _Length_, indica qual protocolo de rede (como IPv4 ou IPv6) está encapsulado no payload ou define o tamanho exato dos dados.

	- O campo Type/Length tem 2 bytes - um valor de 1500 ou menos vai indicar o campo Length do pacote encapsulado, já um valor de 1536 pra cima vai indicar o campo Type (o comprimento será determinado por outros métodos nesse caso).
	
	- 0x0800 = 2048 bits, esse número hexadecimal indica o IPv4; já o 0x86DD = 34525, indicando o IPv6.

- O corpo do quadro contém os dados propriamente ditos, que devem respeitar limites específicos de tamanho. O padrão estabelece uma Unidade Máxima de Transmissão (MTU) de 1500 bytes para os dados. Caso a informação a ser enviada seja inferior a 46 bytes, o protocolo aplica obrigatoriamente um preenchimento chamado _padding_ para garantir que o quadro atinja o tamanho mínimo de 64 bytes (excluindo preâmbulo e SFD). Esta dimensão mínima é um requisito histórico necessário para a detecção de colisões no meio físico. 

- O quadro encerra-se com a _Frame Check Sequence_ (FCS), um campo de 4 bytes que utiliza um cálculo matemático (CRC) para verificar se o quadro sofreu corrupção durante o trajeto; se o cálculo do recetor não coincidir com o valor no FCS, o quadro é descartado.


Apesar dos campos Preamble e SFD serem enviados em cada Ethernet frame, eles geralmente não são considerados parte do cabeçalho Ethernet.

Assim, o cabeçalho Ethernet consiste nos campos destino, origem e type/length. Com isso, o tamanho do cabeçalho Ethernet + trailer será igual a 18 bytes.

Além disso, existe um tamanho mínimo para um quadro Ethernet, que é de 64 bytes (header + payload(packet) + trailer). 

Portanto, o tamanho mínimo do payload (packet) é de 46 bytes (64 bytes - 18 bytes (header + trailer)). Caso o payload enviado seja menor que 46 bytes, bytes de preenchimento são adicionados, e esses bytes são todos zeros.


## Endereçamento MAC (Media Access Control)

O endereçamento físico em redes Ethernet é realizado através do endereço MAC, um identificador único de 48 bits (6 bytes) gravado no hardware das interfaces de rede. A representação deste endereço é feita em formato hexadecimal, geralmente dividida por dois pontos ou hifens. 

A estrutura do endereço MAC é dividida em duas partes iguais de 24 bits cada. A primeira metade é o Identificador Único de Organização (OUI), atribuído pelo IEEE ao fabricante do hardware, permitindo identificar a marca do dispositivo (como Cisco, Intel ou Nokia). A segunda metade é o Identificador de Controlador de Interface de Rede, uma sequência única atribuída pelo próprio fabricante, garantindo que não existam dois dispositivos com o mesmo endereço MAC a nível global.

- No que diz respeito à lógica de entrega, a Ethernet utiliza três tipos de endereçamento MAC. O primeiro é o _Unicast_, utilizado para a comunicação direta entre um único emissor e um único recetor específico.

- O segundo é o _Broadcast_, cujo endereço é composto inteiramente por bits 1 (representado como FF:FF:FF:FF:FF:FF), e tem como função enviar a informação a todos os dispositivos presentes no mesmo domínio de broadcast. 

- Por fim, existe o endereçamento _Multicast_, que permite o envio de dados a um grupo selecionado de dispositivos que pertençam a um determinado grupo de interesse. Estes endereços são identificáveis pelo primeiro byte, onde o bit menos significativo é definido como 1. 

Este sistema de endereçamento é a base para que switches e outros dispositivos de camada de enlace possam gerir o tráfego de forma eficiente e organizada.

---
## Funcionamento da tabela de endereços MAC

Diferente dos hubs, que operam na Camada 1 e simplesmente replicam sinais elétricos para todas as portas, o switch Ethernet é um dispositivo de Camada 2 que toma decisões baseadas em software e hardware especializado.

O componente central dessa operação é a tabela de endereços MAC, também conhecida como tabela CAM (_Content-Addressable Memory_). Esta tabela armazena o mapeamento entre os endereços MAC dos dispositivos finais e as portas físicas do switch às quais eles estão conectados.

No início da operação, a tabela está vazia e é populada dinamicamente à medida que o tráfego atravessa o dispositivo.

A lógica de um switch baseia-se em duas etapas fundamentais executadas para cada quadro recebido: o aprendizado e o encaminhamento.

Ao receber um quadro, o switch inspeciona primeiramente o **endereço MAC de origem**. Se esse endereço ainda não constar na tabela MAC, o switch cria uma nova entrada vinculando o endereço à porta de entrada. Caso o endereço já exista, o switch apenas atualiza o cronômetro de expiração (_aging timer_) dessa entrada. Esse processo garante que o switch saiba exatamente onde cada dispositivo está localizado na rede local.

Após a fase de aprendizado, o switch analisa o **endereço MAC de destino**. Ele consulta sua tabela para determinar por qual porta o quadro deve ser enviado. Se o endereço de destino for encontrado na tabela, o switch realiza o encaminhamento, enviando os dados especificamente para a porta correspondente. Esse comportamento otimiza a largura de banda, pois evita que o tráfego desnecessário chegue a segmentos da rede onde não é solicitado.

Quando um switch recebe um quadro destinado a um endereço MAC que não consta em sua tabela, ocorre o processo de _Unknown Unicast Flooding_. Nessa situação, o switch replica o quadro para todas as portas ativas, exceto para a porta por onde o quadro foi originalmente recebido.

O objetivo é garantir que o destinatário, onde quer que esteja, receba a informação e responda, permitindo que o switch aprenda sua localização na próxima interação. O mesmo comportamento de inundação é aplicado obrigatoriamente a quadros de _Broadcast_ (destinados a FF:FF:FF:FF:FF:FF), garantindo que todos os dispositivos no domínio de transmissão recebam a mensagem.

A implementação de switches Ethernet transformou radicalmente a topologia lógica das redes ao isolar os domínios de colisão. Em redes legadas com hubs, todos os dispositivos compartilhavam o mesmo meio e podiam colidir ao transmitir simultaneamente. Com o switch, cada porta individual representa um domínio de colisão isolado. 

Se o dispositivo conectado e a porta do switch suportarem o modo _Full-Duplex_, a transmissão e a recepção de dados podem ocorrer simultaneamente sem risco de colisões, eliminando a necessidade do protocolo CSMA/CD em redes modernas cabeadas. Contudo, o switch ainda mantém todos os dispositivos dentro do mesmo domínio de _Broadcast_, o que significa que mensagens de difusão ainda atingem todas as estações da rede local.