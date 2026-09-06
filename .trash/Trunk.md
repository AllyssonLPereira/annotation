## Link Trunk

Imagine um cenário onde a estrutura da sua rede cresceu e agora os mesmos departamentos estão divididos entre blocos ou andares diferentes, exigindo o uso de mais de um switch físico. Se mantivermos a lógica de utilizar apenas portas de acesso para interconectar esses switches, seremos obrigados a passar um cabo físico dedicado para cada VLAN configurada no ambiente.

Para atender três VLANs, seriam necessários três cabos interligando os switches; se a empresa expandisse para trinta VLANs, gastaríamos trinta interfaces físicas apenas para conectar um switch ao outro, o que inviabiliza o projeto devido ao desperdício de portas e ao custo de cabeamento.

A porta trunk resolve essa limitação física permitindo que o tráfego de múltiplas VLANs seja transportado simultaneamente através de um único link físico. 

![[frame-forwarding-over-trunk-link.gif]]

Diferente da porta de acesso, que pertence estritamente a uma única rede virtual e trabalha com quadros comuns, a interface trunk funciona como um canal compartilhado entre os ativos da rede. Isso permite que os switches consolidem todo o tráfego que precisa trafegar entre os equipamentos em conexões únicas de alta velocidade, otimizando a infraestrutura física e garantindo o isolamento lógico das sub-redes sem exigir hardware extra.

## IEEE 802.1Q

Para que esse link compartilhado funcione sem misturar as informações de setores distintos, o switch de origem precisa marcar os dados antes de enviá-los pelo tronco.

O padrão da indústria utilizado para realizar esse processo é o IEEE 802.1Q, também conhecido no dia a dia como dot1q. Quando um quadro Ethernet convencional está prestes a sair por uma porta Trunk, o switch intercepta essa estrutura e injeta uma etiqueta (ou _tag_) de 4 bytes (32 bits) diretamente no cabeçalho original, posicionando-a especificamente entre o campo de endereço MAC de Origem e o campo de Tipo/Comprimento.

Essa etiqueta inserida é dividida tecnicamente em duas partes principais: o TPID (Tag Protocol Identifier) e o TCI (Tag Control Information). 

O campo TPID consome os primeiros 16 bits da etiqueta e carrega sempre o valor hexadecimal fixo 0x8100. Quando o switch posicionado na outra ponta do link recebe o pacote e lê esse código específico bem no local onde esperava encontrar o campo de Tipo padrão, ele entende na hora que está processando um quadro modificado pelo protocolo 802.1Q e que deve analisar os bits seguintes para processar a VLAN.

Os 16 bits restantes pertencem ao bloco TCI, que dita o comportamento do quadro através de três subcampos específicos. 

- Os primeiros 3 bits compõem o PCP (Priority Code Point), utilizado para classificação de Qualidade de Serviço (QoS) para priorizar tráfegos críticos, como voz ou vídeo, quando a rede estiver saturada.

- O bit seguinte é o DEI (Drop Eligible Indicator), que serve para marcar quadros de menor importância que podem ser descartados em cenários de congestionamento extremo. 

- Por fim, os últimos 12 bits formam o VID (VLAN ID), que armazena a numeração exata da VLAN de origem, garantindo que o switch receptor saiba exatamente a qual domínio de broadcast aquela informação pertence.

![[Ethernet_802.1Q_Insert.svg.png]]

## Divisão de faixas de VLAN

Como o campo VID no cabeçalho 802.1Q possui exatamente 12 bits dedicados à identificação da rede virtual, a matemática nos dá um total de 4096 combinações possíveis (2 elevado a 12). No entanto, o administrador não pode utilizar todos esses números na prática. 

Os IDs 0 e 4095 são estritamente reservados pelo protocolo e não podem ser atribuídos, o que deixa uma faixa útil real que vai do ID 1 ao ID 4094. Para fins de organização e compatibilidade, essa faixa utilizável é subdividida em duas grandes categorias: as VLANs de faixa normal e as VLANs de faixa estendida.

A faixa normal engloba as VLANs numeradas de 1 a 1005. Dentro desse grupo, a VLAN 1 desempenha um papel especial por ser a VLAN padrão (_default_) do sistema, vindo associada de fábrica a todas as interfaces do switch. Já os IDs de 1002 a 1005 são historicamente reservados para tecnologias legadas de rede, como Token Ring e FDDI, que não são utilizadas em arquiteturas modernas. 

Por outro lado, a faixa estendida compreende os números que vão de 1006 a 4094. No passado, alguns equipamentos antigos apresentavam limitações de memória e não conseguiam processar esses IDs mais altos, mas em qualquer switch moderno você encontrará suporte total a toda a extensão de IDs para projetar a rede.

## Native VLAN 

Uma das características exclusivas do padrão IEEE 802.1Q é o conceito de VLAN Nativa. Por padrão, em qualquer link Trunk de um switch, a VLAN Nativa é definida automaticamente como a VLAN 1, embora essa definição possa ser alterada manualmente em cada porta Trunk de forma individual. 

O comportamento técnico desse recurso é bem específico: sempre que um switch precisa enviar um quadro que pertença à VLAN Nativa através de um link de tronco, ele não insere a etiqueta de 4 bytes do 802.1Q, enviando o quadro de forma limpa, ou seja, desmarcada (_untagged_). Da mesma forma, quando o switch na outra ponta recebe um quadro sem marcação em sua porta Trunk, ele assume imediatamente que essa informação pertence à sua própria VLAN Nativa.

Para que o tráfego flua corretamente pela infraestrutura, é mandatório que a configuração da VLAN Nativa seja idêntica nas duas pontas do link de tronco. Se houver uma divergência, conhecida no diagnóstico de redes como _native VLAN mismatch_, falhas críticas de comunicação vão acontecer. Se o Switch A considerar a VLAN 10 como nativa e o Switch B considerar a VLAN 30, um quadro da VLAN 10 sairá do Switch A sem etiqueta. Ao receber esse quadro sem marcação, o Switch B assumirá que ele pertence à VLAN 30, encaminhando o tráfego para o destino errado ou descartando o pacote.

Por questões de segurança e desempenho, a boa prática de engenharia recomenda alterar a VLAN Nativa padrão de cada tronco para um ID de VLAN que não seja utilizado por nenhum usuário ou dispositivo final na rede.

## Router-on-a-Stick (ROAS)

Como já estabelecemos, um switch de Camada 2 opera em domínios de broadcast isolados e não possui a capacidade de encaminhar tráfego entre VLANs diferentes por conta própria. Se um computador localizado na VLAN 10 precisar se comunicar com um servidor situado na VLAN 20, esse tráfego terá que passar obrigatoriamente por um dispositivo de Camada 3, como um roteador, para que os pacotes sejam devidamente roteados.

No modelo tradicional de redes, ligaríamos um cabo físico do roteador para cada VLAN presente no switch, o que esgotaria rapidamente as portas físicas do roteador. Para solucionar esse problema de escala de forma eficiente, a engenharia de redes utiliza a técnica conhecida como Router-on-a-Stick (ROAS).

O método ROAS elimina o desperdício de hardware ao utilizar uma única interface física do roteador conectada a uma porta configurada como Trunk no switch. Do ponto de vista do switch, essa porta apenas transporta os quadros etiquetados com o padrão 802.1Q de todas as VLANs autorizadas a transitar pela infraestrutura. 

O grande segredo dessa arquitetura está na configuração lógica dentro do roteador. Em vez de atribuir um endereço IP diretamente à interface física, o administrador divide essa única porta em múltiplas subinterfaces virtuais, onde cada uma delas opera como se fosse uma interface física totalmente independente.

Quando a topologia está em plena operação, o fluxo de comunicação entre setores diferentes segue um caminho bem definido de ida e volta pelo mesmo meio físico. Se a VLAN 10 envia dados para a VLAN 20, o switch recebe o quadro, insere a tag de ID 10 e despacha a informação pelo link de tronco até o roteador. O roteador intercepta o pacote na subinterface correspondente, remove a etiqueta antiga, consulta sua tabela de roteamento interna para encontrar a rede de destino e direciona o pacote para a subinterface da VLAN 20. Antes de devolver o tráfego para o switch pelo mesmo cabo, o roteador insere a nova tag com o ID 20, permitindo que o switch receba o quadro e realize a entrega correta na porta de acesso do destinatário.