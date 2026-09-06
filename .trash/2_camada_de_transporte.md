---
tags:
  - arquivo
---
##### Propósito da Camada de Transporte

Os programas da camada de aplicação geram dados que devem ser trocados entre os hosts de origem e de destino. A camada de transporte é responsável pela [comunicação lógica entre aplicativos executados em hosts diferentes]. 

Isso pode incluir serviços como o estabelecimento de uma sessão temporária entre dois hosts e a transmissão confiável de informações para um aplicativo.

A camada de transporte não tem conhecimento do tipo de host de destino, o tipo de mídia pela qual os dados devem percorrer, o caminho percorrido pelos dados, o congestionamento em um link ou o tamanho da rede.

A camada de transporte inclui dois protocolos:

- Protocolo [TCP]
- Protocolo [UDP] (User Datagram Protocol)

---
##### Responsabilidades da Camada de Transporte


- **[Rastreamento de Conversações Individuais]**

	Na camada de transporte, [cada conjunto de dados que flui entre um aplicativo de origem e um aplicativo de destino é conhecido como conversa] e é rastreado separadamente. É responsabilidade da camada de transporte manter e monitorar essas várias conversações.

	Um host pode ter vários aplicativos que estão se comunicando pela rede simultaneamente.

	A maioria das redes tem uma limitação da quantidade de dados que pode ser incluída em um único pacote. Portanto, os dados devem ser divididos em partes gerenciáveis.


- **[Segmentação de Dados e Remontagem de Segmentos]**

	É responsabilidade da camada de transporte [dividir os dados do aplicativo em blocos de tamanho adequado]. Dependendo do protocolo de camada de transporte usado, os blocos de camada de transporte são chamados de segmentos ou datagramas.

	A camada de transporte divide os dados em blocos menores (ou seja, segmentos ou datagramas) que [são mais fáceis de gerenciar e transportar].


- **[Adicionar Informações de Cabeçalho]**

	O protocolo da camada de transporte [também adiciona informações de cabeçalho contendo dados binários organizados em vários campos a cada bloco de dados]. São os valores nesses campos que permitem que os vários protocolos da camada de transporte realizem diferentes funções no gerenciamento da comunicação de dados.

	Por exemplo, as informações de cabeçalho são usadas pelo host de recebimento para remontar os blocos de dados em um fluxo de dados completo para o programa de camada de aplicativo de recebimento.

	***A camada de transporte garante que, mesmo com vários aplicativos em execução em um dispositivo, todos os aplicativos recebam os dados corretos.


- **[Identificação das Aplicações]**

	A camada de transporte deve separar e gerenciar várias comunicações com as diferentes necessidades de requisitos de transporte. Para passar fluxos de dados para os aplicativos adequados, [a camada de transporte identifica o aplicativo de destino usando um identificador chamado número da porta]. 

	Cada processo de software que precisa acessar a rede recebe um número de porta exclusivo para esse host.


- **[Multiplexação das Conversas]**

	O envio de alguns tipos de dados (por exemplo, um vídeo de streaming) através de uma rede, como um fluxo de comunicação completo, pode consumir toda a largura de banda disponível. Isso impediria que outras conversas de comunicação ocorressem ao mesmo tempo. Isso também dificultaria a recuperação de erro e retransmissão dos dados danificados.

	A camada de transporte usa [segmentação e multiplexação] ***(vários apps podem usar a rede ao mesmo tempo)*** para permitir que diferentes conversas de comunicação sejam intercaladas na mesma rede.

	A verificação de erros pode ser realizada nos dados do segmento, para determinar se o segmento foi alterado durante a transmissão.

---
##### Protocolos da Camada de Transporte

O IP está preocupado apenas com a estrutura, endereçamento e roteamento de pacotes. O IP não especifica como a entrega ou o transporte de pacotes ocorrem.

Os protocolos de camada de transporte [especificam como transferir mensagens entre hosts] e são responsáveis pelo [gerenciamento dos requisitos de confiabilidade de uma conversa]. A camada de transporte inclui os protocolos TCP e UDP.

Diferentes aplicações têm diferentes necessidades de confiabilidade de transporte. Portanto, o TCP/IP fornece dois protocolos de camada de transporte.

---
##### O Protocolo de Camada de Transporte Certo para a Aplicação Certa

Alguns aplicativos podem tolerar a perda de dados durante a transmissão pela rede, mas não atrasos na transmissão. Para esses aplicativos, [o UDP] é a melhor escolha, pois [requer menos sobrecarga da rede]. 

O UDP é preferível para aplicativos como Voz sobre IP (VoIP). Agradecimentos e retransmissão atrasariam a entrega e tornariam a conversa por voz inaceitável.

O UDP também é usado por aplicativos de solicitação e resposta onde os dados são mínimos, e a retransmissão pode ser feita rapidamente. Por exemplo, o Domain Name System (DNS) usa UDP para esse tipo de transação. 

O cliente solicita endereços IPv4 e IPv6 para um nome de domínio conhecido de um servidor DNS. Se o cliente não receber uma resposta em um período predeterminado de tempo, ele simplesmente envia a solicitação novamente.

Por exemplo, se um ou dois segmentos de uma transmissão de vídeo ao vivo não conseguir chegar, isso criará apenas uma interrupção momentânea na transmissão. Isso pode aparecer como uma distorção na imagem ou no som, mas pode não ser notado pelo usuário. 

Se o dispositivo de destino considerasse os dados perdidos, a transmissão poderia atrasar, enquanto aguardasse as retransmissões, causando, portanto, grandes perdas de áudio e vídeo. Nesse caso, é melhor fornecer a melhor experiência de mídia com os segmentos recebidos e ***descartar a confiabilidade.

Para outras aplicações, é importante que todos os dados cheguem e que possam ser processados em sua sequência adequada. Para esses tipos de aplicativos, o TCP é usado como o protocolo de transporte. 

Por exemplo, aplicações como bancos de dados, navegadores e clientes de e-mail exigem que todos os dados enviados cheguem ao destino em seu estado original. Quaisquer dados ausentes podem corromper uma comunicação, tornando-a incompleta ou ilegível. 

Por exemplo, é importante, ao acessar informações bancárias pela web, certificar-se de que todas as informações são enviadas e recebidas corretamente.

Os desenvolvedores de aplicações devem escolher que tipo de protocolo de transporte é apropriado com base nas necessidades de suas aplicações. O vídeo pode ser enviado através de TCP ou UDP. 

*Os aplicativos que transmitem áudio e vídeo armazenados normalmente usam TCP*. O aplicativo usa TCP para executar buffer, sondagem de largura de banda e controle de congestionamento, a fim de controlar melhor a experiência do usuário.

Vídeo e voz em tempo real geralmente usam UDP, mas também podem usar TCP, ou UDP e TCP. Um aplicativo de videoconferência pode usar UDP por padrão, mas como muitos firewalls bloqueiam UDP, o aplicativo também pode ser enviado por TCP.

Os aplicativos que transmitem áudio e vídeo armazenados usam TCP. Por exemplo, se sua rede, repentinamente, não comportar a largura de banda necessária para a transmissão de um filme sob demanda, a aplicação interrompe a reprodução. 

Durante essa interrupção, você deverá ver uma mensagem de “buffering...” , enquanto o TCP age para restabelecer a transmissão. Quando todos os segmentos estão em ordem e um nível mínimo de largura de banda é restaurado, a sessão TCP é retomada e o filme retoma a reprodução.