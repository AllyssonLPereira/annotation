---
tags:
  - arquivo
---
### Par trançado não blindado (UTP)

O cabeamento de par trançado não blindado (UTP) é o meio físico de rede mais comum. O cabeamento UTP, terminado com conectores RJ-45, é usado para interconectar hosts de rede com dispositivos de rede intermediários, como switches e roteadores.

Nas LANs, o cabo UTP consiste em quatro pares de cabos codificados por cores que foram trançados e depois colocados em uma capa plástica flexível que protege contra danos físicos menores. *O processo de trançar cabos ajuda na proteção contra interferência de sinais de outros cabos.

---
### Propriedades do Cabo UTP

Quando usado como meio de rede, o cabeamento UTP consiste em quatro pares de fios de cobre com código de cores que foram torcidos juntos e depois envoltos em uma bainha de plástico flexível. Seu tamanho reduzido pode ser vantajoso durante a instalação.

[O cabo UTP não usa blindagem para contrabalançar os efeitos de EMI e RFI]. Em vez disso, os projetistas de cabos descobriram outras maneiras de limitar o efeito negativo da diafonia:

- **[Cancelamento]** 

	***Os designers agora dispõe os fios em um circuito em pares***. Quando dois fios de um circuito elétrico são colocados próximos um do outro, seus campos magnéticos serão opostos. *Assim, os dois campos magnéticos cancelam um ao outro e também podem cancelar sinais externos de EMI e RFI.

- **[Variando o número de torções por par de fios]** 

	*Para aumentar ainda mais o efeito de cancelamento de fios de circuitos pareados, os projetistas variam o número de torções de cada par de fios em um cabo*. 

	O cabo UTP deve seguir especificações precisas que orientam quantas tranças são permitidas por metro (3,28 pés) do cabo. O par laranja/laranja e branco é menos trançado do que o par azul/azul e branco. Cada par colorido é trançado um número de vezes diferente.
	

O cabo UTP depende exclusivamente do efeito de cancelamento produzido pelos pares de fios trançados para limitar a degradação de sinal e fornecer efetivamente a autoblindagem para cabos trançados na mídia de rede.

---
### Padrões de Cabeamento e Conectores UTP

O cabeamento UTP está em conformidade com os padrões estabelecidos conjuntamente pela [ANSI/TIA]. Especificamente, o [ANSI/TIA-568] estipula os padrões de cabeamento comercial para instalações de LAN e é o padrão mais comumente usado em ambientes de cabeamento de LAN. Alguns dos elementos definidos são os seguintes:

- Tipos de cabo
- Comprimento do cabo
- Conectores
- Terminação do cabo
- Métodos de teste de cabo

As características elétricas do cabeamento de cobre são definidas pelo Instituto de Engenharia Elétrica e Eletrônica (IEEE). O IEEE classifica o cabeamento UTP de acordo com o desempenho. Os cabos são colocados nas categorias, com base na capacidade de transportar taxas de largura de banda mais altas. 

Por exemplo, o cabo Categoria 5 é usado normalmente em instalações 100BASE-TX Fast Ethernet. Outras categorias incluem cabo Categoria 5 aprimorado (5e), Categoria 6 e Categoria 6a.

Os cabos em categorias mais altas são desenvolvidos e construídos para suportar taxas de dados mais elevadas. 

À medida que novas tecnologias Ethernet de velocidade de gigabit estão sendo desenvolvidas e adotadas, a Categoria 5e é agora o tipo de cabo minimamente aceitável, com a Categoria 6 sendo o tipo recomendado para novas instalações prediais.

Alguns fabricantes produzem cabos que excedem as especificações da Categoria ANSI/TIA 6a e os classificam como Categoria 7.

---
### RJ-45

O cabo UTP geralmente é terminado com um conector RJ-45. O padrão ANSI/TIA-568 descreve os códigos de cores dos fios, para atribuições de pinos (pinagem), para cabos Ethernet.

O conector RJ-45 é o componente macho, prensado na extremidade do cabo. Já o soquete é o componente fêmea de um dispositivo de rede, tomada de parede, tomada de conduíte ou painel de conexões. 

Quando terminado incorretamente, o cabo é uma fonte potencial de degradação do desempenho da camada física.

> [!NOTE] 
> A terminação inadequada do cabo pode afetar o desempenho da transmissão.

---
### Cabos UTP diretos e cruzados

Situações diversas podem exigir que os cabos UTP sejam conectados de acordo com diferentes convenções de fiação. Isso significa que os fios individuais do cabo precisam ser conectados em ordem diferente para conjuntos diferentes de pinos nos conectores RJ-45.

Estes são os principais tipos de cabo obtidos com o uso de convenções de cabeamento específicas:

- **[Ethernet direto]**

	O tipo mais comum de cabo de rede. Geralmente é usado para interconectar um host a um switch e um switch a um roteador.

- **[Ethernet Cruzado (Crossover)]**

	Um cabo usado para [interconectar dispositivos semelhantes]. Por exemplo, para conectar um switch a um switch, um host a um host ou um roteador a um roteador. 

	No entanto, os cabos cruzados agora são considerados legados, pois as NICs usam o cruzamento de interface dependente médio [(Auto-MDIX)] para detectar automaticamente o tipo de cabo e fazer a conexão interna.


![[ORDEM-CABO-DE-REDE.webp]]

> [!NOTE]
> Outro tipo de cabo é o cabo rollover, que é proprietário da Cisco. É usado para conectar uma estação de trabalho a uma porta do console do roteador ou do switch.

[O uso incorreto de um cabo crossover ou direto entre dois dispositivos não danifica os dispositivos, mas a conectividade e comunicação entre os dispositivos não será realizada]. Este é um erro comum e verificar se as conexões do dispositivo estão corretas deve ser a primeira ação de solução de problemas se a conectividade não for alcançada.

---
### Função dos fios em redes Fast Ethernet (100 Mbps - 100BASE-TX)

Nos cabos CAT5e e superiores, em redes 100 Mbps, [apenas dois pares (4 fios) são usados para transmissão de dados], enquanto os outros dois pares ficam reservados para futuras expansões ou são usados para alimentação em dispositivos PoE (Power over Ethernet).

| Pino | Cor do Fio (T568B) | Função                          |
| ---- | ------------------ | ------------------------------- |
| 1    | Branco/Laranja     | Transmissão + (TX+)             |
| 2    | Laranja            | Transmissão - (TX-)             |
| 3    | Branco/Verde       | Recepção + (RX+)                |
| 6    | Azul               | Não usado (PoE em alguns casos) |
| 4    | Branco/Azul        | Não usado (PoE em alguns casos) |
| 5    | Verde              | Recepção - (RX-)                |
| 7    | Branco/Marrom      | Não usado (PoE em alguns casos) |
| 8    | Marrom             | Não usado (PoE em alguns casos) |

---
### Função dos fios em redes Gigabit Ethernet (1000 Mbps - 1000BASE-T)

Nas redes Gigabit Ethernet (1000 Mbps), todos os 8 fios são utilizados para transmissão e recepção de dados simultaneamente.

| Pino | Cor do Fio (T568B) | Função |
| ---- | ------------------ | ------ |
| 1    | Branco/Laranja     | Dados  |
| 2    | Laranja            | Dados  |
| 3    | Branco/Verde       | Dados  |
| 4    | Azul               | Dados  |
| 5    | Branco/Azul        | Dados  |
| 6    | Verde              | Dados  |
| 7    | Branco/Marrom      | Dados  |
| 8    | Marrom             | Dados  |

---
### Power over Ethernet (PoE)

Em redes que utilizam PoE, os fios não usados na transmissão de dados em 100 Mbps (pinos 4, 5, 7 e 8) podem ser utilizados para fornecer energia elétrica para dispositivos como câmeras IP, telefones VoIP e pontos de acesso Wi-Fi.