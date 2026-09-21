# OSPF 

## Tópicos que abordaremos
Então, vamos ver o que abordaremos neste arquivo. Primeiro, apresentarei algumas das operações básicas do OSPF (esta será apenas uma introdução rápida, em outro artigo, vamos nos aprofundar realmente no assunto). Depois, falarei sobre as áreas do OSPF, que são um recurso exclusivo do protocolo, dividindo redes maiores em seções menores. Por fim, mostrarei algumas configurações básicas do OSPF, assim como fiz anteriormente para o RIP e o EIGRP. 

Certo, vamos começar com o OSPF.

## Revisão – Tipos de Protocolos de Roteamento Dinâmico

Primeiramente, aqui está o mesmo gráfico dos diferentes tipos de protocolos de roteamento que mostrei antes.

![](../../../../../../z_imgs/123046.png)

Lembre-se de que o OSPF é um protocolo de roteamento dinâmico do tipo *Link State* (estado do enlace). Você verá neste arquivo que ele funciona de maneira bem diferente dos protocolos de roteamento do tipo *Distance Vector* (vetor de distância), como o RIP e o EIGRP. Para recapitular: protocolos *Distance Vector* utilizam o conceito de "roteamento por boato" (*routing by rumor*), no qual cada roteador compartilha informações sobre as rotas que conhece e o custo da métrica para alcançar cada destino. No entanto, os roteadores não possuem um mapa completo da rede; eles apenas utilizam as informações fornecidas pelos roteadores vizinhos para determinar a melhor rota para cada destino.

Agora, vamos revisar como funcionam os protocolos *Link State*.

## Revisão – Como funcionam os protocolos *Link State*

Ao utilizar um protocolo de roteamento *Link State*, cada roteador cria um "mapa de conectividade" da rede. Para permitir isso, cada roteador anuncia informações sobre suas interfaces (suas redes conectadas) aos seus vizinhos. Esses anúncios são repassados ​​a outros roteadores, até que todos os roteadores da rede construam o mesmo mapa da rede. Isso é importante: todos os roteadores possuem o mesmo mapa completo da rede.

Então, cada roteador usa esse mapa de forma independente para calcular as melhores rotas para cada destino. Devido a esse processo, os protocolos de estado de link consomem mais recursos do roteador, pois mais informações são compartilhadas. Eles exigem mais do roteador. No entanto, os protocolos de estado de link tendem a reagir mais rapidamente a mudanças na rede do que os protocolos de vetor de distância.

Essa foi uma breve revisão dos protocolos de roteamento de estado de link. Agora, vamos nos aprofundar no funcionamento do OSPF; você entenderá melhor o significado de tudo isso e verá como ele difere do RIP e do EIGRP, mas também perceberá as semelhanças. Então, vamos começar com o OSPF.

## Introdução ao OSPF

OSPF significa "Open Shortest Path First" (Abrir o Caminho Mais Curto Primeiro). O protocolo OSPF utiliza o algoritmo "shortest path first" (caminho mais curto primeiro), criado pelo cientista da computação holandês Edsger Dijkstra. Outro nome para o algoritmo é "algoritmo de Dijkstra".

Existem três versões do OSPF.

- A versão 1 foi lançada em 1989. É antiga e não é mais utilizada.
- A versão 2 foi lançada em 1998 e é, tipicamente, a versão utilizada em redes IP versão 4.
- Existe também o OSPF versão 3, desenvolvido para IPv6. Ele também pode ser usado com IPv4, mas a versão 2 é mais comum em redes IPv4.

Certo, agora alguns pontos gerais sobre o OSPF.

Os roteadores armazenam informações sobre a rede em LSAs (Link State Advertisements — Anúncios de Estado de Link), que são organizados em uma estrutura chamada LSDB (Link State Database — Banco de Dados de Estado de Link). LSA e LSDB são dois termos importantes no OSPF. Falarei mais sobre eles ao longo destes arquivos sobre o protocolo.

Os roteadores propagam (fazem o *flood* de) LSAs até que todos os roteadores na área OSPF tenham o mesmo mapa da rede, ou seja, o mesmo LSDB. Portanto, esses são mais dois termos importantes: *flood* e *area* (área). 

Você já conhece o termo *flood*; os switches fazem isso quando recebem um quadro de *broadcast* ou *unicast* desconhecido. No caso do OSPF, isso significa enviar os LSAs para todos os seus vizinhos OSPF. As "áreas" do OSPF são uma característica única do protocolo, e falarei mais sobre elas mais adiante neste arquivo. Deixe-me detalhar brevemente sobre LSAs e o LSDB.

### Propagação (Flood) de LSA

![](../../../../../../z_imgs/125436.png)

Então, digamos que esta rede de quatro roteadores esteja executando o OSPF. Todos esses roteadores são vizinhos OSPF, possuem o mesmo banco de dados de estado de link e a rede está estável. Então, o OSPF é habilitado na interface G1/0 do roteador R4.

Assim, o R4 precisa informar aos outros roteadores sobre esse novo segmento de rede. Para isso, o R4 cria um LSA para comunicar aos seus vizinhos a existência da rede na interface G1/0. Um LSA do OSPF contém algumas informações básicas, como o RID, ou seja, o ID do roteador. Para esta demonstração, o ID do roteador R4 é 4.4.4.4; nenhuma de suas interfaces físicas possui o endereço IP 4.4.4.4; portanto, ou o R4 tem uma interface de loopback com o endereço IP 4.4.4.4, ou o ID do roteador foi configurado manualmente.

A rede na interface G1/0 está, naturalmente, incluída no LSA, já que esse é o objetivo principal do LSA. O custo do R4 também está incluído. Falarei mais sobre a métrica do OSPF, chamada de custo, no próximo arquivo, mas esta interface GigabitEthernet tem um custo de 1. 

![](../../../../../../z_imgs/173624.png)

O LSA é então propagado (flooded) por toda a rede até que todos os roteadores recebam uma cópia. O processo ocorre desta forma. 

![](../../../../../../z_imgs/173924.png)

Isso resulta em todos os roteadores da área OSPF possuindo o mesmo LSDB. O LSDB tem esta aparência da imagem anterior, contendo LSAs para todos os diferentes links da rede. Agora que o OSPF foi ativado na interface G1/0 do R4, esse novo LSA é adicionado ao
7:25
LSDB. Tenho certeza de que repetirei isso muitas vezes, mas lembre-se de que esse LSDB é idêntico
7:31
para todos os roteadores na área OSPF. Cada roteador então utiliza o algoritmo SPF — o algoritmo de Dijkstra — para calcular sua melhor rota para
7:41
192.168.4.0/24. Lembre-se: cada um desses roteadores possui um mapa completo da rede.
7:47
Assim, por exemplo, ao olharmos para este diagrama, você e eu podemos ver que a melhor rota do R2 para
7:53
192.168.4.0/24 é esta rota via G1/0. Bem, o R2 está basicamente analisando o mesmo diagrama, então ele consegue calcular que enviar
8:03
o tráfego pela interface G1/0 é a melhor rota. É claro que ele não está olhando para um diagrama visual como nós, mas, na prática, é a mesma
8:11
coisa. Por fim, observe que cada LSA individual possui um temporizador de envelhecimento, que é de 30 minutos por padrão.
8:17
O LSA será propagado novamente (flooded) após o término do temporizador; portanto, isso ocorre a cada 30 minutos, por padrão.
Processo Básico do OSPF
8:25
Deixe-me resumir o processo. No OSPF, existem três etapas principais no processo de compartilhamento de LSAs e determinação da
8:31
melhor rota para cada destino na rede. A Etapa 1 consiste em estabelecer uma relação de vizinhança com outros roteadores conectados ao mesmo segmento.
8:40
Na rede do slide anterior, por exemplo, o R4 era vizinho OSPF do R2 e
8:45
do R3. A Etapa 2 consiste em trocar LSAs com os roteadores vizinhos, algo que você viu no slide anterior.
8:52
Em seguida, cada roteador calcula de forma independente suas melhores rotas para cada destino e as insere
8:57
na tabela de roteamento. Abordarei essas etapas detalhadamente na próxima aula.
9:02
Apenas tenha em mente esse processo básico do OSPF. Vamos passar para outro conceito fundamental do OSPF, que não existe no RIP ou no EIGRP.
Áreas OSPF
9:13
Áreas OSPF. O OSPF utiliza áreas para dividir a rede.
9:19
No entanto, redes pequenas podem operar com uma única área sem efeitos negativos no desempenho da rede.
9:25
Por exemplo, esta rede com quatro roteadores é uma rede pequena. Ao configurar o OSPF em uma rede como essa, podemos utilizar apenas uma única "área" OSPF e
9:35
não haverá degradação do desempenho da rede. Em redes maiores, contudo, um projeto de área única pode acarretar alguns efeitos negativos. 9:44
Por exemplo, se a rede OSPF tivesse 500 roteadores com mais de 1000 sub-redes, em vez de 4 roteadores
9:50
e apenas algumas sub-redes, usar uma única área OSPF seria uma má ideia.
9:56
Você deve dividir uma rede grande como essa em várias áreas menores. Agora, quais são alguns dos efeitos negativos de usar um design de área única em uma rede grande?
10:05
Bem, por exemplo, o algoritmo SPF leva mais tempo para calcular rotas em uma rede grande.
10:12
Ele também exige exponencialmente mais poder de processamento em cada roteador para realizar os cálculos.
10:18
O fato de cada roteador compartilhar um único e enorme banco de dados de estado de enlace também consome mais memória nos
10:23
roteadores. Além disso, qualquer pequena alteração na rede — por exemplo, uma nova interface sendo
10:29
ativada — faria com que LSAs fossem propagados (inundados) para todos os 500 roteadores, e todos eles
10:34
teriam que refazer o cálculo SPF. Ao dividir uma rede OSPF grande em várias áreas menores, você pode evitar esses efeitos
10:43
negativos. Verificando os tópicos do exame mais uma vez, note que apenas o OSPF de área única é mencionado.
10:50
Portanto, darei apenas uma breve visão geral das áreas OSPF e de como elas funcionam; você não precisa
10:55
de muitos detalhes para o CCNA. Não vou criar um diagrama com 500 roteadores, mas aqui está um exemplo de uma rede
11:02
maior do que a anterior. É possível transformar esta em uma rede grande de área única.
11:07
Todas as interfaces de todos os roteadores são atribuídas à área 0, também conhecida como área backbone.
11:12
Você verá em breve que a área 0 tem importância especial no OSPF, sendo chamada de
11:18
área "backbone". Agora, em vez de uma única área grande, vou mostrar como a rede pode ser dividida em áreas
11:25
separadas. Veja como isso é feito. Existem algumas regras e terminologias sobre áreas OSPF que você precisa conhecer; vou explicá-las
11:33
agora. Primeiramente, o que é uma área? É um conjunto de roteadores e links que compartilham o mesmo LSDB — banco de dados de estado de link.
11:43
Olhando para este diagrama...



Mais uma vez: quantas áreas existem? Área 0, Área 1, Área 2 e Área 3.
11:50
Portanto, existem quatro áreas. Cada uma dessas áreas mantém um LSDB exclusivo.
11:56
Em seguida, a área de backbone (que é a área 0) é uma área — uma área especial — à qual todas as outras
12:02
áreas devem se conectar. Vamos verificar aquele diagrama de rede novamente.
12:07
Observe que a área 1, a área 2 e a área 3 se conectam à área 0, a área de backbone.
12:14
Esse tipo de projeto de rede, por exemplo, não é permitido no OSPF. Observe que a área 1 não está conectada à área 0, a área de backbone.
12:23
Ela está conectada apenas à área 2. Isso não é permitido no OSPF.
12:28
A seguir: roteadores com todas as interfaces na mesma área são chamados de "roteadores internos". Então, neste diagrama, quais são os roteadores internos?
12:36
Se todas as interfaces do roteador estiverem na mesma área, ele é um roteador interno.
12:42
Este roteador aqui é interno à área 0. Estes roteadores são roteadores internos da área 1.
12:48
O mesmo vale para estes roteadores na área 2 e estes roteadores na área 3. Portanto, esses são roteadores internos: roteadores com todas as suas interfaces na mesma área OSPF.
13:00
A seguir: roteadores com interfaces em múltiplas áreas são chamados de "roteadores de borda de área" (ABRs),
13:05
porque constituem a fronteira entre diferentes áreas OSPF. Nesta rede, quais roteadores são ABRs?
13:13
Este roteador, conectado à área 0 e à área 1, é um ABR. Este roteador, conectado à área 0 e à área 2, também é um ABR.
13:22
E este roteador, conectado à área 0 e à área 3, é um ABR. Lembre-se de que os ABRs (Area Border Routers — Roteadores de Fronteira de Área) são roteadores com interfaces em múltiplas áreas OSPF.
13:33
Mais uma informação sobre os ABRs: eles mantêm um LSDB separado para cada área à qual estão conectados.
13:41
Recomenda-se conectar um ABR a, no máximo, duas áreas. Conectar um ABR a três ou mais áreas pode sobrecarregar o roteador.
13:49
Portanto, um projeto como o que mostro aqui representa um bom design de rede OSPF, com cada ABR conectado apenas
13:55
a duas áreas. A seguir, os roteadores conectados à área de backbone — que, como mencionei anteriormente, é a área 0 — são chamados de
14:03
roteadores de backbone. Isso inclui os roteadores de fronteira de área (ABRs), aliás. Então, quais roteadores nesta rede são roteadores de backbone?
14:12
É claro que este roteador está conectado apenas à área 0; portanto, é um roteador de backbone.
14:17
Ele é um roteador de backbone e também um roteador interno — interno à área 0.
14:22
Este roteador também é um roteador de backbone, além de ser um ABR. O mesmo vale para este roteador e para este outro.
14:30
Ambos são roteadores de backbone e roteadores de fronteira de área (ABRs).
14:35
Próximo termo: uma "rota intra-área" é uma rota para um destino dentro da mesma área OSPF.
14:41
Por exemplo, de um roteador na área 1 para um destino que também está na área 1.
14:46
Vamos ver um exemplo. Se este roteador aprender uma rota para esta sub-rede, ela será considerada uma rota
14:54
intra-área, porque o destino está na mesma área que o roteador. Aqui está o último termo.
15:00
Uma "rota interáreas" é uma rota para um destino em uma área OSPF diferente. 15:06
Por exemplo, se um roteador na área 1 aprende uma rota para um destino na área 2, essa é
15:11
uma rota interárea. Vamos ver mais um exemplo. Se este roteador na área 1 aprende uma rota para esta sub-rede na área 2, ela é considerada uma
15:21
rota interárea. O roteador e o destino estão em duas áreas OSPF diferentes.
15:26
Então, esses são alguns termos importantes do OSPF relacionados às áreas OSPF.
15:32
Certifique-se de aprender e entender esses termos, e use os flashcards para memorizá-los. Área, área backbone, roteador interno, roteador de borda de área (ABR), roteador backbone, intra-área
15:43
rota e rota interárea — lembre-se desses termos. A seguir, vamos abordar algumas regras adicionais sobre áreas OSPF.
Regras de Área OSPF
15:52
Primeiro, as áreas OSPF devem ser "contíguas". O que isso significa? Significa que cada área individual deve ser conectada, e não dividida.
16:01
É mais fácil demonstrar com o diagrama de rede. Então, esta rede satisfaz essa regra.
16:09
Todas as áreas são contíguas. Agora, vamos ver o que significa ser não contígua.
16:15
A área 1 agora é não contígua. Em vez de estar toda conectada, metade da área 1 está aqui e a outra metade está aqui.
16:23
Esse tipo de projeto de rede não é permitido no OSPF e causará problemas. Então, em vez de ter a área 1 dividida e não contígua dessa forma,
16:31
você deve transformar esta seção à direita em uma área separada: a área 3. Agora, todas as áreas são contíguas e o OSPF pode funcionar corretamente.
16:41
Próxima regra: todas as áreas OSPF devem ter pelo menos um ABR conectado à área backbone.
16:47
Na verdade, já mencionei isso, mas vale a pena repetir. Vamos olhar novamente para o diagrama de rede. 16:54
Então, observe que a área 1 possui um ABR conectado tanto à área 1 quanto à área 0; a área 2 possui um ABR
17:01
conectado tanto à área 2 quanto à área 0; e a área 3 também possui um ABR conectado tanto à área 3
17:07
quanto à área 0. Esse é um projeto de rede OSPF correto. Como mostrei anteriormente, uma rede como esta não representa um projeto OSPF correto e causará
17:17
problemas, pois a área 1 não possui um ABR conectado à área de backbone,



área 0.
17:24
Mais uma regra: interfaces OSPF na mesma sub-rede devem estar na mesma área.
17:29
Se não estiverem na mesma área, elas não se tornarão vizinhas OSPF e não trocarão informações sobre as redes que conhecem.
17:36
Em um vídeo futuro, detalharei outros requisitos para que roteadores se tornem vizinhos OSPF, mas, por enquanto, vamos ficar apenas com esta regra.
17:43
Então, deixe-me demonstrar. Neste exemplo, estes três roteadores possuem uma interface na área 0, na sub-rede
17:53
192.168.1.0/29. Este roteador também possui uma interface na sub-rede 192.168.1.0/29, mas a interface está na área 1, e não na
18:02
área 0. Embora todas as quatro interfaces estejam na mesma sub-rede e o OSPF esteja habilitado nelas, o
18:08
roteador da área 1 não se tornará vizinho OSPF dos outros. Desta vez, a interface do ABR da área 1 na sub-rede 192.168.1.0/29 está configurada corretamente
18:20
na área 0. Assim, todos os quatro roteadores se tornarão vizinhos OSPF. Aqui está um resumo dessas três regras.
18:28
É claro que abordarei muitos outros pontos sobre o OSPF nos próximos vídeos. Falarei detalhadamente sobre vizinhos OSPF, LSAs OSPF e outros tópicos.
18:37
Mas agora vamos abordar algumas configurações básicas do OSPF para que possamos praticá-las no vídeo de laboratório.
Configuração Básica de OSPF
18:44
Então, vamos usar a mesma topologia de rede que utilizamos para RIP e EIGRP, já que você já está familiarizado com ela. 18:50
Embora seja importante entender as regras e os termos relacionados às áreas OSPF, para
18:55
o CCNA você só precisa configurar o OSPF de área única; portanto, todas essas interfaces de roteador estão
19:01
na área OSPF 0. Já configurei os roteadores R2, R3 e R4, então vamos configurar o OSPF no R1.
19:10
Aqui está a configuração básica do OSPF; vamos analisá-la. Primeiramente, para entrar no modo de configuração do OSPF, usa-se o comando `router ospf`, seguido
19:20
de um ID de processo. Um roteador pode executar vários processos OSPF simultaneamente, e esse ID é usado no roteador para
19:28
identificar cada um deles. Normalmente, utiliza-se apenas um único processo OSPF, então não se preocupe muito com esse número;
19:34
eu escolhi usar o 1. Se você se lembra da configuração do EIGRP, utilizava-se o comando `router eigrp`, seguido
19:43
de um número de AS. Para que roteadores EIGRP se tornem vizinhos, seus números de AS precisam coincidir.
19:49
No entanto, o ID de processo do OSPF é diferente. O ID de processo do OSPF tem significado local.
19:56
Roteadores com IDs de processo diferentes podem se tornar vizinhos OSPF. Geralmente, uso apenas o ID de processo 1, mas você poderia, por exemplo, usar o ID de processo 1 no R1 e
20:08
o ID de processo 2 no R2; eles ainda assim se tornariam vizinhos OSPF e trocariam LSAs.
20:15
Observe que esse ID de processo não tem relação alguma com a área. Você verá a seguir que a área é configurada separadamente.
20:22
Então, em seguida, tentei usar o comando `network`, assim como fiz no EIGRP.
20:27
Note que o OSPF utiliza máscaras curinga (*wildcard masks*), exatamente como o EIGRP. Se precisar revisá-las, volte e assista ao vídeo do Dia 25.
20:35
Basicamente, trata-se de uma máscara de sub-rede invertida. Enfim, tentei usar aquele comando, mas o roteador respondeu com "Incomplete command" (comando incompleto).
20:43
Isso acontece porque o comando `network` do OSPF exige que você especifique a área.
20:49
Então, ativei o OSPF em todas essas interfaces, na área 0.
20:54
Mais uma vez: para o CCNA, você só precisa configurar o OSPF de área única e, geralmente,
20:59
você usará a área 0. No OSPF de área única, é possível usar qualquer número de área, mas considera-se
21:06
uma boa prática utilizar a área 0. Antes de prosseguir, deixe-me revisar a função do comando `network`; ele funciona exatamente como no
21:14
RIP e no EIGRP. O comando `network` instrui o OSPF a procurar interfaces com um endereço IP contido
21:21
na faixa especificada no comando e, em seguida, ativar o OSPF nessa interface
21:26
na área especificada. Por exemplo, no primeiro comando `network`, especifiquei 10.0.12.0 com uma máscara curinga (wildcard) /28,
21:35
na área 0. A interface G0/0 do R1 tem o endereço IP 10.0.12.1, que está contido na faixa 10.0.12.0/28.
21:45
Portanto, o OSPF será ativado na interface G0/0, na área 0.
21:51
Quando o OSPF é ativado na interface, o roteador tenta estabelecer uma vizinhança OSPF com outros roteadores vizinhos que também tenham o OSPF ativado.
22:00
Nesse caso, o R1 estabelecerá vizinhança OSPF com o R2 e o R3. Explicarei esse processo detalhadamente no próximo vídeo.
22:08
Então, lembre-se apenas de que o comando `network` serve simplesmente para indicar ao roteador em quais interfaces o OSPF deve ser ativado.
22:15
Ele não instrui o roteador a "anunciar essas redes". Mas já abordamos isso no vídeo anterior; agora, vamos ver algumas outras configurações
22:23
que você pode realizar no OSPF. Para começar, o comando `passive-interface`.
comando passive-interface
22:29
Você já conhece esse comando do RIP e do EIGRP; ele funciona exatamente da mesma forma no OSPF.
22:35
O comando `passive-interface` instrui o roteador a parar de enviar mensagens "hello" do OSPF por meio daquela interface.
22:42
O OSPF utiliza mensagens "hello" para se anunciar a outros roteadores — aguarde o vídeo do Dia 27 para mais detalhes sobre isso.
22:48
No entanto, o roteador continuará enviando LSAs para informar seus vizinhos...



...da sub-rede configurada na interface.
22:55
Então, embora o R1 não envie pacotes *hello* pela interface G2/0 nem tente encontrar vizinhos OSPF, ele
23:01
ainda informará aos seus outros vizinhos sobre a rede 172.16.1.0/28.
23:08
Você deve sempre usar esse comando em interfaces que não possuem vizinhos OSPF. É um desperdício enviar continuamente mensagens *hello* por uma interface à qual não há outros
23:17
roteadores conectados. Portanto, esse é o comando PASSIVE-INTERFACE; ele é basicamente o mesmo utilizado para RIP e EIGRP.
anunciar uma rota padrão no OSPF
23:26
A seguir, vamos ver como anunciar uma rota padrão no OSPF, assim como mostrei anteriormente para o RIP.
23:32
Então, adicionei uma conexão com a Internet ao R1. Em seguida, configurei uma rota padrão no R1, sendo que o próximo salto (*next hop*) é o endereço IP do provedor (ISP):
23:41
203.0.113.2. Aqui estão essas informações na tabela de roteamento do R1.
23:47
Fique à vontade para pausar aqui se quiser conferir também as outras rotas OSPF que o R1 aprendeu.
23:54
Assim como mostrei no RIP, o comando para anunciar a rota padrão no OSPF é DEFAULT-INFORMATION ORIGINATE.
24:01
No OSPF, isso fará com que o roteador crie um novo LSA e o propague (*flood*). Verifiquei a tabela de roteamento do R2 e é possível ver que ele adicionou a rota padrão via R1 à sua
24:11
tabela de rotas. O R3 e o R4 fariam o mesmo. Agora, vamos dar uma olhada no comando SHOW IP PROTOCOLS sob a perspectiva do OSPF, e vamos
show ip protocols
24:22
verificar também alguns outros comandos. Na parte superior, aparece a informação "routing protocol is ospf 1".
24:28
1 é o ID do processo que configurei anteriormente. O OSPF também utiliza um Router ID, e esse identificador é determinado exatamente da mesma forma que
24:37
no EIGRP; vamos relembrar. Aqui está a ordem de prioridade para determinar o Router ID do OSPF.
24:46
Primeiramente, se você configurar o Router ID manualmente, esse será o Router ID utilizado.
24:51
Se você não configurar o Router ID manualmente, o endereço IP mais alto em uma interface loopback
24:57
será definido como o Router ID. Se o roteador não possuir interfaces loopback com endereço IP, o endereço IP mais alto em uma
25:04
interface física será definido como o Router ID. Atualmente, o Router ID do R1 é 172.16.1.14, pois não configurei manualmente o
25:13
Router ID e também não configurei uma interface loopback no R1. Vamos ver como configurar o Router ID manualmente.
25:22
No modo de configuração do OSPF, utilize o comando ROUTER-ID. Isso é um pouco diferente do EIGRP; no EIGRP, o comando é EIGRP ROUTER-ID, mas
25:33
no OSPF é apenas ROUTER-ID. Então, inseri o Router ID 1.1.1.1, mas o roteador exibiu esta mensagem:
25:43
"Reinicie ou use o comando 'clear ip ospf process' para que isso entre em vigor".
25:49
Portanto, no momento, o Router ID ainda é 172.16.1.14; para que o 1.1.1.1 entre em vigor, precisamos
25:57
reiniciar o roteador ou usar aquele comando para limpar o processo OSPF e reiniciá-lo.
26:02
Eu fiz isso: a partir do modo EXEC privilegiado, utilizei o comando CLEAR IP OSPF PROCESS.
26:10
Basicamente, isso reinicia o OSPF no roteador. Essa é uma má ideia em uma rede real, pois o roteador perderá todas as suas rotas OSPF
26:18
por um curto período e não conseguirá encaminhar tráfego para esses destinos. Em um laboratório como este, no entanto, não há problema.
26:27
Uma observação: note o "no" entre colchetes. Quando você vê isso após inserir um comando, significa que "no" é a opção padrão.
26:35
Se você apenas pressionar Enter, o roteador assumirá "no" e não limpará o processo OSPF.
26:41
No entanto, eu digitei "yes", então ele foi limpo. Depois, executei o comando SHOW IP PROTOCOLS novamente e você pode ver que o Router ID agora é 1.1.1.1.
26:53
Agora, vamos analisar o restante do comando. Veja isto: "It is an autonomous system boundary router" (É um roteador de borda de sistema autônomo).
26:59
Um roteador de borda de sistema autônomo, ou ASBR, é um roteador OSPF que conecta a rede OSPF
27:06
a uma rede externa. O R1 está conectado à Internet. Ao usar o comando DEFAULT-INFORMATION ORIGINATE, o R1 se torna um ASBR; ele conecta a
27:16
rede OSPF à Internet. É por isso que vemos essa saída aqui no R1.
27:23
A seguir, o número de áreas neste roteador é 1: 1 normal, 0 stub, 0 nssa.
27:31
Esses são três tipos diferentes de áreas OSPF; não é necessário conhecer os diferentes tipos para o CCNA, mas queria destacar que você pode ver o número de áreas em que este
27:40
roteador está inserido — apenas uma, pois trata-se de OSPF de área única. Em seguida, o número máximo de caminhos é 4.
27:49
Ao contrário do EIGRP, o OSPF não suporta balanceamento de carga com custos desiguais, mas suporta balanceamento de carga ECMP
27:56
em até 4 caminhos por padrão. Para alterar o número máximo de caminhos, use o comando MAXIMUM-PATHS, assim como no RIP
28:05
e no EIGRP. Aqui, alterei o número para 8. A seção "routing for networks" mostra os comandos de rede que utilizamos.
28:14
Vale ressaltar que isso determina apenas em quais interfaces o OSPF será ativado; não
28:20
instrui o OSPF a propagar (flood) LSAs para essas redes específicas. Aqui está a interface passiva que configuramos, e aqui estão os vizinhos do R1.
28:30
Observe os IDs do roteador; eu configurei essas interfaces de loopback



...nos roteadores R2, R3 e R4 e
28:37
seus endereços IP tornaram-se os IDs de roteador. Por fim, aqui embaixo é exibida a AD (Distância Administrativa) do OSPF; o padrão é 110, como vocês sabem.
28:46
Se quiser alterá-la, o comando é o mesmo usado para RIP e EIGRP.
28:51
No modo de configuração do OSPF, basta usar o comando DISTANCE. Por exemplo, eu a alterei para 85, de modo que as rotas OSPF tenham preferência sobre as rotas EIGRP neste roteador.
29:02
É isso para esta aula. Abordamos muitas informações, mas grande parte delas é semelhante ou igual ao que
Tópicos abordados
29:08
aprendemos sobre RIP e EIGRP. Claro, também houve muitas informações novas.
29:14
Antes de passar para o quiz, vamos revisar o que vimos. Apresentei uma visão geral básica das operações do OSPF, incluindo uma breve análise das LSAs, que
29:23
abordaremos com mais detalhes posteriormente. Introduzi o conceito de áreas OSPF.
29:29
Embora o CCNA exija apenas a configuração de OSPF de área única, você ainda precisa ter uma compreensão básica
29:34
sobre áreas OSPF. Lembre-se das regras e termos básicos do OSPF, como *area border router* (ABR) e
29:42
*autonomous system boundary router* (ASBR). Por fim, vimos algumas configurações básicas do OSPF.
29:50
A maioria delas era igual à do RIP e do EIGRP, com algumas pequenas diferenças.





