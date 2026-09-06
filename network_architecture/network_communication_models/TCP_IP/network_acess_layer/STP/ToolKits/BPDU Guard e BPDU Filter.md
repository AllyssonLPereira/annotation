
Antes de apresentar o BPDU Guard e o Filter, vamos ver como uma porta com PortFast habilitado lida com BPDUs de STP.

O PortFast faz com que uma porta inicie no estado de encaminhamento (Forwarding) quando conectada, mas não desativa o STP na porta. Portanto, a porta G0/1 deste switch tem o PortFast ativado e envia BPDUs a cada 2 segundos, como uma porta STP comum. 

O PC, que não executa STP, ignora os BPDUs, mas a porta G0/1 continua enviando-os. 

Usei o comando `SHOW SPANNING-TREE INTERFACE G0/1 DETAIL`, o mesmo que mostrei algumas vezes no vídeo anterior. Como destacado, o PortFast está habilitado na G0/1, e ela enviou 77 BPDUs até agora, mas recebeu 0 do PC. 

Como hosts finais não executam STP nem enviam BPDUs, uma porta com PortFast habilitado não deveria receber BPDUs. Mas eis a questão: e se receber? Talvez um usuário traga seu próprio switch para o trabalho e o conecte à rede. 

O que acontece então? Vamos ver. 

Em vez de um PC, a porta G0/1 do SW1 agora está conectada a outro switch, o SW2. Como você sabe, quando um switch entra em operação, ele assume que é a *root bridge* (ponte raiz) e envia seus próprios BPDUs. 

Então, o que o SW1 faz ao receber um BPDU do SW2? Se uma porta com PortFast habilitado recebe um BPDU de STP, ela passa a agir como uma porta STP comum, sem o PortFast. 

Digamos que a prioridade do SW1 seja 32768, e a do SW2 seja 4096. Como o SW2 tem uma prioridade menor — e, portanto, um *bridge ID* menor —, o SW2 torna-se a *root bridge*, e a porta G0/1 do SW1 torna-se uma porta raiz (*root port*). Então, qual é o problema aqui?

## BPDU Guard – o problema

Vamos voltar um pouco. Aqui temos uma LAN simples com três switches. O SW1 é a *root bridge*, com todas as portas designadas. Os switches SW2 e SW3 possuem, cada um, uma porta raiz voltada para o SW1, e o link entre SW2 e SW3 está bloqueado.

Bob, do departamento de contabilidade, é um usuário no escritório. Normalmente, os usuários não se conectam diretamente a um switch. Em vez disso, há um ponto de rede na parede próximo ao usuário, como na parede de sua sala, caso ele tenha uma sala própria. 

O switch se conecta a esse ponto de rede, assim como o dispositivo do usuário. Essa é uma configuração bastante comum. Mas digamos que Bob esteja cansado de ir até a impressora e decida trazer sua própria impressora para o trabalho.

E talvez o Wi-Fi esteja lento, então ele queira conectar seu notebook à rede cabeada em vez de usar o Wi-Fi. Mas o ponto de rede em sua sala tem apenas uma porta. Então, o que ele faz?

Em vez de seguir o procedimento e abrir um chamado no departamento de TI, Bob resolve agir por conta própria. Ele traz um switch antigo que tinha em casa para o trabalho e o conecta à rede. Depois, ele conecta seus dispositivos ao seu switch, e todos conseguem acessar a LAN.

Problema resolvido, certo? Bem, talvez o problema do Bob tenha sido resolvido, mas o switch dele e o SW3 começam a trocar BPDUs do Spanning Tree, e isso pode afetar a rede. 

Por exemplo, e se o switch do Bob se tornar a *root bridge* (ponte raiz)? Se o switch do Bob tiver um Bridge ID de STP menor e se tornar a *root bridge*, isso pode afetar o restante da topologia STP. 

Agora, a porta raiz de cada switch aponta para o switch do Bob, e o link SW1-SW2 fica bloqueado. Isso é um problema: não queremos que o switch de um usuário afete a topologia STP. 

Por exemplo, talvez o SW1 fosse a *root bridge* por estar conectado ao roteador da LAN. Ao definir o SW1 como *root bridge*, garantimos que todos os outros switches tenham um caminho eficiente para chegar ao SW1 e, consequentemente, ao roteador. 

Mas agora, o caminho mais eficiente do SW2 está bloqueado, e os quadros provenientes de hosts conectados ao SW2 precisam seguir pelo caminho menos eficiente, passando pelo SW3. 

Isso não é um desastre, mas, de qualquer forma, não queremos que dispositivos de usuários não autorizados afetem negativamente a rede. Vamos resumir e então veja como o BPDU Guard resolve esse problema.

O PortFast deve ser habilitado apenas em portas conectadas a dispositivos que não sejam switches, como hosts finais ou roteadores. E esses dispositivos não enviam BPDUs.

No entanto, uma porta com PortFast habilitado ainda envia BPDUs e operará como uma porta STP comum se receber BPDUs de um vizinho. Portanto, se um usuário final conectar descuidadamente um switch a uma porta destinada a hosts finais — como o Bob, da Contabilidade —, isso poderá afetar a topologia STP. Que feio, Bob. Melhore. 

Mas, felizmente, o BPDU Guard atua como uma proteção contra essa situação.

## BPDU Guard – a solução

Vamos ver como o BPDU Guard funciona. 

O BPDU Guard protege a rede contra a conexão de switches não autorizados a portas destinadas a hosts finais, como a porta G0/1 do SW3 neste exemplo. O BPDU Guard pode ser configurado independentemente do PortFast, mas ambos os recursos geralmente são usados ​​em conjunto, pois ambos aprimoram a funcionalidade do STP em portas destinadas a hosts finais. 

Então, o que exatamente o BPDU Guard faz? Uma porta com BPDU Guard habilitado continua enviando BPDUs, mas, se receber um BPDU, entra no estado *error-disabled* (desativada por erro). 

Assim, se o Bob conectar seu switch à tomada de rede e ele enviar um BPDU para o SW3, o SW3 colocará sua porta G0/1 em estado de erro (*error-disable*). Na prática, isso desativa a porta. Ela não consegue mais enviar ou receber dados ou BPDUs.

Isso impede que o switch do Bob afete a topologia STP; o Bob vai pensar "a internet não funciona" e vir reclamar com o departamento de TI. Missão cumprida.

## Configuração do BPDU Guard

Vamos ver como configurar o BPDU Guard. Assim como o PortFast, ele pode ser configurado de duas maneiras. 

Primeiro, pode ser configurado por porta, no modo de configuração de interface. O comando para isso é `spanning-tree bpduguard enable`. E aqui está a saída do comando `show spanning-tree interface detail` para a G0/1.

Como destaquei, o BPDU Guard está habilitado. Certo, então você pode configurar o BPDU Guard em cada porta individual, ou pode habilitá-lo por padrão no modo de configuração global. 

O comando para isso é `spanning-tree portfast bpduguard default`. E note que, no Cisco IOS moderno, você pode adicionar opcionalmente a palavra-chave `edge` ao configurá-lo.

De qualquer forma, o dispositivo adicionará automaticamente a palavra-chave à configuração, como vimos no vídeo sobre PortFast. Aqui está aquele mesmo comando `show`, mostrando que o BPDU Guard está habilitado por padrão. 

Agora, quando você habilita o PortFast por padrão, ele é ativado em todas as portas de acesso. Mas o BPDU Guard funciona de forma um pouco diferente. Quando você habilita o BPDU Guard por padrão, ele é ativado em todas as portas com PortFast habilitado. Não necessariamente em todas as portas de acesso.

Lembre-se dessa diferença – pontos como esse certamente podem ser cobrados no exame CCNA.

Mas, assim como o PortFast, depois de habilitar o BPDU Guard por padrão, você pode desabilitá-lo em portas específicas, se quiser: o comando é `spanning-tree bpduguard disable` no modo de configuração de interface. 

Certo, é assim que se configura o BPDU Guard. Use o método que for mais adequado para você, mas certifique-se de não habilitá-lo em uma porta que deva estar conectada a outro switch, pois isso desabilitará a porta. 

## ErrDisable

Continuando com o tópico de desativação da porta, vamos ver como isso funciona.

A porta do SW3 com BPDU Guard habilitado recebeu um BPDU do switch do Bob; portanto, ela entrou em estado de erro (*err-disabled*). 

Na CLI do SW3, você verá esta mensagem aparecer: "Received BPDU on port GigabitEthernet0/1 with BPDU Guard enabled. Disabling port" (BPDU recebido na porta GigabitEthernet0/1 com BPDU Guard habilitado. Desativando porta). 

E outra mensagem semelhante: "bpduguard error detected on G0/1, putting G0/1 in err-disable state" (erro de bpduguard detectado na G0/1, colocando a G0/1 em estado err-disable).

E, em seguida, essas duas mensagens informando que o status da interface mudou para *down* e *down*. Na saída do comando `SHOW INTERFACES G0/1`, você pode ver que a interface entrou em estado *err-disabled*. 

O ErrDisable é um recurso de switches Cisco que desativa uma porta sob certas condições, como uma violação do BPDU Guard.

Se uma porta com BPDU Guard habilitado recebe um BPDU, isso constitui uma violação, e a porta é desativada. Você aprenderá alguns outros exemplos para o exame CCNA, como violações de *power policing*, violações de *Port Security* e DAI, violações de inspeção dinâmica de ARP (*Dynamic ARP Inspection*). 

Mas esses são tópicos para mais adiante no curso. Vamos ver o BPDU Guard em ação em um switch Cisco.

Configurei o PortFast e o BPDU Guard na porta 1, à esquerda do switch superior. Abaixo dele há outro switch Cisco; então, vamos conectá-los.

Desconectar o cabo do switch não resolve o problema de uma porta em estado de *err-disabled*. Então, vamos ver como reativá-la. para que a porta possa ser usada novamente. 

Primeiramente, para reativar uma porta em estado *err-disabled*, você deve primeiro resolver o problema subjacente. Isso é fundamental, porque se você reativar a porta sem corrigir o problema, ela simplesmente entrará em estado *err-disabled* novamente. 

Neste exemplo, se eu reativar a porta G0/1 do SW3, ela receberá outro BPDU do switch do Bob e será desativada novamente de imediato. Então, vamos desconectar o switch do Bob da tomada de rede na parede.

E, em seguida, reconectar o PC do Bob. Agora, vamos ver como reativar a porta que está em estado *err-disabled*. 

Existem duas maneiras de reativar uma porta que entrou nesse estado: a primeira é manual, usando os comandos `SHUTDOWN` e `NO SHUTDOWN` para reiniciar a porta desativada. 

A segunda é automática, usando um recurso chamado *ErrDisable Recovery*. Vamos ver como ele funciona.

### ErrDisable Recovery

O ErrDisable Recovery é um recurso que reativa automaticamente portas em estado *err-disabled* após um determinado período de tempo. Para visualizar o status do ErrDisable Recovery no switch, use o comando `SHOW ERRDISABLE RECOVERY`. Aqui está a saída do comando. 

No topo, há uma lista de "motivos para *err-disable*" e seus status. A lista é bem longa, então omiti a maior parte dela, mas, como destaquei, o BPDU Guard é o segundo da lista. E, como indicado, o ErrDisable Recovery vem desativado por padrão. 

Isso significa que portas em estado *err-disabled* não se recuperarão automaticamente por padrão; você precisa ativar o ErrDisable Recovery se quiser utilizá-lo. 

Como destaquei em rosa, o temporizador de recuperação padrão é de 300 segundos, ou seja, 5 minutos. Isso significa que as portas em estado *err-disabled* serão reativadas automaticamente após 5 minutos se você habilitar a recuperação *errdisable*. 

Você pode modificar esse intervalo, se quiser, usando o comando `errdisable recovery interval` seguido pelo tempo em segundos. Mas, mesmo que você altere o intervalo, ainda precisa habilitar a recuperação *ErrDisable* para que ela funcione; então, vamos fazer isso.

Use `errdisable recovery cause`, seguido pela causa, para habilitá-la para portas desativadas por uma causa específica. A "causa" é o recurso que desativou as portas. 

Neste vídeo, estamos falando sobre o BPDU Guard, mas, como mencionei anteriormente, abordaremos outras causas mais adiante no curso. Por exemplo, se você olhar para o topo da lista "ErrDisable Reason" na saída acima, o primeiro item é "arp-inspection", referindo-se a DAI (*Dynamic ARP Inspection*), outro tópico do CCNA. 

Para habilitá-lo para o BPDU Guard, use `errdisable recovery cause bpduguard`, como fiz aqui. Desta vez, o comando `show errdisable recovery` mostra que o recurso está habilitado para o BPDU Guard.

E a porta G0/1 aparece na parte inferior da saída, o que significa que ela será reativada automaticamente após 296 segundos. Quando a contagem regressiva chegar a zero, a interface será reativada.

Um último ponto: mesmo que você use a recuperação *ErrDisable* para reativar automaticamente portas desativadas, ainda é necessário resolver o problema subjacente, como mencionei anteriormente.

No nosso cenário, se o switch do Bob ainda estiver conectado à porta G0/1, logo após o recurso de recuperação de ErrDisable reativar a porta, ela será desativada novamente assim que receber um BPDU.

---
## BPDU Filter – o problema

Certo, já abordamos o BPDU Guard; agora vamos passar para o BPDU Filter. Antes de vermos como ele funciona, vamos analisar o problema que ele resolve. 

Uma porta de switch conectada a um dispositivo final continua enviando BPDUs a cada 2 segundos. E isso acontece independentemente de o PortFast e o BPDU Guard estarem habilitados. 

Portanto, mesmo que o PC do Bob não execute o Spanning Tree e simplesmente ignore quaisquer BPDUs, o SW3 continua enviando BPDUs para o PC do Bob, uma vez a cada 2 segundos. Se a porta não estiver conectada a um switch, o envio de BPDUs é desnecessário e também indesejável, por alguns motivos.

- O primeiro é que o envio de BPDUs consome largura de banda e poder de processamento do switch, embora isso seja mínimo. Não é algo crítico, mas ainda assim é desnecessário.

- O segundo motivo é que os BPDUs contêm informações sobre a topologia STP da LAN. E, se a segurança máxima for uma preocupação, você deve evitar enviar essas informações para dispositivos de usuários. 

O BPDU Filter resolve isso impedindo que a porta envie BPDUs.

## BPDU Filter – a solução

Vamos explorar como o BPDU Filter funciona. Como acabei de mencionar, ele impede que a porta envie BPDUs. Assim, se você o habilitar na porta G0/1 do SW3, ela não enviará mais BPDUs para o PC do Bob. 

Mas, ao contrário do BPDU Guard, o BPDU Filter não desativa a porta caso ela receba um BPDU. A forma como o switch reage ao receber um BPDU depende de como você configura o BPDU Filter; então, vamos ver como fazer isso. 

O BPDU Filter pode ser habilitado de duas maneiras, assim como o PortFast e o BPDU Guard: pode ser configurado por porta no modo de configuração de interface ou globalmente, no modo de configuração global.

No entanto, ao contrário do PortFast e do BPDU Guard, o BPDU Filter funciona de maneira diferente dependendo de como é configurado.

Para configurá-lo em uma porta específica, utilize o comando `spanning-tree bpdufilter enable` na configuração da interface.

Com o BPDU Filter habilitado, a porta não enviará BPDUs. Além disso, a porta ignorará quaisquer BPDUs que receber.
Basicamente, isso desativa o STP na porta e, por esse motivo, você deve usá-lo com cautela.

O PortFast habilitado na porta errada pode causar loops temporários de Camada 2. Mas o BPDU
Filter habilitado na porta errada pode causar loops permanentes de Camada 2, sendo uma ótima maneira
de provocar uma tempestade de broadcast e derrubar a rede.

O STP é um protocolo fundamental para evitar
loops; portanto, desativá-lo em uma porta pode ser muito arriscado. Uma escolha melhor é habilitar o BPDU Filter
por padrão no modo de configuração global. 

O comando é `spanning-tree portfast bpdufilter default`. E, novamente, você pode usar opcionalmente a palavra-chave `edge` após `portfast`. Assim como ao habilitar o BPDU Guard por padrão, o BPDU Filter será ativado em todas as portas com PortFast habilitado.

E então você pode usar `spanning-tree bpdufilter disable` para desativá-lo em portas específicas, se necessário.

Quando o BPDU Filter é ativado em uma porta por padrão, a porta não envia BPDUs, assim como mencionado anteriormente. Mas aqui está a diferença: se a porta receber um BPDU, o PortFast e o BPDU Filter são desativados, e ela opera como uma porta STP normal. 

É o melhor dos dois mundos. Em circunstâncias normais, a porta não envia BPDUs, mas, se receber BPDUs, ela consegue reagir adequadamente — não os ignora simplesmente.

Antes de encerrarmos, deixe-me apresentar minha recomendação e uma observação final sobre
o BPDU Guard e o BPDU Filter. 

Você pode habilitar o PortFast e o BPDU Guard da maneira que preferir, seja por porta ou globalmente (por padrão). Isso não afeta o funcionamento deles. Independentemente de como você os configure, apenas certifique-se de habilitá-los nas interfaces corretas. 

Mas recomendo habilitar o BPDU Filter apenas globalmente, no modo de configuração global, a menos que você tenha um motivo muito bom para habilitá-lo por porta. 

Desabilitar o STP em uma porta é arriscado. 

Certo, uma última observação sobre o BPDU Guard e o BPDU Filter: eles podem ser habilitados na mesma porta simultaneamente, mas o resultado final depende de como você configurou o BPDU Filter. 

Se o BPDU Filter estiver habilitado no modo de configuração global, ou seja, habilitado por padrão, e a porta receber um BPDU, o BPDU Filter será desabilitado, e o BPDU Guard será acionado, colocando a interface em estado de *err-disable*. 

Mas e se o BPDU Filter estiver habilitado no modo de configuração de interface — ou seja, habilitado por porta — e a porta receber um BPDU? Nesse caso, o BPDU será ignorado e o BPDU Guard não será acionado.

Basicamente, o BPDU Guard não tem efeito algum nessa situação. 

Portanto, mais uma vez, acho melhor ativar o BPDU Filter no modo de configuração global, em vez do modo de configuração de interface.