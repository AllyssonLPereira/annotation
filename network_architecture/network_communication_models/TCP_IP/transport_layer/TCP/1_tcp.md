---
tags:
  - arquivo
---
##### Protocolo de Controle de Transmissão (TCP)

O IP se preocupa apenas com a estrutura, o endereçamento e o roteamento de pacotes, do remetente original ao destino final. O IP não é responsável por garantir a entrega ou determinar se uma conexão entre o remetente e o destinatário precisa ser estabelecida.

O TCP é considerado um [protocolo de camada de transporte confiável, completo, que garante que todos os dados cheguem ao destino]. O TCP inclui campos que garantem a entrega dos dados do aplicativo. Esses campos exigem processamento adicional pelos hosts de envio e recebimento.

> [!NOTE]
> O TCP divide os dados em segmentos.

[O transporte TCP é análogo a enviar pacotes que são rastreados da origem ao destino]. Se um pedido pelo correio estiver dividido em vários pacotes, um cliente poderá verificar on-line a sequência de recebimento do pedido.

[O TCP fornece confiabilidade e controle de fluxo] usando estas operações básicas:

- Número e rastreamento de segmentos de dados transmitidos para um host específico a partir de um aplicativo específico

- Confirmar dados recebidos

- Retransmitir quaisquer dados não reconhecidos após um certo período de tempo

- Dados de sequência que podem chegar em ordem errada

- Enviar dados a uma taxa eficiente que seja aceitável pelo receptor

Para manter o estado de uma conversa e rastrear as informações, o TCP deve primeiro estabelecer uma conexão entre o remetente e o receptor. É por isso que o TCP é conhecido como um [protocolo orientado a conexão].

---
##### Recursos TCP

Além de suportar as funções básicas de segmentação e remontagem de dados, o TCP também fornece os seguintes serviços:

- **[Estabelece uma sessão]**

	O TCP é um [protocolo orientado à conexão que negocia e estabelece uma conexão/sessão] permanente entre os dispositivos de origem e de destino antes de encaminhar qualquer tráfego. 
	
	Com o estabelecimento da sessão, os dispositivos negociam o volume de tráfego esperado que pode ser encaminhado em determinado momento e os dados de comunicação entre os dois.

- **[Garante a entrega confiável]**

	Por várias razões, é possível que um segmento seja corrompido ou perdido completamente, pois é transmitido pela rede. O TCP garante que cada segmento enviado pela fonte chegue ao destino.

- **[Fornece entrega no mesmo pedido]**

	Como as redes podem fornecer várias rotas que podem ter taxas de transmissão diferentes, os dados podem chegar na ordem errada. 
	
	Ao numerar e sequenciar os segmentos, o TCP garante que os segmentos sejam remontados na ordem correta.

- **[Suporta controle de fluxo]** 

	Os hosts de rede têm recursos limitados (ou seja, memória e poder de processamento). 
	
	Quando percebe que esses recursos estão sobrecarregados, o TCP pode requisitar que a aplicação emissora reduza a taxa de fluxo de dados. Para isso, o[ TCP regula o volume de dados transmitido pelo dispositivo origem]. 
	
	O controle de fluxo pode impedir a necessidade de retransmissão dos dados quando os recursos do host receptor estão sobrecarregados.


> [!NOTE]
> Para obter mais informações sobre o TCP, procure o RFC 793 na Internet.

---
##### Cabeçalho TCP

TCP é um protocolo stateful, o que significa que ele controla o estado da sessão de comunicação. Para manter o controle do estado de uma sessão, o TCP registra quais informações ele enviou e quais informações foram confirmadas. 

***A sessão com estado começa com o estabelecimento da sessão e termina com o encerramento da sessão.

Um segmento TCP adiciona 20 bytes (ou seja, 160 bits) de sobrecarga ao encapsular os dados da camada de aplicativo.

![[cabecalho_camada_de_transporte_tcp_ip.webp]]

|Campo de cabeçalho TCP|Descrição|
|---|---|
|Porta de origem|Um campo de 16 bits usado para identificar o aplicativo de origem por número de porta.|
|Porta de destino|Um campo de 16 bits usado para identificar o aplicativo de destino pelo número da porta.|
|Número de Sequência|Um campo de 32 bits usado para fins de remontagem de dados.|
|Número de Confirmação|Um campo de 32 bits usado para indicar que os dados foram recebidos e o próximo byte esperado da origem.|
|Tamanho do cabeçalho|Um campo de 4 bits conhecido como “offset de dados” que indica o comprimento do cabeçalho de segmento TCP.|
|Reservado|Um campo de 6 bits que é reservado para uso futuro.|
|Bits de controle|Um campo de 6 bits que inclui códigos de bits, ou sinalizadores, que indicam a finalidade e a função do segmento TCP.|
|Tamanho da janela|Um campo de 16 bits usado para indicar o número de bytes que podem ser aceitos ao mesmo tempo.|
|Checksum|Um campo de 16 bits usado para verificação de erros do cabeçalho e dos dados do segmento.|
|Urgente|Um campo de 16 bits usado para indicar se os dados contidos são urgentes.|

---
##### Aplicações que usam TCP

O TCP é um bom exemplo de como as diferentes camadas do conjunto de protocolos TCP/IP têm funções específicas. 

O TCP lida com todas as tarefas associadas à divisão do fluxo de dados em segmentos, fornecendo confiabilidade, controlando o fluxo de dados e reordenando segmentos. O TCP libera a aplicação da obrigação de gerenciar todas essas tarefas. 

---
##### Confiabilidade TCP - entrega garantida e ordenada

A razão pela qual o TCP é o melhor protocolo para alguns aplicativos é porque, ao contrário do UDP, ele [reenvia pacotes descartados] e [números de pacotes para indicar sua ordem correta] antes da entrega. O TCP também pode ajudar a [manter o fluxo de pacotes] para que os dispositivos não fiquem sobrecarregados.

Pode haver momentos em que os segmentos TCP não chegam ao seu destino. Outras vezes, os segmentos TCP podem chegar fora de ordem. Para que a mensagem original seja entendida pelo destinatário, todos os dados devem ser recebidos e os dados nesses segmentos devem ser remontados na ordem original. 

Os números de sequência são atribuídos no cabeçalho de cada pacote para alcançar esse objetivo. ***O número de sequência representa o primeiro byte de dados do segmento TCP.

Durante o estabelecimento de uma sessão, um [número de sequência inicial] (ISN) é definido de forma aleatória, por questões de segurança. Este ISN representa o valor inicial dos bytes que são transmitidos ao aplicativo receptor. 

À medida que os dados são transmitidos durante a sessão, o [número de sequência é incrementado do número de bytes que foram transmitidos]. Esse rastreamento dos bytes de dados permite que cada segmento seja identificado e confirmado de forma única. Segmentos perdidos podem então, ser identificados.


> [!NOTE] 
> Os números de sequência do segmento indicam como remontar e reordenar os segmentos recebidos


O processo TCP receptor coloca os dados de um segmento em um buffer receptor. Os segmentos são então colocados na ordem de sequência correta e passados para a camada de aplicativo quando remontados. 

Qualquer segmento que chegue com números de sequência fora de ordem são retidos para processamento posterior. Por isso, quando os segmentos com os bytes que faltavam chegam, esses segmentos são processados.

---
##### Confiabilidade TCP - Perda e Retransmissão de Dados

Não importa o quão bem projetada uma rede é, a perda de dados ocasionalmente ocorre. O TCP fornece métodos de [gerenciamento dessas perdas de segmento]. Entre esses métodos há um mecanismo que retransmite segmentos dos dados não confirmados.

O [número de sequência] (SEQ) e o [número de confirmação] (ACK) são usados juntamente para confirmar o recebimento dos bytes de dados contidos nos segmentos.

O número SEQ identifica o primeiro byte de dados no segmento que está sendo transmitido. O TCP usa o número de confirmação (ACK) enviado de volta à origem para indicar o próximo byte que o destino espera receber. Isto é chamado de confirmação antecipatória.

Antes de melhorias posteriores, o TCP só podia reconhecer o próximo byte esperado. Por exemplo, usando números de segmento para simplicidade, o host A envia os segmentos 1 a 10 para o host B. Se todos os segmentos chegarem, exceto os segmentos 3 e 4, o host B responderia com confirmação especificando que o próximo segmento esperado é o segmento 3. 

O Host A não tem ideia se outros segmentos chegaram ou não. O host A, portanto, reenviaria os segmentos 3 a 10. Se todos os segmentos reenviados chegarem com sucesso, os segmentos 5 a 10 seriam duplicados. Isso pode levar a atrasos, congestionamentos e ineficiências.

Hoje em dia, os sistemas operacionais de host utilizam um recurso TCP opcional chamado [reconhecimento seletivo] (SACK), negociado durante o handshake de três vias. Se ambos os hosts suportarem SACK, o receptor pode reconhecer explicitamente quais segmentos (bytes) foram recebidos, incluindo quaisquer segmentos descontínuos. 

O host de envio, portanto, só precisa retransmitir os dados ausentes. Por exemplo, novamente usando números de segmento para simplicidade, o host A envia segmentos 1 a 10 para o host B. 

Se todos os segmentos chegarem, exceto os segmentos 3 e 4, o host B pode reconhecer que recebeu segmentos 1 e 2 (ACK 3) e reconhecer seletivamente os segmentos 5 a 10 (SACK 5-10). O host A só precisaria reenviar os segmentos 3 e 4.

---
##### Controle de Fluxo TCP - Tamanho da Janela e Confirmações

O TCP também fornece mecanismos para controle de fluxo. Controle de fluxo é a quantidade de dados que o destino pode receber e processar de forma confiável. O controle de fluxo ajuda a manter a confiabilidade da transmissão TCP definindo a taxa de fluxo de dados entre a origem e o destino em uma determinada sessão. 

***Para realizar isso, o cabeçalho TCP inclui um campo de 16 bits chamado de tamanho da janela.

O tamanho da janela determina o [número de bytes que podem ser enviados antes de esperar uma confirmação]. O número de reconhecimento (acknowledgment) é o número do próximo byte esperado.

O tamanho da janela é número de bytes que o dispositivo de destino de uma sessão TCP pode aceitar e processar de uma vez. 

Por exemplo, o tamanho da janela inicial do PC B para a sessão TCP é de 10.000 bytes. No caso do primeiro byte ser número 1, o último byte que PC A pode enviar sem receber uma confirmação é o byte 10.000. Isso é conhecido como janela de envio do PC A. 

***O tamanho da janela é incluído em todos os segmentos TCP, para que o destino possa modificar o tamanho da janela a qualquer momento, dependendo da disponibilidade do buffer.

O tamanho da janela inicial é determinado quando a sessão é estabelecida durante o handshake triplo. 

O dispositivo de origem deve limitar o número de bytes enviados ao dispositivo de destino com base no tamanho da janela do destino. Somente depois que o dispositivo de origem receber uma confirmação de que os bytes foram recebidos, ele poderá continuar a enviar mais dados para a sessão. 

Normalmente, o destino não esperará que todos os bytes que a sua janela comporta sejam recebidos para responder confirmando. À medida que os bytes forem recebidos e processados, o destino enviará confirmações para informar à origem que pode continuar a enviar bytes adicionais.

Por exemplo, é típico que o PC B não espere até que todos os 10.000 bytes tenham sido recebidos antes de enviar uma confirmação. Isso significa que o PC A pode ajustar sua janela de envio ao receber confirmações do PC B. 

Quando o PC A recebe uma confirmação com o número de confirmação 2.921, que é o próximo byte esperado. A janela de envio do PC A irá incrementar 2.920 bytes. Isso altera a janela de envio de 10.000 bytes para 12.920. O PC A agora pode continuar enviando até outros 10.000 bytes para o PC B, desde que não envie mais do que sua nova janela de envio em 12.920.

Um destino que envia confirmações enquanto processa os bytes recebidos e o ajuste contínuo da janela de envio de origem é conhecido como [janelas deslizantes]. No exemplo anterior, a janela de envio do PC A incrementa ou desliza sobre outros 2.921 bytes de 10.000 para 12.920.

Se a disponibilidade do espaço de buffer do destino diminui, ele pode reduzir o tamanho da sua janela para informar à origem que reduza o número de bytes que ela deveria enviar sem receber uma confirmação.

> [!NOTE]
> Os dispositivos hoje usam o protocolo de janelas deslizantes. O receptor normalmente envia uma confirmação após cada dois segmentos que recebe. O número de segmentos recebidos antes de ser confirmado pode variar. 
> 
> A vantagem de janelas móveis é que permite que o emissor transmita continuamente segmentos, desde que o receptor esteja reconhecendo segmentos anteriores.

---
##### Controle de Fluxo TCP - Tamanho Máximo do Segmento (MSS)

Na figura, a fonte está transmitindo 1.460 bytes de dados dentro de cada segmento TCP. Normalmente, este é o [tamanho máximo do segmento (MSS)] que o dispositivo de destino pode receber. 

O MSS faz parte do campo de opções no cabeçalho TCP que especifica a maior quantidade de dados, em bytes, que um dispositivo pode receber em um único segmento TCP. O tamanho do MSS não inclui o cabeçalho TCP. O MSS é normalmente incluído durante o handshake de três vias.

![[mss_camada_transpote.png]]
**CISCO

Um MSS comum é 1.460 bytes ao usar IPv4. Um host determina o valor do campo de MSS subtraindo os cabeçalhos de IP e de TCP da MTU (Maximum transmission unit, Unidade máxima de transmissão) da Ethernet. 

Em uma interface Ethernet, a MTU padrão é 1500 bytes. Subtraindo o cabeçalho IPv4 de 20 bytes e o cabeçalho TCP de 20 bytes, o tamanho padrão do MSS será 1460 bytes.

---
##### Controle de Fluxo TCP - Prevenção de Congestionamento

Quando ocorre um congestionamento em uma rede, isso resulta em pacotes sendo descartados pelo roteador sobrecarregado. Quando pacotes contendo segmentos TCP não atingem seu destino, eles são deixados sem serem reconhecidos. 

Ao determinar a taxa na qual os segmentos TCP são enviados, mas não confirmados, a origem pode pressupor um certo nível de congestionamento da rede.

Sempre que ocorrer um congestionamento, ocorrerá a retransmissão de segmentos TCP perdidos por parte da origem. Se a retransmissão não for devidamente controlada, a retransmissão adicional dos segmentos TCP pode agravar o congestionamento. 

Não só novos pacotes com segmentos TCP são introduzidos na rede, como também o efeito de feedback dos segmentos retransmitidos que foram perdidos aumentarão o congestionamento. Para evitar e controlar o congestionamento, o TCP emprega alguns mecanismos para lidar com o congestionamento, [temporizadores e algoritmos].

Se a origem determina que os segmentos TCP não são confirmados ou não são confirmados em tempo hábil, isso pode reduzir o número de bytes enviados antes do recebimento de uma confirmação.


> [!NOTE] 
> Os números de confirmação são para o próximo byte esperado e não para um segmento.
