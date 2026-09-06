---
tags:
  - arquivo
---
### Características do Cabeamento de Cobre

O cabeamento de cobre é o tipo mais comum de cabeamento usado nas redes hoje em dia. Na verdade, o cabeamento de cobre não é apenas um tipo de cabo. Existem três tipos diferentes de cabeamento de cobre que são usados em situações específicas.

As redes usam mídia de cobre porque é barata, fácil de instalar e tem baixa resistência à corrente elétrica. Entretanto, [ela é limitada pela distância e interferência de sinal].

Os dados são transmitidos por cabos de cobre como pulsos elétricos. Um [detector na interface de rede de um dispositivo de destino] tem que receber um sinal que poderá ser decodificado com êxito para corresponder ao sinal enviado. No entanto, quanto mais o sinal viaja, mais ele se deteriora. Isso se chama [atenuação de sinal]. 

Por isso, todas as mídias de cobre [devem seguir limitações de distância rigorosas], conforme especificado nos padrões de orientação.

A temporização e a voltagem dos pulsos elétricos também são suscetíveis à interferência de duas fontes:

- **[Interferência eletromagnética (EMI) ou interferência de radiofrequência (RFI)]**

	Os sinais EMI e RFI podem distorcer e corromper os sinais de dados transportados pelo meio físico de cobre. Possíveis fontes de EMI e RFI são dispositivos de ondas de rádio e eletromagnéticos, como luzes fluorescentes ou motores elétricos.

- **[Crosstalk]**

	Crosstalk é um distúrbio causado pelos campos elétricos ou magnéticos de um sinal em um fio para o sinal em um fio adjacente. Nos circuitos de telefone, a diafonia pode fazer com que parte de outra conversa de voz de um circuito adjacente seja ouvida (linha cruzada). 

	Especificamente, quando uma corrente elétrica flui através de um cabo, ela cria um pequeno campo magnético circular ao redor do cabo, que pode ser captado por um cabo adjacente.


Para contrabalançar os efeitos negativos da EMI e da RFI, alguns tipos de cabos de cobre têm proteção metálica e exigem conexões devidamente aterradas.

Para contrabalançar os efeitos negativos do crosstalk, alguns tipos de cabos de cobre têm pares de cabos de circuitos opostos juntos, o que efetivamente cancela o crosstalk.

A suscetibilidade dos cabos de cobre ao ruído eletrônico também pode ser limitada usando estas recomendações:

- Selecionar o tipo ou categoria de cabo mais adequado para um determinado ambiente de rede
- Projetar uma infraestrutura de cabos para evitar fontes conhecidas e potenciais de interferência na estrutura do edifício
- Usar técnicas de cabeamento que incluem o manuseio e a terminação adequados dos cabos

---
### Tipos de cabeamento de cobre

- [Par trançado não blindado (UTP)]

O cabeamento de par trançado não blindado (UTP) é o meio físico de rede mais comum. O cabeamento UTP, terminado com conectores RJ-45, é usado para interconectar hosts de rede com dispositivos de rede intermediários, como switches e roteadores.

Nas LANs, o cabo UTP consiste em quatro pares de cabos codificados por cores que foram trançados e depois colocados em uma capa plástica flexível que protege contra danos físicos menores. O processo de trançar cabos ajuda na proteção contra interferência de sinais de outros cabos.


- [Par Trançado Blindado (STP)]

O par trançado blindado (STP) oferece maior proteção contra ruído do que o cabeamento UTP. No entanto, em comparação com o cabo UTP, o cabo STP é significativamente mais caro e de difícil instalação. Assim como o cabo UTP, o STP usa um conector RJ-45.

Os cabos STP combinam as técnicas de blindagem para contrabalançar a EMI e a RFI, e são trançados para conter o crosstalk. Para aproveitar totalmente a blindagem, os cabos STP são terminados com conectores de dados STP blindados especiais. *Se o cabo não estiver devidamente aterrado, a blindagem poderá atuar como uma antena e captar sinais indesejados.


- [Cabo Coaxial]

O cabo coaxial, ou coax para abreviar, recebeu seu nome porque tem dois condutores que compartilham o mesmo eixo. O cabo coaxial consiste no seguinte:

- Um condutor de cobre é usado para transmitir os sinais eletrônicos.

- Uma camada de isolamento plástico flexível envolve um condutor de cobre.

- O material de isolamento é envolvido em uma malha de cobre com tecido, ou uma folha metálica, que atua como o segundo cabo no circuito e uma proteção para o condutor interno. Essa segunda camada, ou blindagem, também reduz a quantidade de interferência eletromagnética externa.

- Todo o cabo é coberto com um revestimento para evitar danos físicos menores.

Há tipos diferentes de conectores utilizados com o cabo coax. Os conectores Bayonet Neill-Concelman (BNC), tipo N e tipo F.

Embora o cabo UTP tenha substituído essencialmente o cabo coaxial nas modernas instalações Ethernet, o design do cabo coaxial é usado nas seguintes situações:

- **[Instalações sem fio]** 

	Cabos coaxiais conectam antenas aos dispositivos sem fio. O cabo coaxial transporta a energia de radiofrequência (RF) entre as antenas e o equipamento de rádio.

