---
tags:
  - arquivo
---
Para realizar comunicações de ponta a ponta através dos limites da rede, os protocolos de camada de rede executam quatro operações básicas:

- **[Endereçamento de dispositivos finais]**

	Os dispositivos finais devem ser configurados com um endereço IP exclusivo para identificação na rede.

- **[Encapsulamento]**

	A camada de rede encapsula a unidade de dados de protocolo (PDU) da camada de transporte em um pacote. O processo de encapsulamento adiciona informações de cabeçalho IP, como os endereços IP dos hosts origem e destino.

- **[Roteamento]**

	A camada de rede fornece serviços para direcionar os pacotes para um host de destino em outra rede. Para trafegar para outras redes, o pacote deve ser processado por um roteador. 

	A função do roteador é escolher o melhor caminho e direcionar os pacotes para o host de destino em um processo conhecido como roteamento. *Cada roteador que um pacote atravessa para chegar ao host de destino é chamado de salto **(hop).

- **[Desencapsulamento]**

	Quando o pacote chega à camada de rede do host de destino, o host verifica o cabeçalho IP do pacote. Se o endereço IP de destino no cabeçalho corresponder ao seu próprio endereço IP, o cabeçalho IP será removido do pacote. 

	Depois que o pacote é desencapsulado pela camada de rede, a PDU resultante da Camada 4 é transferida para o serviço apropriado na camada de transporte.


Diferentemente da camada de transporte (OSI Layer 4), que gerencia o transporte de dados entre os processos em execução em cada host, ***os protocolos de comunicação da camada de rede*** (ou seja, IPv4 e IPv6) ***especificam a estrutura de pacotes e o processamento usado para transportar os dados de um host para outro hospedeiro***. 

A operação não leva em consideração os dados contidos em cada pacote, permitindo que a camada de rede leve os pacotes para diversos tipos de comunicações entre vários hosts.

---
### Encapsulamento IP


O processo de encapsulamento camada por camada possibilita o desenvolvimento dos serviços nas diferentes camadas e suas expansões sem afetar outras camadas. 

Isso significa que os segmentos da camada de transporte podem ser imediatamente empacotados por IPv4, IPv6 ou qualquer protocolo que venha a ser desenvolvido no futuro.

O cabeçalho IP é examinado por dispositivos de Camada 3 (ou seja, roteadores e switches de Camada 3) à medida que viaja através de uma rede até seu destino. 

É importante notar que as informações de endereçamento IP permanecem as mesmas desde o momento em que o pacote sai do host de origem até chegar ao host de destino, exceto quando traduzidas pelo dispositivo que executa a Tradução de Endereços de Rede (NAT) para IPv4.

Os roteadores implementam protocolos de roteamento para rotear pacotes entre redes. O roteamento realizado por esses dispositivos intermediários examina o endereçamento da camada de rede no cabeçalho do pacote. 

Em todos os casos, a parte de dados do pacote, ou seja, a PDU da camada de transporte encapsulada ou outros dados, permanece inalterada durante os processos da camada de rede.

---
### Características do IP

O IP foi desenvolvido como um protocolo com baixa sobrecarga. Ele fornece apenas as funções necessárias para enviar um pacote de uma origem a um destino por um sistema interconectado de redes. 

O protocolo não foi projetado para rastrear e gerenciar o fluxo de pacotes. Essas funções, se exigido, são realizadas por outros protocolos em outras camadas, principalmente TCP na Camada 4.

Estas são as características básicas da IP:

- **[Sem conexão]** 

	Não há conexão com o destino estabelecido antes do envio de pacotes de dados. 

	A comunicação sem conexão é conceitualmente semelhante a enviar uma carta a alguém sem notificar o destinatário com antecedência

- **[Melhor esforço]**

	O IP é inerentemente não confiável, porque a entrega de pacotes não é garantida.

	O IP também não requer campos adicionais no cabeçalho para manter uma conexão estabelecida. Esse processo reduz bastante a sobrecarga do IP. 

	No entanto, sem conexão de ponta a ponta pré-estabelecida, os remetentes não sabem se os dispositivos de destino estão presentes e funcionais ao enviar pacotes, nem sabem se o destino recebe o pacote ou se o dispositivo de destino pode acessar e ler o pacote.

- **[Independente da mídia]**

	Isso significa que o IP não tem a capacidade de gerenciar e recuperar pacotes não entregues ou corrompidos. 

	Isso ocorre porque, embora os pacotes IP sejam enviados com informações sobre o local da entrega, eles não contêm informações que podem ser processadas para informar ao remetente se a entrega foi bem-sucedida. 

	Os pacotes podem chegar ao destino corrompidos, fora de sequência ou simplesmente não chegar. O IP não tem capacidade de retransmitir os pacotes em caso de erros.

	Se os pacotes forem entregues fora de ordem ou estiver faltando algum pacote, as aplicações que usam os dados, ou serviços de camada superior, deverão resolver esses problemas. Isso permite que o IP funcione de forma bem eficiente. 

	No conjunto de protocolos TCP/IP, a confiabilidade é o papel do protocolo TCP na camada de transporte.

	O IP opera independentemente da mídia que transporta os dados nas camadas inferiores da pilha de protocolos.


Os pacotes IP podem trafegar por diferentes meios físicos.

A camada de enlace de dados OSI é responsável por pegar um pacote IP e prepará-lo para transmissão pelo meio de comunicação. Isso significa que a entrega de pacotes IP não se limita a nenhum meio específico.

Há, no entanto, uma característica muito importante dos meios físicos que a camada de rede considera: o [tamanho máximo da PDU] que cada meio consegue transportar. Essa característica é chamada de [unidade máxima de transmissão (maximum transmission unit - MTU)]. 

Parte das comunicações de controle entre a camada de enlace de dados e a camada de rede é a definição de um tamanho máximo para o pacote. 

A camada de enlace de dados passa o valor da MTU para a camada de rede. A camada de rede então determina o tamanho que os pacotes podem ter.

Em alguns casos, um dispositivo intermediário, geralmente um roteador, deve dividir um pacote IPv4 ao encaminhá-lo de um meio para outro com uma MTU menor. 

Esse processo é chamado fragmentação do pacote ou fragmentação. A fragmentação causa latência. *Os pacotes IPv6 não podem ser fragmentados pelo roteador.