Primeiro, vamos ver o que abordaremos neste arquivo. 

- Começando pelos tipos de rede OSPF. Eles se referem aos diferentes tipos de conexão entre roteadores OSPF e como essas conexões influenciam o comportamento do OSPF;
- Em seguida, abordaremos os requisitos de vizinhança e adjacência no OSPF. No arquivo "OSPF_1.md", vimos o processo que os roteadores utilizam para se tornarem vizinhos OSPF; no entanto, não analisamos detalhadamente os requisitos para uma adjacência de vizinhança bem-sucedida;
-  Depois, veremos alguns tipos de LSA (*Link State Advertisement* — Anúncio de Estado de Link). Existem muitos.

## Interfaces Loopback

Antes de entrarmos nesses tópicos, quero dedicar um momento para explicar um pouco sobre as interfaces loopback. Já as mencionei nos arquivos anteriores, mas deixe-me explicá-las com mais detalhes. Uma interface loopback é uma interface virtual no roteador. Você já sabe disso. Ela está sempre no estado *up/up* (a menos que você a desative manualmente). Isso significa que o status de uma interface loopback não depende de uma interface física. Interfaces físicas podem apresentar problemas de hardware e falhar; no entanto, isso não acontece com uma interface loopback, a menos que o próprio roteador falhe.

Assim, ela fornece um endereço IP consistente que pode ser usado para acessar e identificar o roteador. Às vezes, é necessário enviar tráfego diretamente para um roteador.

![](../../../../../../z_imgs/074923.png)

Digamos que o R1 não tenha uma interface loopback no momento, e o R4 receba um pacote destinado ao R1 no endereço IP 10.0.13.1, que é o endereço da sua interface G1/0. Ele poderia encaminhá-lo para o R1 via sua interface f2/0. E se a interface G1/0 do R1 cair por algum motivo? Se o R4 receber um pacote destinado ao R1 no endereço 10.0.13.1, ele não conseguirá enviar o pacote para o R1.

Que tal se o R1 tiver uma interface loopback, 1.1.1.1, e ela for usada para identificar o R1 em vez do endereço 10.0.13.1? Mesmo que uma interface física falhe, quando o R4 receber um pacote destinado à interface loopback do R1, ele ainda conseguirá enviar o pacote para o R1. Então, é por isso que é uma boa ideia configurar uma interface loopback em um roteador. Ela fornece uma interface com um endereço IP que está sempre ativo e pode ser usada de forma consistente para identificar e alcançar o roteador. Agora, vamos analisar os diferentes tipos de rede OSPF. 

## Tipos de Rede OSPF

O tipo de rede OSPF refere-se ao tipo de conexão entre vizinhos OSPF, e esse tipo influencia a maneira como o OSPF se comporta em alguns aspectos. O tipo de conexão mais comum em redes modernas é o Ethernet, é claro. Existem três tipos principais de rede OSPF. 

- O primeiro é o tipo de rede ***Broadcast***, que é habilitado por padrão em interfaces Ethernet e FDDI. O FDDI é uma tecnologia antiga e você não precisa perder tempo aprendendo sobre ela. O tipo de rede OSPF *broadcast* é utilizado por padrão;
- O próximo é o tipo de rede ***Ponto a Ponto*** (*Point-to-Point*), que é habilitado por padrão em interfaces PPP e HDLC; e
- O último tipo de rede principal é o ***Non-broadcast*** (não broadcast). Ele é habilitado por padrão em interfaces Frame Relay e X.25.

### Tipo de rede Broadcast

Primeiro, o tipo de rede *broadcast*. Como acabei de mencionar, esse tipo de rede é habilitado em interfaces Ethernet e FDDI por padrão.

![](../../../../../../z_imgs/125829.png)

Nos arquivos anteriores, todas as conexões OSPF que analisamos utilizaram o tipo de rede *Broadcast*, pois são todas conexões Ethernet. No diagrama de rede acima, todas são conexões Ethernet; lembre-se de que "G" significa "Gigabit Ethernet", e, portanto, essas conexões entre os roteadores utilizam o tipo de rede *Broadcast*. Agora, vamos abordar algumas características do tipo de rede *Broadcast*. 

Primeiro, os roteadores descobrem vizinhos dinamicamente enviando e escutando mensagens "Hello" do OSPF, utilizando o endereço multicast 224.0.0.5. Você já sabe disso pelo arquivo passado, quando mostrei como os roteadores OSPF se tornam vizinhos. No entanto, nem todos os tipos de rede descobrem vizinhos dinamicamente dessa forma. Não abordaremos esse tipo de rede aqui, mas, no caso do tipo de rede "Non-broadcast" (não broadcast), é necessário configurar os vizinhos manualmente.

Certo, próximo ponto. Um DR, ou roteador designado, e um BDR (Backup Designated Router) deve ser eleito em cada sub-rede. No entanto, em casos como a interface G1/0 dos roteadores R1, R3, R4 e R5, onde não há vizinhos OSPF, existe apenas um DR, sem BDR. Roteadores que não são o DR ou o BDR da sub-rede tornam-se "DROther". Então, vamos analisar a rede acima. Cada sub-rede precisa de um DR. Nas sub-redes da interface G1/0 dos roteadores R1, R3, R4 e R5 é simples: não há vizinhos OSPF, então cada roteador se torna o DR da sub-rede. 

E quanto à sub-rede 192.168.1.0/30 entre R1 e R2? Mais adiante, mostrarei como o DR é eleito, mas vamos supor que R2 seja o DR. 

![](../../../../../../z_imgs/174324.png)

Assim, R1 torna-se o BDR do segmento. E quanto à sub-rede 192.168.2.0/29 à qual R2, R3, R4 e R5 se conectam? Por exemplo, R5 poderia ser o DR, R4 o BDR, e então R2 e R3 tornam-se DROthers. Você provavelmente está se perguntando como essas eleições funcionam e qual é a finalidade do DR e do BDR. Bem, vamos abordar isso.

### Broadcast - Eleição de DR/BDR

Então, é assim que o DR e o BDR são eleitos. Existe uma ordem de prioridade. 

Primeiramente, o roteador com a maior prioridade de interface OSPF na sub-rede torna-se o DR do segmento. No entanto, todas as interfaces têm a mesma prioridade por padrão; portanto, os roteadores comparam seus IDs de roteador OSPF. O roteador com o maior ID de roteador OSPF vence. O "primeiro lugar" na eleição torna-se o DR da sub-rede, e o "segundo lugar" torna-se o BDR. A prioridade padrão da interface OSPF é 1 em todas as interfaces. Então, como eu disse, por padrão, o roteador com o maior ID de roteador se tornará o DR do segmento. Aqui está uma saída parcial do comando `show ip ospf interface g0/0` no R5. 

![](../../../../../../z_imgs/075127.png)

Observe o ID do roteador. Configurei uma interface loopback em cada roteador, e o endereço IP da interface loopback tornou-se o ID do roteador. O estado é DR, e a prioridade é o padrão 1. O R5 tem o maior ID de roteador entre os roteadores conectados à sub-rede 192.168.2.0/29; por isso, ele se tornou o DR. Aqui embaixo, o DR (o próprio R5) e o BDR (R4) do segmento estão listados, incluindo seus IDs de roteador e o endereço IP da interface na sub-rede. E aqui está a mesma saída para o R2. 

![](../../../../../../z_imgs/075746.png)

A principal diferença que quero destacar é o estado DROTHER. Agora, e se eu quiser tornar o R2 o DR do segmento em vez do R5? Vamos ver como alterar a prioridade da interface OSPF. 

### Broadcast - Prioridade OSPF

O comando para alterar a prioridade OSPF de uma interface é `ip ospf priority`, seguido pela prioridade, com uma faixa de 0 a 255. Eu a alterei para o valor máximo, 255, no R2. 

![](../../../../../../z_imgs/080001.png)

Uma observação: se você definir a prioridade da interface OSPF como 0, o roteador NÃO poderá ser o DR/BDR para a sub-rede, em hipótese alguma. Então, vamos verificar se o R2 se tornou o DR do segmento.

![](../../../../../../z_imgs/113853.png)

Isso é estranho. O estado do R2 ainda é DROTHER, mesmo tendo a maior prioridade. Por que isso acontece? É porque a eleição de DR/BDR não é "preemptiva". O que "não preemptivo" significa é que, uma vez selecionados, o DR e o BDR mantêm suas funções até que o OSPF seja reiniciado, a interface falhe ou seja desativada, etc. Então, embora seja uma má ideia fazer isso em uma rede em produção, vou reiniciar o processo OSPF no R5 e vamos ver o que acontece. Reiniciei o processo OSPF no R5 e você pode ver que todos os seus vizinhos ficaram inativos (estado DOWN).

![](../../../../../../z_imgs/114250.png)

Depois, o R2 e o R4 retornaram ao estado FULL, mas o R3 não. Há uma razão importante para isso, que você aprenderá em breve. Em seguida, usei o comando `show ip ospf neighbor` para visualizar o estado dos vizinhos do R5. Veja aqui: há dois pontos importantes sobre o OSPF que podemos aprender analisando esta seção. 

- Primeiro, o R4 tornou-se o DR, e não o R2. O R2 tornou-se o BDR. O que podemos aprender com isso? Podemos aprender que, quando o DR cai, o BDR assume o papel de novo DR. Em seguida, é realizada uma eleição para o próximo BDR. O R4, que era o BDR, imediatamente assumiu como o novo DR, e então foi feita uma eleição entre os outros roteadores para o próximo BDR. O R2 tem a maior prioridade, 255, então ele se tornou o BDR.

- Certo, próximo ponto. O R3 é um DROther e permanece estável no estado 2-way. O R5 também se tornou um DROther, aliás. O que podemos aprender com isso? Podemos aprender que os DROthers só avançam para o estado FULL com o DR e o BDR da sub-rede. O estado de vizinhança com outros DROthers será 2-way. Isso nos dá uma pista sobre a finalidade do DR e do BDR, assunto que abordarei em seguida.

Mas lembre-se destes dois pontos: o BDR se torna o DR se o DR atual for removido, mesmo que não tenha a prioridade mais alta. Além disso, os DROthers não formam adjacências completas com outros DROthers; eles permanecem no estado 2-way. Repetindo: no tipo de rede broadcast, os roteadores só formam uma adjacência OSPF completa com o DR e o BDR do segmento. Portanto, os roteadores só trocam LSAs com o DR e o BDR. Os DROthers não trocam LSAs entre si. Lembre-se de que, no estado "2-way", os roteadores ainda não compartilharam LSAs entre si. Todos os roteadores ainda terão o mesmo LSDB, mas isso reduz a quantidade de LSAs inundando a rede. Vamos ver um exemplo.

![](../../../../../../z_imgs/075739.png)

Se 6 roteadores estiverem conectados ao mesmo segmento e todos compartilharem LSAs entre si, o resultado será este: uma enorme quantidade de LSAs inundando e congestionando a rede. E se usarmos um DR e um BDR? Se os roteadores trocarem LSAs apenas com o DR e o BDR, como você pode ver, o número de LSAs inundando a rede é reduzido. 

![](../../../../../../z_imgs/075940.png)

Para ser sincero, em roteadores modernos isso provavelmente não é um grande problema na maioria dos casos, mas ainda assim ajuda a reduzir o tráfego de rede desnecessário. Aliás, quando os roteadores precisam enviar mensagens para o DR e o BDR, eles usam o endereço multicast 224.0.0.6. Isso é diferente do endereço multicast OSPF "todos os roteadores" (all routers), que é 224.0.0.5.

Aqui está uma rápida revisão do processo de vizinhança do OSPF.

![](../../../../../../z_imgs/114119.png)

Lembra que eu disse que esses primeiros passos envolvem tornar-se vizinho? Então, quando os roteadores chegam a esse ponto do processo, eles já são vizinhos OSPF. As conexões entre dois DROthers param nesse ponto. Os roteadores só prosseguirão para trocar LSAs e formar uma adjacência OSPF completa com o DR e o BDR. Então, resumindo, isso significa que o DR e o BDR estabelecem uma adjacência completa com TODOS os roteadores na sub-rede, incluindo os DROthers. E os DROthers estabelecerão uma adjacência completa apenas com o DR/BDR. 

Eu mostrei esse comando, `show ip ospf interface brief`, anteriormente. 

![](../../../../../../z_imgs/114303.png)

Aqui, executei-o no R3, que é um DROther. Observe a contagem de vizinhos na interface G0/0 dele. "F" indica o número de adjacências completas, e "C" indica a contagem total de vizinhos. Portanto, o R3 tem duas adjacências completas, com o R2 e o R4. Mas ele tem um total de três vizinhos: R2, R4 e R5. Para mais detalhes, aqui está o comando `show ip ospg interface g0/0` no R3.

![](../../../../../../z_imgs/114539.png)

Ele fornece a mesma informação aqui: "Neighbor Count is 3" (Contagem de vizinhos é 3); esse é o número total de vizinhos OSPF do R3. "Adjacent neighbor count is 2" (Contagem de vizinhos adjacentes é 2); esses são os vizinhos com os quais o R3 estabeleceu uma adjacência completa. E abaixo disso, seus dois vizinhos adjacentes estão listados: R2, o BDR, e R4, o DR. Certo, isso é suficiente por enquanto para o tipo de rede Broadcast; vamos seguir em frente. Agora, vamos analisar o tipo de rede "ponto a ponto". 

## Tipo de rede ponto a ponto

Observe que alterei a conexão entre o R1 e o R2 para uma conexão "serial". Farei uma breve apresentação sobre conexões seriais a seguir, mas, antes, deixe-me apresentar os conceitos básicos do tipo de conexão ponto a ponto.

![](../../../../../../z_imgs/174609.png)

Esse tipo de rede é habilitado em interfaces seriais que utilizam encapsulamento PPP ou HDLC por padrão. Tanto o PPP quanto o HDLC são encapsulamentos de Camada 2, semelhantes ao Ethernet, exceto pelo fato de serem usados ​​em conexões seriais. Assim como no tipo de rede Broadcast, os roteadores descobrem vizinhos dinamicamente enviando e escutando mensagens Hello do OSPF, utilizando o endereço multicast 224.0.0.5. No entanto, há uma diferença: não são eleitos DR nem BDR. Por que isso acontece?

Como o nome do tipo de rede sugere, esses encapsulamentos são usados ​​para conexões "ponto a ponto" entre dois roteadores. Portanto, não faz sentido eleger um DR e um BDR. Os dois roteadores estabelecerão uma adjacência completa (*Full adjacency*) entre si, sem a necessidade de eleger um DR e um BDR.

### Interfaces Seriais

Certo, deixe-me fazer uma breve apresentação sobre conexões seriais. Digo "breve" porque as conexões seriais são uma tecnologia antiga que já não é muito comum. Elas ainda existem, mas o Ethernet é muito mais predominante. 

![](../../../../../../z_imgs/175235.png)

Esta foto mostra algumas interfaces e cabos seriais. Observe que tanto as portas quanto os cabos são diferentes dos cabos Ethernet. Para explicar as conexões seriais, vou mostrar como configuro a interface S2/0 do roteador R1. Primeiramente, um lado de uma conexão serial funciona como DCE, que significa *Data Communications Equipment* (Equipamento de Comunicação de Dados). O outro lado funciona como DTE, que significa *Data Terminal Equipment* (Equipamento Terminal de Dados). Por que isso é importante? 

![](../../../../../../z_imgs/175359.png)

Bem, em conexões seriais, o lado DCE precisa especificar a taxa de clock, ou seja, a velocidade da conexão. Portanto, neste caso, o R1 está conectado à extremidade DCE do cabo e, por isso, precisa informar ao R2 em qual velocidade a conexão irá operar. O comando é `clock rate`, e você pode ver alguns valores padrão que podem ser utilizados. Todos eles são expressos em bits por segundo, aliás. Configurei uma taxa de clock de 64.000 bits por segundo — ou seja, 64 kilobits por segundo — e adicionei um endereço IP e usei o comando `no shutdown`. 

> Aqui está um ponto importante. Interfaces Ethernet usam o comando `speed` para configurar a velocidade de operação da interface. Interfaces seriais usam o comando `clock rate`. Vamos continuar. 

Verifiquei a interface com `show interface s2/0`. Observe que o encapsulamento é HDLC.

![](../../../../../../z_imgs/072840.png)

Em roteadores Cisco, o encapsulamento padrão em uma interface serial é HDLC. Na verdade, é a versão da própria Cisco chamada "cHDLC" (Cisco HDLC), mas ela aparece apenas como "HDLC" na CLI. Mais uma vez, trata-se de um encapsulamento de Camada 2, assim como o Ethernet, exceto pelo fato de ser usado em conexões seriais. Aqui está a estrutura de um quadro HDLC, extraída da Wikipedia. 

![](../../../../../../z_imgs/073054.png)

Um detalhe importante é que não existe campo para endereço MAC. Portanto, endereços MAC, na verdade, não são utilizados. Mencionei também o encapsulamento PPP; vamos ver como configurar o roteador para usar esse encapsulamento. Basta usar o comando `encapsulation ppp` na interface.

![](../../../../../../z_imgs/073204.png)

Observe que, se você alterar o encapsulamento, ele deve ser compatível em ambas as extremidades; caso contrário, a interface ficará inativa (*down*). Se utilizarem encapsulamentos diferentes, é como se estivessem falando dois idiomas distintos: não conseguirão se comunicar. Executei o comando `show interface s2/0` novamente e você pode ver que o encapsulamento mudou para PPP. Fiz o mesmo no R2, aliás, então a interface está ativa (*up*). Aqui está a configuração que realizei no R1. 

![](../../../../../../z_imgs/073755.png)

O comando `serial restart-delay 0` já estava lá por padrão, então configurei apenas a *clock rate* (taxa de clock), o encapsulamento e o endereço IP. Na imagem também está ilustre a configuração no R2, sem o comando `clock rate`, pois ele é a extremidade DTE. Agora você deve estar se perguntando: como saber qual lado é DCE e qual é DTE? O comando para verificar isso é `show controllers`, seguido pelo ID da interface.

![](../../../../../../z_imgs/074106.png)

Como você pode ver, o R1 é o lado DCE e possui a *clock rate* de 64.000 bits que configurei. Usei o mesmo comando no R2; você pode ver que ele é o lado DTE e detectou os clocks de Tx (transmissão) e Rx (recepção) vindos do R1. Então, essa é uma visão geral bem básica sobre conexões seriais. Vamos voltar ao tipo de rede OSPF ponto a ponto.

## Ponto a ponto (cont.)

Aqui está a saída do comando `show ip ospf neighbor` no R2. 

![](../../../../../../z_imgs/074410.png)

Observe que o R2 tem uma adjacência completa com o R1, mas, em vez de DR, BDR ou DROTHER, é exibido um traço. Isso ocorre porque o tipo de rede ponto a ponto não utiliza DRs nem BDRs, como mencionei anteriormente. 

Um último ponto sobre este tópico: você pode configurar manualmente o tipo de rede utilizado por uma interface. O comando é `ip ospf network`, seguido pelo tipo de rede.

![](../../../../../../z_imgs/074658.png)

Você talvez note mais um tipo que não mencionei: o tipo de rede "ponto a multiponto". Ele é mais um "subtipo". Então, por que você alteraria o tipo de rede OSPF? Por exemplo, se dois roteadores estiverem conectados diretamente por um link Ethernet, como no diagrama abaixo, não há necessidade de DR/BDR. Você pode configurar o tipo de rede ponto a ponto nesse caso, embora não seja obrigatório. Observe que nem todos os tipos de rede funcionam em todos os tipos de link. Por exemplo, um link serial não pode utilizar o tipo de rede broadcast. Isso acontece porque links seriais não suportam quadros de broadcast de Camada 2, o que é necessário para o tipo de rede broadcast.

Uma coisa que ainda não mencionei é que redes ponto a ponto utilizam os mesmos temporizadores padrão que as redes broadcast. O temporizador Hello padrão é de 10 segundos e o temporizador Dead padrão é de 40 segundos. A título de informação, o tipo de rede não broadcast utiliza um temporizador Hello padrão de 30 segundos e um temporizador Dead de 120 segundos.

Certo, vamos seguir em frente. Agora, vamos analisar alguns requisitos para o estabelecimento de relações de vizinhança OSPF. 

## Requisitos de Vizinhança OSPF

Normalmente, roteadores se tornarão vizinhos OSPF sem problemas, mas vou apresentar alguns dos problemas que podem ocorrer. Já mencionei alguns deles em arquivos anteriores, mas vamos recapitular.

### Número da área deve coincidir

Primeiro requisito: o número da área deve coincidir para que dois roteadores se tornem vizinhos OSPF. 

![](../../../../../../z_imgs/075355.png)

Usaremos essa pequena topologia com dois roteadores para demonstrar. Nela, podemos ver a configuração OSPF do R1. O OSPF está habilitado na interface G0/0 na área 0. No entanto, a interface G0/0 do R2 está na área 1. Quando executo o comando `show ip ospf neighbor` em ambos os dispositivos, eles não apresentam vizinhos OSPF. Vamos corrigir o problema.

![](../../../../../../z_imgs/075655.png)

Alterei o comando *network* no R2 para usar a área 0. Como você pode ver, eles conseguiram se tornar vizinhos OSPF. Então, essa é a primeira regra. Para que dois roteadores se tornem vizinhos OSPF, eles devem estar na mesma área. Mas já abordamos isso antes. Próxima regra.

### Interfaces na mesma subrede

As interfaces devem estar na mesma sub-rede para se tornarem vizinhos OSPF. Também já abordamos isso antes, mas deixe-me demonstrar. Observe que as interfaces G0/0 do R1 e do R2 agora estão em sub-redes diferentes.

![](../../../../../../z_imgs/123052.png)

Ativei o OSPF em ambas as interfaces. Mas, ao verificar os vizinhos OSPF, eles não aparecem. Configurei novamente a interface do R2 na mesma sub-rede que a do R1 e também me certifiquei de editar o comando *network* para que o OSPF fosse ativado novamente na G0/0. Agora, R1 e R2 são vizinhos OSPF novamente.

![](../../../../../../z_imgs/123214.png)

A seguir, aqui está um ponto que ainda não abordamos. 

### Processo OSPF deve estar ativado

O processo OSPF não deve estar desativado (shutdown). Na verdade, você pode desativar ("shutdown") o processo OSPF no roteador, assim como faria com uma interface. Isso interrompe a operação do OSPF, sem remover as configurações do OSPF. Vamos ver como isso funciona. Veja como fazer. 

![](../../../../../../z_imgs/123436.png)

A partir do modo de configuração do OSPF no R2, usei o comando `shutdown`. Então, uma mensagem é exibida indicando que o vizinho R1 passou de FULL para DOWN, e nenhum vizinho aparece no comando `show ip ospf neighbor`. Em seguida, reativo o OSPF com o comando `no shutdown`. 

![](../../../../../../z_imgs/123643.png)

Uma mensagem indica que o vizinho está ativo novamente, e é possível vê-lo no comando `show ip ospf neighbor`. Isso não será um problema, a menos que você desative manualmente o processo OSPF; portanto, geralmente não é uma questão crítica. 

### Router IDs devem ser únicos

O próximo requisito é que os Router IDs do OSPF sejam únicos. Vamos ver como isso funciona. 

![](../../../../../../z_imgs/124002.png)

Eu não configurei os Router IDs de R1 e R2 e também não configurei nenhuma interface loopback; assim, cada roteador selecionou seu endereço IP da interface G0/0 como seu Router ID: 192.168.1.1 para o R1 e 192.168.1.2 para o R2. Então, configurei 192.168.1.1 como o Router ID do R2, o mesmo do R1. Como mostrei anteriormente, é necessário reiniciar o roteador ou usar o comando `clear ip ospf process` para que o novo Router ID entre em vigor. Então, usei o comando `clear ip ospf process`. 

Imediatamente, a adjacência com o vizinho cai, pois limpei o processo OSPF. Mas então, em vez de o vizinho voltar a ficar ativo, esta mensagem é exibida: "OSPF detectou um router-id duplicado 192.168.1.1 vindo de 192.168.1.1 na interface GigabitEthernet0/0", e então o vizinho permanece inativo. Então, vamos corrigir isso. Removi o router ID configurado manualmente com o comando `no router-id`. Observe que não é necessário especificar o router ID ao remover o comando. `no router-id` tem o mesmo efeito que `no router-id 192.168.1.1`; ambos removem o comando. 

Desta vez, sem precisar reiniciar o processo OSPF, o router ID do R2 retorna para 192.168.1.2 e o vizinho volta a ficar ativo. Por que não precisei usar o comando `clear ip ospf process`? Na verdade, eu não esperava isso, mas percebi que foi porque o R2 não tinha outros vizinhos OSPF naquele momento; assim, o roteador estava livre para alterar o router ID do R2 sem se preocupar com impactos em outros vizinhos.

Portanto, fique atento a router IDs duplicados. Próximo requisito. 

### Os temporizadores Hello e Dead devem coincidir

Em ambos os tipos de rede que analisamos hoje — Broadcast e Ponto a Ponto —, os valores padrão são 10 segundos e 40 segundos. Mas você pode alterar essas configurações manualmente. Os temporizadores Hello e Dead são configurados diretamente na interface. Veja como configurar o temporizador Hello: `ip ospf hello-interval`, seguido pelo intervalo em segundos. Eu defini para 5. Depois, o temporizador Dead. `ip ospf dead-interval`, e defini para 20. 

![](../../../../../../z_imgs/125035.png)

Como você pode ver, o vizinho fica inativo. Note que alterei ambos os valores, o temporizador Hello e o Dead, mas mesmo se você alterar apenas um, o vizinho ainda ficará inativo. Então, vamos corrigir isso. Usei `no ip ospf hello-interval` e `no ip ospf dead-interval` para retornar os temporizadores aos seus valores padrão. Observe o método que usei para retorná-los aos padrões; é o mesmo usado para o Router ID. Não precisei especificar `no ip ospf hello-interval 5` ou `dead-interval 20` para remover os comandos. De qualquer forma, agora que os temporizadores Hello e Dead coincidem novamente, o vizinho está ativo novamente.

Portanto, lembre-se de verificar os intervalos Hello e Dead se estiver tendo problemas com adjacências OSPF. 

### As configurações de autenticação devem coincidir.

O que isso significa? Bem, você pode configurar uma senha OSPF; assim, o roteador só estabelecerá adjacência com roteadores que possuam uma senha OSPF correspondente. Vamos dar uma olhada.

![](../../../../../../z_imgs/125536.png)

A senha OSPF também é configurada diretamente na interface. Usei o comando `ip ospf authentication-key`, seguido pela senha 'allysson'. Observe que isso não habilita, de fato, a autenticação OSPF na interface. A senha está configurada, mas precisamos habilitar a autenticação OSPF. Então, usei o comando `ip ospf authentication` para habilitá-la na interface. Em seguida, a adjacência cai, porque o R1 não está fornecendo ao R2 uma senha correspondente. Na verdade, ainda não configurei a autenticação OSPF no R1, então ele não está fornecendo nenhuma senha OSPF ao R2. 

Portanto, para resolver isso, poderíamos configurar as mesmas definições de autenticação no R1 ou remover a autenticação do R2. Eu as removi do R2 e, agora, a adjacência foi restabelecida. Certo, há mais duas coisas a mencionar.

### Configurações de IP MTU devem ser compatíveis.

O IP MTU é o tamanho máximo de um pacote IP que será enviado pela interface. O padrão geralmente é 1500 bytes, mas pode ser configurado. Observe que este requisito e o próximo são especiais: mesmo que as configurações não coincidam, os roteadores podem estabelecer adjacência OSPF, mas o OSPF não funcionará corretamente. Vamos ver.

![](../../../../../../z_imgs/173959.png)

Você pode configurar o IP MTU de uma interface com este comando: `ip mtu`, seguido pelo valor do MTU em bytes. Alterei para 1400 na interface G0/0 do R2, então não coincide com o valor padrão de 1500 na interface G0/0 do R1. Esperei um minuto e verifiquei a tabela de vizinhos; o R1 e o R2 na verdade continuaram sendo vizinhos. Então, reiniciei o processo OSPF no R2. Esperei um minuto, mas não surgiu nenhuma mensagem indicando que os vizinhos haviam atingido o estado FULL. 

Verifiquei a tabela de vizinhos novamente e ela estava travada no estado EXSTART. Após alguns minutos de espera, mais algumas mensagens foram exibidas — e elas continuavam se repetindo, aliás. Portanto, fica claro que o OSPF não está funcionando corretamente. Usei o comando `no ip mtu` para retornar o MTU ao valor padrão e, finalmente, o R1 e o R2 atingiram o estado FULL. Então, se seus vizinhos OSPF estiverem com dificuldade para atingir o estado FULL, não deixe de verificar as configurações de MTU. 

Certo, o último ponto. 

### Os tipos de rede OSPF devem coincidir

O tipo de rede OSPF deve coincidir. Vamos ver o que acontece se não coincidirem. Para demonstrar esse problema, configurei uma interface loopback no R2 com um endereço IP e a anunciei para o R1. 

![](../../../../../../z_imgs/174436.png)

Em seguida, alterei o tipo de rede na interface G0/0 do R2 para ponto a ponto. A interface G0/0 do R1 continua usando o tipo de rede padrão *broadcast*. Uma mensagem é exibida informando que a conexão com o vizinho caiu, mas logo em seguida ela voltou para o estado FULL. O R1 chega a exibir o estado FULL no comando `show ip ospf neighbor`. Então, qual é o problema? Vamos ver no R1.

![](../../../../../../z_imgs/174634.png)

O R2 aparece na tabela de vizinhos com o estado FULL, então você pode pensar que o OSPF está funcionando corretamente. Mas observe a tabela de roteamento. O endereço de loopback do R2 deveria estar na tabela de roteamento do R1, mas não está. É isso que acontece quando os tipos de rede OSPF não coincidem. Pode ser difícil diagnosticar o problema porque o estado do vizinho é Full, dando a impressão de que tudo está funcionando bem. Fique atento a isso ao solucionar problemas no OSPF. Certo, vou encerrar por aqui. 

O último tópico do arquivo são os tipos de LSA.

## Tipos de LSA do OSPF

Peguei a topologia anterior e a modifiquei, adicionando um link de Internet no R4. O R4 possui uma rota padrão para a Internet e
33:18
uso o comando DEFAULT-INFORMATION ORIGINATE para fazê-lo anunciar essa rota aos outros roteadores. Então, vamos falar sobre LSAs. Como você já sabe, o LSDB do OSPF é composto por LSAs. Todos os roteadores
33:31
na mesma área OSPF compartilham o mesmo LSDB. Existem 11 tipos de LSA, mas há apenas
33:38
3 que você precisa conhecer para o CCNA. Esses são do tipo 1, o "router LSA". O tipo 2, o
33:46
"network LSA". E o tipo 5, o "AS external LSA". Vamos dar uma breve olhada em cada
33:52
tipo. Primeiro, o tipo 1, o router LSA. Todo roteador que executa o OSPF gera esse tipo de
34:00
LSA. O router LSA identifica o roteador usando seu Router ID. O router LSA também lista
34:07
as redes conectadas às interfaces do roteador que estão com o OSPF ativado. Em seguida, o tipo 2, ou seja, o network
34:14
LSA. Ele é gerado pelo DR de cada rede de "acesso múltiplo" (multi-access). Um exemplo de rede de acesso múltiplo
34:22
é uma rede Ethernet que utiliza o tipo de rede broadcast. Esse tipo de LSA lista os roteadores
34:28
que estão conectados à rede de acesso múltiplo. O último tipo de hoje,



o tipo 5, também conhecido como AS-external
34:35
LSA. Esse tipo de LSA é gerado por ASBRs para descrever rotas para destinos fora
34:42
do sistema autônomo, ou seja, do domínio OSPF. Vamos dar uma olhada na LSDB do R1, usando o comando SHOW IP OSPF DATABASE. Observe que
34:53
não importa realmente em qual roteador eu executo o comando; a saída será a mesma, pois todos os roteadores da área possuem a mesma LSDB. Note que cada roteador gerou
35:03
um LSA de Roteador (Tipo 1) que o identifica. Essa visualização não mostra o conteúdo de cada LSA,
35:10
mas cada um desses LSAs de roteador contém informações sobre as redes às quais o roteador está conectado. Observe que existe apenas um LSA de Rede (Tipo 2), gerado pelo R4 para a sub-rede
35:23
192.168.2.0/29. Embora R1, R3 e R5 sejam DRs em suas interfaces G1/0, nenhum outro roteador
35:31
está conectado a essas interfaces; portanto, nenhum LSA Tipo 2 é gerado. Finalmente, note que um
35:37
LSA AS-External (Tipo 5) é gerado pelo R4. Ele está compartilhando sua rota padrão para a Internet
35:44
com os outros roteadores. Certo, isso é tudo sobre LSAs.
e com os conceitos básicos de interfaces seriais que apresentei neste vídeo. Em seguida, apresentei
36:46
alguns requisitos para vizinhos e adjacências OSPF. Você não precisa memorizar a lista completa,
36:52
mas certifique-se de conseguir identificar todos eles e solucionar eventuais problemas. Por fim, apresentei brevemente
36:58
os três tipos mais básicos de LSA do OSPF: Tipo 1, o Router LSA; Tipo 2, o Network LSA.
