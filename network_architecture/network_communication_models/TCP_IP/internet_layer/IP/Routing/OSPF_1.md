# OSPF

## Tópicos que abordaremos
Vamos ver o que abordaremos neste arquivo. Trataremos de três tópicos principais.

Primeiro, a métrica do OSPF, que, como você sabe, é chamada de "custo". O próximo tópico será como os roteadores se tornam vizinhos OSPF. Já mencionei vizinhos OSPF anteriormente, mas ainda não mostrei o processo em si. Vamos detalhá-lo neste arquivo. Por fim, apresentarei mais algumas configurações do OSPF.

Vamos falar sobre a métrica do OSPF.

## Custo OSPF

Como você já sabe, a métrica do OSPF é chamada de "custo". Ela é calculada automaticamente com base na largura de banda — ou seja, a velocidade — da interface. Você também pode configurar manualmente o custo de cada interface, mas mostrarei isso mais adiante. O custo da interface é calculado dividindo-se um valor chamado "largura de banda de referência" pela largura de banda da interface.

A largura de banda de referência padrão do OSPF é de 100 megabits por segundo. Então, por exemplo, uma interface Ethernet comum com velocidade de 10 megabits por segundo tem um custo OSPF de 10, pois 100 dividido por 10 é igual a 10. Uma interface FastEthernet, com velocidade de 100 megabits por segundo, tem um custo OSPF de 1, pois 100 dividido por 100 é 1. 

Agora, e quanto a uma interface Gigabit Ethernet, com velocidade de 1000 megabits por segundo? Ela tem custo 1, embora 100 dividido por 1000 seja igual a 0,1. E quanto a uma interface Ethernet de 10 Gigabits, com velocidade de 10.000 megabits por segundo? Ela também tem custo 1, embora 100 dividido por 10.000 seja igual a 0,01. Por que isso acontece?

Bem, no OSPF, todos os valores menores que 1 são convertidos para 1. Portanto, FastEthernet, Gigabit Ethernet, Ethernet de 10 Gigabits, etc., são equivalentes e todas têm custo 1 por padrão. Vou mostrar na CLI. Aqui está a mesma topologia de rede de antes. 

112511

Vamos verificar o custo da interface F2/0 do R3. Usei o comando SHOW IP OSPF INTERFACE F2/0.
3:25
Consegue encontrar o custo? Na verdade, ele aparece em dois lugares: aqui e aqui. 3:31
Como eu disse, o custo padrão de uma interface FastEthernet é 1, pois ela possui uma velocidade de 100 megabits por segundo e a largura de banda de referência padrão é de 100 megabits por segundo.
3:43
Agora, vamos verificar o custo OSPF padrão na interface G0/0 do R3. Digitei `SHOW IP OSPF INTERFACE G0/0` e, como você pode ver, o custo aqui também é 1.
3:56
Claramente, a situação padrão não é a ideal. Felizmente, é possível alterar isso.
Alterando a largura de banda de referência
4:01
Você pode — e deve — alterar a largura de banda de referência usando este comando, a partir do modo de configuração do OSPF:
4:07
`AUTO-COST REFERENCE-BANDWIDTH`, seguido pelo valor da largura de banda de referência em megabits por segundo.
4:14
Vamos analisar esse comando. Como mostrei no slide anterior, a largura de banda de referência é configurada em megabits por segundo.
4:23
Configurei o valor como 100.000; então, qual será o custo das interfaces FastEthernet e Gigabit Ethernet?
4:29
100.000 dividido por 100 resulta em 1.000; esse é, portanto, o custo de uma interface FastEthernet.
4:36
E quanto à Gigabit Ethernet? 100.000 dividido por 1.000 resulta em 100; esse é o custo de uma interface Gigabit Ethernet.
4:46
Por que configurar um valor tão alto para a largura de banda de referência? Bem, você deve configurar uma largura de banda de referência superior à velocidade dos links mais rápidos da sua rede,
4:54
para permitir futuras atualizações. Os 100 (*100.000) megabits por segundo que configurei como largura de banda de referência equivalem a uma interface de 100
5:03
gigabits por segundo, o que é 100 vezes mais rápido do que as interfaces mais velozes desta rede: a Gigabit Ethernet padrão.
5:11
Por fim, observe a mensagem exibida ao configurar a largura de banda de referência: "Certifique-se de que a largura de banda de referência seja consistente em todos os roteadores".
5:20
Portanto, para garantir um custo consistente para a largura de banda de cada interface em toda a rede, você
5:25
deve configurar a mesma largura de banda de referência em todos os roteadores OSPF da rede. Certo, defini a mesma largura de banda de referência OSPF de 100 gigabits por segundo em todos os roteadores.
Custo OSPF (cont.)
5:38
O custo OSPF até um destino é a soma dos custos das interfaces de "saída" (ou *outgoing*).
5:44
Isso funciona exatamente como o custo do Spanning Tree. Por exemplo: qual é o custo para o R1 alcançar a rede 192.168.4.0/24?
5:54
Para chegar a 192.168.4.0, um pacote sairia pelas interfaces G0/0 do R1, G1/0 do R2 e G1/0 do R4.
6:05
Ou seja: 100 mais 100 mais 100, resultando em um custo total de 300.
6:10
Verificaremos a tabela de roteamento do R1 em breve, mas há mais um detalhe: interfaces Loopback têm custo 1.
6:17
Então, qual é o custo para o R1 alcançar o endereço 2.2.2.2, que corresponde à interface Loopback0 do R2? 6:25
Para chegar a 2.2.2.2, o pacote deve sair pela interface G0/0 do R1 e pela interface loopback0 do R2.
6:32
Agora, isso não acontece.




...não chega a sair por nenhuma interface física para alcançar a interface de loopback virtual,
6:38
mas um custo de 1 é adicionado à métrica. Portanto, o custo do R1 para alcançar 2.2.2.2 é 101.
6:47
Aqui está a tabela de roteamento do R1 antes de alterar a largura de banda de referência em todos os roteadores,
6:52
de modo que todos mantêm a largura de banda de referência padrão de 100 megabits por segundo. Observe que existem duas rotas para 192.168.4.0: uma via R2 e outra via R3.
7:04
Embora a conexão entre R3 e R4 seja uma conexão FastEthernet mais lenta, ela possui o mesmo custo de 1 que as interfaces Gigabit Ethernet.
7:14
E aqui está a tabela de roteamento do R1 após alterar a largura de banda de referência de cada roteador para 100.000 megabits por segundo.
7:22
Agora, o R1 insere apenas uma rota para 192.168.4.0 na tabela de roteamento, e o custo é 300,
7:29
conforme calculamos anteriormente. Observe que o custo para 2.2.2.2 é 101, como também calculamos antes.
7:38
Agora, vou mostrar como configurar manualmente o custo OSPF de uma interface. O comando é `ip ospf cost`, seguido pelo valor de custo que você deseja definir.
7:49
Você configura isso diretamente na interface, e esse custo terá prioridade sobre o custo calculado automaticamente. 7:55
Por exemplo, configurei o custo da interface G0/0 do R1 como 10.000 e agora você pode
8:01
ver que o custo é 10.000 em vez de 100. Outra opção para alterar o custo OSPF de uma interface é modificar a largura de banda
8:10
da interface usando o comando BANDWIDTH. Relembrando: a fórmula para calcular o custo OSPF é a largura de banda de referência dividida pela largura de banda
8:19
da interface. Mostrei como alterar a largura de banda de referência, mas você também pode alterar a largura de banda da interface.
8:25
Agora, preciso esclarecer a diferença entre "velocidade" e "largura de banda" da interface.
8:31
Embora a largura de banda corresponda à velocidade da interface por padrão, alterar a largura de banda da interface não altera, de fato, a velocidade de operação da interface.
8:40
A largura de banda é apenas um valor utilizado para calcular o custo OSPF, a métrica EIGRP, etc.
8:47
Para alterar a velocidade de operação da interface, utilize o comando SPEED. É assim que você realmente altera a velocidade com que a interface transmite dados fisicamente.
8:57
Se você alterar a largura de banda de uma interface Gigabit Ethernet para 100 megabits por segundo, ela continuará operando a 1 gigabit por segundo.
9:04
No entanto, para fins de cálculo de custo OSPF, será utilizada a largura de banda de 100 megabits
9:09
por segundo. Como o valor da largura de banda é usado em outros cálculos, e não apenas no custo OSPF,
9:17
não é recomendável alterar esse valor para modificar o custo OSPF da interface.
9:22
Recomenda-se alterar a largura de banda de referência e, em seguida, utilizar o comando `ip ospf cost` para modificar o custo de interfaces individuais, se desejar. 9:31
No entanto, se você quiser alterar a largura de banda da interface, aqui está o comando: `bandwidth`, seguido pela largura de banda em kilobits por segundo.
9:40
Observe que isso é diferente da largura de banda de referência, que é inserida em megabits por segundo. O comando de largura de banda da interface é inserido em kilobits por segundo.
9:49
Antes de inserir qualquer comando desse tipo, recomendo fortemente usar o ponto de interrogação para verificar as unidades em que o comando deve ser inserido.
9:55
Por exemplo, em comandos que envolvem tempo, alguns são inseridos em segundos, outros em minutos.
10:02
Para comandos que envolvem velocidade, alguns são inseridos em kilobits, outros em megabits,
10:07
etc. Sempre verifique se você está inserindo as unidades corretas. Vamos resumir.
Resumo do custo OSPF
10:13
Existem três maneiras de modificar o custo OSPF. A primeira é alterar a largura de banda de referência.
10:19
O comando é `auto-cost reference-bandwidth` seguido pela largura de banda de referência em megabits por segundo, inserido no modo de configuração OSPF.
10:28
A próxima forma é configurar manualmente o custo OSPF da interface com o comando `ip ospf cost`, inserido no modo de configuração da interface.
10:37
Por fim, você também pode alterar a largura de banda da interface, embora isso não seja recomendado. O comando é `bandwidth`, seguido pela largura de banda em kilobits por segundo, inserido
10:46
no modo de configuração da interface. Já mostrei o comando `show ip ospf interface`, mas aqui está uma maneira mais rápida de verificar
10:53
o custo OSPF de cada interface. O comando `show ip ospf interface brief` fornece uma visão geral conveniente de cada interface com OSPF habilitado
11:02
no roteador. Certo, vamos passar para o próximo tópico. Este é outro tópico muito importante no OSPF: vizinhos OSPF. Vizinhos OSPF
11:12
Garantir que os roteadores se tornem vizinhos OSPF com sucesso é a tarefa principal na configuração e na resolução de problemas do OSPF.
11:20
Assim que os roteadores se tornam vizinhos, eles realizam automaticamente o trabalho de compartilhar informações de rede, calcular rotas, etc.
11:26
Portanto, basta garantir que o OSPF esteja ativado nas interfaces corretas e que
11:31
as condições adequadas sejam atendidas para permitir que os roteadores se tornem vizinhos. Claro, existem configurações OSPF mais avançadas que você pode realizar, mas para a operação básica do OSPF elas
11:42
não são necessárias. No entanto, se os roteadores não conseguirem se tornar vizinhos OSPF...


vizinhos, o OSPF não consegue operar de forma alguma, então isso é muito
11:49
importante. Então, como os roteadores se tornam vizinhos OSPF?
11:54
Quando o OSPF é ativado em uma interface, o roteador começa a enviar mensagens "hello" do OSPF
12:00
a partir da interface em intervalos regulares (determinados pelo temporizador "hello"). Elas são usadas para apresentar o roteador a possíveis vizinhos OSPF.
12:09
Ao trocar mensagens "hello", eles verificam se são compatíveis para se tornarem vizinhos OSPF,
12:14
e então negociam seu relacionamento de vizinhança. A propósito, o temporizador "hello" padrão é de 10 segundos em uma conexão Ethernet.
12:21
Lembre-se deste número! As mensagens "hello" do OSPF são enviadas via multicast para o endereço IP 224.0.0.5, que é o endereço multicast
12:30
para todos os roteadores OSPF. Você se lembra do endereço multicast do RIP?
12:36
É 224.0.0.9. E o EIGRP? 224.0.0.10.
12:43
Além disso, as mensagens OSPF são encapsuladas em um cabeçalho IP, e o campo "protocol" (protocolo) do
12:49
cabeçalho IP tem o valor 89 para indicar o OSPF. Se você precisar de uma revisão sobre o cabeçalho IP, volte e assista novamente ao Dia 10 do curso.
Estados de vizinhança - Down
12:59
Certo, para que os roteadores OSPF se tornem vizinhos, eles precisam passar por vários estados de vizinhança.
13:04
Vou dar uma visão geral básica de cada um dos estados de vizinhança. Recomendo fazer anotações nesta seção.
13:11
Embora seja apenas uma visão geral básica, vou fornecer muitas informações nos próximos slides.
13:17
Então, vamos supor que o OSPF já esteja ativado na interface G0/0 do R2. 13:23
Em seguida, o OSPF é ativado na interface G0/0 do R1. Ele envia uma mensagem Hello do OSPF para o endereço 224.0.0.5.
13:33
Há mais campos na mensagem Hello, mas dois importantes são o Router ID do R1
13:38
e o Router ID do vizinho. No entanto, o R1 ainda não conhece o R2, portanto, o campo de Router ID do vizinho é 0.0.0.0.
13:45
O R1 ainda não conhece nenhum vizinho OSPF, então o estado atual do vizinho é Down.
13:52
Este é o primeiro estado de vizinho OSPF: "Down". Quando o R2 receber o pacote Hello, ele adicionará uma entrada para o R1 em sua tabela de vizinhos OSPF.
Estados de vizinho – Init
14:03
Na tabela de vizinhos do R2, o relacionamento com o R1 está agora no estado Init.
14:09
Observe que o R1 ainda não conhece o R2, portanto, não terá entradas em sua tabela de vizinhos OSPF.
14:15
Basicamente, o estado Init significa que um pacote Hello foi recebido, mas o Router ID do próprio R2
14:20
não está no pacote Hello. O Router ID do R2 é 2.2.2.2, mas o Router ID do vizinho no pacote Hello do R1 é 0.0.0.0.
14:30
Então, esse é o estado Init. O próximo estado é o estado 2-way.
Estados de vizinho – 2-way
14:37
O R2 enviará um pacote Hello contendo o RID de ambos os roteadores. O R1 inserirá o R2 em sua tabela de vizinhos OSPF no estado 2-way.
14:46
Em seguida, o R1 enviará outra mensagem Hello, desta vez contendo o RID do R2. 14:53
Agora, ambos os roteadores estão no estado "2-way". O estado "2-way" significa que o roteador recebeu um pacote Hello contendo o seu próprio RID.
15:03
Se ambos os roteadores atingirem o estado "2-way", isso significa que todas as condições foram atendidas para que se tornem vizinhos OSPF.
15:10
Eles estão agora prontos para compartilhar LSAs e construir uma LSDB comum. Por outro lado, se não conseguirem atingir esse estado "2-way", você sabe que precisa realizar a solução de problemas
15:19
e descobrir o que os impede de alcançá-lo. Em alguns tipos de rede, um DR (Designated Router) e um BDR (Backup Designated Router) serão
15:29
eleitos neste momento. Falarei sobre tipos de rede OSPF e eleições de DR/BDR no Dia 28, então não se preocupe com
15:37
eles por enquanto. Eu só queria apresentar os termos DR e BDR.
15:42
Neste ponto, os roteadores já são vizinhos OSPF. Nos próximos estados de vizinhança, eles compartilharão LSAs e formarão uma adjacência OSPF completa.
15:52
Vamos para o próximo estado de vizinhança. Após o estado "2-way", os dois roteadores se prepararão para trocar informações sobre
Estados de vizinhança - Exstart
16:00
suas LSDBs. Antes disso, eles precisam escolher qual deles iniciará a troca.
16:06
Assim, eles decidirão qual será o roteador Master (mestre) e qual será o roteador Slave
16:11
(escravo). Observe que esses papéis são diferentes do DR e do BDR que mencionei no slide anterior.
16:17
Essa relação Master/Slave é necessária apenas para essa troca inicial de informações da LSDB.
16:24
Eles decidem qual será o Master e qual será o Slave durante o estado Exstart. 16:29
O roteador com o RID mais alto se tornará o Master e iniciará a troca.
16:35
O roteador com o RID mais baixo se tornará o Slave. Portanto, neste caso, o R2 será o master e o R1 será o slave.
16:43
Para definir quem é Master e quem é Slave, eles trocam pacotes DBD (Database Description).
16:50
Os pacotes DBD também são importantes no próximo estado; por isso, falarei mais sobre eles no próximo slide.
16:55
Basicamente, o estado Exstart serve apenas para preparar o próximo estado. O R1 envia um pacote DBD alegando ser o master.
17:04
No entanto, o R2 corrige o R1. O R2 possui o Router ID mais alto e afirma que ele será o master.
Estados de vizinhança – Exchange
17:13
No próximo estado, o estado Exchange, os roteadores trocam pacotes DBD que...



...contêm uma lista
17:18
das LSAs em seus LSDBs. Esses DBDs não incluem informações detalhadas sobre as LSAs, apenas informações básicas indicando
17:27
ao vizinho quais LSAs eles possuem. Basicamente, os roteadores informam uns aos outros: "Eu tenho estas LSAs", mas não estão
17:35
enviando as LSAs propriamente ditas ainda. Os roteadores comparam as informações do DBD recebido com as informações de seus
17:42
próprios LSDBs para determinar quais LSAs precisam receber do vizinho.
17:48
Após a troca de DBDs, eles passam para o próximo estado.
Estados de vizinhança – Loading (Carregamento)
17:53
O próximo estado é o estado de Loading. Nesse estado, os roteadores enviam mensagens LSR (Link State Request) para solicitar que seus
18:02
vizinhos enviem quaisquer LSAs que eles não possuam. No estado de Exchange (Troca), eles trocaram pacotes DBD, então sabem quais LSAs seus vizinhos
18:10
possuem. Assim, essas mensagens LSR são usadas para solicitar quaisquer LSAs ausentes, garantindo que cada roteador tenha as mesmas
18:17
LSAs. Vou mostrar apenas um lado da troca, mas o R2 também enviará mensagens LSR ao R1 para quaisquer
18:24
LSAs ausentes. Em seguida, as próprias LSAs são enviadas em mensagens LSU (Link State Update).
18:32
O R2 envia ao R1 as LSAs solicitadas em uma mensagem LSU como esta. O R1 também fará o mesmo para o R2.
18:39
Finalmente, os roteadores enviam mensagens LSAck — outro tipo de mensagem OSPF — para confirmar
18:45
o recebimento das LSAs. Agora, o estado de Loading está concluído e os roteadores possuem o mesmo LSDB.
18:52
Chegamos ao estado final do OSPF. No estado Full, os roteadores possuem uma adjacência OSPF completa e LSDBs idênticos. Estados de vizinhança – Full
19:03
Mas isso não significa que o processo esteja concluído. Eles continuam enviando e aguardando pacotes Hello — por padrão, a cada 10 segundos —
19:10
para manter a adjacência de vizinhança. Para manter essa adjacência, utiliza-se outro temporizador, chamado de temporizador "Dead" (ou de inatividade).
19:17
Sempre que um pacote Hello é recebido, o temporizador "Dead" — cujo padrão é de 40 segundos —
19:23
é reiniciado. No entanto, se a contagem regressiva do temporizador "Dead" chegar a zero sem que nenhuma mensagem Hello seja recebida, o vizinho
19:29
é removido. Se a vizinhança permanecer ativa, os roteadores continuarão compartilhando LSAs à medida que a rede sofrer alterações,
19:37
garantindo que cada roteador possua um mapa completo e preciso da rede. Essa é a principal vantagem dos protocolos de roteamento dinâmico: os roteadores reagem automaticamente
19:45
a mudanças na rede, adicionando, removendo ou alterando rotas conforme necessário.
Resumo sobre vizinhos OSPF
19:51
Vamos resumir esse processo. Primeiramente, a conexão entre R1 e R2 é estabelecida, ou o OSPF é ativado nas interfaces,
20:00
iniciando o processo. O primeiro estado é o estado "Down" (Inativo); R1 e R2 ainda não se conhecem, mas
20:08
enviam pacotes Hello por meio de suas interfaces. Vamos supor que R1 envie o primeiro pacote Hello.
20:15
O estado "Init" (Inicialização) ocorre quando R2 recebe esse primeiro pacote Hello de R1, mas o próprio Router ID de R2
20:21
ainda não consta no pacote. No estado "2-way" (Bidirecional), os roteadores trocam mais pacotes Hello, mas o Router ID de R1 é incluído
20:30
nos pacotes Hello de R2, e o Router ID de R2 é incluído nos pacotes Hello de R1. 20:37
Em alguns tipos de conexões OSPF, ocorre uma eleição para o roteador designado e o roteador designado de backup.
20:42
Falarei mais sobre isso no Dia 28.
20:48
A seguir, temos o estado Exstart. Os roteadores trocam pacotes DBD para determinar qual será o Master (Mestre) e qual será
20:55
o Slave (Escravo). O Master é o roteador que inicia a troca de DBD no próximo estado, o estado Exchange (Troca).
21:03
Eles trocam pacotes DBD para informar um ao outro sobre o conteúdo de suas LSDBs. O próximo estado é o estado Loading (Carregamento).
21:11
Eles usam LSRs (Link State Requests – Solicitações de Estado de Link) para solicitar LSAs uns aos outros.
21:18
As LSAs são enviadas em pacotes LSU (Link State Update – Atualização de Estado de Link). Finalmente, pacotes LSAck são enviados para confirmar o recebimento das LSAs solicitadas.
21:29
Por fim, os roteadores atingem o estado Full (Completo) e estabelecem uma adjacência OSPF completa.
21:36
Você se lembra deste slide do Dia 26? As três etapas principais no processo de compartilhamento de LSAs e determinação das melhores rotas para cada
21:43
destino são: 1) tornar-se vizinho, 2) trocar LSAs e 3) calcular as melhores rotas.
21:53
Analisando esse processo novamente: estes três primeiros estados envolvem tornar-se vizinho; estes três envolvem a troca de LSAs para sincronizar a LSDB; e, então, os roteadores usam a métrica
22:03
que ensinei para calcular a melhor rota para cada destino. Essa é uma visão geral básica de como o OSPF funciona.
22:10
Além disso, aqui está um quadro-resumo rápido dos 5 tipos diferentes de mensagens OSPF. Tabela de tipos de mensagens OSPF
22:16
Observe que elas são numeradas de 1 a 5: 1 é Hello, 2 é DBD, etc.
22:23
Já descrevi a finalidade básica de cada uma dessas mensagens; portanto, você pode pausar o vídeo aqui ou tirar uma captura de tela se quiser usar esta tabela para revisar.
22:34
Após essa visão geral, vamos analisar novamente alguns comandos "show" do OSPF; agora você deve compreender melhor a saída desses comandos.
Comandos "show" do OSPF
22:42
Aqui está o comando SHOW IP OSPF NEIGHBOR; eu o executei no R1.
22:47
Observe o estado "Full" com ambos os vizinhos



...R2 e R3. Além disso, tanto R2 quanto R3 são DRs.
22:54
Novamente, explicarei o que são DRs no próximo vídeo. Observe também o *dead time* (tempo de inatividade).
23:00
Ele faz uma contagem regressiva a partir de 40, mas reinicia assim que o R1 recebe um pacote Hello do vizinho.
23:06
Então, supondo que um pacote Hello seja recebido a cada 10 segundos, a contagem deve ir até 30, reiniciar
23:12
para 40, contar até 30, reiniciar para 40, etc. Agora, vamos dar outra olhada no comando `SHOW IP OSPF INTERFACE`, focando na interface G0/0 do R1.
23:25
Aqui você pode ver os temporizadores padrão de Hello e Dead: 10 e 40.
23:30
"Hello due in 7 seconds" (Hello previsto para daqui a 7 segundos) significa que o R1 enviará uma mensagem Hello por essa interface em 7 segundos, como ele faz a cada 10 segundos.
23:40
A contagem de vizinhos é 1, e a contagem de vizinhos adjacentes é 1. O R1 tem apenas um vizinho conectado à sua interface G0/0: o R2.
23:49
No próximo vídeo, explicarei a diferença entre um vizinho e um vizinho adjacente.
23:54
Por fim, vizinho adjacente 2.2.2.2, roteador designado (*Designated Router*).
24:00
Como vimos anteriormente no comando `SHOW IP OSPF NEIGHBOR`, o R2 é um roteador designado. Novamente, falarei sobre isso no Dia 28, mas sinta-se à vontade para pesquisar no Google se tiver curiosidade
24:11
sobre o assunto. Certo, por hoje é só sobre vizinhos OSPF; abordaremos mais alguns detalhes no
24:17
Dia 28. Vamos prosseguir e ver um pouco mais sobre a configuração do OSPF. Configuração do OSPF (continuação)
24:23
Já mostrei algumas novas configurações do OSPF quando falamos sobre a métrica do OSPF, especificamente
24:30
os comandos `auto-cost reference-bandwidth` e `ip ospf cost`. Então, vamos analisar mais algumas configurações adicionais.
24:40
Primeiro, você se lembra da finalidade do comando `network`? Ele funciona da mesma forma para RIP, EIGRP e OSPF.
24:48
Ele simplesmente indica ao roteador em quais interfaces o protocolo de roteamento deve ser ativado. Bem, na verdade, você pode habilitar o OSPF diretamente em uma interface, sem usar o comando
24:58
`network`. Por exemplo, vamos supor que o R1 ainda não tenha nenhuma configuração de OSPF.
25:05
Veja como habilitar o OSPF nas interfaces. Você pode ativar o OSPF diretamente em uma interface com este comando: `ip ospf`, seguido pelo
25:15
ID do processo, depois `area` e o ID da área. Observe que isso é feito no modo de configuração de interface.
25:24
Agora o OSPF está habilitado nessas interfaces, e eu nem precisei entrar no modo de configuração do OSPF.
25:30
A seguir, outro método para configurar interfaces passivas. Consegue perceber a diferença?
25:37
Você pode configurar todas as interfaces do roteador como interfaces passivas do OSPF por padrão com
25:42
o comando `passive-interface default`. Depois, pode usar o comando `no passive-interface` para remover essa configuração apenas de interfaces específicas.
25:52
Essa é simplesmente outra maneira de configurar interfaces passivas. Dependendo da quantidade de interfaces passivas que você precisa configurar, esse método pode ser
26:00
mais rápido, ou talvez o método convencional seja mais rápido. De qualquer forma, o resultado é o mesmo.
26:07
Se você configurar o OSPF diretamente nas interfaces, verá uma saída ligeiramente diferente no comando `show ip protocols`. 26:14
A seção "routing for networks" (roteamento para redes) está vazia; em vez disso, são exibidas aqui as interfaces nas quais você ativou o OSPF, sob o título "routing on interfaces configured explicitly" (roteamento em interfaces configuradas explicitamente).
26:25
No entanto, o restante da saída é o mesmo. Antes de passarmos para o quiz de hoje, vamos recapitular o que vimos.
Tópicos abordados
26:33
Primeiro, mostrei a métrica do OSPF, chamada de "custo" (cost). Por padrão, ela é calculada automaticamente dividindo-se a largura de banda de referência pela
26:41
largura de banda real da interface. No entanto, se o resultado for um valor menor que 1, ele é convertido para 1.
26:49
A largura de banda de referência padrão é 100; portanto, qualquer interface com velocidade igual ou superior a 100 megabits por segundo terá um custo igual a 1.
26:58
Você pode modificar a largura de banda de referência com o comando `AUTO-COST REFERENCE-BANDWIDTH`.
27:04
Também é possível configurar manualmente o custo de uma interface usando o comando `IP OSPF COST`.
27:11
Outra opção para modificar o custo de uma interface é alterar a largura de banda com o comando `BANDWIDTH`, embora esse não seja o método recomendado.
27:19
Por fim, a métrica de uma rota é o custo total das interfaces de saída que compõem essa rota.
27:25
Em seguida, estudamos o processo que os roteadores utilizam para se tornarem vizinhos OSPF. Aqui está o diagrama de resumo.
27:32
Esta é, provavelmente, a parte mais difícil desta aula. Recomendo assisti-la algumas vezes e, talvez, pesquisar no Google por "ospf neighbor
27:40
states" (estados de vizinhança OSPF) para saber mais sobre o processo. Por último, apresentei mais algumas configurações do OSPF.
27:48
Em vez de usar o comando `NETWORK`, você pode ativar o OSPF diretamente em uma interface usando este comando. 27:55
Como um método alternativo para configurar interfaces passivas, você pode configurar todas as interfaces como passivas usando o comando PASSIVE-INTERFACE DEFAULT e, em seguida, tornar ativas apenas interfaces específicas
28:05
posteriormente.



