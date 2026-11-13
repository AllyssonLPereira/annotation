# IPv6

Eu falei sobre o sistema hexadecimal quando abordamos os endereços MAC, mas vamos garantir que você realmente entenda o sistema hexadecimal, pois os endereços IPv6 também são escritos nesse formato. Em seguida, farei uma breve explicação sobre por que o IPv6 é necessário e por que estamos começando a deixar o IPv4 de lado. Apresentarei uma visão geral básica do IPv6, focando especificamente nos endereços IPv6. Por fim, mostrarei como configurar endereços IPv6 em dispositivos Cisco. Antes de falarmos sobre o IPv6, talvez você se pergunte: e o IPv5? 

Acho que mencionei isso anteriormente no curso, mas aqui vai uma rápida recapitulação. O *Internet Stream Protocol* foi desenvolvido no final da década de 1970, embora nunca tenha sido, de fato, lançado para uso público. Ele nunca foi chamado de "IPv5", mas utilizava o valor 5 no campo "versão" do cabeçalho IP. Se você se lembra, no arquivo sobre IPv4, abordamos o cabeçalho IPv4 — e o primeiro campo dele é, justamente, o campo "versão".

O IPv4 utiliza o valor 4, enquanto o *Internet Stream Protocol* utilizava o valor 5. Portanto, para evitar confusões, quando o sucessor do IPv4 estava sendo desenvolvido, ele foi batizado de IPv6, e utiliza o valor 6 no campo "versão" do cabeçalho.

## Revisão sobre o sistema hexadecimal

Agora, vamos revisar o sistema hexadecimal. Os três sistemas de numeração são: o binário, também chamado de base 2. O prefixo "0b" pode ser usado antes de um número binário para indicar que ele está nesse sistema. Por exemplo, observe este número: 10, um 1 e um 0. Seria o número 10 em decimal? Ou seria o número 10 em binário, que equivale a 2 em decimal? Ou, talvez, o número 10 em hexadecimal, que equivale a 16 em decimal? Não há como saber. Ao usar o prefixo "0b", deixamos claro que se trata de um número binário. Mas por que "base 2" é outro nome para o sistema binário? 

Porque, no sistema binário, existem apenas dois dígitos disponíveis: 0 e 1. Todos os números são representados usando apenas esses dois dígitos. Mas você já está familiarizado com o sistema binário. 

O próximo sistema de numeração é o decimal, ou base 10. Você pode usar o prefixo "0d" para indicar o sistema decimal. Como o nome "base 10" sugere, existem 10 dígitos disponíveis: 0, 1, 2, 3, 4, 5, 6, 7, 8 e 9. 

Por fim, temos o sistema hexadecimal, também conhecido como base 16. Você pode usar o prefixo "0x" para indicar o sistema hexadecimal, como mencionei algumas vezes ao longo do curso. Estes são os 16 dígitos disponíveis no sistema hexadecimal: de 0 a 9, eles são iguais aos do sistema decimal; além disso, utilizam-se também as letras A, B, C, D, E e F. Aqui está uma tabela comparando os três sistemas, de 0 até o número decimal 15.

Primeiro, observe que, até o 9, os sistemas decimal e hexadecimal são iguais. No entanto, o sistema decimal esgota seus dígitos, sendo necessário adicionar uma segunda coluna; assim, o número dez é escrito como 1 e 0, 10. O sistema hexadecimal expressa esse mesmo valor com um único dígito: A. O 11 é B, o 12 é C, o 13 é D, o 14 é E e o 15 é F. Muito bem, agora deixe-me destacar mais alguns pontos.

074541

Note que estes números binários apresentam zeros à esquerda. Por exemplo, o número decimal 3 é escrito como 0 0 1 1, em vez de apenas 1 1. Na verdade, não é obrigatório fazer isso em binário; você poderia escrever apenas 1 1. Então, por que escrevi todos esses números com quatro dígitos, mesmo sendo os zeros à esquerda desnecessários? É porque quero enfatizar que cada dígito hexadecimal contém 4 bits de informação.

Por exemplo, o valor máximo representado por quatro bits — 1 1 1 1 — corresponde ao maior dígito hexadecimal: o F. Isso é fundamental para realizar conversões entre binário e hexadecimal, bem como entre decimal e hexadecimal.

Vamos analisar algumas conversões.

### Prática: Binário para Hexadecimal

O número binário 1101 1011 equivale a qual valor em hexadecimal? Bem, temos aqui 8 bits. Lembre-se de que cada dígito hexadecimal corresponde a 4 bits de informação. Portanto, divida o número em grupos de 4 bits: 1101 e 1011. Em seguida, converta cada um desses grupos de 4 bits para decimal. 1101 é 8 + 4 + 1, ou seja, 13. 1011 é 8 + 2 + 1, ou seja, 11. Agora, converta esses números decimais para hexadecimal.

Você deve ter essas conversões memorizadas: 13 equivale a D, e 11 equivale a B. Basta juntar esses dois dígitos hexadecimais e você terá a resposta. O número binário 1101 1011 equivale ao hexadecimal DB. Vamos fazer mais alguns exercícios de conversão de binário para hexadecimal.

## Por que IPv6?

O próximo tópico é: "Por que IPv6?". O motivo principal é que, simplesmente, não existem endereços IPv4 suficientes disponíveis. Quantos endereços IPv4 existem? Um endereço IPv4 tem 32 bits de extensão; isso significa que existem 4 bilhões, 294 milhões, 967 mil e 296 endereços IPv4 disponíveis (4.294.967.296). Pode parecer um número grande, mas, no nosso mundo moderno, onde a Internet está em toda parte, isso simplesmente não é suficiente. Quando o IPv4 foi projetado, há 30 anos, seus criadores não imaginavam que a Internet chegaria ao tamanho que tem hoje; eles acreditavam que 32 bits ofereceriam endereços mais do que suficientes.

No entanto, já sabemos há muito tempo sobre o problema do esgotamento dos endereços IPv4, e várias técnicas têm sido utilizadas para preservar esse espaço. O VLSM (máscaras de sub-rede de tamanho variável) é uma das técnicas que permite preservar o espaço de endereçamento IPv4. Endereços IPv4 privados e o NAT (Network Address Translation — Tradução de Endereços de Rede) são outras duas soluções que também fizeram uma enorme diferença. Ambas serão abordadas em breve neste curso.

Essas técnicas foram muito úteis para preservar o espaço de endereçamento IPv4; contudo, são apenas soluções de curto prazo. A solução de longo prazo é a transição para o IPv6. Deixe-me explicar brevemente como os endereços IPv4 são atribuídos. A atribuição de endereços IPv4 é controlada pela IANA (Internet Assigned Numbers Authority — Autoridade para Atribuição de Números na Internet).

Eu também mencionei a IANA no arquivo sobre TCP e UDP. A IANA distribui o espaço de endereçamento IPv4 para vários RIRs (Regional Internet Registries — Registros Regionais da Internet), que, por sua vez, os atribuem a empresas que precisam deles. Por exemplo, um provedor de serviços de Internet solicitaria ao seu RIR local a atribuição de endereços IP, que poderiam, então, ser utilizados por seus clientes. Este é um mapa que mostra os vários RIRs.

074123

A AFRINIC controla a África; a APNIC controla a região da Ásia-Pacífico; a ARIN controla o Canadá, grande parte do Caribe e a região norte do Atlântico. O LACNIC gerencia a América Latina e o Caribe, enquanto o RIPE NCC gerencia a Europa, o Oriente Médio e partes da Ásia Central. No entanto, os estoques de endereços IPv4 de quase todos esses RIRs (Registros Regionais da Internet) estão esgotados.

Por exemplo, em setembro de 2015, o ARIN declarou o esgotamento de seu conjunto de endereços IPv4. Eles não possuem mais endereços para atribuir, a menos que, por exemplo, uma empresa encerre suas atividades e o ARIN consiga recuperar os endereços que ela detinha. Outro caso: em agosto de 2020, o LACNIC anunciou que havia realizado sua última alocação de endereços IPv4. Portanto, como se pode notar, a situação é bastante séria; simplesmente não há endereços IPv4 suficientes para o nosso mundo moderno. Precisamos de algo capaz de sustentar nosso mundo interconectado, tanto agora quanto por um longo período no futuro. Esse algo é o IPv6. Vamos, finalmente, entrar nos detalhes.

## Introdução ao IPv6

Existe, na verdade, uma história bastante interessante sobre o esgotamento dos endereços IPv4 e o surgimento do IPv6, mas isso já é o suficiente para este arquivo. Creio que agora fica claro por que precisamos fazer a transição para o IPv6. Se quiser ler um pouco mais sobre o assunto, pesquise por "esgotamento de endereços IPv4" na Wikipédia. Então, vamos falar sobre o IPv6.

Um endereço IPv6 possui 128 bits. Isso equivale a 4 vezes o número de bits de um endereço IPv4, que tem 32 bits. À primeira vista, pode parecer que, por ter 4 vezes mais bits, o número de endereços também seria 4 vezes maior. Isso está incorreto. Cada bit adicional DOBRA o número de endereços possíveis. 32 bits permitem cerca de 4 bilhões de endereços. 33 bits permitiriam cerca de 8 bilhões, 34 bits permitiriam cerca de 16 bilhões, e assim por diante.

Então, quantos endereços IPv6 existem? Existem 340 undecilhões, 282 decilhões, 366 nonilhões, 920 octilhões, 938 septilhões, 463 sextilhões, 463 quintilhões, 374 quatrilhões, 607 trilhões, 431 bilhões, 768 milhões, 211 mil e 456 endereços IPv6.

Veja um exemplo de endereço IPv6 em binário.

075754

É uma grande quantidade de 1s e 0s. Se você escrever isso no formato decimal com pontos, como um endereço IPv4, o resultado é este.

075838

No entanto, como já mencionei, os endereços IPv6 não são escritos em formato decimal com pontos; eles são escritos em hexadecimal. Aqui está esse mesmo endereço escrito em hexadecimal. 






Um endereço IPv6 tem 128 bits e, como eu disse, cada dígito hexadecimal contém 4 bits de
16:30
informação. 128 bits divididos por 4 resultam em 32. Portanto, um endereço IPv6 é escrito como 32 caracteres hexadecimais, divididos em 8 grupos de 4, usando
16:42
dois-pontos. Isso ainda é mais longo e mais difícil de ler e memorizar do que um endereço IPv4, mas
16:48
isso é inevitável. Há quatro vezes mais informações neste endereço, em comparação com um endereço IPv4.
16:56
Mas há uma boa notícia. Os endereços IPv6 utilizam a notação de "barra" (slash) para indicar o tamanho do prefixo, inclusive ao configurar
17:03
o endereço na CLI do Cisco IOS. Nada mais de máscaras de sub-rede em formato decimal pontuado.
17:09
Este /64, por exemplo, significa que a primeira metade do endereço corresponde à parte de rede,
17:15
e a segunda metade, à parte de host. Além disso, existem alguns métodos para encurtar endereços IPv6, tornando-os mais simples.
Abreviação de endereços IPv6
17:23
Vamos analisar esses métodos para encurtar endereços IPv6.
17:29
Primeiramente, os zeros à esquerda (leading zeros) podem ser removidos. Observe este endereço IPv6.
17:34
"Zeros à esquerda" são todos os zeros que aparecem no início de qualquer um dos quartetos de 4 dígitos hexadecimais.
17:41
Estes são os zeros à esquerda neste endereço. Portanto, podemos simplesmente removê-los. Agora, o endereço pode ser escrito desta forma.
17:48
Os zeros ainda fazem parte do endereço, mas não há necessidade de escrevê-los; dessa maneira, ele fica mais simples.
17:54
Muito bem, existe mais uma técnica para encurtar um endereço IPv6.
17:59
Quartetos consecutivos compostos apenas por zeros podem ser substituídos por dois-pontos duplos (::). Por exemplo, no endereço abaixo, há quatro quartetos consecutivos formados apenas por zeros.
18:09
Você pode encurtar o endereço desta forma, substituindo esses quartetos por dois-pontos duplos. Por que é possível fazer isso? 18:15
Isso ocorre porque sabemos que um endereço IPv6 é composto por 8 quartetos. No momento, conseguimos ver apenas quatro quartetos; portanto, sabemos que os dois-pontos duplos indicam a presença de quatro
18:24
quartetos formados apenas por zeros. Mas não vamos parar por aí. É possível combinar ambos os métodos: remover os zeros à esquerda e utilizar os dois-pontos duplos.
18:34
Agora, este endereço parece bem mais fácil de lidar. Contudo, existe uma limitação.
18:40
Em um endereço IPv6, a abreviação de quartetos consecutivos formados por zeros só pode ser feita uma única vez.
18:45
Por que isso? Bem, observe este endereço aqui. Você poderia tentar abreviá-lo desta forma:
18:51
Mas, agora, temos um problema. Sabemos que o total deve ser de 8 quartetos, o que significa que há cinco quartetos compostos apenas por zeros.
18:58
Mas quantos quartetos de zeros existem aqui? Dois? Três? Não é possível saber.
19:03
E neste caso? Talvez existam 2 quartetos à esquerda e 3 à direita, ou, quem sabe, 3 à esquerda e
19:09
2 à direita. É por isso que só podemos...



Abrevie os quartetos compostos apenas por zeros uma única vez em um endereço.
19:16
Em vez disso, devemos encurtar o endereço desta forma. O lado esquerdo contém três quartetos compostos apenas por zeros; por isso, substituí-os por dois-pontos duplos.
19:25
No lado direito, que possui dois quartetos compostos apenas por zeros, simplesmente removi os zeros à esquerda.
19:31
Aqui estão algumas questões para praticar o encurtamento de endereços IPv6.
19:36
Pause o vídeo e tente resolver cada uma. Muito bem, aqui estão as respostas.
19:42
Aqui está a primeira: você pode remover os zeros à esquerda e usar os dois-pontos duplos.
19:48
A próxima. Observe que há dois conjuntos de zeros consecutivos, mas você só pode usar os dois-pontos duplos
19:53
para substituir um desses conjuntos. Certo, a próxima. Assim como nos dois casos anteriores, você pode remover os zeros à esquerda e usar os dois-pontos duplos.
20:02
A próxima. Neste caso, há alguns zeros à esquerda que podem ser removidos, mas não há quartetos consecutivos compostos apenas por zeros.
20:08
Muito bem, a última. Você pode substituir cinco quartetos compostos por zeros pelos dois-pontos duplos.
Expandindo endereços IPv6 abreviados
20:15
Você também deve ser capaz de pegar um endereço IPv6 abreviado e expandi-lo para um endereço IPv6 completo.
20:21
Aqui está um exemplo de como fazer isso. Primeiro, adicione os zeros à esquerda onde for necessário; lembre-se de que todos os quartetos devem conter 4 caracteres hexadecimais
20:29
— é por isso que são chamados de "quartetos". Onde podemos adicionar zeros à esquerda neste exemplo de endereço abreviado?
20:37
Nestes três quartetos aqui. Portanto, agora o endereço fica assim. Mas ainda não terminamos. 20:43
Se um "dois-pontos duplo" (::) for utilizado, devemos substituí-lo por grupos de quatro dígitos (quartetos) compostos apenas por zeros, garantindo que haja um total de 8 desses grupos.
20:50
Há um "dois-pontos duplo" aqui, então podemos expandir o endereço. Quantos grupos de quatro dígitos existem?
20:56
Existem 5. Na verdade, são 8 no total, mas, no momento, apenas 5 estão escritos.
21:01
Para completar os 8 grupos, basta adicionar três grupos compostos apenas por zeros.
21:07
Aqui estão algumas questões para praticar a expansão de endereços IPv6 abreviados. Pause o vídeo para resolvê-las.
21:15
Muito bem, aqui estão as respostas. A primeira.
21:20
A segunda. A terceira. A quarta. E a quinta. Falarei sobre os diferentes tipos de endereços IPv6 em outro vídeo, mas cada um desses endereços
21:30
corresponde a um tipo diferente. O IPv4 possui diversos tipos de endereços, como endereços multicast, endereços de loopback, etc.,
21:38
e o mesmo ocorre com o IPv6. Mas, como mencionei, esse é um assunto para outro vídeo.
Identificando o prefixo IPv6
21:44
A seguir, veremos como encontrar o prefixo IPv6 — ou seja, o endereço de rede — a partir de um endereço de host específico.
21:51
Já fizemos isso anteriormente para o IPv4: basta definir todos os bits de host como 0 para obter o prefixo, que é o endereço de rede.
21:58
Vamos aplicar esse conceito ao IPv6. Normalmente, uma empresa que solicita endereços IPv6 ao seu provedor de serviços (ISP) recebe um bloco /48.
22:09
Além disso, as sub-redes IPv6 costumam utilizar um prefixo de comprimento /64.
22:14
Portanto, a empresa recebeu um bloco /48, mas o comprimento de prefixo padrão é /64. 22:22
Isso significa que uma empresa tem 16 bits disponíveis para criar sub-redes. E os 64 bits restantes podem ser usados ​​para hosts.
22:30
Acho que um exemplo tornará isso mais claro. Aqui está um endereço IPv6. Esta parte em azul é o bloco /48 atribuído pelo provedor de serviços (ISP); ele é chamado de "prefixo de roteamento global"
22:41
(global routing prefix). Observe que este exemplo refere-se ao tipo de endereço IPv6 "unicast global" (global unicast).
22:47
Como mencionei anteriormente, existem vários tipos de endereços IPv6, os quais abordarei em outro vídeo.
22:53
Mas esses endereços "unicast global" são os endereços IPv6 padrão que os hosts podem utilizar na Internet; não se trata de endereços privados, endereços multicast, etc.
23:02
Certo, os 16 bits seguintes — ou seja, 4 dígitos hexadecimais — são chamados de "identificador de sub-rede" (subnet identifier).
23:09
Como a empresa recebeu um bloco /48 do provedor, mas os endereços IPv6 geralmente utilizam
23:15
um prefixo de comprimento /64, esses 16 bits ficam livres para a criação de diferentes sub-redes.
23:21
Juntas, essas duas partes formam a "porção de rede" do endereço, ou seja, o prefixo de rede IPv6.
23:26
Por sua vez, os últimos 64 bits correspondem aos bits de host. Isso representa uma quantidade enorme de hosts por sub-rede — você certamente nunca precisará de tantos.
23:35
Contudo, a convenção é utilizar um prefixo de comprimento /64. Isso não significa, porém, que você encontrará apenas prefixos de comprimento /64.
23:43
Portanto, vamos praticar o uso de endereços IPv6 com diferentes comprimentos de prefixo.
23:49
Determinar o prefixo de um endereço IPv6 com um prefixo de comprimento /64 é simples.
23:55
Basta definir a segunda metade do endereço como zeros. Foi isso que fiz aqui; note que encurtei o endereço removendo um zero inicial e substituí
24:02
a parte do host — que consiste apenas em zeros — por dois-pontos duplos.
24:08
Mesmo que o comprimento do prefixo não seja /64, se ele for um múltiplo de 4,
24:13
é fácil determiná-lo. Por quê? Porque cada caractere hexadecimal equivale a 4 bits.
24:20
56 é um múltiplo de 4; portanto, vou mostrar como encontrar o prefixo deste endereço IPv6.
24:27
Este primeiro quarteto corresponde aos primeiros 16 bits do endereço. O próximo leva a um total de 32 bits.
24:33
48 bits. Este "2" contém os 4 bits seguintes, totalizando 52.
24:38
E este "1" contém mais 4 bits, chegando a 56 bits. Assim, estes primeiros 14 caracteres constituem a parte de rede do endereço, ou seja, o prefixo.
2



4:48
Tudo o que vem depois compõe a parte do host; portanto, podemos definir todos esses valores como 0 para encontrar o prefixo.
24:54
Aqui está, após remover os zeros à esquerda e utilizar o "dois-pontos duplo" (::). Vale ressaltar que nem todos esses zeros podem ser removidos.
25:02
Embora façam parte da porção do host no endereço, eles não são zeros à esquerda, por isso não podem ser omitidos.
25:07
Por exemplo, se você encurtasse o endereço dessa forma — removendo aqueles dois zeros — e depois...
25:13
...adicionasse os zeros à esquerda novamente, o prefixo resultante seria outro, o que configuraria um endereço de rede totalmente diferente...
25:18
...do original. Portanto, lembre-se disso: você só pode remover os zeros que aparecem "à esquerda" (no início de um segmento).
25:24
Até aí, tudo bem simples: basta identificar onde termina a parte da rede e definir todos os dígitos seguintes como 0.
25:31
No entanto, para um endereço IPv6 como este, é necessário seguir alguns passos adicionais.
25:36
O comprimento do prefixo é /93, o que não é um múltiplo de 4. Isso significa que a parte da rede termina no meio de um dos dígitos hexadecimais.
25:46
Vamos descobrir qual é: 16 bits, 32 bits, 48 ​​bits, 64 bits, 80 bits, 84, 88... e este "7" nos leva até 92...
25:59
...bits. Portanto, a parte da rede inclui todos esses caracteres, além do primeiro bit deste "B".
26:05
Assim, para escrever corretamente o prefixo da rede, precisamos analisar a representação binária.
26:12
Como você sabe, o caractere hexadecimal "B" equivale ao número decimal 11. Em binário, o decimal 11 é representado como 1011. 26:21
Apenas este primeiro bit faz parte da porção de rede do endereço; portanto, vamos definir todos os outros bits como 0.
26:27
Agora temos o valor binário 1000. Convertendo-o de volta para decimal, obtemos 8.
26:33
Em hexadecimal, ele também é representado como 8. Assim, ao escrever o prefixo de rede, precisamos substituir o ‘B’ por um ‘8’,
26:41
já que definimos todos os bits de host como 0. Portanto, aqui está o prefixo de rede.
26:46
Observe o ‘8’ no lugar do ‘B’. Espero que você consiga perceber a importância de realmente compreender o sistema binário.
26:53
Se você não conhece o sistema binário, seria difícil entender por que o ‘B’ se torna ‘8’ quando todos os bits de host são definidos como 0.
26:59
O mesmo se aplica ao IPv4. Sem o conhecimento do sistema binário, torna-se impossível compreender de fato o endereçamento e a sub-rede (subnetting) em IPv4.
27:07
Aqui estão alguns exercícios: determine o prefixo de cada um destes endereços IPv6.
27:12
Pause o vídeo agora para realizar a tarefa. Muito bem, aqui estão as respostas.
27:20
Primeiro, segundo, terceiro, quarto e quinto.
27:25
Vale ressaltar que não é obrigatório utilizar a versão abreviada; você pode escrever o endereço completo, se preferir.
27:31
Se desejar praticar um pouco mais, tente escrever alguns endereços IPv6 aleatórios com comprimentos de prefixo variados e, em seguida, determine o prefixo de cada um deles.
27:40
Portanto, abordamos apenas os conceitos fundamentais do IPv6, especificamente no que diz respeito aos endereços IPv6. Configuração de endereços IPv6
27:48
Como quero incluir um laboratório em cada videoaula sempre que possível, vamos abordar uma configuração básica de IPv6.
27:55
Vou mostrar como configurar endereços IPv6 em interfaces de roteador e, no
28:00
próximo vídeo, você poderá praticar no Packet Tracer. O roteador R1 possui três interfaces, cada uma conectada a uma sub-rede diferente:
28:09
2001:db8:0:0::/64 na interface G0/0, 0:1::/64 na G0/1 e 0:2::/64 na G0/2.
28:22
Neste exemplo, a empresa recebeu um bloco de endereços /48 e está utilizando o último quarteto do prefixo para criar sub-redes distintas.
28:30
Um detalhe: talvez você esteja se perguntando por que tenho usado tanto a faixa 2001:db8.
28:36
Isso ocorre porque essa faixa de endereços IPv6 foi reservada especificamente para exemplos e documentação.
28:43
Ela nunca deve ser utilizada em redes reais, mas você pode usá-la livremente em exemplos como este.
28:48
Então, aqui está a configuração. Primeiro, é necessário utilizar o comando `ipv6 unicast-routing`.
28:56
Esse comando permite que os roteadores realizem o roteamento IPv6. Se você não o habilitar, o roteador não encaminhará pacotes IPv6.
29:05
Em seguida, configurei a interface G0/0. O comando para definir um endereço IPv6 é `ipv6 address`, seguido pelo endereço e pelo tamanho do prefixo.
29:14 Você notará que muitos comandos IPv6 são iguais aos do IPv4, exceto pelo fato de que, em vez de
29:21
"IP", o comando utiliza "IPV6". Observe também que você pode usar a versão abreviada do endereço IPv6; o roteador
29:29
entenderá. Lembre-se também de usar o comando "no shutdown" para habilitar a interface.
29:35
Fiz o mesmo na interface G0/1 e, depois, na G0/2, mas, desta vez, digitei o endereço completo.
29:42
Você pode usar o endereço completo, o endereço abreviado ou até mesmo um endereço parcialmente abreviado; o roteador entenderá o que você quer dizer.
29:51
Agora, vamos confirmar as configurações. Usei o comando "show ipv6 interface brief".
29:56
Novamente, assim como no comando para IPv4, basta utilizar "ipv6".
30:02
Há alguns pontos a destacar aqui. Primeiro, observe que é exibida a versão abreviada do endereço, e não todos os 32 dígitos
30:10
hexadecimais. Na verdade, o endereço na interface G0/0 está ainda mais abreviado do que a versão
30:16
que eu digitei. Vale ressaltar que os quatro primeiros quartetos...



...são a parte de rede. Eu digitei estes
30:23
dois zeros aqui no diagrama de rede e ao inserir o comando. Mas eles também podem ser incluídos no "dois-pontos duplo" (::), caso você queira encurtar o endereço o
30:32
máximo possível. Certo, outro ponto a destacar — algo que você provavelmente já notou — é que cada uma dessas interfaces
30:39
possui dois endereços IPv6, embora tenhamos configurado apenas um.
30:44
Esses são chamados de endereços "link-local" (locais de enlace); eles são configurados automaticamente em uma interface assim que você configura um endereço IPv6 — ou seja, quando o IPv6 é habilitado na interface.
30:55
Falarei sobre eles no Dia 32, quando abordarei os diversos tipos de endereços IPv6. Mas, se você
31:00
quiser ler a respeito antes disso, a Wikipédia traz um bom artigo sobre o assunto. O IPv4 também possui endereços "link-local", embora não sejam habilitados automaticamente em interfaces
31:10
IPv4. De qualquer forma, como mencionei, tratarei disso no Dia 32.
Tópicos abordados
31:16
Antes de passarmos para o quiz, vamos recapitular o que vimos no vídeo de hoje. Primeiro, revisamos o sistema hexadecimal e praticamos a conversão entre ele e o sistema binário.
31:26
Embora tenhamos abordado brevemente o sistema hexadecimal ao estudar endereços MAC, no contexto do IPv6 é ainda mais importante estar familiarizado com ele.
31:34
Em seguida, expliquei por que o IPv6 é necessário. Basicamente, não existem endereços IPv4 suficientes para o nosso mundo moderno.
31:41
Abordei os fundamentos do IPv6, com foco principal nos endereços IPv6,
31:48
que possuem 128 bits de extensão e são, geralmente, representados em formato hexadecimal.
31:53
Por fim, mostrei os comandos básicos para habilitar o IPv6 em um roteador e, na sequência, configurar endereços IPv6 em uma interface. 32:00
Ainda há muito mais a abordar sobre IPv6, mas espero que este vídeo tenha sido um bom começo.





