
## Propriedades físicas e a atenuação do sinal

O cabeamento de cobre é amplamente adotado em infraestruturas de rede devido à sua condutividade superior, apresentando baixa resistência à corrente elétrica, além de ser uma solução de baixo custo e alta maleabilidade para instalação. Contudo, a transmissão de dados através de pulsos elétricos é inerentemente limitada por fenômenos físicos, sendo a atenuação o mais crítico.

A atenuação consiste na perda gradativa da intensidade do sinal conforme ele percorre o condutor, o que exige o cumprimento de normas rígidas de distância para garantir que o dispositivo de destino decodifique os dados sem erros. Pelos padrões internacionais, o limite máximo para um segmento de rede é de 100 metros, divididos tecnicamente em 90 metros de cabo de instalação (link permanente) e 10 metros destinados aos cabos de manobra (patch cords). 

Caso a distância necessária ultrapasse esse limite, torna-se obrigatória a implementação de repetidores ou extensores para regenerar o sinal e permitir segmentos adicionais.

## Vulnerabilidades e interferências externas

A sinalização elétrica em meios de cobre é altamente suscetível a ruídos externos que podem distorcer ou corromper os pacotes de dados. A Interferência Eletromagnética (EMI) e a Interferência de Radiofrequência (RFI) são causadas por dispositivos que emitem ondas eletromagnéticas ou de rádio, como motores elétricos, sistemas de iluminação fluorescente e equipamentos de transmissão sem fio. 

Além das fontes externas, existe o Crosstalk (ou diafonia), que é a interferência causada pelos campos elétricos ou magnéticos de um sinal em um fio sobre o sinal do fio adjacente dentro do mesmo cabo. Um tipo específico de monitoramento técnico para esse fenômeno é o NEXT (_Near-End Crosstalk_), que mede o desacoplamento dos pares para assegurar que a indução mútua não comprometa a largura de banda disponível.

---

# Arquitetura e categorização das mídias de cobre

### UTP e a técnica de cancelamento

O cabo UTP é a mídia mais utilizada em redes locais (LANs) modernas, sendo comumente terminado com conectores RJ-45. Sua construção interna baseia-se em quatro pares de fios de cobre isolados e trançados entre si. 

A principal defesa do UTP contra interferências não é uma barreira física, mas sim a técnica de cancelamento. Ao dispor os fios em pares, os engenheiros garantem que os campos magnéticos gerados por cada fio sejam opostos, resultando na anulação mútua de ruídos internos e externos. 

Para potencializar essa proteção e evitar o crosstalk, cada par de fios dentro do cabo possui um número diferente de torções por metro, garantindo que os sinais de pares distintos não se sincronizem e causem interferência mútua.

### STP e critérios de aterramento

Para ambientes com níveis extremos de EMI e RFI, como plantas industriais, o cabo STP é a solução técnica adequada. 

Ele combina as propriedades do trançamento com camadas adicionais de blindagem, que podem ser folhas metálicas envolvendo cada par ou uma malha de cobre tecida que envolve todo o conjunto de fios. Essa proteção atua como uma gaiola de Faraday, bloqueando ruídos externos antes que atinjam os condutores internos. 

No entanto, a eficiência do STP depende obrigatoriamente de um aterramento correto através de conectores blindados especiais. Caso o sistema não esteja devidamente aterrado, a blindagem metálica pode passar a atuar como uma antena, captando sinais indesejados e injetando ruído diretamente na rede, o que anula sua finalidade original.

### O design axial e o papel do cabo coaxial

Embora tenha sido amplamente substituído pelo UTP nas instalações Ethernet devido à complexidade de manuseio e custo, o cabo coaxial ainda desempenha funções vitais em sistemas de radiofrequência e redes de banda larga.

Sua estrutura axial consiste em quatro camadas: um condutor central de cobre para a transmissão de sinais, um isolante plástico flexível, uma blindagem de malha ou folha metálica que serve como segundo condutor e proteção contra EMI, e um revestimento externo protetor.

![[00100000000030219001.jpg]]

Este design permite que o cabo transporte energia de radiofrequência com alta eficiência entre antenas e equipamentos de rádio. No mercado, os conectores mais comuns para essa mídia incluem o BNC (tipo baioneta), o Tipo N e o Tipo F, cada um aplicado conforme a necessidade de vedação ou frequência do sinal transmitido.


---


## Padronização UTP e configuração de conectividade

O cabeamento de par trançado não blindado utiliza o conector RJ-45 como interface padrão, exigindo a disposição precisa dos condutores internos para garantir a continuidade do sinal. A norma TIA/EIA define dois padrões de pinagem, T568A e T568B, sendo este último o mais amplamente adotado em infraestruturas modernas. 

É tecnicamente vital que o trançamento dos fios seja mantido o mais próximo possível do ponto de terminação no conector, pois a desfazia excessiva dos pares na extremidade aumenta drasticamente a suscetibilidade ao Near-End Crosstalk (NEXT), degradando a performance do link.


![[licensed-image.jpeg]]


A funcionalidade dos fios dentro do cabo varia conforme a tecnologia de rede aplicada. Em redes Fast Ethernet (100BASE-TX), operando a 100 Mbps, apenas dois dos quatro pares são efetivamente utilizados para dados: o par laranja (pinos 1 e 2) atua na transmissão de sinais, enquanto o par verde (pinos 3 e 6) é responsável pela recepção, permanecendo os pares azul e marrom inativos ou disponíveis para aplicações como Power over Ethernet (PoE) em versões simplificadas. 

Em contrapartida, as redes Gigabit Ethernet (1000BASE-T) otimizam a infraestrutura utilizando os oito fios simultaneamente para a transmissão e recepção bidirecional de dados. Essa operação plena exige cabos de maior qualidade e conectores que suportem frequências mais elevadas para gerir o tráfego de 1 Gbps sem erros de colisão interna.

![[Screenshot_20260422-125221_Brave.jpg]]


### MDIX (Medium Dependent Interface Crossover)

A tecnologia **MDIX** (Medium Dependent Interface Crossover) é uma variação da interface física (MDI) utilizada em redes Ethernet que define como os pares de fios de um cabo de cobre são mapeados nos pinos do conector RJ-45. Essa distinção é fundamental para garantir que o sinal de transmissão ($TX$) de um dispositivo seja corretamente entregue ao pino de recepção ($RX$) do dispositivo remoto.

### Diferenciação MDI e MDIX

Originalmente, as interfaces de rede eram classificadas em dois tipos distintos para permitir a comunicação direta via cabos de rede comuns (diretos). Os dispositivos finais, como estações de trabalho (PCs), servidores e interfaces de roteadores, utilizam portas do tipo **MDI**. Nestas portas, os pinos 1 e 2 são dedicados à transmissão de dados ($TX$), enquanto os pinos 3 e 6 são dedicados à recepção ($RX$).

Em contrapartida, dispositivos intermediários, como switches e hubs, utilizam portas do tipo **MDIX**. Nestas interfaces, a configuração é internamente invertida: os pinos 1 e 2 recebem dados ($RX$) e os pinos 3 e 6 transmitem dados ($TX$). 

Essa alternância interna permite que um cabo "direto" (straight-through) conecte um PC a um switch, pois os pinos de transmissão do PC (1 e 2) alinham-se naturalmente com os pinos de recepção do switch (1 e 2).

### Necessidade de cabos cruzados (Crossover)

A complicação técnica ocorria ao conectar dois dispositivos do mesmo tipo (como dois switches ou dois computadores diretamente). Se ambos utilizassem portas MDI, ambos tentariam transmitir pelos pinos 1 e 2 e receber pelos pinos 3 e 6, resultando em uma colisão elétrica e falha total no link.

Para solucionar isso, antes da popularização da tecnologia automática, era necessário o uso de um **cabo cruzado (crossover)**. Neste cabo, os pares de transmissão em uma extremidade são fisicamente cruzados para os pinos de recepção na outra extremidade (conectando os pinos 1 e 2 de um lado aos pinos 3 e 6 do outro). Isso cruzava manualmente o sinal, simulando a inversão que uma porta MDIX faria.

### O mecanismo Auto-MDIX

A tecnologia moderna eliminou a necessidade de diferenciar cabos diretos de cruzados através do **Auto-MDIX**. Este recurso, integrado na camada física (PHY) da interface de rede, utiliza um algoritmo para detectar automaticamente a configuração de pinagem do dispositivo na outra ponta do cabo.

Durante o processo de negociação do link, a interface testa as combinações de sinais. Se detectar que os sinais de transmissão estão chegando nos pinos de transmissão (configuração incorreta para um cabo direto entre dispositivos iguais), o chip controlador inverte internamente as funções das trilhas de recepção e transmissão.

Para que o Auto-MDIX funcione corretamente, as seguintes condições devem ser atendidas:

- **Auto-negociação habilitada:** O recurso geralmente depende que a velocidade e o modo duplex estejam em modo "auto". Se a velocidade for forçada manualmente em ambos os lados, o Auto-MDIX pode falhar em alguns chipsets mais antigos.
    
- **Padrão IEEE:** O Auto-MDIX tornou-se obrigatório a partir do padrão Gigabit Ethernet (1000BASE-T), o que explica por que quase não se utilizam mais cabos cruzados em infraestruturas atuais, independentemente do tipo de dispositivo conectado.

### Categorias de performance e evolução da largura de banda

A classificação dos cabos de rede em categorias define a capacidade de vazão e a frequência máxima de operação, funcionando como uma analogia a rodovias com diferentes números de faixas. A Categoria 5 (Cat 5), atualmente considerada obsoleta, suportava apenas 100 Mbps em frequências de 100 MHz. 

Ela foi sucedida pela Categoria 5e (Enhanced), que introduziu especificações mais rigorosas para reduzir o crosstalk, permitindo o suporte estável a redes de 1 Gbps (Gigabit Ethernet) mantendo a mesma frequência de 100 MHz. O Cat 5e continua sendo a escolha de base para instalações residenciais e comerciais simples devido ao seu equilíbrio entre custo e desempenho.

Para demandas de maior desempenho, a Categoria 6 (Cat 6) opera em frequências de até 250 MHz e suporta taxas de 10 Gbps em distâncias reduzidas, geralmente entre 37 e 55 metros, dependendo do nível de interferência no ambiente. 

Fisicamente, os cabos Cat 6 costumam incluir um separador plástico central (spline) que isola os pares uns dos outros, reduzindo significativamente a diafonia. Já a Categoria 6A (Augmented) dobra a frequência de operação para 500 MHz e é projetada especificamente para sustentar 10 Gbps ao longo de toda a extensão de 100 metros do canal de cabeamento.

Em patamares superiores, as Categorias 7 e 8 elevam as frequências para 600 MHz e 2 GHz, respetivamente, com o Cat 8 sendo capaz de atingir taxas de 25 a 40 Gbps, embora sua aplicação seja restrita a distâncias curtas, como em interconexões de switches dentro de racks de Data Centers. Independentemente da categoria, a regra de ouro do cabeamento estruturado permanece a divisão de 90 metros de cabo rígido horizontal e 10 metros de cabos flexíveis de manobra para assegurar a integridade do link.