
Neste vídeo, continuaremos nosso estudo sobre o Spanning Tree, focando em uma versão atualizada chamada Rapid Spanning Tree. Mais especificamente, veremos a versão da Cisco: Rapid Per-VLAN Spanning Tree.

Você viu na aula anterior que o Spanning Tree clássico pode ser bastante lento, levando até 50 segundos para a rede convergir após uma mudança na topologia. Como o nome sugere, o Rapid Spanning Tree melhora esse tempo, levando apenas alguns segundos para responder a mudanças na rede. 

Por ser superior ao Spanning Tree clássico, o Rapid Spanning Tree é o padrão na maioria dos dispositivos atualmente, e os tópicos do exame CCNA mencionam apenas o Rapid Spanning Tree. No entanto, acredito que seja importante entender o Spanning Tree clássico; agora que você já o conhece, será muito mais fácil aprender o Rapid Spanning Tree. 

Vamos ver o que abordaremos neste vídeo. Primeiramente, dedicaremos alguns minutos para comparar diferentes versões do STP.

## Tópicos que abordaremos

Nos vídeos anteriores, mencionei várias versões: STP, PVST+, Rapid STP, Rapid PVST+ e Multiple Spanning Tree. Para evitar confusão, farei um resumo de cada versão e esclarecerei a diferença entre os padrões da indústria e as versões proprietárias da Cisco. Depois, o restante do vídeo será dedicado ao Rapid Spanning Tree, especificamente à versão que opera em switches Cisco: o Rapid Per-VLAN Spanning Tree Plus.

Vamos começar resumindo as diferentes versões do Spanning Tree.

## Comparação de Versões do STP

À esquerda, listarei as versões padrão da indústria, os padrões IEEE. À direita, listarei as versões proprietárias da Cisco — as melhorias da Cisco em relação a algumas das versões padrão.

Primeiro, o protocolo Spanning Tree clássico, o padrão IEEE 802.1D. Este é o protocolo Spanning Tree original; segundo a Wikipedia, foi publicado originalmente em 1990, embora o Spanning Tree original tenha sido criado, na verdade, em 1985, antes de ser padronizado. 

No STP clássico, todas as VLANs compartilham uma única instância de STP. Portanto, não podemos realizar balanceamento de carga usando o STP clássico, pois existe apenas uma instância; não podemos bloquear portas diferentes em cada VLAN para obter balanceamento de carga. Então, a Cisco decidiu aprimorar isso.

Eles desenvolveram o Per-VLAN Spanning Tree Plus. Na verdade, antes disso, desenvolveram o Per-VLAN Spanning Tree comum que, como mencionei anteriormente, suportava apenas encapsulamento de tronco ISL, e não dot1q; mas vamos esquecer essa versão, já que hoje em dia todos usam dot1q para encapsulamento de tronco.

É a atualização da Cisco para o 802.1D. Cada VLAN tem sua própria instância de STP. No vídeo anterior do laboratório, quando configuramos o STP, tivemos que incluir o número da VLAN em cada comando — por exemplo, `spanning-tree vlan 1 root primary`. Isso ocorre porque uma instância STP separada é executada para cada VLAN.

Por que isso é bom? Bem, como você já sabe, podemos realizar o balanceamento de carga bloqueando portas diferentes em cada VLAN, ou seja, em cada instância STP. Podemos utilizar a largura de banda da rede de forma mais eficaz, já que não temos conexões ficando totalmente ociosas, apenas aguardando a falha de outra conexão. 

Agora, como você também sabe, o Spanning Tree clássico e o PVST+ são bastante lentos. O temporizador *max age* é de 20 segundos, e os estados de *listening* (escuta) e *learning* (aprendizado) duram 15 segundos cada; portanto, pode levar até 50 segundos para responder a alterações na rede. Isso simplesmente não é rápido o suficiente para as redes modernas.

Esse problema foi resolvido com o Rapid Spanning Tree Protocol, o padrão IEEE 802.1w. Ele é muito mais rápido na convergência e na adaptação a mudanças na rede do que o 802.1D. No entanto, assim como o 802.1D, o Rapid Spanning Tree Protocol (padrão da indústria) executa apenas uma instância STP, compartilhada por todas as VLANs. Consequentemente, ele também não consegue realizar o balanceamento de carga.

A Cisco desenvolveu, mais uma vez, uma versão aprimorada do padrão da indústria: o Rapid Per-VLAN Spanning Tree Plus, ou Rapid PVST+. É a evolução da Cisco para o 802.1w, que oferece a velocidade aprimorada do Rapid STP e, além disso, executa uma instância STP separada para cada VLAN. Portanto, ele pode realizar o balanceamento de carga bloqueando portas diferentes em cada VLAN, assim como o PVST+ anterior. 

A versão final é o Multiple Spanning Tree Protocol, o padrão IEEE 802.1s. Ele utiliza RS modificado...


...mecânicas do STP. Mas a principal melhoria é que ele pode agrupar várias VLANs em instâncias diferentes; por exemplo, se houver 10 VLANs, você pode colocar as VLANs de 1 a 5 na instância 1 e as VLANs de 6 a 10 na instância 2 para realizar o balanceamento de carga. Finalmente, temos uma versão do STP baseada em padrão da indústria que permite balanceamento de carga e que, na verdade, é superior ao Rapid-PVST da Cisco. 

Se você tiver muitas VLANs na sua rede — digamos, 200 —, configurar *root bridges* primários e secundários em cada VLAN dá muito trabalho. No entanto, com o MSTP, basta atribuir as VLANs de 1 a 100 à instância 1 e as VLANs de 101 a 200 à instância 2, e então configurar os *root bridges* primários e secundários para as instâncias 1 e 2; assim, a configuração e o gerenciamento tornam-se muito mais fáceis.

Na verdade, a Cisco não desenvolveu uma versão própria do MSTP; os dispositivos Cisco simplesmente executam o padrão da indústria 802.1s. Para redes grandes, o ideal é usar o MSTP; porém, para redes de pequeno a médio porte sem um número enorme de VLANs, o Rapid PVST+ da Cisco é o que você provavelmente utilizará em seus switches, e essa é a versão na qual vamos focar hoje. 

É também a versão mencionada na lista oficial de tópicos do exame. Além disso, todas essas informações aqui se aplicam ao padrão 802.1w, mas essa não é a versão executada nos switches Cisco. A boa notícia é que, como você já entende o STP clássico e o PVST+, será muito mais fácil aprender o Rapid STP e o Rapid PVST+ fazendo comparações com as versões anteriores.

Vamos começar. Antes de entrar nos detalhes, aqui está o resumo da Cisco sobre o RSTP.

## Introdução ao RSTP

RSTP não é um algoritmo de *spanning tree* baseado em temporizadores, como o 802.1D. Portanto, o RSTP oferece uma melhoria em relação aos 30 segundos ou mais que o 802.1D leva para colocar um link no estado de encaminhamento (*forwarding*).

O coração do protocolo é um novo mecanismo de *handshake* (aperto de mão) entre bridges, que permite que as portas passem diretamente para o estado de encaminhamento. Essa é a grande diferença entre o RSTP e o STP 802.1D. 

O 802.1D utiliza temporizadores longos para determinar quando é seguro passar para o próximo estado; esses temporizadores são bastante longos para garantir que nenhum loop seja criado acidentalmente quando uma porta começa a encaminhar tráfego.

Na época em que o STP original foi criado, era aceitável que uma porta levasse de 30 a 50 segundos para reagir a uma mudança e começar a encaminhar tráfego. No entanto, isso não é mais o caso. Por isso, o RSTP utiliza um mecanismo de *handshake* que permite aos switches negociar ativamente com outros switches e colocar as portas imediatamente no estado de encaminhamento, se apropriado.

Certo, agora vou apresentar algumas das especificidades do RSTP. Aliás, provavelmente direi RSTP às vezes e Rapid PVST+ em outras. Na verdade, estou falando da mesma coisa. O Rapid PVST+ da Cisco opera da mesma forma que o RSTP, mas com a adição de uma instância separada para cada VLAN; portanto, usarei os dois termos de forma intercambiável.

## Semelhanças entre STP e RSTP

Vamos resumir algumas semelhanças entre o STP e o RSTP.

Primeiramente, o RSTP tem a mesma finalidade que o STP: bloquear portas específicas para evitar loops de Camada 2. O RSTP elege uma *root bridge* (ponte raiz) seguindo as mesmas regras do STP. Tenho certeza de que você já sabe: o switch com o menor Bridge ID torna-se a bridge raiz (root bridge).

O RSTP também elege portas raiz seguindo as mesmas regras do STP. Assim, a interface com o menor custo para a raiz torna-se a porta raiz, utilizando os mesmos critérios de desempate: Bridge ID do vizinho e, em seguida, Port ID do vizinho. Você estudou isso no vídeo do dia 20, nossa primeira aula sobre STP.

Por fim, o RSTP elege portas designadas seguindo as mesmas regras do STP. Portanto, a interface no switch com o menor custo para a raiz será designada, e a interface no outro switch será não designada. Em caso de empate, o switch com o menor Bridge ID definirá sua interface como designada.

A Cisco afirmou que o RSTP não é uma "revolução" do STP, mas apenas uma "evolução". Ele trouxe melhorias significativas para acelerar o STP, mas não o alterou completamente, como você pode ver aqui.

Agora, vamos analisar algumas diferenças entre o STP e o RSTP.

## Diferenças
### Custos de Porta no RSTP

Primeiramente, os custos de porta foram atualizados para o Rapid Spanning Tree. O Spanning Tree clássico define custos para velocidades de porta de até 10 Gbps; acredito que, para velocidades superiores a essa, atribui-se um custo de 1. Para acomodar velocidades mais altas, os valores de custo do RSTP foram ampliados.

- 2 milhões para 10 Mbps;
- 200 mil para 100 Mbps;
- 20 mil para 1 Gbps;
- 2.000 para 10 Gbps;
- 200 para 100 Gbps; e 
- 20 para 1 Tbps.

### Estados de Porta do STP

Aqui está um slide do dia 21, mostrando os diferentes estados de porta do protocolo Spanning Tree clássico. Espero que você se lembre desses estados: quais enviam e recebem BPDUs, qual encaminha tráfego, quais aprendem endereços MAC, etc. No entanto, o Rapid Spanning Tree simplifica os estados de porta, reduzindo-os a...


...combinando três desses estados em um só.

Os três estados combinados em um são: *blocking* (bloqueio), *listening* (escuta) e *disabled* (desativado). Na verdade, uma forma mais precisa de dizer é que os estados de porta *blocking* e *disabled* foram combinados em um único estado, e o estado *listening* simplesmente não é utilizado. Portanto, o estado *listening* deixou de existir, e os estados *blocking* e *disabled* passaram a ser o estado *discarding* (descarte) no RSTP. 

Se uma porta estiver administrativamente desativada — ou seja, se o comando *shutdown* tiver sido aplicado a ela —, ela ficará no estado *discarding* no RSTP. Esse estado correspondia anteriormente ao estado *disabled*. Se uma porta estiver ativada, mas bloqueando o tráfego para evitar loops de Camada 2, ela também estará no estado *discarding*. Esse estado correspondia anteriormente ao estado *blocking*. 

A seguir, que tal falarmos sobre as funções de porta?

### Funções de Porta RSTP

Lembre-se de que as três funções originais de porta são: *root* (raiz), *designated* (designada) e *non-designated* (não designada).

A função de porta *root* permanece inalterada no RSTP. A porta mais próxima da *root bridge* (ponte raiz) torna-se a porta *root* do switch. Naturalmente, "mais próxima" significa a porta com o menor custo para a raiz (*root cost*). Além disso, a *root bridge* é o único switch que não possui uma porta *root*. Portanto, esses pontos são iguais ao que você já aprendeu sobre o Spanning Tree clássico.

A função de porta *designated* também permanece inalterada no RSTP. A porta em um segmento (que é outro nome para domínio de colisão) que envia o melhor BPDU é a porta *designated* daquele segmento, e só pode haver uma porta *designated* por segmento. A outra porta no segmento é uma porta *root* ou uma porta *non-designated* no Spanning Tree clássico. 

No entanto, a função de porta *non-designated* foi dividida em duas funções distintas no RSTP. Trata-se das funções de porta *alternate* (alternativa) e *backup* (reserva). Vamos analisar essas duas funções.

#### Funções de Porta RSTP – Alternate (+UplinkFast)

Primeiro, a função de porta *alternate*. A função de porta *alternate* no RSTP refere-se a uma porta em estado de descarte (*discarding*) que recebe um BPDU superior de outro switch. Isso é o mesmo que você já aprendeu sobre portas em estado de bloqueio (*blocking*) no STP clássico.

Na nossa pequena topologia aqui embaixo, o SW1 é a *root bridge* (ponte raiz). Quando BPDUs são enviados nesta topologia, o SW3 recebe um BPDU superior do SW2. Ele é superior porque o *bridge ID* do SW2 é menor que o do SW3. Assim, a interface do SW2 é designada (*designated*), e a do SW3 é uma porta *alternate*.

Uma porta *alternate* funciona basicamente como um *backup* para a porta raiz (*root port*). Se a porta raiz falhar, o switch pode imediatamente mudar sua melhor porta *alternate* para o estado de encaminhamento (*forwarding*), passando a ser a nova porta raiz. Se a porta raiz do SW3 falhar, sua porta *alternate* estará pronta para se tornar imediatamente a porta raiz, sem estados de transição.

Essa mudança imediata para o estado de encaminhamento funciona como um recurso opcional do STP clássico chamado UplinkFast. Como ele já está integrado ao RSTP, você não precisa ativar o UplinkFast ao usar RSTP ou Rapid PVST+. 

Não abordamos o UplinkFast nos vídeos anteriores; ele não é mencionado na lista de tópicos do exame, mas tente lembrar que suas funções estão integradas ao Rapid Spanning Tree; você pode ser questionado sobre isso na prova.

##### RSTP: Funcionalidade BackboneFast

Então, o UplinkFast é um recurso opcional do STP que foi incorporado ao RSTP. Já que mencionei um, gostaria de explicar brevemente mais um que foi incorporado ao RSTP. 

Nenhum desses itens consta na lista de tópicos do exame, então você não precisa estudá-los a fundo; basta estar ciente de sua funcionalidade geral, pois fazem parte do RSTP.

Mais um recurso opcional do STP que foi incorporado ao RSTP é o BackboneFast. Digamos que a porta raiz do SW2 seja desconectada, fazendo com que ele pare de receber BPDUs da bridge raiz. Ele então assumirá que é a bridge raiz e enviará seus próprios BPDUs para o SW3.

No entanto, o SW3 passa a receber BPDUs tanto do SW1 quanto do SW2, mas os BPDUs do SW2 são inferiores; eles possuem um Bridge ID mais alto. Sem a funcionalidade BackboneFast, o SW3 simplesmente ignoraria esses BPDUs do SW2 até que sua porta não designada — no STP clássico — finalmente mudasse para o estado de encaminhamento e encaminhasse os BPDUs superiores para o SW2, que então aceitaria novamente o SW1 como sua bridge raiz.

Contudo, o BackboneFast permite que o SW3 expire o temporizador *max age* (tempo máximo de vida) nessa interface e encaminhe rapidamente os BPDUs superiores para o SW2. Essa funcionalidade já vem integrada ao RSTP, portanto, não precisa ser configurada.

Essa é uma explicação bem básica sobre o BackboneFast. 

UplinkFast e BackboneFast são dois recursos opcionais do STP clássico. Eles precisam ser configurados para operar no switch, mas não é necessário saber como fazê-lo para o exame CCNA. Ambos os recursos já estão integrados ao RSTP; portanto, se o switch estiver executando RSTP, você não precisa configurá-los. 

Eles operam por padrão em todos os switches que executam RSTP. 

#### Funções de Porta RSTP - Backup

Acabamos de ver a função de porta alternativa, que é exatamente como a função de porta não designada que vimos nas aulas anteriores.

A seguir, vamos ver a função de porta de backup. A função de porta de backup no RSTP é uma porta em estado de descarte que recebe um BPDU superior de outra interface no mesmo switch. Isso só acontece quando duas interfaces estão conectadas ao mesmo domínio de colisão, via um hub. 

Observe que agora há um hub Ethernet conectado entre o SW2 e o SW3 Quando BPDUs são enviados nesta rede, o BPDU enviado pela porta designada do SW2 é propagado (flooded) pelo hub e, como você pode ver aqui, ele recebe esse mesmo BPDU em uma interface diferente.

É por isso que essa interface é uma porta de backup, e não uma porta alternativa. No entanto, já mencionei que hubs não são usados ​​em redes modernas, então você provavelmente não encontrará uma porta de backup RSTP. Ainda assim, é algo que você deve saber.

As portas de backup RSTP funcionam como um backup para uma porta designada. Se a porta designada do SW2 falhar, sua porta de backup começa imediatamente a encaminhar o tráfego como uma porta designada. Agora, quanto a como o switch escolhe qual porta será a designada e qual será a porta de backup: a interface com o menor ID de porta será selecionada como a porta designada e a outra será a porta de backup.

## Configuração/Verificação do RSTP na CLI

Agora, vamos dar uma olhada rápida na CLI; estou no SW3 aqui. Como mostrei no vídeo anterior, existem três modos de STP que você pode executar em um switch Cisco: MST, PVST e Rapid-PVST.

O Rapid-PVST é o padrão nos switches Cisco modernos, então você provavelmente não precisará usar este comando, mas digitei `spanning-tree mode rapid-pvst` para garantir que ele opere no modo rapid pvst. Depois, usei `show spanning-tree` para confirmar.

Observe que aparece a mensagem "Spanning tree enabled protocol rstp". Anteriormente, quando usávamos o STP clássico, aparecia "ieee"; agora aparece "rstp". Embora apareça "rstp", trata-se, na verdade, do Rapid PVST+ da Cisco em execução.

Agora, a única outra diferença que quero destacar é esta. Como mostrado no diagrama de rede, a interface G0/1 do SW3 tem a função 'backup'. O status ainda aparece como BLK, de 'blocking' (bloqueio), embora esse estado seja, na verdade, chamado de 'discarding' (descarte) no Rapid STP. Também utilizei o comando SHOW SPANNING-TREE no SW4.

Assim como no diagrama de rede, a interface G0/0 do SW4 é uma porta 'Alternate' (alternativa).

Mais uma vez, este comando



...lista o status como "blocking" (bloqueio), mas lembre-se de que o nome do Rapid STP para esse estado é, na verdade, "discarding" (descarte).
22:33
Apenas uma observação sobre a execução de diferentes versões de STP: o Rapid STP É compatível com o STP clássico.
22:39
A interface — ou as interfaces — no switch com Rapid STP habilitado, conectado ao switch com
22:46
STP clássico habilitado, operará no modo STP clássico, com os mesmos temporizadores e o mesmo processo de transição de estados
22:53
(de blocking para listening, learning e forwarding, etc.). Portanto, se você tiver um switch muito antigo que não suporte Rapid STP, ainda poderá usá-lo em uma rede
23:03
de switches com Rapid STP habilitado; eles ajustarão a operação dessas interfaces específicas
23:08
para se adequarem ao switch mais lento. Assim, em nosso diagrama de rede, se o SW4 estivesse executando STP clássico, o SW2 e o SW3 fariam com que essas
23:18
interfaces operassem no modo STP clássico, mas as interfaces deles conectadas ao SW1 permaneceriam no
23:24
modo Rapid STP. A seguir, vamos analisar o BPDU atualizado para RSTP.
BPDU do RSTP (captura de pacotes no Wireshark)
23:31
Aqui à esquerda está o BPDU do STP clássico para comparação; eu o reduzi para que você possa ver
23:37
melhor o BPDU do Rapid STP. A maior parte do BPDU permanece inalterada, mas há algumas diferenças que você deve conhecer.
23:46
Como mencionei anteriormente, você não precisa memorizar o BPDU; isso vai além do nível de detalhe exigido para o CCNA.
23:53
Você só precisa conhecer alguns aspectos dele e que tipo de informações estão incluídas nele.
23:59
A primeira diferença a ser observada entre esses dois BPDUs está aqui. Note que o BPDU do RSTP
24:05
tem a versão de protocolo 2, enquanto o Spanning Tree clássico tem a versão 0.
24:11
Lembre-se desses números de versão para o exame: 0 para STP clássico, 2 para Rapid STP. 24:18
O BPDU do Rapid STP também possui o tipo de BPDU 2. Agora, aqui está a próxima diferença.
24:27
O BPDU do STP clássico utiliza apenas dois bits dos sinalizadores (flags) do BPDU: o 1º bit e o 8º bit.
24:35
No entanto, o BPDU do Rapid STP utiliza todos os 8 bits.
24:41
Esses sinalizadores são usados ​​no processo de negociação que permite ao Rapid STP convergir muito mais rapidamente
24:46
do que o STP clássico. Isso é tudo o que você realmente precisa saber sobre o BPDU do Rapid STP em si, em comparação com a
24:54
versão anterior. Mas há mais uma diferença importante. No STP clássico, apenas a *root bridge* (ponte raiz) originava BPDUs; os outros switches apenas encaminhavam os
25:05
BPDUs que recebiam. No Rapid STP, TODOS os switches originam e enviam seus próprios BPDUs a partir de suas portas designadas.
25:14
Vamos analisar algumas outras diferenças. Primeiro, como acabei de dizer, todos os switches que executam o Rapid STP enviam seus próprios BPDUs.
Temporizador Hello e Envelhecimento (Aging) do RSTP
25:25
Os switches também processam o "envelhecimento" (*aging*) das informações do BPDU muito mais rapidamente. No STP clássico, um switch aguarda 10 intervalos de *hello*, o que equivale a 20 segundos.
25:35
No Rapid STP, um switch considera um vizinho perdido se não receber 3 BPDUs consecutivos, o que equivale a 6 segundos.
25:43
Ele então realiza um *flush* — ou seja, exclui — todos os endereços MAC aprendidos naquela interface.
25:48
Por que ele faz isso? Porque, como o vizinho está inativo, ele sabe que não consegue mais alcançar nada através daquela interface.
25:54
Por exemplo, nesta rede, o tráfego do PC1 para o PC2 geralmente segue este caminho.
26:04
Mas e se essa conexão for interrompida? Este switch pensará: "Não consigo mais alcançar esse vizinho". 26:10
Vou limpar todas as entradas referentes a esta interface da minha tabela MAC, e a outra interface dela
26:15
passará a ser a porta raiz (root port). Então, se o PC1 quiser enviar tráfego para o PC2 novamente, ele passará pelo processo normal
26:23
de *flooding* (difusão) até aprender o endereço MAC nesta nova interface, e o tráfego seguirá agora por esse caminho.
26:29
Essa é apenas uma visão geral de como as mudanças de topologia são tratadas no Rapid STP.
26:35
Poderíamos nos aprofundar muito nesse assunto, mas não é necessário para o CCNA.
26:41
Se você quiser avançar para obter as certificações CCNP e CCIE, certamente terá que estudar esses processos com mais profundidade.
Tipos de Link no RSTP
26:50
Antes de resumir tudo e passar para o quiz, há mais um conceito do RSTP que você deve conhecer: os tipos de link do RSTP.
26:58
O RSTP distingue três "tipos de link" diferentes. O primeiro tipo é o *edge* (borda).
27:05
Uma porta *edge* é uma porta conectada a um dispositivo final (*host*). Ela passa diretamente para o estado de encaminhamento (*forwarding*) sem negociação.
27:13
Isso lhe parece familiar? Lembra o PortFast. Bem, a funcionalidade PortFast foi incorporada ao RSTP.
27:20
Então, há outro recurso opcional do STP integrado ao RSTP por padrão — além de UplinkFast e BackboneFast,
27:28
temos agora o PortFast. O próximo tipo de link é o ponto a ponto (*point-to-point*).
27:34
Ele é usado para conexões diretas entre dois switches. No entanto, existe mais um tipo, embora seja um que você provavelmente nunca utilizará.
27:43
Esse tipo é o compartilhado (*shared*). Trata-se de uma conexão com um hub, como vimos anteriormente no vídeo.
27:49
Essas conexões devem operar em *half-duplex* para evitar colisões. Não confunda esses tipos de link com as funções de porta (*port roles*) ou estados de porta (*port states*) do Spanning Tree. 27:59
Basicamente, os tipos de link ponto a ponto e compartilhado apenas distinguem entre conexões
28:05
full-duplex e half-duplex, e o tipo "edge" é uma porta que utiliza o PortFast. Certo, vamos...


Vamos dar uma olhada rápida em cada tipo.
Tipos de Link RSTP – Edge (Borda)
28:15
Como eu disse, as portas de borda (*edge ports*) são conectadas a dispositivos finais (*hosts*). Como não há risco de criar um *loop*, elas podem passar diretamente para o estado de encaminhamento (*forwarding*)
28:23
sem o processo de negociação. Elas funcionam como uma porta STP clássica com o PortFast habilitado.
28:30
Na verdade, você configura uma porta de borda simplesmente habilitando o PortFast nela. Aqui está o comando, assim como no STP clássico.
28:39
Então, na prática, o PortFast e uma porta de borda RSTP são a mesma coisa.
28:45
Nesta rede aqui embaixo, quais portas devem ser configuradas como portas de borda? Pause o vídeo se quiser pensar sobre isso.
28:52
Já tem a resposta? Todas essas portas — aquelas conectadas aos PCs — devem ser configuradas como portas de borda.
Tipos de Link RSTP – Ponto a Ponto
29:02
A seguir, ponto a ponto. Essas portas se conectam diretamente a outro *switch*.
29:08
Como elas se conectam a um *switch*, e não a um *hub*, funcionam em modo *full-duplex*.
29:14
Você não precisa configurar a interface como ponto a ponto; o *switch* deve ser capaz de detectar que está conectado diretamente a outro *switch* e operará em *full-duplex*
29:23
como uma porta ponto a ponto. No entanto, se você quiser configurar explicitamente o tipo de link como ponto a ponto, use este comando:
29:32
`spanning-tree link-type point-to-point`. Então, quais conexões no diagrama são ponto a ponto?
29:39
Pause o vídeo para pensar sobre isso. Encontrou a resposta?
29:45
São estas três: as conexões diretas entre dois *switches*.
Tipos de Link RSTP – Compartilhado
29:51
Finalmente, as portas compartilhadas conectam-se a um *hub*. Devido à natureza dos *hubs* e à probabilidade de colisões, esses links devem funcionar em
30:01
*half-duplex*. Mais uma vez, não é necessário configurar a interface no modo compartilhado; o switch irá
30:06
detectá-la. No entanto, para configurá-la manualmente, use este comando: SPANNING-TREE LINK-TYPE SHARED.
30:15
Embora você deva estar ciente desse tipo de link RSTP, como eu já disse, provavelmente nunca verá esse tipo de link em redes reais; hubs são uma tecnologia antiga
30:25
que foi totalmente substituída por switches. Então, quais conexões no diagrama são conexões compartilhadas?
30:31
Acho que a resposta é bem óbvia agora: todas as restantes, que estão conectadas ao hub.
30:38
Portanto, estas conexões aqui são links compartilhados.
Tópicos abordados
30:43
Antes de passar para o quiz, vamos resumir o que abordamos hoje. Primeiro, comparamos as diferentes versões do STP.
30:51
O STP clássico é o 802.1D, e a atualização da Cisco é o PVST+, que executa uma instância
30:58
de spanning tree separada para cada VLAN. Em seguida, a próxima versão padrão é o 802.1w, o Rapid Spanning Tree Protocol.
31:06
A versão da Cisco para isso é o Rapid PVST+, que, novamente, executa uma instância separada para cada
31:12
VLAN. Há também outro padrão da indústria, o Multiple Spanning Tree (MST), com o qual você pode
31:18
criar múltiplas instâncias de spanning tree e agrupar várias VLANs dentro de cada instância.
31:25
Não existe uma versão Cisco do MSTP; os switches Cisco executam o protocolo padrão da indústria.
31:32
Depois, analisamos o Rapid PVST+, mas, na verdade, todas as informações que vimos também se aplicam ao RSTP, que é o padrão da indústria.
31:40
O RSTP é uma evolução do STP clássico. Em vez de usar temporizadores, ele utiliza um processo de negociação para permitir a rápida transição das
31:51
portas necessárias para o estado de encaminhamento e o ajuste rápido a mudanças na topologia da rede. 31:56
Não mencionei detalhes específicos do processo de negociação; esse nível de profundidade não é necessário
32:03
para o CCNA. Falei sobre os estados de porta no RSTP; existem apenas três.
32:10
Discarding (Descarte), Learning (Aprendizado) e Forwarding (Encaminhamento). O estado "Listening" (Escuta) foi considerado desnecessário e, de fato, o estado "Learning" é frequentemente ignorado
32:19
devido aos recursos nativos do Rapid STP, como UplinkFast e BackboneFast.
32:26
Falamos sobre as funções de porta no RSTP; existem quatro. As portas Root (Raiz) e Designated (Designada) são as mesmas, mas o RSTP distingue dois tipos de portas
32:35
no estado de descarte (discarding). Portas Alternate (Alternativas) são portas em descarte que recebem um BPDU superior de outro switch;
32:43
esse é o caso mais comum. Já as portas Backup recebem um BPDU superior de uma interface no mesmo
32:51
switch. Isso só ocorre se houver conexão com um hub — uma situação que você provavelmente nunca encontrará,
32:58
pois hubs não são mais utilizados. Também mencionei alguns recursos opcionais do STP clássico que foram incorporados ao RSTP.
33:08
Primeiro, mostrei o UplinkFast e o BackboneFast, mas o PortFast também está integrado, por meio da
33:13
função de porta de borda (edge ​​port). Embora você precise conhecer o PortFast para o CCNA, não é necessário ter um entendimento detalhado
33:20
sobre UplinkFast e BackboneFast. Mostrei brevemente o BPDU do RSTP; lembre-se apenas de que a versão do protocolo em um BPDU RSTP
33:30
é 2, enquanto no STP clássico é 0. Lembre-se também do ponto importante de que, no RSTP, TODOS os switches enviam BPDUs, e não apenas o
33:41
root bridge (ponte raiz). Por fim, mostrei os tipos de link do RSTP.
33:47
Portas de borda (edge ​​ports) são conectadas a hosts finais, e você configura uma porta de borda habilitando...


ng portfast
33:52
na interface. Ponto a ponto significa que está conectado diretamente a outro switch, e compartilhado significa que está
34:00
conectado a um hub e deve usar half-duplex. Como eu disse antes, hubs não são muito usados ​​hoje em dia, então você provavelmente não verá um link 'compartilhado'
34:0
em nenhuma rede real. 



