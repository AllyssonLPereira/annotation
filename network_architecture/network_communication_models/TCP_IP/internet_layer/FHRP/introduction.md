# First Hop Redundancy Protocols

## Tópicos que abordaremos

Neste arquivo, abordaremos tudo o que você precisa saber sobre os "protocolos de redundância de primeiro salto" (first hop redundancy protocols), ou FHRPs. Este não é o nome de um protocolo específico, mas sim um tipo de protocolo; 

Primeiro, apresentarei o propósito dos protocolos de redundância de primeiro salto (FHRPs). Em seguida, apresentarei três FHRPs diferentes: HSRP (Hot Standby Router Protocol), VRRP (Virtual Router Redundancy Protocol) e GLBP (Gateway Load Balancing Protocol).

## Introdução ao FHRP

![](../../../../z_imgs/185359.png)

Utilizei este mesmo diagrama ao falar sobre o protocolo Spanning Tree, para demonstrar o conceito e a importância da redundância em redes. Por exemplo, se houvesse apenas uma conexão com a Internet e ela falhar devido a um problema de hardware ou qualquer outro motivo, os PCs não conseguirão mais acessar a Internet. Em sua casa, perder o acesso à Internet por algum tempo seria frustrante, mas provavelmente não chegaria a ser um desastre. Para a maioria das empresas modernas, no entanto, isso representaria um grande problema.

Por isso, podemos utilizar conexões redundantes com a Internet, como mostrado aqui. Observe que adicionei nomes aos dispositivos e endereços IP na rede 172.16.0.0/24 para facilitar a explicação. Agora, caso a conexão entre o R1 e a Internet falhe, o PC1 pode utilizar um caminho alternativo para acessar a Internet via R2. Pode tratar-se, por exemplo, de uma conexão mais lenta e barata, utilizada apenas até que a conexão principal seja restabelecida. Mas vamos parar para refletir sobre isso, pois a questão não é tão simples assim. 

Nesta rede, digamos que o endereço IP do R1, 172.16.0.254, esteja configurado como gateway padrão. Isso significa que cada PC está configurado com o endereço 172.16.0.254 como seu gateway padrão. Portanto, sempre que esses PCs precisarem enviar tráfego para fora da sub-rede local, eles o enviarão para o gateway padrão, o R1. Mas o que acontece se o R1 ficar indisponível por algum motivo, talvez uma falha de hardware?

Felizmente, existe um roteador de backup conectado à Internet: o R2. Mas há um problema aqui. Você consegue identificar qual é? Bem, o problema é que o gateway padrão dos PCs está definido como .254, o endereço do R1. Embora o R2 esteja disponível como backup, os PCs não sabem que o R1 está indisponível e que deveriam passar a usar o R2 como gateway padrão. Se um PC precisar enviar tráfego para a Internet, ele continuará tentando enviá-lo para o R1.

Então, como podemos fazer com que o R2 se torne automaticamente o novo gateway padrão, caso o R1 não possa mais ser utilizado? Essa é a função de um protocolo de redundância de primeiro salto, ou FHRP (First-Hop Redundancy Protocol).

Aqui está uma breve explicação sobre FHRPs, extraída da Wikipedia: "Um protocolo de redundância de primeiro salto (FHRP) é um protocolo de rede de computadores projetado para proteger o gateway padrão utilizado em uma sub-rede, permitindo que dois ou mais roteadores forneçam redundância para esse endereço;" Em caso de falha de um roteador ativo, o roteador de backup assume o endereço, geralmente em poucos segundos.

O termo "protocolo de redundância de primeiro salto" (first-hop redundancy protocol – FHRP) é utilizado porque o gateway padrão é o "primeiro salto" — ou seja, o primeiro roteador no caminho para qualquer destino para o qual o PC esteja enviando tráfego. É assim que os FHRPs funcionam: os dois roteadores compartilham um VIP (endereço IP virtual), por exemplo, 172.16.0.252. Você configura os PCs na rede para utilizarem esse IP virtual como gateway padrão, em vez do endereço IP real do R1.

![](../../../../z_imgs/075356.png)

Agora, os roteadores possuem negociar seus papéis entre si. Como eles fazem isso? Eles enviam mensagens "Hello" (olá) via multicast um para o outro, assim. 

![](../../../../z_imgs/075530.png)

Certo, então quais papéis eles negociaram? Bem, um deles — digamos, o R1 — se tornará o roteador ativo. O outro, R2, se tornará o roteador em espera (standby). Observe que os termos específicos, como "ativo" e "em espera", variam dependendo de qual FHRP está sendo utilizado, pois, como mostrei anteriormente, existem diferentes tipos de FHRP. Portanto, o R1 é o ativo, o que significa que ele atuará como o gateway padrão da rede. O R2 está em espera, o que significa que ele não funcionará como gateway padrão, a menos que o R1 falhe.

Se o R1 falhar, o R2 assumirá automaticamente o papel de gateway padrão. Então, digamos que configuramos nosso FHRP nesta rede; agora, o PC1 precisa enviar tráfego para um destino em outra rede. Eis o que o PC1 "pensa": "Preciso enviar tráfego para um destino em outra rede. Meu gateway padrão é 172.16.0.252, mas ainda não sei qual é o endereço MAC dele. Vou enviar uma solicitação ARP para descobrir o endereço MAC de 172.16.0.252." 

Para que o PC1 possa encapsular o pacote em um quadro (frame) destinado ao gateway padrão, ele precisa conhecer o endereço MAC desse gateway. Portanto, o PC1 fará uma solicitação ARP, mais ou menos assim: "Olá, 172.16.0.252. Aqui é o 172.16.0.1. Qual é o seu endereço MAC?" Lembre-se de que a mensagem de solicitação ARP é um *broadcast*. Portanto, ela será enviada pela rede dessa forma, alcançando todos os *hosts*.

![](../../../../z_imgs/123820.png)

Felizmente, o *Spanning Tree* evita uma tempestade de *broadcast* ao desativar algumas das interfaces do *switch*. Assim, tanto o R1 quanto o R2 recebem a solicitação ARP, e ambos compartilham o mesmo endereço IP virtual, 172.16.0.252 — o endereço que consta na solicitação ARP. O que acontece agora? Qual deles enviará a resposta ARP?

O R1 é o roteador ativo e o R2 é o roteador em espera (*standby*); logo, você provavelmente pode deduzir que o R1 enviará a resposta ARP. E isso está correto. O R1 enviará uma resposta ARP do tipo *unicast*, da seguinte forma: "Olá, 172.16.0.1. Aqui é o 172.16.0.252. Meu endereço MAC é..." — e, em seguida, ele informará ao PC1 qual é o endereço MAC virtual. Exatamente; não é utilizado apenas um endereço IP virtual, mas também um endereço MAC virtual. Cada protocolo FHRP utiliza um endereço MAC virtual diferente — falarei sobre eles mais adiante. Portanto, a resposta ARP é enviada ao PC1.

Agora, o PC1 conhece o endereço MAC do seu *gateway* padrão. Suponhamos, então, que o PC1 precise enviar tráfego para o endereço IP 8.8.8.8 — que, aliás, é um servidor do Google. Quais serão os campos de origem e destino no quadro (*frame*) e no pacote? 

- O IP de origem será o do PC1: 172.16.0.1;
- O IP de destino será o do servidor do Google, 8.8.8.8;
- O MAC de origem será o endereço MAC do PC1; e
- O endereço MAC de destino será o endereço MAC virtual utilizado pelo FHRP.

O quadro (frame) será enviado para o R1 e, em seguida, o pacote será encaminhado pela Internet. Agora, e se o R1 ficar inativo? Não haverá um gateway padrão para a rede. Mas, após alguns segundos, o R2 perceberá: "Não recebo mensagens 'Hello' do R1 há algum tempo... vou assumir o papel de roteador ativo!". Portanto, o R2 passa a ser o roteador ativo. Mas como ele informa aos outros dispositivos que o tráfego deve ser enviado para ele, em vez de para o R1?

Observe que os hosts finais — os PCs — não precisam alterar suas tabelas ARP. A entrada na tabela ARP do PC está configurada de tal forma que mapeia o endereço IP virtual 172.16.0.252 para o endereço MAC virtual. Então, o que precisa ser atualizado para que o tráfego passe a ser encaminhado pelo R2? A resposta são os switches. O R2 precisa fazer com que os switches atualizem suas tabelas de endereços MAC.

Lembre-se de como os switches atualizam suas tabelas de endereços MAC: ao receber um quadro, eles verificam o campo de endereço MAC de origem e o utilizam para atualizar as informações na tabela de endereços MAC. Portanto, o R2 precisa enviar quadros que contenham o endereço MAC virtual como endereço MAC de origem. Para isso, ele enviará respostas "ARP gratuitas" (gratuitous ARP).
 
Mensagens de "ARP gratuito" são respostas ARP enviadas sem que tenham sido solicitadas. Normalmente, as respostas ARP são enviadas em resposta a uma solicitação ARP; no entanto, no ARP gratuito (*gratuitous ARP*), as mensagens de resposta ARP são enviadas sem que tenha havido uma solicitação ARP prévia. 

Eis outra diferença entre o ARP gratuito e as respostas ARP convencionais: os quadros são enviados via *broadcast* para o endereço MAC composto apenas por valores "F" (endereço de *broadcast*), enquanto as respostas ARP normais são enviadas via *unicast*. Como se trata de um *broadcast*, todos os switches recebem esses quadros e atualizam suas tabelas de endereços MAC. Portanto, o R2 enviará mensagens ARP gratuitas da seguinte forma: elas serão propagadas por toda a rede via *broadcast* e, mais uma vez, o protocolo *Spanning Tree* evitará a ocorrência de uma tempestade de *broadcast* (*broadcast storm*).Em seguida, os switches atualizarão suas tabelas de endereços MAC. 

Agora, o R2 é o roteador ativo, e todos os switches atualizaram suas tabelas de endereços MAC. Vamos supor que o PC1 queira enviar tráfego para o mesmo servidor do Google, 8.8.8.8, novamente. O quadro (frame) e o pacote são exatamente os mesmos de antes. O IP de origem é o do PC1, o IP de destino é o do servidor do Google, o MAC de origem é o do PC1 e o MAC de destino é o MAC virtual. No entanto, desta vez, o quadro será enviado para o R2, que encaminhará o pacote pela Internet. Agora, e se o R1 voltar a ficar online? Ele se tornará o roteador ativo novamente? Não, ele passará a ser o roteador em espera (standby).

Como mencionei a respeito do DR e do BDR no OSPF, os FHRPs são "não preemptivos" (non-preemptive). O roteador ativo atual não abrirá mão de sua função automaticamente, mesmo que o roteador que era ativo anteriormente retorne. Contudo, embora esse seja o comportamento padrão, é possível alterar essa configuração para fazer com que o R1 exerça a preempção sobre o R2, retomando sua função de roteador ativo automaticamente; assim, o R2 voltará a ser o roteador em espera.

Muito bem, essa foi uma visão geral básica de como funcionam os protocolos de redundância de primeiro salto (FHRPs).

### Resumo sobre FHRPs

Ainda não falei sobre nenhum FHRP específico, mas a maior parte dessas informações se aplica a todos eles. Antes de prosseguir para explicar alguns FHRPs específicos, aqui está uma breve revisão.

- Um IP virtual é configurado nos dois roteadores, e um MAC virtual é gerado para esse IP virtual. Cada FHRP utiliza um formato diferente para o endereço MAC virtual; abordarei esses endereços MAC na próxima seção;
- São eleitos um roteador ativo e um roteador em espera (*standby*). Vale ressaltar que diferentes FHRPs utilizam terminologias distintas. Alguns suportam uma configuração do tipo "ativo-ativo", na qual dois roteadores operam como ativos simultaneamente — mas explicarei isso mais adiante;
- Em seguida, os dispositivos finais (*hosts*) na rede são configurados para utilizar o IP virtual como seu *gateway* padrão;
- O roteador ativo responde às solicitações ARP utilizando o endereço MAC virtual; assim, o tráfego destinado a outras redes é encaminhado a ele. Ele atua como o *gateway* padrão da rede;
- Caso o roteador ativo falhe, o roteador em espera assume a função de roteador ativo. O novo roteador ativo envia mensagens ARP gratuitas (*gratuitous ARP*), permitindo que os *switches* atualizem suas tabelas de endereços MAC. A partir desse momento, ele passa a atuar como o *gateway* padrão da rede. Se o roteador que era ativo anteriormente voltar a ficar *online*, por padrão, ele não reassume sua função de roteador ativo; ele passa a ser o roteador em espera. Isso é semelhante ao conceito de DR e BDR no protocolo OSPF: eles não abrem mão de suas funções automaticamente, mesmo que outro roteador seja configurado com uma prioridade mais alta. Contudo, nos FHRPs, é possível configurar a "preempção" (*preemption*), permitindo que o roteador que era ativo anteriormente reassuma sua função original caso retorne à operação.

Vamos em frente. Agora, apresentarei uma breve visão geral de três dos principais protocolos FHRP. A funcionalidade de cada um é bem semelhante, por isso esta seção será bastante breve, começando pelo HSRP (Hot Standby Router Protocol).

## HSRP

O HSRP é proprietário da Cisco, portanto, funciona apenas em dispositivos Cisco. Você não pode utilizá-lo em roteadores Juniper, por exemplo. No HSRP, são eleitos um roteador ativo (active) e um roteador de espera (standby). Esses são os dois termos que mencionei anteriormente, mas você verá que o próximo FHRP utiliza termos diferentes.

Existem duas versões do HSRP: a versão 1 e a versão 2. A versão 2 adiciona suporte a IPv6 e aumenta o número de "grupos" que podem ser configurados. Você entenderá o que é um grupo quando configurarmos o HSRP mais adiante. No nosso exemplo de hoje, havia apenas uma sub-rede, 172.16.0.0/24, e uma VLAN. Mas, em situações com múltiplas sub-redes e VLANs, será necessário configurar um endereço IP virtual para cada sub-rede, já que cada uma delas precisa do seu próprio gateway padrão. Cada um desses IPs virtuais é configurado em um grupo HSRP separado. De qualquer forma, como mencionei, você verá como isso funciona mais adiante.

Lembra quando expliquei que os roteadores se comunicam entre si enviando mensagens "hello" via multicast? Estes são os endereços utilizados: 224.0.0.2 para a versão 1 e 224.0.0.102 para a versão 2.

A seguir, veremos os formatos de endereço MAC virtual. Estes são mais difíceis de memorizar. Então, a versão 1 utiliza `0000.0c07.ac`, seguida pelo número do grupo. Por exemplo, digamos que, no meu exemplo anterior, eu tenha configurado o endereço IP virtual no grupo 1. Se estiver usando o HSRP versão 1, qual seria o endereço MAC virtual? Seria `0000.0c07.ac01`, já que o número do grupo é 1.

Já o HSRP versão 2 utiliza o formato `0000.0c9F.Fxxx`, onde, novamente, `xxx` corresponde ao número do grupo. Observe que, agora, 3 dígitos hexadecimais estão disponíveis em vez de 2; portanto, há mais números de grupo disponíveis. De qualquer forma, se o número de grupo 1 for utilizado, qual seria o endereço MAC virtual na versão 2 do HSRP? É `0000.0c9f.f001`.

Um último ponto: em uma situação com múltiplas sub-redes/VLANs, você pode configurar um roteador ativo diferente em cada sub-rede para realizar o balanceamento de carga. Semelhante ao protocolo Spanning Tree, você pode configurar um *root bridge* (ponte raiz) diferente em cada VLAN, de modo que o tráfego seja distribuído (balanceado) entre os switches.

Pois bem, ao configurar múltiplos grupos HSRP — um para cada sub-rede e VLAN —, você pode definir um roteador ativo diferente para cada uma delas. Por exemplo, o R1 poderia ser o roteador ativo na VLAN1 e *standby* (em espera) na VLAN2, enquanto o R2 poderia ser o *standby* na VLAN1 e o ativo na VLAN2. Deixe-me demonstrar brevemente o conceito.

![](../../../../z_imgs/075808.png)

Digamos que a VLAN1 esteja atribuída aos hosts na sub-rede 172.16.1.0/24. O PC1 e o PC3 estão na VLAN1. O R1 e o R2 possuem seus próprios endereços IP na VLAN1, mas também compartilham o IP virtual 172.16.1.252, que é utilizado como *gateway* padrão da sub-rede. O R1 é o roteador ativo, e o R2 é o roteador *standby*. Por sua vez, a sub-rede 172.16.2.0/24 corresponde à VLAN2. O PC2 e o PC4 estão na VLAN2. R1 e R2 possuem seus próprios endereços IP na VLAN2, conectando-se aos switches por meio da topologia "router-on-a-stick".

Eles também compartilham o endereço IP virtual 172.16.2.252, que é utilizado como gateway padrão para a sub-rede. R2 é o roteador ativo, e R1 é o roteador em espera (standby). Agora, o tráfego pode ser balanceado entre os dois caminhos: a VLAN1 utiliza R1 e a VLAN2 utiliza R2 como gateway padrão da sub-rede; além disso, cada sub-rede conta com um roteador em espera, caso o roteador ativo falhe.

Essa é, portanto, uma visão geral básica do HSRP. Embora ele não permita o balanceamento de carga dentro de uma única sub-rede, é possível configurar um roteador ativo diferente para cada sub-rede, de modo que o tráfego seja balanceado entre os roteadores. Vamos passar para o próximo FHRP.

## VRRP

A seguir, temos o VRRP (Virtual Router Redundancy Protocol). Ao contrário do HSRP, ele é um padrão aberto, podendo ser executado em dispositivos de qualquer fabricante. Roteadores Cisco também o suportam; portanto, você pode optar pelo HSRP ou pelo VRRP. Na verdade, em termos de funcionalidade, eles são praticamente idênticos, apresentando apenas algumas pequenas diferenças.

Em vez de um roteador "ativo" (active) e um "em espera" (standby), são eleitos um roteador "mestre" (master) e um "reserva" (backup). A função é a mesma; apenas a nomenclatura muda. O "mestre" equivale ao "ativo" do HSRP, e o "reserva" equivale ao "em espera" (standby) do HSRP.

O endereço multicast IPv4 utilizado também é diferente: 224.0.0.18. O formato do endereço MAC virtual também é diferente. `0000.5e00.01xx`, seguido pelo número do grupo VRRP. Vamos tentar algo um pouco mais desafiador. E se eu configurasse o grupo VRRP `200`, em vez do grupo 1? Qual seria o endereço MAC virtual? Você precisa converter 200 para hexadecimal. Muito bem, a resposta é `0000.5e00.01c8`. O valor hexadecimal `c8` equivale a `200` em decimal. Assim como no HSRP — embora o VRRP não consiga realizar balanceamento de carga para hosts em uma mesma sub-rede —, é possível realizar o balanceamento de carga entre sub-redes diferentes, configurando um roteador "master" (principal) distinto em cada uma delas.

Aqui está o mesmo diagrama de antes, mostrando o balanceamento de carga entre as duas sub-redes.

![](../../../../z_imgs/072825.png)

A única diferença é que os termos "master" e "backup" são utilizados em vez de "active" e "standby". Antes de prosseguir, gostaria de mencionar um ponto que não está diretamente relacionado aos protocolos FHRP.

Observe que todos os hosts na VLAN1 pertencem à mesma sub-rede, 172.16.1.0/24, e todos os hosts na VLAN2 pertencem à mesma sub-rede, 172.16.2.0/24. É assim que sub-redes e VLANs são utilizadas. As sub-redes dividem a rede na Camada 3 (Layer 3), enquanto as VLANs a dividem na Camada 2 (Layer 2). Elas trabalham em conjunto, sendo que cada sub-rede corresponde a uma VLAN específica. 

### Tabela comparativa: HSRP/VRRP

Antes de prosseguirmos para o último FHRP, aqui está uma tabela comparativa entre HSRP e VRRP. 

![](../../../../z_imgs/073049.png)

Em termos de funcionalidade, eles são praticamente iguais. Mas lembre-se das diferenças na terminologia, nos endereços IP multicast e nos endereços MAC virtuais. Lembre-se também de que o HSRP é proprietário da Cisco, enquanto o VRRP é um padrão aberto que pode funcionar em qualquer dispositivo de rede que ofereça suporte a ele. A seguir, veremos o GLBP.

## GLBP

O último FHRP que você deve conhecer é o GLBP (Gateway Load Balancing Protocol). Ele é um pouco diferente do HSRP e do VRRP. Assim como o HSRP, é proprietário da Cisco; portanto, funciona apenas em dispositivos Cisco. Aqui está a grande diferença: ele realiza o balanceamento de carga entre vários roteadores dentro de uma mesma sub-rede. Por exemplo, se o PC1 e o PC2 estiverem ambos na VLAN1, o PC1 pode usar o R1 como seu gateway padrão, e o PC2 pode usar o R2 como seu gateway padrão. Isso é diferente do que ocorre no HSRP e no VRRP, no qual todos os hosts na mesma sub-rede devem usar o mesmo roteador como gateway padrão para a sub-rede. 

No GLBP, um único AVG (Active Virtual Gateway – Gateway Virtual Ativo) é eleito para a sub-rede. Em seguida, até quatro AVFs (Active Virtual Forwarders – Encaminhadores Virtuais Ativos) são atribuídos pelo AVG, sendo que o próprio AVG também pode atuar como um AVF. Cada AVF funciona como o gateway padrão para uma parte dos hosts na sub-rede. Assim, o balanceamento de carga é obtido dentro de uma única sub-rede. 

O endereço IPv4 multicast é 224.0.0.102, o mesmo utilizado pelo HSRP versão 2. O formato do endereço MAC virtual é `0007.b400.xxyy`, seguido pelo número do grupo GLBP e pelo número do AVF. Por exemplo, qual é o endereço MAC virtual do AVF número 1 no grupo GLBP 1? É `0007.b400.0101`. 

Portanto, as funções do GLBP são um pouco mais complexas do que as do HSRP e do VRRP; lembre-se de que o GLBP permite que vários roteadores ativos realizem o balanceamento de carga do tráfego dentro de uma única sub-rede. Lembre-se também do endereço IP multicast e do formato do endereço MAC virtual. Aqui está a tabela novamente, agora com o GLBP incluído.

![](../../../../z_imgs/074350.png)

## Configuração de HSRP

Para que tudo coubesse na tela e fosse possível exibir a CLI ao mesmo tempo, simplifiquei a rede. Nosso foco será configurar o R1 e o R2 para usar o HSRP, fornecendo um endereço de gateway padrão redundante para a sub-rede 172.16.0.0/24.

![](../../../../z_imgs/074537.png)

Já configurei todos os endereços IP das interfaces; portanto, só precisamos configurar o HSRP. Observe que, desta vez, estou usando .254 como IP virtual, em vez de .252. Então, vamos começar configurando o R1.

O HSRP é configurado diretamente na interface — neste caso, a G0/0. Certifique-se de realizar a configuração na interface correta: aquela conectada à rede para a qual o dispositivo atuará como gateway padrão. O HSRP é configurado por meio do comando `standby`. Usei o ponto de interrogação para verificar quais opções estão disponíveis. Existem muitas outras opções, mas a que queremos utilizar é esta: o número do grupo. 

Observe que a versão 1 do HSRP é o padrão; portanto, o intervalo de grupos disponível vai de 0 a 255. Se você utilizar a versão 2 do HSRP, esse intervalo passa a ser de 0 a 4095. Na verdade, vou mostrar como alterar para a versão 2. O comando é `standby version 2`. Se eu verificar o comando `standby` novamente, você verá que o intervalo de números de grupo agora vai de 0 a 4095.

Esta rede simples utiliza apenas uma única VLAN, a VLAN 1; por isso, escolhi o número de grupo HSRP 1. Não é obrigatório fazer isso — não é uma regra —, mas gosto de fazer com que o número do grupo HSRP corresponda ao número da VLAN utilizada para a sub-rede. Vale ressaltar que esse número de grupo precisa ser idêntico em ambos os roteadores; isso é importante.

![](../../../../z_imgs/075600.png)

Então, utilizei o ponto de interrogação novamente para conferir as opções disponíveis. Vamos analisar três delas: `ip`, `preempt` e `priority`.  Primeiro, configura-se o IP virtual usando o comando `standby`, seguido pelo número do grupo e pela palavra-chave `ip`, e, na sequência, pelo endereço IP que você deseja definir como gateway padrão. 

Em seguida, utilizei o comando `priority` — note que o intervalo é de 0 a 255 — e defini a prioridade do R1 como 200. Para que serve a prioridade? Ela é utilizada para determinar qual roteador será o roteador ativo. O roteador ativo é definido seguindo esta ordem: primeiramente, o roteador com a maior prioridade HSRP dentro do grupo torna-se o roteador ativo. A prioridade padrão é 100. Se os roteadores tiverem a mesma prioridade, o roteador com o endereço IP mais alto se tornará o roteador ativo. Neste caso, o endereço IP do R1, 172.16.0.253, é maior que o endereço IP do R2, 172.16.0.252. Portanto, mesmo sem configurar a prioridade, o R1 ainda se tornaria o roteador ativo; mas, ainda assim, eu a configurei. 

Por fim, habilitei a "preempção" (preemption). Habilitar o comando de preempção faz com que o roteador assuma a função de roteador ativo, mesmo que outro roteador já esteja ocupando essa posição — embora o roteador que realiza a preempção precise ter uma prioridade maior ou um endereço IP mais alto. Por exemplo, digamos que o R1 seja o roteador ativo e o R2 seja o roteador em espera (standby). Se uma falha fizer com que o R1 seja reiniciado, o R2 se tornará o roteador ativo. Quando o R1 voltar a ficar online, se a preempção não estiver habilitada, o R2 continuará sendo o roteador ativo e o R1 ficará em espera. No entanto, com a preempção habilitada, o R1 retomará sua função como roteador ativo, pois ele possui a prioridade mais alta.

Observe que você só precisa configurar a preempção no roteador que você deseja que se torne o roteador ativo. Mesmo que eu não configure a preempção no R2, o R1 ainda será capaz de realizar a preempção sobre o R2 e assumir de volta a função de roteador ativo. Agora, vamos configurar o R2.

![](../../../../z_imgs/075705.png)

Primeiramente, habilitei o HSRP versão 2 na interface G0/0 do R2. Isso é importante: o HSRP versão 1 e a versão 2 não são compatíveis. Portanto, se o R1 utiliza a versão 2, o R2 também deve utilizar a versão 2; caso contrário, surgirão problemas.

Em seguida, configurei o mesmo IP virtual utilizado no R1: 172.16.0.254. Os dois comandos seguintes — a definição da prioridade e da preempção — são, na verdade, desnecessários. O R1 já possui uma prioridade maior que a do R2, e a preempção não precisa estar habilitada no roteador em espera (*standby*). No entanto, eu os configurei de qualquer forma, para que a configuração permaneça consistente entre os dois roteadores; mas, na prática, isso não faz diferença. Por fim, vamos analisar a saída do comando `show standby`.

![](../../../../z_imgs/075759.png)

Esta é a saída tanto para o R1 quanto para o R2; vamos focar no R1. 

- Observe, primeiramente, que o número do grupo HSRP é 1 e que a versão 2 está sendo utilizada;
- O estado é *active* (ativo), uma vez que o R1 é o roteador ativo;
- Aqui, é exibido o endereço IP virtual que configuramos;
- Temos os endereço MAC virtual; trata-se do endereço padrão;
- Os temporizadores (*timers*) do HSRP também estão presentes. Como não os configuramos, eles permanecem com os valores padrão;
- A preempção está habilitada, pois configuramos o comando `standby 1 preempt`;
- O roteador ativo é o local, pois o próprio R1 é o roteador ativo;
- O roteador em espera (*standby*) é o 172.16.0.252, que corresponde ao R2; e
- Finalmente, aqui está o valor de prioridade 200 que configuramos.

O mesmo serve para o R2.

