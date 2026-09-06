Primeiro, vou mostrar o que é o EtherChannel e quais problemas ele resolve. Uma dica: o grande problema aqui é o Spanning Tree Protocol.  
1:05  
Também veremos vários métodos para configurar EtherChannels tanto de Camada 2 quanto de Camada 3.  
1:11  
Um EtherChannel de Camada 2 é um grupo de portas de switch que operam como uma única interface,  
1:17  
e um EtherChannel de Camada 3 é um grupo de portas roteadas que operam como uma única interface,  
1:22  
à qual você atribui um endereço IP, justamente por ser de Camada 3. Não deixe de assistir até o final do vídeo para ver uma pergunta bônus do Boson Software,  
1:31  
o ExSim, que oferece os melhores simulados para o exame CCNA. Eu usei o Boson ExSim para me preparar para os exames CCNA e CCNP e realmente acredito  
1:41  
que ele foi a chave para eu passar em todas as provas logo na primeira tentativa. Muito bem, vamos começar o vídeo.  
Por que o EtherChannel é necessário  
1:48  
Então, deixe-me demonstrar um problema. Temos dois switches aqui: ASW1 e DSW1.  
1:55  
Falarei sobre o design básico de redes mais adiante no curso, mas ASW significa *access switch* (switch de acesso),  
2:03  
que é o switch ao qual dispositivos finais, como PCs e servidores, se conectam. DSW significa *distribution layer switch* (switch da camada de distribuição),  
2:13  
ao qual os switches da camada de acesso se conectam. Para esta demonstração, vamos supor que haja muitos dispositivos finais conectados ao ASW1 — digamos,  
2:20  
40 dispositivos — e todos estejam tentando acessar a Internet para realizar suas tarefas.  
2:25  
O administrador da rede percebe que a conexão com o DSW1 está congestionada, então decide  
2:31  
adicionar outro link para aumentar a largura de banda e, assim, suportar todos os dispositivos finais.  
2:36  
O administrador adiciona, então, outro link e monitora a situação.  
2:42  
No entanto, o link adicional não parece ajudar. A conexão entre o ASW1 e o DSW1 continua congestionada e os usuários finais estão relatando problemas.  
2:52  
Então, o administrador decide adicionar outro link entre o ASW1 e o DSW1.  
2:58  
Ele adiciona mais um link à conexão entre o ASW1 e o DSW1. Certamente, isso será suficiente.  
3:05  
A largura de banda total das conexões com os hosts finais ainda é maior do que a largura de banda da conexão com o DSW1, mas tudo bem; nem todos os hosts da rede estão sempre em  
3:15  
um estado constante de envio e recebimento de tráfego da Internet. Falarei mais sobre isso mais adiante no curso, mas quando a largura de banda das interfaces conectadas  
3:24  
aos hosts finais é maior do que a largura de banda da conexão com os switches de distribuição,  
3:29  
isso é chamado de *oversubscription* (sobreassinatura ou excesso de subscrição). Certo nível de *oversubscription* é aceitável, mas o excesso causará congestionamento.  
3:37  
No entanto, mesmo com três links para o DSW1, o congestionamento não parece ter melhorado, então o  
3:43  
administrador de rede decide, mais uma vez, adicionar outro link entre o ASW1 e o DSW1.  
3:49  
Assim, agora existem quatro links entre o ASW1 e o DSW1.  
3:55  
Você acha que a situação melhorou? Bem, não melhorou; a conexão entre os dois switches continua tão congestionada quanto antes.  
4:03  
Por que isso acontece? Você deveria ser capaz de descobrir a resposta. Aqui vai uma dica: pense no que você acabou de estudar nos dias 20, 21 e 22 deste curso.  
4:13  
Se você sabe a resposta, parabéns; se não, não se preocupe, você saberá agora. Digamos que o administrador tenha ido verificar fisicamente as luzes das portas dos dois switches.  
4:23  
Que cor você acha que elas tinham? Bem, o administrador de rede verifica o DSW1 e todas as luzes das portas estão verdes, então não  
4:30  
parece haver um problema. No entanto, ao verificar o ASW1, ele percebe que, dos links conectados ao DSW1, apenas uma luz  
4:38  
está verde, enquanto as outras estão laranja. Por que isso acontece? É devido ao que estudamos nos últimos dias deste curso: o protocolo Spanning Tree.  
4:48  
Se você conectar dois switches usando múltiplos links, todos, exceto um, serão desativados pelo Spanning Tree.  
4:54  
Por que ele faz isso? Bem, se todas as interfaces do ASW1 estivessem encaminhando tráfego, loops de Camada 2 seriam formados entre o ASW1 e o  
5:02  
DSW1, resultando em tempestades de broadcast. Os outros links permaneceriam ociosos, a menos que o link ativo falhasse.  
5:10  
Nesse caso, um dos links inativos passaria a encaminhar tráfego. Portanto, embora ter links de backup seja algo positivo — já que falhas podem ocorrer por diversos  
5:19  
motivos —, é um desperdício de largura de banda manter essas três interfaces desativadas, sem encaminhar nenhum tráfego.  
5:25  
No entanto, ao combinar essas quatro interfaces físicas em uma única interface lógica, o EtherChannel pode  
5:31  
resolver esse problema, proporcionando tanto redundância quanto maior largura de banda.  
Introdução ao EtherChannel  
5:38  
Um EtherChannel é representado em diagramas de rede por um círculo desenhado ao redor das interfaces agrupadas, como mostrado aqui.  
5:45  
O EtherChannel agrupa múltiplas interfaces para que atuem como uma única interface.  
5:51  
O STP tratará esse grupo como uma interface única. Assim, após agrupar essas interfaces em um EtherChannel, o administrador de rede  
5:59  
verifica novamente as luzes dos links. Desta vez, todas estão verdes. Isso não causará um loop de Camada 2?  
6:06  
Na verdade, não, pois esse grupo de quatro links se comporta como se fosse um único link.  
6:13  
Por exemplo, digamos que um PC envie um quadro de broadcast. Então,


...ele é propagado (flooded) por todas as interfaces do ASW1.  
6:22  
Todos os PCs conectados ao ASW1 receberão uma cópia do quadro. Agora, quantas cópias do quadro o DSW1 receberá?  
6:29  
Lembre-se: embora existam quatro interfaces físicas, elas se comportam como uma única interface.  
6:36  
A resposta é: o DSW1 receberá apenas uma cópia. Esse EtherChannel transforma essas quatro interfaces físicas em uma única interface lógica; o ASW1  
6:46  
não enviará quatro cópias do mesmo quadro de broadcast a partir de uma única interface.  
6:52  
O tráfego que utiliza o EtherChannel terá sua carga balanceada entre as interfaces físicas do grupo.  
6:57  
Um algoritmo é usado para determinar qual tráfego utilizará qual interface física. Darei mais detalhes sobre isso mais adiante.  
7:04  
Então, o DSW1 recebeu o quadro de broadcast. O que ele fará agora?  
7:10  
Ele propagará o quadro de broadcast por todas as interfaces, exceto aquela pela qual o quadro foi recebido.  
7:15  
Digamos que o DSW1 tenha estes outros dois links aqui. Por quais interfaces o DSW1 encaminhará o quadro?  
7:23  
Apenas por essas duas. Por que ele não encaminhou o quadro pelas outras três interfaces do EtherChannel?  
7:29  
Vou repetir mais uma vez: embora esse EtherChannel contenha quatro interfaces físicas  
7:34  
separadas, elas se comportam como uma única interface. O DSW1 não enviará o quadro de broadcast de volta pela mesma interface pela qual ele foi recebido.  
7:42  
Portanto, ele não é encaminhado de volta ao ASW1, e nenhum loop de Camada 2 é formado.  
7:48  
Funciona mais ou menos assim: em vez de quatro interfaces separadas — talvez interfaces  
7:54  
Gigabit Ethernet — conectando o ASW1 ao DSW1, é como se houvesse uma única interface  
8:00  
Ethernet de quatro gigabits. A largura de banda das quatro interfaces separadas é combinada para formar uma interface mais rápida,  
8:06  
uma interface virtual de quatro gigabits. A diferença entre as características físicas e as características lógicas ou virtuais  
8:15  
de uma rede é algo que você precisa entender como engenheiro de redes. Por exemplo, estudamos as VLANs.  
8:23  
Vários PCs podem estar conectados ao mesmo switch e, portanto, na mesma LAN; no entanto,  
8:29  
as VLANs dividem virtualmente esses PCs em LANs virtuais separadas, cada uma comportando-se como uma  
8:35  
LAN distinta. Da mesma forma, essas interfaces existem como quatro interfaces físicas separadas, mas agora formam uma única  
8:43  
interface virtual. Outros nomes para EtherChannel são Port Channel e LAG, que significa Link  
8:51  
Aggregation Group (Grupo de Agregação de Links). Você verá que, para configurar um EtherChannel no Cisco IOS, é preciso usar alguns  
8:58  
termos diferentes. Agora, vamos ver como o EtherChannel realiza o balanceamento de carga.  
Balanceamento de Carga no EtherChannel  
9:04  
Ele realiza o balanceamento de carga com base em "fluxos". O que é um fluxo? Um fluxo é uma comunicação entre dois nós na rede.  
9:12  
Como, por exemplo, entre o PC1 e o SRV1. Aliás, normalmente você não verá um servidor ou uma impressora conectados diretamente a um switch da camada de distribuição;  
9:21  
esses também são dispositivos finais (end hosts) que você deve conectar aos switches da camada de acesso.  
9:27  
No entanto, apenas para simplificar este diagrama de rede, vou deixá-lo assim. Então, digamos que o PC1 inicie uma troca de dados com o SRV1 e envie alguns quadros  
9:36  
para isso. O quadro é recebido pelo ASW1 e, supondo que ele já conheça o endereço MAC do SRV1,  
9:44  
ele encaminhará o quadro através do Port Channel para o DSW1. Mas qual interface física ele usará?  
9:51  
Bem, existe um algoritmo utilizado para calcular por qual interface física o tráfego será realmente enviado; digamos que ele determine que esta interface deve ser usada. 10:01  
Agora, quando o PC1 envia o próximo quadro do fluxo, na comunicação entre o PC1 e  
10:07  
o SRV1, a mesma interface será usada para encaminhar o tráfego para o SRV1. Portanto, a questão é que quadros de um mesmo fluxo serão encaminhados usando a mesma interface  
10:17  
física. Se quadros de um mesmo fluxo fossem encaminhados usando interfaces físicas diferentes, alguns  
10:22  
quadros poderiam chegar ao destino fora de ordem, o que pode causar problemas.  
10:28  
Algumas aplicações conseguem lidar com quadros que chegam fora de ordem, mas outras não. Agora, se o PC1 quiser imprimir algo e iniciar um fluxo de comunicação separado com a PR1, o ASW1  
10:40  
encaminhará novamente o quadro usando sua interface virtual de *port channel*. No entanto, ele fará um cálculo separado para determinar qual interface física  
10:49  
será usada para o fluxo. Por exemplo, ele pode determinar que esta interface será usada para o fluxo.  
10:55  
Assim como antes, quando o PC1 envia outro quadro do fluxo, a mesma interface membro  
11:00  
do *EtherChannel* será usada para encaminhá-lo. E se o PC2 também quiser imprimir algo?  
11:07  
Ele envia o primeiro quadro do fluxo para o ASW1, que então fará um cálculo para determinar qual interface física do *EtherChannel* será usada.  
11:15  
Talvez esta seja a escolhida. Então, é assim que o *EtherChannel* realiza o balanceamento de carga: usando interfaces físicas diferentes  
11:23  
dentro do *EtherChannel* para fluxos diferentes. O cálculo realizado para determinar qual interface física usar leva em  
11:30  
conta alguns parâmetros de entrada.


Na verdade, você pode alterar os parâmetros de entrada usados no cálculo de seleção de interface.  
11:37  
Aqui estão os parâmetros que podem ser usados: endereço MAC de origem. Assim, todos os quadros com o mesmo endereço MAC de origem usarão sempre a mesma interface no  
11:46  
EtherChannel. Ou o endereço MAC de destino. Nesse caso, todos os quadros com o mesmo endereço MAC de destino usarão sempre a mesma interface  
11:56  
física. Você também pode usar ambos os endereços MAC, de origem E de destino.  
12:02  
Por exemplo, quadros do PC1 para o SRV1 usarão sempre uma determinada interface; quadros  
12:08  
do PC2 para o SRV1 usarão sempre uma determinada interface, que pode ser a mesma ou diferente  
12:14  
daquela usada para o tráfego do PC1 para o SRV1; quadros do PC1 para o PR1 podem usar outra  
12:20  
interface diferente, etc. O cálculo é feito com base nos endereços MAC de origem e de destino.  
12:28  
Você também pode configurar o EtherChannel para selecionar a interface com base no endereço IP de origem,  
12:34  
endereço IP de destino ou em ambos os endereços IP, de origem E de destino.  
12:40  
Alguns switches também suportam balanceamento de carga com base nos números de porta TCP ou UDP da Camada 4,  
12:46  
mas esse é um assunto para outra aula. Além disso, os métodos que o switch pode utilizar dependem do modelo do switch; alguns podem suportar apenas  
12:54  
o uso de endereços MAC, outros podem suportar apenas endereços MAC ou IP, e alguns podem suportar  
13:00  
todos os métodos. Então, ainda não configuramos um EtherChannel, mas, já que o mencionei, vamos  
Verificação e configuração do balanceamento de carga do EtherChannel  
13:08  
dar uma olhada em como verificar e configurar o método de balanceamento de carga. Use o comando SHOW ETHERCHANNEL LOAD-BALANCE para ver o método de balanceamento de carga atual.  
13:19  
Você pode ver que o padrão para este modelo de switch é realizar o balanceamento de carga com base nos endereços IP de origem e de destino. 13:25  
Então, por exemplo, todo o tráfego vindo de 10.0.0.1 com destino a 10.0.0.2 sempre  
13:34  
usará uma determinada interface física dentro do EtherChannel. Aqui embaixo, você pode ver um detalhamento mais específico.  
13:41  
Quadros que encapsulam pacotes IP, sejam IPv4 ou IPv6, terão seu balanceamento de carga realizado com base  
13:47  
nos endereços IP de origem e destino. No entanto, observe que, na parte superior, é indicado que tráfego não-IP usará os endereços MAC de origem e destino.  
13:56  
Bem, isso acontece porque, se um pacote IP não estiver encapsulado no quadro Ethernet, não  
14:02  
há endereço IP que possa ser usado para determinar o balanceamento de carga; portanto, os endereços MAC são  
14:07  
usados em seu lugar. Agora, quanto a como alterar o método de balanceamento de carga, entre no modo de configuração global e use este  
14:14  
comando: `port-channel load-balance`, seguido pelo método.  
14:20  
Neste caso, alterei para usar os endereços MAC de origem e destino do quadro.  
14:26  
Depois confirmei mais uma vez, e você pode ver que a configuração de balanceamento de carga foi alterada com sucesso.  
14:32  
A propósito, aqui estão as opções disponíveis neste dispositivo. Ele pode realizar o balanceamento de carga com base em endereços MAC ou IP e, em ambos os casos, pode fazê-lo com base  
14:41  
nos endereços de origem, de destino ou em ambos (origem E destino).  
14:47  
Agora, quero destacar um ponto que é um pouco frustrante na configuração de EtherChannel em dispositivos Cisco.  
14:55  
Qual palavra-chave você usa para configurar o método de balanceamento de carga? `port-channel`.  
15:00  
E qual palavra-chave você usa para visualizar o método de balanceamento de carga? `etherchannel`.  
15:06  
Palavras diferentes são usadas para a mesma coisa, o que é um pouco frustrante. Na verdade, mais adiante você descobrirá que há ainda mais uma que precisa memorizar. 15:15  
Então, estes são os dois primeiros comandos para lembrar neste vídeo: `SHOW ETHERCHANNEL LOAD-BALANCE`, para verificar o método de balanceamento de carga em uso.  
15:23  
E `PORT-CHANNEL LOAD-BALANCE`, seguido pelo método de balanceamento de carga, para configurar o  
15:29  
balanceamento de carga. Agora, vamos passar para a criação efetiva de um EtherChannel entre dois switches.  
Protocolos de EtherChannel - PAgP, LACP, Estático  
15:36  
Existem três métodos de configuração de EtherChannel. O primeiro é o PAgP, que significa *Port Aggregation Protocol* (Protocolo de Agregação de Portas).  
15:45  
É um protocolo proprietário da Cisco, portanto, só pode ser usado em switches Cisco.  
15:51  
Se você estiver tentando formar um EtherChannel com um switch Juniper, por exemplo, não poderá usar o PAgP.  
15:56  
Agora, o que o PAgP faz? Ele negocia dinamicamente a criação e a manutenção do EtherChannel.  
16:05  
Há poucos dias, abordamos o DTP, que faz algo semelhante em relação à formação de troncos (*trunks*).  
16:11  
Quadros são enviados ao switch vizinho para verificar se ele deseja formar um EtherChannel e, então, os switches concordam ou não em formar o EtherChannel.  
16:19  
Certo, o próximo método de configuração é o LACP, que significa *Link Aggregation Control*  
16:26  
*Protocol* (Protocolo de Controle de Agregação de Links). É um protocolo padrão da indústria — mais uma vez, dos nossos amigos do IEEE; seu código  
16:32  
é 802.3ad. Basicamente, ele faz a mesma coisa que o PAgP.  
16:39  
Ele negocia dinamicamente a criação e a manutenção do EtherChannel, assim como o DTP faz para troncos.  
16:46  
Por ser um padrão da indústria...


protocolo padrão; ele não funciona apenas em switches Cisco, então  
16:51  
pode ser usado para formar EtherChannels com switches de outros fabricantes. Por isso, o LACP é o método preferido para configurar EtherChannels.  
17:01  
Na verdade, a lista de tópicos do exame menciona apenas o LACP. No entanto, para a prova, você realmente deve estar familiarizado com os outros métodos, pois, por algum  
17:10  
motivo, as listas de tópicos de exames da Cisco não são muito confiáveis. Então, o último método é o EtherChannel estático.  
17:19  
Nesse caso, não se utiliza um protocolo para determinar se um EtherChannel deve ser formado.  
17:24  
Em vez disso, as interfaces são configuradas estaticamente para formar um EtherChannel. Isso geralmente é evitado, pois o ideal é que os switches mantenham o EtherChannel de forma dinâmica;  
17:34  
por exemplo, você quer que o switch remova uma interface do EtherChannel caso ocorra algum tipo de problema nela.  
17:40  
Certo, por fim: é possível agrupar até 8 interfaces em um único EtherChannel.  
17:46  
Na verdade, o LACP permite até 16, mas apenas 8 ficam ativas; as outras 8 permanecem em modo de espera  
17:53  
(standby), aguardando a falha de uma interface ativa. Então, vamos ver como configurar cada método.  
Configuração de EtherChannel – PAgP  
18:01  
A configuração de cada um é quase idêntica; basta substituir algumas palavras-chave.  
18:07  
Primeiro, usei o comando `interface range` para configurar todas as interfaces membro de uma só vez.  
18:12  
Essa é uma boa prática para EtherChannel, pois as configurações de cada interface membro precisam ser idênticas; ao configurá-las simultaneamente, você garante isso.  
18:21  
Falarei mais sobre isso depois de mostrar as configurações. De qualquer forma, para configurar o EtherChannel propriamente dito, utilize este comando, que inclui mais uma palavra-chave nova. 18:31  
CHANNEL-GROUP, seguido por um número que identifica a interface virtual, MODE e, então, como você  
18:37  
pode ver, usei o ponto de interrogação para verificar quais opções estão disponíveis. Existem cinco opções: duas são usadas para PAgP, duas para LACP e uma para EtherChannel  
18:48  
estático. Estas duas são usadas para PAgP. Você reconhece esses nomes de algum outro protocolo proprietário da Cisco?  
18:57  
O DTP usava os mesmos modos para formar trunks, e a função de cada modo é basicamente a  
19:03  
mesma. O modo "desirable" tenta ativamente formar um EtherChannel, enquanto o modo "auto" só formará um EtherChannel  
19:10  
se o outro lado estiver configurado como "desirable", mas não se o outro lado estiver configurado como "auto".  
19:16  
Então, aqui está um resumo: se ambos os lados da conexão estiverem configurados como "auto", nenhum EtherChannel será formado.  
19:23  
No entanto, "auto" e "desirable", ou "desirable" e "desirable", formarão um EtherChannel.  
19:29  
De qualquer forma, decidi configurar este lado como "desirable". Você pode ver que a interface virtual "port-channel" foi criada, com o número que  
19:38  
usamos no comando channel-group. Você pode vê-la aqui na saída do comando SHOW IP INTERFACE BRIEF, lá embaixo.  
19:46  
Então, lembre-se de que o comando CHANNEL-GROUP é usado para configurar o EtherChannel, mas  
19:52  
o nome da interface virtual criada é "port-channel". Aliás, esse número do grupo de canal (channel group) precisa coincidir entre as interfaces do mesmo switch;  
20:02  
no entanto, ele NÃO precisa coincidir com o número do channel-group no outro switch. Por exemplo, o channel-group 1 no ASW1 pode formar um EtherChannel com o channel-group 2 no DSW1.  
20:14  
O número serve apenas para identificar a interface virtual no switch local. 20:20  
Como é possível ter múltiplos EtherChannels em um único switch, você precisa de um número para identificá-los.  
Configuração de EtherChannel - LACP  
20:27  
A seguir, vamos ver a configuração do LACP. Depois de explicar tudo isso, não há muito mais o que explicar sobre o LACP.  
20:36  
Observe apenas que os nomes dos modos são diferentes. Em vez de *desirable*, o LACP usa o modo *active*.  
20:43  
E, em vez de *auto*, o LACP usa o modo *passive*. Portanto, se ambas as pontas estiverem configuradas no modo *passive*, um EtherChannel não será formado.  
20:52  
No entanto, as combinações *active* e *passive*, ou *active* e *active*, formarão um EtherChannel.  
20:58  
Neste caso, configurei este lado como *active*. Mais uma vez, a interface *port-channel* é criada.  
21:05  
Note que, mesmo se você configurar ambos os lados como *passive*, a interface virtual ainda será criada em cada switch.  
21:12  
No entanto, ela não funcionará efetivamente como um EtherChannel a menos que um dos lados esteja no modo *active*.  
21:18  
Assim, como você pode ver, o comando é basicamente o mesmo; apenas os nomes dos modos são diferentes.  
21:24  
Mais uma vez, o número do *channel-group* deve coincidir entre as interfaces membro no switch local, mas não precisa coincidir com o número no switch vizinho.  
Configuração de EtherChannel - Estático  
21:32  
Finalmente, vamos ver como o EtherChannel estático é configurado. Não existem dois modos separados, apenas um: o modo "ON", que instrui manualmente essas interfaces  
21:42  
a formar um EtherChannel. Isso criará uma interface *port-channel*, assim como antes.  
21:48  
Vale ressaltar que o modo "on" só funciona com o modo "on". As combinações "on" e *desirable*, ou "on" e *active*, não formarão um EtherChannel com sucesso.  
Configuração manual do protocolo de negociação (PAgP ou LACP)


)  
21:59  
Outro comando que você deve conhecer é o comando CHANNEL-PROTOCOL. Ele configura manualmente o protocolo de negociação do EtherChannel que as interfaces membro  
22:07  
devem utilizar. Na verdade, esse comando não é muito útil, pois não há necessidade de configurá-lo.  
22:14  
Se você configurar CHANNEL-GROUP 1 MODE DESIRABLE ou AUTO, a interface utilizará automaticamente  
22:20  
o PAgP; ou, se configurar CHANNEL-GROUP 1 MODE ACTIVE ou PASSIVE, a interface  
22:27  
utilizará automaticamente o LACP. Portanto, não faz muito sentido usar esse comando.  
22:32  
No entanto, acho que você deve conhecê-lo, pelo menos para o exame; então, aqui está uma breve explicação.  
22:38  
É claro que existem duas opções, LACP e PAgP, e decidi configurar o LACP.  
22:45  
Então, tentei o comando CHANNEL-GROUP 1 MODE DESIRABLE, mas ele foi rejeitado devido à  
22:50  
incompatibilidade de protocolos. Eu havia configurado manualmente essas interfaces para usar LACP, mas o modo "desirable" (desejável) refere-se ao PAgP,  
22:59  
por isso o comando foi rejeitado. Se eu tentar CHANNEL-GROUP 1 MODE ON, ele também é rejeitado.  
23:06  
Então, executo CHANNEL-GROUP 1 MODE ACTIVE e o comando funciona, pois o modo ativo corresponde  
23:11  
ao LACP. Assim, após configurar o EtherChannel — seja em qual modo for: PAgP, LACP ou estático —, você  
23:21  
pode configurar a própria interface port-channel. Note que estou usando apenas o exemplo do LACP aqui, já que todas essas informações são  
23:29  
as mesmas, independentemente do método utilizado. Também realizei as mesmas configurações no DSW1, de modo que o EtherChannel está operacional.  
23:38  
Entrei no modo de configuração da interface port-channel 1 e a configurei como trunk. 23:46  
Agora, na saída do comando `SHOW INTERFACES TRUNK`, você pode ver o port-channel 1, listado como Po1,  
23:52  
como um trunk. Observe que as interfaces físicas individuais não são listadas aqui, apenas a interface  
23:59  
port-channel. Aqui está uma parte da saída do comando `SHOW RUNNING-CONFIG`. Há algo interessante a notar aqui.  
24:06  
As configurações de trunk que apliquei à interface port-channel também foram aplicadas às interfaces físicas; eu não configurei manualmente as interfaces físicas como trunks.  
24:17  
Agora, mais um ponto importante sobre a configuração do EtherChannel.  
Requisitos do EtherChannel (correspondência de duplex, velocidade, etc.)  
24:23  
As interfaces membro — as interfaces físicas no EtherChannel — devem ter configurações compatíveis.  
24:29  
O que quero dizer com isso? Elas devem ter a mesma configuração de duplex. Devem ter a mesma velocidade.  
24:36  
Devem ter o mesmo modo de porta (switchport mode), ou seja, acesso ou trunk. Se forem trunk, devem ter as mesmas VLANs permitidas e VLANs nativas.  
24:45  
Se as configurações de uma interface individual não coincidirem com as das outras, ela será excluída  
24:50  
do EtherChannel. Ao verificar o status de um EtherChannel usando comandos `SHOW`, o comando mais  
Verificação do EtherChannel (show etherchannel summary)  
24:58  
útil é o `SHOW ETHERCHANNEL SUMMARY`. Aqui embaixo há uma lista das interfaces port-channel no switch.  
25:06  
Ao lado do port-channel 1, há duas flags: um "S" maiúsculo e um "U" maiúsculo.  
25:13  
Para verificar o significado delas, observe a legenda na parte superior. "S" significa que é um EtherChannel de Camada 2 (Layer 2).  
25:20  
"S" vem de *switchport*, aliás. "U" significa *in use* (em uso), indicando que o EtherChannel está ativo e sendo utilizado.  
25:29  
Ao lado das portas físicas, há a flag "P". Isso significa que essas portas estão corretamente agrupadas no port-channel.  
25:36  
Estas são as flags que você espera ver em um EtherChannel de Camada 2 operacional. Agora, vamos analisar algumas situações em que veremos outras flags.  
25:45  
Então, desativei (shutdown) a interface port-channel 1. Agora, ao lado tanto da interface port-channel quanto das interfaces membro, você pode ver a  
25:54  
flag "D". Isso significa "down" (inativa). Certo, vou reativar a interface e mostrar outra flag que você pode encontrar.  
26:04  
Agora alterei uma das interfaces membro para o modo de acesso. Agora ela apresenta a flag "s" minúscula.  
26:11  
Observe que isso é diferente da flag "S" maiúscula. Ela significa "suspended" (suspensa). Portanto, apenas a G0/0 está suspensa, mas o EtherChannel continua operando com apenas três interfaces:  
26:22  
G0/1, 2 e 3. Outro comando que você pode usar é o SHOW ETHERCHANNEL PORT-CHANNEL.  
Verificação do EtherChannel (show etherchannel port-channel)  
26:31  
Você pode ver o número de portas no port-channel, qual protocolo está sendo usado, etc.  
26:37  
Uma informação importante que não aparece no SHOW ETHERCHANNEL SUMMARY, mas é exibida neste comando, é o modo do channel-group — "active" (ativo), neste caso, porque usei  
26:47  
o comando CHANNEL-GROUP 1 MODE ACTIVE anteriormente. No entanto, para EtherChannel, o comando que você certamente mais utilizará é o  
26:55  
SHOW ETHERCHANNEL SUMMARY. Eu só queria mostrar outra opção.  
27:01  
Como comecei este vídeo falando sobre Spanning Tree, vamos ver como ele é afetado quando o EtherChannel é configurado.  
27:08  
Como você pode ver, apenas a interface port-channel é listada; as interfaces físicas não aparecem de forma alguma na saída deste comando.  
27:15  
Então, como eu disse...



...o Spanning Tree trata essas quatro interfaces físicas como uma única  
27:21  
interface lógica. Em vez de bloquear três delas, todas podem encaminhar e receber tráfego, sem a preocupação  
27:27  
com loops de Camada 2. Para encerrar esta aula, vamos dar uma breve olhada nos EtherChannels de Camada 3.  
EtherChannel de Camada 3  
27:35  
Substituí o ASW1 e o DSW1 por switches multicamada (multilayer switches).  
27:40  
Em vez de uma conexão de Camada 2 entre eles, vamos usar uma conexão de Camada 3.  
27:45  
O design de redes moderno frequentemente tende a utilizar conexões de Camada 3 entre switches, pois  
27:50  
dessa forma o Spanning Tree não será um problema em nenhuma parte da rede. Poderíamos ter quatro switches interconectados em uma malha (mesh) e, se os conectássemos  
27:59  
com portas roteadas de Camada 3, todas as interfaces estariam ativas e encaminhando tráfego; nenhuma precisaria  
28:04  
ser desativada devido ao Spanning Tree. Agora você pode estar pensando: você não acabou de mostrar que o EtherChannel significa que o Spanning Tree  
28:11  
não precisa bloquear nenhuma porta? Bem, estamos analisando apenas uma conexão entre dois switches.  
28:17  
Mesmo usando EtherChannel, loops de Camada 2 ainda podem ocorrer se vários switches estiverem conectados entre si formando um loop.  
28:24  
Por exemplo, veja este diagrama. Todas as conexões entre os switches utilizam EtherChannel, mas se não bloquearmos  
28:30  
nenhuma das interfaces port-channel, os broadcasts ainda podem circular pelos switches dessa maneira  
28:36  
e causar uma tempestade de broadcast (broadcast storm). Portanto, o Spanning Tree bloqueará uma dessas interfaces port-channel.  
28:42  
No entanto, se todas essas conexões entre switches fossem feitas usando portas roteadas, e não portas de switch de Camada 2, não haveria necessidade alguma de executar o Spanning Tree.  
28:52  
Portas roteadas não encaminham broadcasts de Camada 2; logo, não podem ser formados loops de Camada 2. 28:57  
Você já sabe como configurar portas roteadas com o comando NO SWITCHPORT. Vamos ver como configurar um EtherChannel de Camada 3.  
29:05  
Então, começando de uma configuração limpa, nenhum port-channel foi configurado ainda no ASW1.  
29:11  
Entro no modo de configuração de intervalo de interfaces (*interface range*) para as interfaces membro e, desta vez, antes de usar  
29:17  
o comando CHANNEL-GROUP, uso o comando NO SWITCHPORT para transformá-las em interfaces roteadas de Camada 3.  
29:24  
Depois, após usar o comando CHANNEL-GROUP, utilizei o comando SHOW RUNNING-CONFIG para verificar a configuração.  
29:31  
Observe que a interface port-channel criada recebe o comando NO SWITCHPORT automaticamente.  
29:37  
Agora, como estamos criando um EtherChannel de Camada 3, precisamos de um endereço IP.  
29:43  
Onde você acha que ele deve ser configurado? Ele deve ser configurado na interface port-channel.  
29:48  
Então, aí está. Agora, vamos verificar o comando SHOW ETHERCHANNEL SUMMARY mais uma vez.  
29:54  
A única diferença na saída é que, em vez da flag 'S' (maiúscula), ela  
29:59  
apresenta a flag 'R'. O que isso significa? Significa que é um EtherChannel de Camada 3; 'R' significa porta roteada (*routed port*).  
30:08  
Na saída do comando SHOW IP INTERFACE BRIEF, você pode ver o endereço IP configurado na interface port-channel  
30:14  
1. Assim, agora o ASW1 e o DSW1 funcionam como dois roteadores conectados entre si.  
30:19  
Eles estão conectados na Camada 3 e o Spanning Tree não está em execução na conexão entre eles.  
30:26  
No entanto, assim como no EtherChannel de Camada 2, o tráfego agora será balanceado entre as  
30:31  
quatro interfaces membro. Certo, vamos revisar rapidamente os comandos que abordamos. Revisão dos comandos de configuração e verificação  
30:38  
O primeiro é o `PORT-CHANNEL LOAD-BALANCE`, seguido pelo modo que, dependendo do modelo do switch, pode envolver endereços MAC, endereços IP ou números de porta da Camada 4, utilizando  
30:49  
a origem, o destino ou ambos (origem e destino) no cálculo para determinar qual interface física  
30:56  
é usada para encaminhar um fluxo de tráfego específico. Para visualizar a configuração atual de balanceamento de carga do EtherChannel, use `SHOW ETHERCHANNEL LOAD-BALANCE`.  
31:07  
Para configurar uma interface para fazer parte de um EtherChannel, use o comando `CHANNEL-GROUP`, seguido pelo número do port-channel, `MODE` e, em seguida, o modo, que pode ser `DESIRABLE`,  
31:18  
`AUTO`, `ACTIVE`, `PASSIVE` ou `ON`. O comando `show` mais útil para EtherChannel é o `SHOW ETHERCHANNEL SUMMARY`, que exibe um  
31:27  
resumo de todos os EtherChannels no switch e seus status. Outro comando `show` que você pode usar é o `SHOW ETHERCHANNEL PORT-CHANNEL`, que exibe  
31:36  
informações mais detalhadas sobre as interfaces port-channel no switch.  
31:42  
Esses são todos os comandos que aprendemos hoje. Claro, existem muitos outros comandos que podem ser usados, mas não precisamos nos aprofundar  
31:48  
mais no conceito de EtherChannels. Desde que você entenda o objetivo básico deles e saiba como configurá-los e verificar seus status,  
31:56  
você estará bem preparado para o CCNA. Certo, vamos para o quiz de hoje.  
32:02  
Assista até o final do quiz para ver uma pergunta bônus do Boson ExSim para CCNA —  
32:07  
sem dúvida, os melhores simulados para o CCNA, e aqueles que usei ao me preparar para os meus  
32:13  
exames CCNA e CCNP.


