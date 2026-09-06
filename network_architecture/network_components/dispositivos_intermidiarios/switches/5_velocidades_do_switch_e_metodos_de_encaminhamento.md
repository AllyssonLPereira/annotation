---
tags:
  - arquivo
---
### Métodos de Encaminhamento de Quadros em Switches da Cisco

Como você aprendeu no tópico anterior, os switches usam suas tabelas de endereço MAC para determinar qual porta usar para encaminhar quadros. 

Com os switches Cisco, existem realmente dois métodos de encaminhamento de quadros e há boas razões para usar um em vez do outro, dependendo da situação.

Os switches usam um dos seguintes métodos de encaminhamento para o switching (comutação) de dados entre suas interfaces de rede:

- [Comutação Armazenar e encaminhar] (Store-and-forward switching ):

	Este método de encaminhamento de quadros recebe o quadro inteiro e calcula o CRC. O CRC usa uma fórmula matemática, baseada no número de bits (valores 1) no quadro para determinar se o quadro recebido apresenta erro. 

	Se o CRC é válido, o switch procura o endereço de destino, que determina a interface de saída. Em seguida, o quadro é encaminhado pela porta correta.

- [Comutação corte direto] (Cut-through switching):

	Esse método de encaminhamento de quadros encaminha o quadro antes de ser totalmente recebido. Pelo menos o endereço de destino do quadro deve ser lido para que o quadro possa ser encaminhado.


Uma grande vantagem da Comutação Armazenar e encaminhar é que ele determina se um quadro tem erros antes de propagar o quadro. Quando um erro é detectado em um quadro, o switch o descarta. 

O descarte de quadros com erros reduz o consumo de largura de banda por dados corrompidos. [A comutação Armazenar e encaminhar é necessária para a análise de qualidade de serviço (QoS)] em redes convergentes onde a classificação de quadros para priorização de tráfego é necessária. 

> Por exemplo, os fluxos de dados de voz sobre IP (VoIP) precisam ter prioridade sobre o tráfego de navegação na web.

---
### Comutação corte direto


Na comutação corte direto, o switch atua nos dados assim que eles são recebidos, mesmo que a transmissão não tenha sido concluída. 

[O switch armazena em buffer apenas a parte do quadro suficiente para ler o endereço MAC de destino] para que possa determinar para qual porta ele deve encaminhar os dados. ***Ou seja, ele armazena em buffer o endereço MAC de destino.

> O endereço MAC de destino está localizado nos primeiros 6 bytes do quadro após o preâmbulo. O switch consulta o endereço MAC de destino na tabela de comutação, determina a porta da interface de saída e encaminha o quadro ao seu destino pela porta de switch designada. 

*O switch não realiza nenhuma verificação de erros no quadro.

Há duas formas de comutação corte direto:

- [Comutação avanço rápido - Fast-forward switching]:

	A comutação avanço rápido oferece o menor nível de latência e encaminha imediatamente um pacote depois de ler o endereço de destino. 

	Como a comutação avanço rápido começa o encaminhamento antes de receber todo o pacote, alguns pacotes podem ser retransmitidos com erros. 

	Isso ocorre com pouca frequência e a NIC de destino descarta o pacote com defeito após o recebimento. 

	No modo avanço rápido, a latência é medida do primeiro bit recebido até o primeiro bit transmitido. *Comutação avanço rápido é o método corte direto típico de comutação.


- [Comutação livre de fragmentos - Fragment-free switching]:

	Na comutação livre de fragmentos, o switch armazena os primeiros 64 bytes do quadro antes de encaminhar. Esse tipo de comutação pode ser encarado como um compromisso entre o switching armazenar e encaminhar e o switching avanço rápido. 

	*O motivo da comutação livre de fragmentos armazenar somente os primeiros 64 bytes do quadro é que a maioria dos erros e das colisões de rede ocorre durante os primeiros 64 bytes. 

	A comutação livre de fragmentos tenta melhorar a comutação avanço rápido executando uma pequena verificação de erros nos primeiros 64 bytes do quadro para garantir que não ocorra uma colisão antes de encaminhar o quadro. 

	A comutação livre de fragmentos é um compromisso entre a alta latência e a alta integridade da comutação armazenar e encaminhar e a baixa latência e a integridade reduzida da comutação avanço rápido.


Alguns switches são configurados para executar a comutação corte direto por porta até que um limite de erro definido pelo usuário seja atingido e, depois, mudam automaticamente para armazenar e encaminhar. 

Quando a taxa de erros fica abaixo do limite, a porta retorna automaticamente para a comutação corte direto.

---
### Buffer de Memória em Switches


Um switch Ethernet pode usar uma técnica de armazenamento de quadros em buffers antes de enviá-los.

O buffer também pode ser usado quando a porta de destino está ocupada devido ao congestionamento. O switch armazena o quadro até a porta ficar livre.

| Método                | Descrição                                                                                                                                                                                                                                                                                                                                                            |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Memória por porta     | Os quadros são armazenados em filas vinculadas a portas específicas de entrada e saída. Um quadro é transmitido para a porta de saída se, e somente se, os quadros à frente na fila forem transmitidos com êxito.                                                                                                                                                    |
| Memória compartilhada | Deposita todos os quadros em um buffer de memória comum a todas as portas do switch. A quantidade de memória necessária para cada porta é alocada dinamicamente. Os quadros no buffer são dinamicamente vinculados à porta de destino, permitindo que um pacote seja recebido em uma porta e depois transmitido em outra porta, sem movê-lo para uma fila diferente. |


O buffer de memória compartilhada também resulta na capacidade de armazenar quadros maiores com, potencialmente, menos perda de quadros. Isso é importante para a comutação assimétrica, que permite taxas de dados diferentes em portas diferentes, como ao conectar um servidor a uma porta de switch de 10 Gbps e PCs a portas de 1 Gbps.

---
### Configurações de Velocidade e Duplex


Duas das configurações mais básicas em um switch são as configurações de *largura de banda* (às vezes denominada "velocidade") e *duplex* para cada porta do switch individual. É fundamental a correspondência dessas configurações na porta do switch e nos dispositivos conectados, como um computador ou outro switch.

Há dois tipos de configurações duplex usadas para comunicação em uma rede Ethernet:

- [Duplex completo]

	As duas extremidades da conexão podem enviar e receber ao mesmo tempo.

- [Meio duplex]

	Somente uma das extremidades da conexão pode enviar e receber por vez.

A negociação automática é uma função opcional encontrada na maioria dos switches Ethernet e das placas de interface de rede (NICs). Ela permite que dois dispositivos negociem automaticamente as melhores capacidades de velocidade e duplex. 

Duplex completo será escolhido se os dois dispositivos tiverem essa capacidade e com a largura de banda mais alta em comum entre eles.

> [!NOTE]
> A maioria dos switches Cisco e das NICs Ethernet faz a negociação automática por padrão para velocidade e duplex. Portas Gigabit Ethernet só operam em duplex completo.
> 

*A incompatibilidade duplex é uma das causas mais comuns de problemas de desempenho nos links Ethernet 10/100 Mbps*. Ocorre quando uma porta no link opera em Meio duplex, enquanto a outra porta opera em duplex completo.

---
### MDIX automático

As conexões entre dispositivos exigiram uma vez o uso de um cabo cruzado ou direto. O tipo de cabo necessário dependia do tipo de dispositivos de interconexão.

> Por exemplo, um cabo cruzado é usado ao conectar dispositivos semelhantes, e um cabo direto é usado para conectar dispositivos diferentes.

> [!NOTE]
> Uma conexão direta entre um roteador e um host requer uma conexão cruzada.

A maioria dos dispositivos de switch agora suporta o recurso de (Auto-MDIX) interface dependente automática. Quando ativado, o switch detecta automaticamente o tipo de cabo conectado à porta e configura as interfaces de acordo. 

Com isso, você pode utilizar um cabo cruzado ou direto para conexões a uma porta 10/100/1000 de cobre no switch, seja qual for o tipo de dispositivo na outra extremidade da conexão.

Mas o recomendado, pelo menos para alguns dispositivos Cisco, é usar o cabo correto.