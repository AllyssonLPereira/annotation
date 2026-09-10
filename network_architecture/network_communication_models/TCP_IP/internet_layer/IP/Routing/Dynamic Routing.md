
Aqui está o que abordaremos no vídeo de hoje. Primeiro, darei uma visão geral dos protocolos de roteamento dinâmico, para demonstrar como eles funcionam e por que geralmente são preferidos em relação às rotas estáticas. 
## Tópicos que abordaremos  

Existem alguns tipos de protocolos de roteamento dinâmico, então vou detalhá-los. Em seguida, analisaremos brevemente as métricas dos protocolos de roteamento dinâmico. 

A "métrica" de um protocolo é a forma como ele mede a "distância" até o destino — como o custo da rota no protocolo Spanning Tree — e é usada para determinar a melhor rota para um destino.  
 
Por fim, falaremos sobre algo chamado "distância administrativa", que é outro fator na determinação da melhor rota para um destino.

## Topologia de rede  

Aqui está a topologia de rede que usarei no início desta demonstração. 

![](../../../../../../tmp_ae9b5890-7bd6-4ea4-9259-145385a9a35a.png)

Quatro roteadores — R1, R2, R3 e R4 — e há uma LAN conectada ao R4: 192.168.4.0/24.  

Vamos focar principalmente na perspectiva do R1 por enquanto. Sem configurar nenhuma rota estática ou protocolo de roteamento dinâmico, a tabela de roteamento do R1 fica assim: apenas rotas conectadas e locais, que foram adicionadas automaticamente quando os endereços IP foram configurados em suas interfaces.  

![](../../../../../../tmp_6b863a73-a12e-4e52-b135-7b9e66a40cea.png)
### Rota de rede/Rota de host  
  
Deixe-me aproveitar um momento para esclarecer alguns pontos da lista de tópicos do exame. As duas rotas, 10.0.12.0/30 e 10.0.13.0/30, são exemplos de rotas de rede. 

Uma rota de rede é simplesmente uma rota para uma rede ou sub-rede. Em outras palavras, uma rota com um comprimento de máscara menor que /32. Por exemplo, se configurarmos uma rota estática para 192.168.4.0/24, essa é uma rota de rede também. Não é uma rota para um único host, mas uma rota para uma sub-rede inteira. 

Essas duas rotas, 10.0.12.1/32 e 10.0.13.1/32, são exemplos de rotas de host. 

Uma rota de host é uma rota para um host específico, um único endereço, especificado com uma máscara /32. Essas duas rotas foram adicionadas automaticamente e são rotas de host para os endereços específicos configurados nas interfaces G0/0 e G1/0 do R1.

Para configurar uma rota estática para um host, use o comando `ip route`, seguido pelo endereço do host e, em seguida, 255.255.255.255, que é uma máscara /32. 

Certo, isso foi apenas uma observação para que você entenda esses dois termos. Agora, vamos falar sobre roteamento dinâmico.  

## Roteamento dinâmico  

Em vez de configurar rotas estáticas em cada um desses roteadores, podemos habilitar um protocolo de roteamento dinâmico neles. Então, o R4 "anunciará" a rede 192.168.4.0/24 para seu vizinho, o R2, dizendo: "você pode alcançar essa rede através de mim".

O R2 adicionará essa rota à sua tabela de rotas. Ele então anunciará a mesma coisa para o R1, informando ao R1 que ele pode alcançar a rede 192.168.4.0/24 através do R2. O R1 adicionará essa rota à sua tabela de rotas. 

Na verdade, o R2 também anunciará a rede 10.0.24.0/30 — situada entre o R2 e o R4 — para o R1, e o R1 a adicionará à sua tabela de rotas. O R1, por sua vez, anunciará isso ao R3, informando-o de que é possível alcançar a rede 192.168.4.0/24 via R1. Ele também anunciará a rede 10.0.24.0/30 que aprendeu com o R2, bem como a rede 10.0.12.0/30 entre o R1 e o R2, mas estamos nos concentrando apenas em uma rede, por enquanto. 

E se ocorrer um erro e a interface G0/0 do R4 cair? Os outros roteadores se adaptarão automaticamente e removerão a rota de suas tabelas de roteamento. Isso evitará que o R1 continue enviando tráfego para um caminho sem saída.  

### Roteamento dinâmico vs. estático  

E se a mesma situação ocorresse ao utilizar roteamento estático? Configurei uma rota estática no R1.

![](../../../../../../tmp_5a0e28a4-d44d-42e6-b050-5d424a3ee5a5.png)

Ele consegue enviar tráfego para a rede do R4 sem problemas. No entanto, e se a mesma falha no link ocorrer? Como não há um protocolo de roteamento dinâmico em uso, o R1 não sabe que não consegue mais alcançar a rede 192.168.4.0. Se ele receber pacotes destinados a essa rede, continuará encaminhando-os para o R2, sem saber que o R2 não consegue mais alcançar a rede. 

Certo, então essa é uma vantagem do roteamento dinâmico: o roteador removerá rotas inválidas. No entanto, realmente devemos garantir que haja uma rota de backup; assim, em vez de remover totalmente a rede de destino da tabela de roteamento, ela é substituída pela próxima melhor rota.  

## Roteamento dinâmico (continuação)  

Então, adicionei outra conexão entre R3 e R4. 

![](../../../../../../tmp_3541e615-f704-4759-af1b-53611dcae41a.png)

Agora, R1 tem dois caminhos válidos para a rede interna de R4: via R2 e via R3. Vamos verificar a tabela de roteamento de R1.

Você pode ver que ela ainda mantém a rota via R2 na tabela, pois indica "via 10.0.12.2". Nesse caso, o que acontecerá se eu desativar a interface G0/0 de R4 para simular uma falha? Bem, vamos verificar a tabela de roteamento de R1 nesse caso. 

![](../../../../../../tmp_c5d9f8e5-7af6-48b6-8f3a-dba6ad620d63.png)

Como você pode ver, a rota via R2 foi substituída automaticamente pela rota via R3; agora indica "via 10.0.13.2". Então, nós perdemos a rota preferencial para 192.168.4.0, mas o tráfego ainda pode seguir por esse caminho. 

Agora, você pode estar se perguntando: por que a rota via R2 foi preferida em relação à rota via R3? Isso acontece porque a conexão via R3 é uma conexão Fast Ethernet, não Gigabit Ethernet. Você já está familiarizado com o conceito de "custo para a raiz" (root cost) do Spanning Tree, usado para determinar o melhor caminho até a bridge raiz. Bem, os protocolos de roteamento dinâmico usam um conceito semelhante para determinar o melhor caminho até um destino.

O R1 aprendeu sobre a rede 192.168.4.0/24 tanto do R2 quanto do R3; no entanto, ele determinou que o caminho via R2 é superior porque "custa" menos. Ok, essa é uma introdução bem rápida aos protocolos de roteamento dinâmico e ao seu objetivo básico. Aqui estão alguns pontos-chave.

## Resumo sobre roteamento dinâmico

Roteadores podem usar protocolos de roteamento dinâmico para anunciar informações sobre suas rotas conectadas, bem como rotas aprendidas de outros dispositivos. Eles formam "adjacencies" — também conhecidas como "neighbor relationships" com roteadores adjacentes para trocar essas informações. 

Por exemplo, nesta rede, o R1 formará adjacências com R2 e R3, seus vizinhos diretamente conectados. Se múltiplas rotas para um destino forem aprendidas, o roteador determina qual rota é superior e a adiciona à tabela de roteamento. Ele usa a "métrica" da rota para decidir qual é a superior, e a métrica mais baixa é a melhor. 

Assim como no Spanning Tree, o custo para a raiz mais baixo é o melhor ao determinar a porta raiz em um switch. Falarei mais sobre métrica mais adiante.  

## Tipos de protocolos de roteamento dinâmico  

Agora, vamos falar sobre os diferentes tipos de protocolos de roteamento dinâmico. Os protocolos de roteamento dinâmico podem ser divididos em duas categorias principais: IGP, que significa *Interior Gateway Protocol* (Protocolo de Gateway Interno), e EGP, que significa *Exterior Gateway Protocol* (Protocolo de Gateway Externo). Vamos defini-los. 

Os IGPs são usados para compartilhar rotas dentro de um único sistema autônomo (AS), que é uma organização única, como uma empresa, por exemplo. Os EGPs são usados para compartilhar rotas entre diferentes sistemas autônomos.  

Talvez este diagrama facilite a compreensão. 

![](../../../../../../tmp_cf939f1a-31ec-4409-9d44-ffc6ea4b66cb.png)

A Empresa A, a Empresa B, o ISP A e o ISP B constituem, cada um, seu próprio sistema autônomo (AS). Dentro de cada organização, utiliza-se um IGP para trocar informações de roteamento. No entanto, para trocar informações de roteamento entre sistemas autônomos (ASs), utiliza-se um EGP. 

O objetivo básico dos IGPs e EGPs é o mesmo: compartilhar informações sobre rotas para destinos. Contudo, eles funcionam de maneira diferente. 

## Tipos de algoritmo IGP/EGP

Agora, vamos detalhar ainda mais essas categorias. Como mencionei, as duas grandes categorias são *Interior Gateway Protocols* (IGPs) e *Exterior Gateway Protocols* (EGPs). No entanto, é possível subdividir essas categorias com base no "tipo de algoritmo". Isso se refere aos processos utilizados por cada protocolo para compartilhar informações de rota e determinar a melhor rota para cada destino.  

![](../../../../../../tmp_555e0606-bb30-4b1b-8ad2-f19a98c8c1b0.png)

Existe apenas um tipo de algoritmo EGP: o *Path Vector* (Vetor de Caminho). Não apenas existe apenas um tipo de algoritmo EGP, como também existe apenas um EGP utilizado em redes modernas. Trata-se do BGP, o *Border Gateway Protocol*.

Agora, os IGPs possuem dois tipos de algoritmo: vetor de distância (Distance Vector) e estado de enlace (link state). Repito: quando digo "algoritmo", refiro-me aos processos que cada protocolo utiliza para compartilhar informações de rota e escolher a melhor rota para cada destino.  

Todos os protocolos de roteamento têm o mesmo objetivo. É o que acabei de dizer: compartilhar informações de rota e selecionar a melhor rota para cada destino. No entanto, o algoritmo utilizado para isso é diferente para cada protocolo de roteamento. 

Existem dois protocolos de vetor de distância: o RIP (Routing Information Protocol) e o EIGRP (Enhanced Interior Gateway Routing Protocol). Não vou abordar esses dois protocolos em profundidade, embora vá apresentar uma visão geral de suas funções para que você possa compará-los com o OSPF. Então, RIP e EIGRP são os dois protocolos de vetor de distância.  

Há também dois protocolos de estado de enlace: o OSPF (Open Shortest Path First) e o IS-IS (Intermediate System to Intermediate System).

Certo, agora eu quero descrever as características dos protocolos de vetor de distância e de estado de enlace. Começarei pelos protocolos de roteamento de vetor de distância. Mais uma vez, os protocolos de vetor de distância que estudaremos são o RIP e o EIGRP. 

### Protocolos de roteamento de vetor de distância

Os protocolos de vetor de distância foram criados antes dos protocolos de estado de enlace, no início da década de 1980. Exemplos iniciais de protocolos de vetor de distância são o RIP e o protocolo proprietário da Cisco, o IGRP, que mais tarde foi atualizado para se tornar o EIGRP.  

Os protocolos de vetor de distância operam enviando as seguintes informações aos seus vizinhos diretamente conectados: suas redes de destino conhecidas e a métrica para alcançar essas redes de destino conhecidas. Esse método de compartilhamento de informações de rota é frequentemente chamado de "roteamento por boato" (routing by rumor). Por que esse nome? 

Porque o roteador não tem conhecimento da rede além de seus vizinhos. Ele conhece apenas as informações que seus vizinhos lhe transmitem. Isso difere dos protocolos de roteamento de estado de enlace, nos quais o roteador desenvolve uma visão mais completa da rede. 

Ao utilizar um protocolo de vetor de distância, por outro lado, tudo o que o roteador sabe são as rotas informadas por seus vizinhos e as respectivas métricas para alcançar esses destinos. A razão para o nome "vetor de distância" é que os roteadores aprendem apenas a "distância" — que é a métrica — e o "vetor" — que é a direção para enviar o tráfego, ou seja, o roteador de próximo salto — de cada rota.

Basicamente, os protocolos de vetor de distância funcionam compartilhando suas tabelas de rotas, ou partes delas, com seus vizinhos. Então, o exemplo que mostrei anteriormente, do R4 anunciando sua rede 192.168.4.0, é um exemplo da lógica de vetor de distância.

O R4 informa ao R2, seu vizinho diretamente conectado: "Você pode alcançar a rede 192.168.4.0/24 através de mim. Minha métrica para alcançá-la é 1". Não se preocupe com os valores das métricas por enquanto; cada protocolo de roteamento utiliza um tipo diferente de métrica, e abordaremos isso em breve. De qualquer forma, o R2 não sabe nada além do fato de que pode alcançar a rede 192.168.4.0/24 através do R4, e que a métrica do R4 é 1. 

Da mesma forma, o R2 informa o mesmo ao R1, exceto que anuncia a métrica como 2. Mais uma vez, o R1 não tem uma visão detalhada da rede; tudo o que ele sabe é que pode alcançar a rede 192.168.4.0/24 através do R2, e que a métrica do R2 para alcançá-la é 2. E, claro, o R1 anuncia a rede para o R3, com sua própria métrica para alcançar a rede de destino.

A seguir, apresentarei brevemente os protocolos de roteamento de estado de enlace (link state). 

### Protocolos de roteamento de estado de enlace

Ao utilizar um protocolo de roteamento de estado de enlace cada roteador cria um "mapa de conectividade" da rede. Esse mapa será o mesmo em todos os roteadores. Para permitir isso, cada roteador anuncia informações sobre suas interfaces e suas redes conectadas aos seus vizinhos. Esses anúncios são repassados a outros roteadores, até que todos os roteadores da rede desenvolvam o mesmo mapa da rede.

Então, cada roteador usa esse mapa de forma independente para calcular as melhores rotas para cada destino. Acho que você consegue perceber como isso difere do "roteamento por boato" dos protocolos de vetor de distância (distance vector). 

Nos protocolos de estado de link (link state), cada roteador obtém uma visão completa da rede para que possa calcular as melhores rotas. Os protocolos de estado de link consomem mais recursos — mais poder de processamento (CPU) e memória — no roteador, pois há mais informações sendo compartilhadas. No entanto, os protocolos de estado de link tendem a reagir mais rapidamente a mudanças na rede do que os protocolos de vetor de distância. 

Os dois protocolos de estado de link utilizados atualmente são o OSPF e o IS-IS. Vou mencionar brevemente alguns aspectos do IS-IS, mas, quanto ao OSPF, vamos analisá-lo em profundidade.  

### Métrica  
  
Agora, vamos falar sobre aquelas métricas que mencionei algumas vezes. A tabela de rotas de um roteador contém a melhor rota para cada rede de destino que ele conhece. Se um roteador que utiliza um protocolo de roteamento dinâmico descobre duas rotas diferentes para o mesmo destino, como ele determina qual é a "melhor"?

Como mencionei brevemente antes, ele utiliza o valor da métrica das rotas para determinar qual é a melhor. Uma métrica mais baixa é considerada melhor. É como o custo de raiz (root cost) no Spanning Tree. Um custo de raiz mais baixo é considerado superior; portanto, a interface com o menor custo de raiz se tornará a porta raiz (root port). 

Para protocolos de roteamento dinâmico, a rota com a menor métrica é considerada a melhor e será inserida na tabela de rotas. Cada protocolo de roteamento usa uma métrica diferente para determinar qual rota é a melhor.  

Nesta imagem que mostrei anteriormente, embora o R1 aprenda dois caminhos para 192.168.4.0/24 — um via R2 e outro via R3 —, apenas a rota via R2 é adicionada à tabela de roteamento. 

![](../../../../../../tmp_f087794d-8860-40fe-97b6-870e2f5e3019.png)

Esta conexão Fast Ethernet aqui tem um custo de métrica mais alto do que as outras conexões Gigabit Ethernet; portanto, essa rota é menos favorável. Agora, você pode estar se perguntando: e se essa também fosse uma conexão Gigabit Ethernet? Ambas as rotas teriam o mesmo custo; então, qual rota seria adicionada à tabela de roteamento? Vamos ver o que acontece.  

Alterei a conexão entre R3 e R4 para ser uma conexão Gigabit Ethernet, assim como as outras. Vamos verificar a tabela de roteamento do R1. 

![](../../../../../../tmp_4c54cb2b-c46f-434a-8e95-750839c8e3f9.png)

Veja só: AMBAS as rotas foram adicionadas à tabela. Via 10.0.13.2 (que é o R3) e via 10.0.12.2 (que é o R2). Portanto, se um roteador aprende duas (ou mais) rotas via o mesmo protocolo de roteamento para o mesmo destino, com a mesma métrica, ambas serão adicionadas à tabela de roteamento. O tráfego será balanceado entre as duas rotas.

Observe que o destino deve ser exatamente o mesmo: o mesmo endereço de rede e o mesmo comprimento de prefixo.

Neste caso, ambas as rotas foram aprendidas pelo protocolo de roteamento dinâmico OSPF, conforme indicado pelo código "O" ao lado das rotas. Ambas apontam para exatamente o mesmo destino, 192.168.4.0/24, e ambas possuem a mesma métrica.

O valor da métrica em si também é exibido nesta saída. Onde ele está? O segundo valor entre os colchetes ao lado da rede 192.168.4.0/24 é o valor da métrica da rota. Ambas as rotas têm métrica 3, então ambas foram adicionadas, e o tráfego será distribuído (balanceado) entre as duas rotas. Isso é chamado de balanceamento de carga ECMP (*Equal Cost MultiPath*). 

Quanto a estes valores à esquerda dos colchetes, trata-se de outro valor importante chamado "distância administrativa" (ou AD). O protocolo OSPF tem uma AD de 110. 

#### ECMP com Rotas Estáticas  

Já que acabei de mostrar o ECMP — balanceamento de carga de múltiplos caminhos de custo igual com um protocolo de roteamento dinâmico —, quero informar que você também pode fazer o mesmo com rotas estáticas. Desativei o OSPF no R1 e configurei duas rotas estáticas para 192.168.4.0: uma via R2 e outra via R3.

![](../../../../../../tmp_c04f9325-a1fa-4009-9f49-5819fed23fef.png)

Assim, ambas são adicionadas à tabela de roteamento, e o tráfego será distribuído entre as duas rotas. Observe que ambas as rotas têm métrica 0. Rotas estáticas não utilizam realmente o conceito de "métrica", então você sempre verá 0 aqui.

Observe também que o valor da distância administrativa (AD) das rotas estáticas é 1. Como já mencionei, cada protocolo de roteamento utiliza uma métrica diferente. Vou abordar cada uma dessas métricas de IGP com mais detalhes em outra aula, mas aqui está um resumo para apresentá-las a você.  

### Continuação das métricas

![](../../../../../../tmp_58518ce3-2ffb-4e8c-bd95-e297b4c27b17.png)

O RIP utiliza, de longe, a métrica mais simples: a contagem de saltos (*hop count*). Cada roteador no caminho até o destino conta como um "salto", e a métrica total é o número total de saltos para alcançar o destino.  

Uma grande desvantagem é que links de todas as velocidades são tratados como iguais; todos contam como um único salto. Um link Ethernet de 10 megabits por segundo conta como um salto, e um link de 10 gigabits por segundo também conta como um salto. Portanto, essa é uma maneira muito primitiva de calcular a métrica e, claramente, não é a ideal. 

O EIGRP utiliza a métrica mais complexa entre os IGPs; por padrão, é um cálculo baseado em largura de banda e atraso (*delay*), embora, mediante configuração, outros fatores também possam ser considerados.

Um ponto importante é que apenas a largura de banda do link mais LENTO na rota é utilizada para calcular a métrica, enquanto os valores de atraso total de todos os links do caminho são considerados. Esse valor de "atraso" pode ser um pouco enganoso, já que, por padrão, é um valor atribuído à interface com base em sua largura de banda.De qualquer forma, falarei mais sobre isso na aula sobre o EIGRP com mais profundidade. 

A seguir, temos o OSPF; sua métrica é chamada de "custo" (*cost*). O custo de cada link é calculado com base na largura de banda, e a largura de banda total dos links na rota compõe a métrica da rota. Essa é uma forma muito simples de calcular a métrica, mas claramente superior à do RIP, que não leva em conta a velocidade do link. 

Por fim, o IS-IS também utiliza uma métrica chamada "custo". No entanto, o custo de cada link não é calculado automaticamente com base na largura de banda. Todos os links têm um custo padrão de 10. Então, sem nenhuma configuração, ele funciona da mesma forma que o RIP, utilizando uma métrica simples de contagem de saltos. 

Certo, então não vou falar muito sobre o IS-IS, mas darei mais detalhes sobre os outros três em aulas futuras. Para agora, lembre-se apenas do básico: o RIP usa a contagem de saltos (*hop count*), o EIGRP usa um cálculo baseado em largura de banda e atraso (*delay*), e o OSPF usa um custo baseado na largura de banda. 

O objetivo de todas essas métricas é o mesmo: permitir que o roteador selecione a melhor rota para o destino. Para demonstrar brevemente como a diferença nas métricas pode afetar as rotas selecionadas pelo roteador, vamos analisar novamente este diagrama sob a perspectiva do R1, ao decidir qual rota para a rede 192.168.4.0/24 selecionar para sua tabela de roteamento. 

![](../../../../../../tmp_06336c40-fd06-40c9-b6aa-9d66dd70833c.png)

Se ele usar o RIP, a métrica é a contagem de saltos. Via R2, a contagem de saltos é 2: um salto até o R2 e um salto até o R4. Via R3, a contagem de saltos também é 2: um salto até o R3 e um salto até o R4, embora a conexão entre R3 e R4 seja uma conexão Fast Ethernet mais lenta. Assim, ambas as rotas serão inseridas na tabela de roteamento do R1, e o R1 fará o balanceamento de carga do tráfego usando as duas rotas, mesmo que uma delas seja mais lenta. 

No entanto, se o OSPF for usado em vez do RIP, qual caminho será utilizado? Ao contrário do RIP, a métrica de custo do OSPF leva em consideração a largura de banda. Portanto, a conexão mais lenta entre R3 e R4 resultará em um valor de métrica mais alto, tornando-a menos favorável. Assim, apenas essa rota será inserida na tabela de roteamento, e o R1 enviará todo o tráfego destinado à rede 192.168.4.0/24 via R2.

O RIP considera ambas as rotas equivalentes, mas o OSPF não. Novamente, o objetivo de todas essas métricas é o mesmo — permitir que o roteador selecione a melhor rota para o destino —, mas alguns protocolos de roteamento podem tomar decisões melhores do que outros. 

### Distância Administrativa

Agora vamos falar sobre a distância administrativa, que mencionei brevemente antes. Na maioria dos casos, uma empresa utilizará apenas um único IGP para sua rede – geralmente o OSPF, mas às vezes o EIGRP, se utilizarem apenas equipamentos Cisco. No entanto, em alguns casos raros, podem utilizar dois.

Por exemplo, se duas empresas conectam suas redes para compartilhar informações, dois protocolos de roteamento diferentes podem estar em uso. Você pode conectar uma rede que utiliza OSPF a uma rede que utiliza EIGRP. A métrica, que acabei de mostrar a vocês, é usada para comparar rotas aprendidas por meio do mesmo protocolo de roteamento.

Se um roteador aprende duas rotas para o mesmo destino via OSPF, ele usa a métrica para escolher qual rota é melhor. No entanto, protocolos de roteamento diferentes usam métricas totalmente diferentes, portanto, não podem ser comparadas. Por exemplo, uma rota OSPF para 192.168.4.0/24 pode ter uma métrica de 30, enquanto uma rota EIGRP para o mesmo destino pode ter uma métrica de 33280.
  
Qual rota é melhor? Qual rota o roteador deve colocar na tabela de roteamento? Não podemos realmente responder a essas perguntas apenas olhando para as métricas, porque OSPF e EIGRP usam métricas totalmente diferentes. Assim, a distância administrativa, ou AD, é usada para determinar qual protocolo de roteamento é preferido. 

Uma AD mais baixa é preferível e indica que o protocolo de roteamento é considerado mais "confiável", ou seja, com maior probabilidade de selecionar boas rotas. Como você viu anteriormente, o sistema de métricas do RIP baseado em contagem de saltos (*hop count*) não é muito bom; por isso, ele tem uma AD alta, já que não é tão confiável. Ele pode indicar que duas rotas são iguais porque têm a mesma contagem de saltos, embora, na realidade, uma rota seja muito pior devido a uma largura de banda menor.

Pronto para memorizar algumas coisas?

![](../../../../../../tmp_da497fd0-9d35-426a-95a6-ad80a1f78ffe.png)

Estas são as distâncias administrativas dos tipos de rota mais comuns.Novamente, um valor de AD menor é preferível e será selecionado em detrimento de uma AD maior. Lembre-se de que esses são os valores usados em dispositivos Cisco; outros fabricantes podem classificá-los de forma diferente. 

Assim, as rotas preferenciais são aquelas para redes diretamente conectadas; elas têm uma AD de 0. Rotas estáticas vêm em seguida, com uma AD de 1. Depois, temos as rotas BGP externo, também conhecidas como eBGP, com uma AD de 20. Existe outro tipo de BGP, o BGP interno (iBGP), que você verá mais adiante. 

As rotas EIGRP têm uma AD de 90. A seguir, temos o IGRP, a versão mais antiga do EIGRP, com uma AD de 100. O OSPF tem uma AD de 110. O IS-IS tem uma AD de 115, e o RIP tem uma AD de 120. 

Portanto, entre os IGPs que mostrei — RIP, EIGRP, OSPF e IS-IS —, o EIGRP é o mais preferido, pois possui a menor AD. No entanto, as rotas externas do EIGRP têm uma AD mais alta: 170. Elas estão além do escopo do CCNA, mas, basicamente, são rotas de fora da rede EIGRP que são anunciadas para dentro do EIGRP. Depois, o BGP interno (iBGP) tem uma AD de 200. E mais uma: rotas com AD de 255 são inutilizáveis. 

Aqui está uma citação da Cisco: "Se a distância administrativa for 255, o roteador não confia na origem dessa rota e não a instala na tabela de roteamento.". Portanto, certifique-se de memorizar esses valores.

Aqui está uma pergunta rápida de teste para ilustrar um ponto. As seguintes rotas para a rede de destino 10.1.1.0/24 são aprendidas: 

- uma rota com próximo salto (next hop) 192.168.1.1, aprendida via RIP, com métrica 5; 
- uma rota com próximo salto 192.168.2.1, aprendida via RIP, com métrica 3; e 
- uma rota com próximo salto 192.168.3.1, aprendida via OSPF, com métrica 10. 

Qual rota para 10.1.1.0/24 será adicionada à tabela de rotas? Bem, a resposta é que a rota OSPF será adicionada à tabela de rotas. A métrica é usada para comparar rotas aprendidas pelo mesmo protocolo de roteamento. No entanto, antes de comparar as métricas, a AD (Distância Administrativa) é usada para selecionar a melhor rota.

A rota OSPF sempre terá precedência sobre as rotas RIP, porque possui uma AD menor. 

![](../../../../../../tmp_f18f9e9d-6eea-48ec-8166-a6e498e2c11f.png)

Revisitando a tabela de rotas que mostrei anteriormente, aqui você pode ver a AD de 1 para essas rotas estáticas. As rotas conectadas e locais acima delas têm AD 0, mas isso não é exibido na tabela de rotas.

E aqui está outra visualização desta tabela de rotas com rotas OSPF.

![](../../../../../../tmp_c9391424-2e7d-4594-9ff4-984524f8379f.png)

Aqui você pode ver a AD de 110. Lembre-se de que o número à esquerda, entre colchetes, é a AD, e o número à direita é a métrica.  

### Configurar a AD de uma Rota Estática  

Um último ponto. Você pode alterar a AD de um protocolo de roteamento, e demonstrarei isso quando abordarmos a configuração do OSPF em uma aula posterior. Se você quiser que as rotas OSPF tenham preferência sobre as rotas EIGRP, pode configurar o roteador para fazer isso. 

Você também pode alterar a AD de uma rota estática. 

![](../../../../../../tmp_eca90876-061a-40ba-b13d-bb1be6fdd145.png)

Observe que aqui usei o comando padrão para configurar uma rota estática: IP ROUTE, seguido pelo destino, pela máscara de sub-rede e, então, pelo endereço do próximo salto (next hop). No entanto, usei o ponto de interrogação para verificar outras opções. Aqui aparece "distance metric" para esta rota.

O termo inclui a palavra "metric" (métrica), mas não a confunda com a métrica sobre a qual falamos anteriormente. Esta é a distância administrativa. Então, configurei a rota com uma AD de 100.

Na saída do comando `show ip route`, você pode ver que a AD agora é 100, em vez do valor padrão 1 para uma rota estática comum. 

Agora, por que você faria isso? Ao alterar a AD de uma rota estática, você pode torná-la menos preferível do que rotas aprendidas por um protocolo de roteamento dinâmico para o mesmo destino. Mas é preciso garantir que a AD da rota estática seja maior que a AD do protocolo de roteamento; caso contrário, a rota estática ainda terá preferência.

Esse tipo de rota estática é chamado de "rota estática flutuante". A rota ficará inativa — ou seja, não aparecerá na tabela de roteamento — a menos que a rota aprendida pelo protocolo de roteamento dinâmico seja removida. 

Por exemplo, talvez o roteador remoto pare de anunciá-la por algum motivo, ou uma falha de interface faça com que a adjacência com um vizinho seja perdida. 