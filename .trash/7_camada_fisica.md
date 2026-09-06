---
tags:
  - arquivo
---
### Placas de Interface de Rede

As [placas de interface de rede] ([Network Interface Cards] - NICs) conectam um dispositivo à rede. 

As NICs Ethernet são usadas para uma conexão com fio, enquanto as NICs da rede local sem fio (WLAN) são usadas para a conexão sem fio. Um dispositivo de usuário final pode incluir um ou os dois tipos de NICs. 

---
### A Camada Física

A camada física do modelo OSI fornece os meios para transportar os bits que formam o quadro da camada de enlace de dados na mídia de rede. Essa camada aceita um quadro completo da camada de enlace de dados e o codifica como uma série de sinais que são transmitidos à mídia local. 

Os bits codificados que formam um quadro são recebidos por um dispositivo final ou por um dispositivo intermediário.

A camada física codifica os quadros e cria os sinais de onda elétrica, óptica ou de rádio que representam os bits em cada quadro. Esses sinais são então enviados pela mídia, um de cada vez.

---
### Padrões da camada física

Os protocolos e operações das camadas OSI superiores são executados usando software desenvolvido por engenheiros de software e cientistas da computação. *Os serviços e protocolos na suíte TCP/IP são definidos pela **Internet Engineering Task Force (IETF).

A camada física, por sua vez, consiste em circuitos eletrônicos, meios físicos e conectores desenvolvidos pelos engenheiros. Portanto, é aconselhável que os padrões que regem esse hardware sejam definidos pelas organizações de engenharia de comunicações e elétrica relevantes.

Há muitas organizações nacionais e internacionais diferentes, organizações reguladoras de governo e empresas privadas envolvidas no estabelecimento e na manutenção de padrões da camada física. 

Por exemplo, os padrões de hardware, mídia, codificação e sinalização da camada física são definidos e governados por essas organizações de padrões:

- Organização Internacional para Padronização (ISO)
- Instituto Nacional de Padrões Americano (ANSI) / Associação da Indústria de Telecomunicações (TIA)
- União Internacional de Telecomunicações (ITU)
- Instituto de Engenheiros Elétricos e Eletrônicos (IEEE)
- Autoridades reguladoras de telecomunicações nacionais, incluem Comissão Federal de Comunicação (FCC) nos EUA e Instituto Europeu de Padrões de Telecomunicações (ETSI)

Além desses, geralmente existem grupos regionais de padrões de cabeamento, como CSA (Associação Canadense de Padrões), CENELEC (Comitê Europeu de Padronização Eletrotécnica) e JSA / JIS (Associação Japonesa de Padrões), que desenvolvem especificações locais.

---
### Componentes Físicos

Os padrões da camada física abordam três áreas funcionais:

- Componentes Físicos
- [Codificação]:

	[Codificação ou codificação de linha é um método de conversão de um fluxo de bits de dados em um "código" predefinido]. ***Os códigos são agrupamentos de bits*** usados para fornecer um padrão previsível que pode ser reconhecido tanto pelo emissor quanto pelo receptor. 

	Em outras palavras, a codificação é o método ou o padrão usado para representar as informações digitais. É semelhante a como o código Morse codifica uma mensagem usando uma série de pontos e traços.

	Por exemplo, a codificação Manchester representa um bit 0 por uma transição de alta para baixa voltagem, e um bit 1 é representado como uma transição de baixa para alta voltagem. 

	Um exemplo de codificação Manchester é ilustrado na figura. A transição ocorre no meio de cada período de bit. 

	Taxas de dados mais rápidas exigem uma codificação mais complexa. A codificação Manchester é usada em padrões Ethernet mais antigos, como o 10BASE-T. A Ethernet 100BASE-TX usa codificação 4B/5B e 1000BASE-T usa codificação 8B/10B.

![[codificacoes.webp]]


> [!NOTE] 
> A codificação de quadro converte um fluxo de bits de dados em um código pré-definido que possa ser reconhecido pelo transmissor e pelo receptor. Esses códigos são usados para vários fins, como para diferenciar os bits de dados dos bits de controle e identificar o início e o fim de um quadro.


- **[Sinalização]**

A camada física deve gerar os sinais elétricos, ópticos ou sem fio que representam os valores “1” e “0” no meio físico. 

A maneira como os bits são representados é chamada de [método de sinalização]. Os padrões de camada física devem definir que tipo de sinal representa o valor “1” e que tipo de sinal representa o valor “0”. 

Isso pode ser tão simples quanto uma alteração no nível de um sinal elétrico ou de um pulso óptico. Por exemplo, um pulso longo pode representar um 1, enquanto um pulso curto pode representar um 0.

---
### Largura de banda

Meios físicos diferentes aceitam a transferência de bits a taxas diferentes. A transferência de dados é geralmente discutida em termos de largura de banda. [Largura de banda é a capacidade na qual um meio pode transportar dados]. 

[A largura de banda digital mede a quantidade de dados que podem fluir de um lugar para outro durante um determinado tempo].

Às vezes, a largura de banda é pensada como a velocidade em que os bits viajam, no entanto, isso não é preciso. Por exemplo, na Ethernet de 10 Mbps e 100 Mbps, os bits são enviados na velocidade da eletricidade. A diferença é o número de bits que são transmitidos por segundo.

[Uma combinação de fatores determina a largura de banda prática de uma rede], como:

- As propriedades do meio físico;
- As tecnologias escolhidas para sinalização e detecção de sinais de rede.

As propriedades do meio físico, as tecnologias atuais e as leis da física desempenham sua função na determinação da largura de banda disponível.

A tabela mostra as unidades de medida comumente usadas para largura de banda.

| Unidades de Largura de Banda | Sigla | Equivalência                   |
| ---------------------------- | ----- | ------------------------------ |
| Bits por segundo             | bps   | 1 bps                          |
| Quilobits por segundo        | Kbps  | 1 Kbps = 1,000 bps             |
| Megabits por segundo         | Mbps  | 1 Mbps = 1,000,000 bps         |
| Gigabits por segundo         | Gbps  | 1 Gbps = 1,000,000,000 bps     |
| Terabits por segundo         | Tbps  | 1 Tbps = 1,000,000,000,000 bps |

---
### Terminologia de largura de banda

Os termos usados para medir a qualidade da largura de banda incluem:

- [Latência]:

	O termo latência se refere ao tempo necessário para os dados viajarem de um ponto a outro, incluindo atrasos.

	Em uma internetwork ou em uma rede com vários segmentos, a taxa de transferência não pode ser mais rápida que o link mais lento no caminho da origem ao destino. 

	Mesmo que todos ou a maioria dos segmentos tenham alta taxa de transferência, será necessário apenas um segmento no caminho com baixa taxa de transferência para criar um gargalo em toda a rede.

- [Taxa de transferência]:

	Taxa de transferência é a medida da transferência de bits através da mídia durante um determinado período.

	Devido a alguns fatores, geralmente a taxa de transferência não corresponde à largura de banda especificada nas implementações da camada física, geralmente é menor que a largura de banda. Existem muitos fatores que influenciam a taxa de transferência:

	- A quantidade de tráfego;
	- O tipo de tráfego;
	- A latência criada pelo número de dispositivos de rede encontrados entre a origem e o destino.

- **[Goodput]**

Há uma terceira medida para avaliar a transferência de dados utilizáveis, ela é conhecida como goodput. *[Goodput é a medida de dados usáveis transferidos em um determinado período]. 

Goodput é a taxa de transferência menos a sobrecarga de tráfego para estabelecer sessões, reconhecimentos, encapsulamento e bits retransmitidos. *O goodput é sempre menor que a taxa de transferência, que geralmente é menor do que a largura de banda.