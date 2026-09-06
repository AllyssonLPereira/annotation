---
tags:
  - arquivo
---
Assim como os seres humanos, os computadores usam [regras] (ou seja, [protocolos]) para se comunicarem. Os protocolos são necessários para que os computadores se comuniquem corretamente na rede. Em ambientes com e sem fio, uma [rede local é definida como uma área onde todos os hosts devem "falar a mesma linguagem"] ou, na terminologia dos computadores, "[compartilhar um protocolo em comum]".

Se todas as pessoas em uma sala falarem uma linguagem diferente, não conseguirão se comunicar. Da mesma forma, se os dispositivos em uma rede local não usarem os mesmos protocolos, eles não poderão se comunicar.

[Os protocolos de rede definem as regras de comunicação pela rede local]. Como mostrado na tabela, eles incluem o formato, o tamanho, o tempo, a codificação, o encapsulamento e os padrões de mensagem.

| Característica de protocolo | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Formato da mensagem         | Quando uma mensagem é enviada, ela deve usar um formato ou estrutura específica. Os formatos da mensagem dependem do tipo de mensagem e do canal usado para entregá-la.                                                                                                                                                                                                                                                                          |
| Tamanho da mensagem         | As regras que regem o tamanho das partes transmitidas por meio da rede são muito rígidas. Eles também podem ser diferentes, dependendo do canal usado. Quando uma mensagem longa é enviada de um host para outro em uma rede, pode ser necessário dividir a mensagem em partes menores para garantir que ela seja entregue de forma confiável.                                                                                                   |
| Temporização                | Muitas funções de comunicação de rede dependem de temporização. A temporização determina a velocidade com que os bits são transmitidos na rede. Também afeta quando um host individual pode enviar dados e a quantidade total de dados que pode ser enviada em qualquer transmissão.                                                                                                                                                             |
| Codificação                 | As mensagens enviadas pela rede são convertidas primeiramente em bits pelo host emissor. Cada bit é codificado em um padrão de sons, de ondas de luz ou de impulsos elétricos, dependendo da mídia de rede em que os bits são transmitidos. O host de destino recebe e decodifica os sinais para interpretar a mensagem.                                                                                                                         |
| Encapsulamento              | Cada mensagem transmitida em uma rede deve incluir um cabeçalho com informações de endereçamento que identifique os hosts de origem e destino. Caso contrário, ela não poderá ser entregue. Encapsulamento é o processo de adicionar essas informações aos dados que compõem a mensagem. Além do endereçamento, podem existir outras informações no cabeçalho que garantem que a mensagem foi entregue ao aplicativo correto no host de destino. |
| Padrão da mensagem          | Algumas mensagens exigem uma confirmação antes que a próxima mensagem possa ser enviada. Esse tipo de padrão de solicitação/resposta é um aspecto comum em muitos protocolos de rede. No entanto, existem outros tipos de mensagens que podem ser simplesmente transmitidas pela rede, sem a preocupação de chegarem ao seu destino.                                                                                                             |


##### A Internet e os Padrões:

Com o número cada vez maior de novos dispositivos e tecnologias on-line, como é possível gerenciar todas as mudanças e continuar oferecendo serviços como e-mail de maneira confiável? A resposta está nos padrões da Internet.

Um [padrão é um conjunto de regras que determina como algo deve ser feito]. Os padrões de rede e de Internet asseguram que todos os dispositivos conectados à rede implementem o mesmo conjunto de regras ou protocolos da mesma forma. O uso de padrões permite que diferentes tipos de dispositivos enviem informações entre si pela Internet. 

Por exemplo, o modo como um e-mail é formatado, encaminhado e recebido por todos os dispositivos segue um padrão. Se uma pessoa enviar um e-mail através de um computador pessoal, outra pessoa poderá usar um celular para receber e ler o e-mail, desde que o telefone celular utilize os mesmos padrões do computador pessoal.

---

##### Encapsulamento:


Ao enviar uma carta, quem a escreve usa um formato aceito para garantir que ela seja entregue e compreendida pelo destinatário. Da mesma forma, a mensagem enviada por uma rede de computadores segue regras específicas de formato para que seja entregue e processada.

O processo de colocar um formato de mensagem (a carta) em outro formato de mensagem (o envelope) é chamado [encapsulamento]. O desencapsulamento ocorre quando o processo é invertido pelo destinatário e a carta é retirada do envelope. Assim como uma carta é colocada dentro de um envelope para ser entregue, no caso das mensagens de computador, elas são encapsuladas.

Cada mensagem de computador é encapsulada em um formato específico, chamado de [quadro - frame], antes de ser enviada pela rede. [Um quadro atua como um envelope]: ele fornece o endereço do destino desejado e o endereço do host de origem. O formato e o conteúdo de um quadro são determinados pelo tipo de mensagem que está sendo enviada e pelo canal no qual é comunicada. As mensagens que não são formatadas corretamente não são entregues ao host destino com êxito, nem processadas por ele.

---
##### Organizações de padronização de rede

Um padrão da Internet é o resultado final de um ciclo completo de discussão, solução de problemas e testes. Esses diferentes padrões são desenvolvidos, publicados e mantidos por diversas organizações, conforme mostrado na figura. 

Quando um novo padrão é proposto, cada etapa do processo de desenvolvimento e aprovação é registrada em um documento numerado de Solicitação de Comentários (Request for Comments - RFC), para que a evolução do padrão seja monitorada. As RFCs sobre padrões da Internet são publicadas e gerenciadas pelo IETF (Internet Engineering Task Force).

Outras organizações de padrões que suportam a Internet são mostradas na figura.

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc05ad2-1c25-11ea-81a0-ffc2c49b96bc.jpg)

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc05ad3-1c25-11ea-81a0-ffc2c49b96bc.jpg)

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc05ad4-1c25-11ea-81a0-ffc2c49b96bc.jpg)

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc081e0-1c25-11ea-81a0-ffc2c49b96bc.jpg)

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc081e1-1c25-11ea-81a0-ffc2c49b96bc.jpg)

![asset.description](https://contenthub.netacad.com/asset/netacad-media/media/2dc05ad0-1c25-11ea-a010-eb2108469056/assets/images/2dc081e2-1c25-11ea-81a0-ffc2c49b96bc.jpg)




