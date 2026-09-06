---
tags:
  - arquivo
---
## Introdução

A base do funcionamento da fibra óptica reside no princípio físico da reflexão interna total, um fenômeno que ocorre quando a luz viaja através de um meio com alto índice de refração e encontra a interface de um meio com índice de refração inferior. 

Conforme documentado pela IBM e em currículos acadêmicos de engenharia, a fibra é construída com um núcleo central de vidro puríssimo cercado por uma camada denominada casca ou revestimento (cladding). 

Para que a luz permaneça confinada ao núcleo, o índice de refração do vidro central deve ser superior ao da casca. Assim, quando os pulsos de luz são injetados na fibra em um ângulo específico, chamado de ângulo crítico, eles não atravessam a casca, mas são refletidos continuamente de volta para o interior do núcleo. 

Esse mecanismo transforma a fibra em um guia de ondas ou "tubo de luz" altamente eficiente, permitindo que a informação seja transportada por vastas distâncias com uma perda de sinal, ou atenuação, extremamente reduzida se comparada aos cabos metálicos.

![[licensed-image (1) 1.jpeg]]

A eficácia dessa transmissão é ampliada pela natureza do material utilizado, geralmente sílica fundida, que é processada para atingir uma transparência tal que um bloco de quilômetros de espessura seria mais claro que um vidro de janela comum. 

Além da eficiência na propagação da luz, essa estrutura garante a imunidade total a interferências eletromagnéticas (EMI) e de radiofrequência (RFI), uma vez que fótons, ao contrário de elétrons, não sofrem influência de campos magnéticos externos. Essa característica técnica permite que os cabos de fibra óptica sejam instalados próximos a redes de alta tensão ou em ambientes industriais ruidosos sem que haja degradação do sinal ou necessidade de blindagens complexas, como as exigidas em cabos de cobre de categoria superior.

## Classificação - SMF e MMF

No que tange à classificação técnica, a fibra óptica divide-se primordialmente em dois tipos baseados em como a luz se propaga em seu interior: monomodo (SMF) e multimodo (MMF). 

### SMF - Single Mode Fiber

A fibra monomodo caracteriza-se por possuir um núcleo extremamente estreito, com diâmetro variando tipicamente entre 8 a 10 mícrons. Essa dimensão reduzida obriga a luz a seguir um único caminho ou "modo" de propagação, o que elimina quase completamente a dispersão modal. 

Como resultado, todos os pulsos de luz chegam ao destino praticamente ao mesmo tempo, permitindo que a fibra monomodo suporte larguras de banda imensas por distâncias que podem ultrapassar os 100 quilômetros sem a necessidade de repetidores. 

Para alimentar esse tipo de fibra, utilizam-se fontes de luz laser, que possuem uma emissão concentrada e coerente, justificando sua aplicação em backbones de operadoras, redes metropolitanas e conexões de longa distância.

![[Single Mode Fiber Optic_0.gif]]
### MMF - Multi Mode Fiber

Em contraste, a fibra multimodo possui um núcleo significativamente maior, geralmente de 50 ou 62,5 mícrons, o que facilita a entrada da luz a partir de fontes menos precisas e mais econômicas, como LEDs ou lasers de cavidade vertical (VCSEL). 

Devido ao diâmetro ampliado, a luz entra na fibra em diversos ângulos, percorrendo múltiplos caminhos ou modos ao longo do núcleo. Esse comportamento físico gera o fenômeno da dispersão modal, onde os raios de luz que viajam por trajetórias mais longas (refletindo mais vezes nas paredes da casca) chegam ligeiramente depois daqueles que seguem um caminho mais direto.

Essa diferença de tempo no recebimento dos pulsos causa um alargamento do sinal que limita a distância útil da fibra multimodo a poucos quilômetros, sendo o padrão ouro para infraestruturas internas de edifícios, redes locais (LANs) e interconexões dentro de Data Centers, onde o custo reduzido dos equipamentos ópticos compensa a limitação de alcance.

![[Multi Mode Fiber Optic_0.gif]]

Por fim, a física da luz aplicada a esses dois tipos de fibras reflete-se na padronização visual e operacional do setor. A Cisco e outras entidades normatizadoras definem cores específicas para os revestimentos externos para evitar erros críticos de compatibilidade: o amarelo identifica universalmente os patch cords monomodo, enquanto o laranja ou aqua (para padrões mais novos como OM3/OM4) sinaliza as fibras multimodo. 

A distinção detalhada entre esses dois tipos de fibra não é apenas uma questão de distância, mas de engenharia de custos e requisitos de largura de banda, onde a escolha correta do tipo de fibra e do comprimento de onda da luz utilizada define a estabilidade e a escalabilidade de toda a infraestrutura de rede corporativa.


## Multiplexação

A evolução da capacidade de transmissão em redes de fibra óptica é impulsionada pela tecnologia de Multiplexação por Divisão de Comprimento de Onda (WDM). Esse processo permite que múltiplos fluxos de dados sejam transmitidos simultaneamente através de uma única fibra, utilizando diferentes comprimentos de onda de luz, ou "cores", para cada sinal.

Conforme detalhado pela Cisco e por fornecedores de infraestrutura de alta performance, o WDM funciona de forma análoga a um prisma que separa a luz branca em seu espectro; no transmissor, um multiplexador combina vários sinais de luz em uma única fibra, enquanto no receptor, um demultiplexador os separa novamente.

A variante mais avançada, o Dense WDM (DWDM), utiliza um espaçamento extremamente estreito entre os comprimentos de onda, permitindo agrupar mais de 80 canais independentes em um único par de fibras. Isso resulta em capacidades de transmissão na ordem de Terabits por segundo, permitindo que provedores de serviços aumentem drasticamente a largura de banda sem a necessidade onerosa de lançar novos cabos físicos no solo ou no oceano.

## Segurança

Sob a perspectiva de segurança de rede defendida pela Fortinet, a fibra óptica oferece vantagens estruturais inerentes que superam significativamente o cabeamento de cobre. Diferente dos cabos metálicos, que emitem radiação eletromagnética e podem ser "escutados" por meio de indução sem que haja contato físico direto, a fibra óptica confina totalmente o sinal luminoso dentro de seu núcleo devido à reflexão interna total. 

Essa ausência de emissão eletromagnética torna virtualmente impossível a interceptação passiva de dados ao longo do trajeto do cabo. Além disso, qualquer tentativa de realizar uma derivação física ou "grampo" (tap) na fibra exige a curvatura excessiva ou o corte do filamento, o que inevitavelmente causa uma queda imediata e mensurável na potência do sinal, conhecida como atenuação.

Com isso, sistemas de monitoramento óptico modernos iriam detectar essa variação de potência instantaneamente, permitindo que a rede identifique a tentativa de intrusão e dispare alertas automáticos, tornando a fibra um componente ativo na arquitetura de segurança física da informação.

## Conectores

A integridade operacional de uma infraestrutura óptica depende rigorosamente de práticas de manutenção e do uso correto de componentes de conexão, conforme os padrões estabelecidos pela Cisco Networking Academy.

Os conectores mais comuns no mercado atual incluem o:

- ST (Straight-Tip), com seu encaixe de baioneta;
- SC (Subscriber Connector), conhecido pelo mecanismo quadrado push-pull; e 
- LC (Lucent Connector), que é amplamente adotado em ambientes de alta densidade devido ao seu tamanho reduzido (Small Form Factor). 

A precisão na conexão é um fator crítico, pois a face final da fibra deve estar perfeitamente alinhada para evitar a perda de inserção. A presença de partículas microscópicas de poeira ou óleos corporais na ponta do conector pode bloquear o caminho da luz ou causar a Reflexão de Retorno Óptico (ORL), onde a luz é refletida de volta para a fonte, podendo degradar o sinal ou danificar permanentemente os transceptores laser.

Para mitigar falhas operacionais e garantir a longevidade dos equipamentos, o uso de capas protetoras de plástico é obrigatório sempre que os cabos não estiverem em uso. Complementarmente, a padronização visual por cores é utilizada universalmente para evitar erros de conexão entre tecnologias incompatíveis. 

O revestimento externo amarelo identifica cabos monomodo (SMF), adequados para longas distâncias, enquanto o laranja ou aqua (para padrões OM3 e OM4) sinaliza cabos multimodo (MMF), destinados a redes locais e data centers.

Respeitar essa codificação e os procedimentos de limpeza a seco ou com solventes específicos é fundamental para sustentar as taxas de transferência nominais e a estabilidade do link óptico em ambientes corporativos de missão crítica.