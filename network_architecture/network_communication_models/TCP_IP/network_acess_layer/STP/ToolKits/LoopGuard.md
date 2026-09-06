
Neste vídeo, abordaremos mais um recurso do conjunto de ferramentas do STP: o Loop Guard, que basicamente atua como uma linha de defesa adicional contra loops de Camada 2. 

Ora, o objetivo principal do Spanning Tree Protocol é justamente evitar loops — é por isso que o utilizamos —, então, qual é o papel do Loop Guard?

Bem, é isso que veremos neste vídeo.

Tópicos que abordaremos

Nos vídeos anteriores, cobrimos estes quatro recursos do conjunto de ferramentas do STP: PortFast, BPDU Guard, BPDU Filter e Root Guard. Agora, passamos para o Loop Guard, que protege a rede contra loops ao desativar uma porta caso ela pare inesperadamente de receber BPDUs, garantindo que ela não entre erroneamente no estado de encaminhamento (Forwarding).

Existem algumas situações em que isso pode ocorrer, como um erro de software em um switch que o impeça de enviar BPDUs. Mas, neste vídeo, analisaremos um cenário específico: o link unidirecional.

## Links unidirecionais

Então, temos estes dois switches, SW1 e SW2, e vamos conectá-los. Em circunstâncias normais, trata-se de um link bidirecional, o que significa que o SW1 pode transmitir dados para o SW2, e o SW2 pode transmitir dados para o SW1.

No entanto, um link unidirecional é um link de rede onde a transmissão de dados ocorre em apenas uma direção. Por exemplo, o SW1 pode enviar quadros para o SW2, mas o SW2 não consegue enviar quadros para o SW1.

Essa, obviamente, não é uma situação desejável e geralmente é causada por um problema de Camada 1, alguma falha física no hardware que impede o fluxo de dados em uma das direções. 

Por exemplo, cabos danificados podem causar isso, ou conectores ou transceptores defeituosos, como os SFP — *small form-factor pluggable* (transceptores de formato compacto conectáveis) usados ​​para conexões de fibra óptica.

Na verdade, links unidirecionais são mais comuns em cabos de fibra óptica do que em cabos de cobre UTP. Por que isso acontece?

Vamos ver. Como vimos no início do curso, conexões de fibra óptica normalmente usam duas fibras separadas, como alterei o diagrama acima para mostrar. O lado Tx (transmissão) do SW1 conecta-se ao lado Rx (recepção) do SW2. E o lado Tx do SW2 conecta-se ao lado Rx do SW1. 

Embora sejam fibras separadas, essas duas fibras são consideradas um único cabo, conectando uma interface no SW1 a uma interface no SW2 e permitindo que ambos enviem e recebam dados.

O problema é que, se uma fibra for danificada, isso pode interromper o fluxo de dados em uma direção, enquanto a outra permanece inalterada. Além disso, cabos de fibra óptica são simplesmente mais vulneráveis ​​a danos físicos do que cabos de cobre UTP. 

Se você dobrar demais um cabo de fibra, ouvirá um pequeno estalo e o cabo estará inutilizado: você não conseguirá mais usá-lo.

Agora, para que uma interface de fibra óptica esteja no estado *up/up* (ativa/ativa), ambas as fibras devem estar conectadas e funcionais.

Por exemplo, veja esta conexão entre dois switches. Eles estão conectados por um cabo de fibra óptica e as duas fibras estão conectadas em ambas as extremidades, portanto, as luzes de link estão verdes. Então, é assim que se apresenta uma conexão de fibra óptica funcional.

Se houver um problema com qualquer uma das fibras, os dispositivos devem ser capazes de detectá-lo e desativar suas interfaces. Então, se você desconectar ou cortar essa fibra, o SW1 e o SW2 devem detectar isso e desabilitar suas interfaces. 

Isso não resulta em um link unidirecional – o link é totalmente desabilitado. Vamos dar uma olhada nessa conexão novamente. Com uma fibra desconectada, as luzes de link agora estão apagadas. E, após danificar a fibra, mesmo que eu a conecte, as luzes de link permanecem apagadas.

Mas nem todos os problemas físicos que impedem a comunicação serão detectados. E se os dispositivos não detectarem o problema físico, isso pode resultar em um link unidirecional. 

Se houver um problema em uma dessas fibras que impeça a transmissão de dados, mas os dispositivos não o detectarem, suas interfaces permanecerão no estado "up/up" e, agora, temos um link unidirecional. O SW1 pode transmitir dados para o SW2, mas os dados que o SW2 transmite não conseguem chegar ao SW1.

Ambos acham que a conexão está ativa e funcionando, mas, na verdade, ela só funciona em uma direção.

## Loop Guard – o problema

Então, qual é o problema de um link unidirecional? Antes de abordarmos o Loop Guard, vamos ver o problema que ele resolve. O Loop Guard não evita links unidirecionais, mas pode proteger contra o efeito negativo que um link unidirecional causa no STP. 

Como você já sabe, os BPDUs se originam da Root Bridge e são encaminhados a partir de portas designadas, como esta, a cada 2 segundos. E é por meio desses BPDUs que os switches compartilham informações entre si para determinar a topologia STP, quais interfaces devem estar encaminhando tráfego e quais devem estar bloqueando.

Nesta rede, a interface G0/1 do SW3 é uma porta de bloqueio não designada porque recebe BPDUs superiores do SW2. Para manter o diagrama simples, não incluí detalhes, mas isso ocorre ou porque SW2 possui um custo de raiz ou um Bridge ID superior em relação ao SW3.

Mas, se o link entre SW2 e SW3 se tornar unidirecional e os BPDUs do SW2 não conseguirem chegar ao SW3, o que acontecerá? 

Vamos supor que exista um problema físico que impeça os quadros do SW2 de chegar ao SW3, mas que não faça com que os switches realmente desabilitem suas interfaces G0/1; os switches não detectam o problema físico subjacente. 

O SW3, que não recebe mais BPDUs do SW2, presumirá que não há mais loop na LAN. Após o vencimento do temporizador *max age*, a interface G0/1 do SW3 se tornará uma porta designada e começará a encaminhar BPDUs para o SW2. 

E, como os BPDUs do SW3 são inferiores aos do SW2, o SW2 simplesmente ignora os BPDUs do SW3. Assim, as interfaces G0/1 do SW2 e do SW3 ficam ambas no estado de encaminhamento (*forwarding*), o que significa que temos um loop de SW1 para SW3 e para SW2.

Vamos ver como esse loop funciona. Se o SW1 receber um quadro de broadcast em uma de suas outras interfaces, ele fará o *flood* (encaminhamento para todas as portas) do quadro em direção ao SW2 e ao SW3. O quadro enviado ao SW2 não causará loop devido ao link unidirecional; os quadros do SW2 não conseguem chegar ao SW3.

Mas o quadro enviado ao SW3 circulará pelos três switches desta forma. Cada switch que o receber fará o *flood* repetidamente. Portanto, esse é o problema de um link unidirecional em uma LAN que utiliza STP.

A interface G0/1 do SW3 para de receber BPDUs, acha que deve se tornar uma porta designada e começar a encaminhar quadros, e então causa um loop. Seria melhor se o problema de hardware fizesse com que o link caísse completamente. 

Nesse caso, tanto o SW2 quanto o SW3 desabilitariam suas portas G0/1, e não haveria loop. Mas como podemos lidar com uma situação como essa, em que um problema de hardware causa um link unidirecional? Você acertou: a resposta é o Loop Guard.

## Loop Guard – a solução

Então, finalmente, vamos ver como o Loop Guard resolve esse problema. Como eu disse antes, o Loop Guard não evita links físicos unidirecionais, mas fornece um mecanismo para detectar links unidirecionais e, assim, impedir loops de Camada 2.

Quando o temporizador *max age* de uma porta com Loop Guard habilitado chega a zero, ela não se torna uma porta designada nem começa a transição para o estado de encaminhamento (*forwarding*). Em vez disso, ela entra no estado *broken* (inconsistência de loop).

Isso provavelmente lhe soa familiar. Assim como o estado *broken* (inconsistência de raiz) acionado por uma violação de Root Guard, isso bloqueia a porta. 

Note que, em ambos os casos, seja com Root Guard ou Loop Guard, as portas permanecem no estado *up/up*. Portanto, a porta não é realmente desativada; é apenas o STP que a bloqueia. 

Então, digamos que o Loop Guard esteja habilitado na porta G0/1 do SW3, e o link SW2-SW3 seja unidirecional, impedindo que os quadros do SW2 cheguem ao SW3. O temporizador *max age* na porta G0/1 do SW3 começa a contagem regressiva. 

Normalmente, quando chega a zero, ela se tornaria uma porta designada e começaria a transição para o estado de encaminhamento. Mas, quando o Loop Guard está habilitado, ela entra no estado *broken*, impedindo a ocorrência de um loop de Camada 2. 

E, assim como no Root Guard, a recuperação é automática. Se o problema físico for resolvido e a porta bloqueada voltar a receber BPDUs, ela será reativada automaticamente. Então, como podemos configurar o Loop Guard? 

Assim como os outros recursos do conjunto de ferramentas do STP, as configurações em si são simples. Ele pode ser ativado de duas maneiras.

- A primeira é por porta, usando `spanning-tree guard loop` no modo de configuração de interface.

- A segunda é como padrão, no modo de configuração global, com `spanning-tree loopguard default`. Isso ativa o Loop Guard em todas as portas por padrão. E então você pode usar `spanning-tree guard none` no modo de configuração de interface para desativá-lo em portas específicas, se necessário.

O Loop Guard deve, normalmente, ser ativado em quaisquer portas que não sejam designadas: portas raiz e portas não designadas. Em outras palavras, portas que devem receber BPDUs de portas designadas.

Assim, se elas pararem de receber BPDUs, o Loop Guard as desativará para evitar loops.

## Loop Guard: demonstração na CLI

Agora, vamos ver o Loop Guard na CLI. Eu ativei o Loop Guard na porta G0/1 do SW3 com o comando `spanning-tree guard loop`. Na saída do comando `show spanning-tree interface detail`, aparece a mensagem "Loop guard is enabled on the port" (Loop guard está ativado na porta). Então, é isso; basta apenas esse comando para ativar o Loop Guard em uma porta.

Mas, antes de vê-lo em ação, vamos ver também como ele aparece quando ativado por padrão. Então, desta vez, em vez de ativá-lo no modo de configuração de interface, usei `spanning-tree loopguar default` para ativá-lo no modo de configuração global. Então, a saída deste comando é basicamente a mesma, mas diz "by default" (por padrão) no final.

Certo, agora vamos ver o que acontece quando o Loop Guard bloqueia uma porta. Atualmente, todos os links estão operacionais e a porta G0/1 do SW3 está recebendo BPDUs do SW2.

Mas e se o link que os conecta se tornar unidirecional? Bem, esta mensagem é exibida na CLI: Loop guard blocking port GigabitEthernet0/1. E na saída do comando SHOW SPANNING-TREE, o status da G0/1 é BKN, e também aparece LOOP_Inc.

Como você provavelmente imaginou, BKN significa *broken* (quebrado) e LOOP_Inc significa *Loop Inconsistent* (loop inconsistente). A porta é bloqueada porque parou de receber BPDUs.

Talvez haja uma dobra acentuada em uma das fibras que degradou o sinal, impedindo que os BPDUs do SW2 chegassem ao SW3.

Mas então, talvez alguém ajuste o cabo e os dados voltem a fluir, e o Loop Guard desbloqueia automaticamente a porta, pois ela volta a receber BPDUs do SW2. Como você pode ver aqui, o status da G0/1 agora é *blocking* (bloqueando), não *broken*, e não aparece mais *Loop Inconsistent*.

Portanto, assim como o Root Guard, o Loop Guard reativa automaticamente uma porta se o problema for resolvido; você não precisa executar nenhum comando para reativar a porta.

## Loop Guard e Root Guard

Adicionei outro switch a esta LAN, um que não é o seu; você não tem controle direto sobre a configuração dele. Antes de encerrarmos este vídeo, deixe-me destacar algo sobre o Loop Guard e o Root Guard. 

Esses dois recursos são mutuamente exclusivos; isso significa que não podem ser habilitados na mesma porta ao mesmo tempo. E isso acontece porque eles basicamente servem a propósitos opostos. 

O Root Guard serve para impedir que portas designadas se tornem portas raiz (*root ports*). Se uma porta designada com Root Guard habilitado começar a receber BPDUs superiores, ela será bloqueada. Já o Loop Guard serve para impedir que portas não designadas ou portas raiz se tornem portas designadas. 

Se uma porta com Loop Guard habilitado parar de receber BPDUs, ela será bloqueada. Então, observando o SW3 na rede acima, as portas G0/0 e G0/1 devem usar o Loop Guard, e a G0/2 deve usar o Root Guard. Não faria sentido configurar o oposto. 

Por exemplo, no SW3, as portas G0/0 e G0/1 devem receber BPDUs do SW1 e do SW2. Se você configurar o Root Guard nelas, ambas serão bloqueadas, interrompendo a comunicação na LAN. Certo, então lembre-se de que não se pode habilitar ambos em uma interface ao mesmo tempo.

Como isso afeta as configurações? Se o Loop Guard estiver configurado em uma porta, com o comando `spanning-tree guard loop`, e você então configurar o Root Guard, com o comando `spanning-tree guard root`, o Loop Guard será desabilitado na porta. O comando Root Guard irá substituí-lo. E vice-versa. 

Se o Root Guard estiver habilitado em uma porta e você então configurar o Loop Guard, o Root Guard será desabilitado. 

E se o Loop Guard estiver habilitado por padrão, no modo de configuração global, e você então configurar o Root Guard em uma porta, o Loop Guard será desabilitado nessa porta. Em outras palavras, a configuração mais específica prevalece. O comando de interface se aplica apenas a uma interface; ele é mais específico do que o comando global, portanto, o comando de interface entra em vigor. 

Isso vale para muitos recursos no IOS. Por exemplo, o mesmo ocorre com PortFast, BPDU Guard e BPDU Filter. Se você habilitar o PortFast por padrão no modo de configuração global, mas depois o desabilitar em uma interface específica, o comando de interface prevalece. 

Lembre-se disso sobre os comandos do IOS. Normalmente, o comando mais específico prevalece sobre o comando menos específico.

## Resumo

Certo, vamos resumir o Loop Guard. O objetivo dele é proteger a rede bloqueando uma porta caso ela pare inesperadamente de receber BPDUs. Isso pode acontecer se, por exemplo, houver um erro de software impedindo um switch de enviar BPDUs. Ou se houver um problema de hardware causando um link unidirecional. 

Um link unidirecional é um link de rede onde a transmissão de dados ocorre em apenas uma direção. Um link normal deve ser bidirecional, permitindo a comunicação em ambas as direções.

Um link unidirecional é tipicamente causado por problemas de Camada 1 em cabos de fibra óptica; esse é o cenário mais comum. Se os dispositivos conectados não detectarem o problema e desativarem suas interfaces, isso pode resultar em um link unidirecional.

Isso impede que os BPDUs cheguem ao switch vizinho. E se uma porta raiz ou não designada parar de receber BPDUs, ela se tornará uma porta designada, podendo causar um loop de Camada 2. O papel do Loop Guard é proteger contra isso. 

Se uma porta com Loop Guard ativado parar de receber BPDUs, ela entra no estado de erro "loop inconsistent" (inconsistência de loop), desativando efetivamente a porta. Mas se ela voltar a receber BPDUs, será automaticamente reativada.

Existem duas formas de configurá-lo. A primeira é por porta, com o comando SPANNING-TREE GUARD LOOP no modo de configuração de interface. 

A segunda é como padrão, com SPANNING-TREE LOOPGUARD DEFAULT no modo de configuração global. Isso o ativa em todas as portas, mas você pode usar SPANNING-TREE GUARD NONE para desativá-lo em portas específicas, se necessário. 

É semelhante a habilitar o PortFast, o BPDU Guard ou o BPDU Filter por padrão e, em seguida, desabilitá-los em portas individuais. Um último ponto: o Loop Guard e o Root Guard são mutuamente exclusivos, portanto, não podem ser ativados na mesma porta ao mesmo tempo. 

Portanto, se o Loop Guard estiver configurado em uma porta e você configurar o Root Guard, o Loop Guard será desativado, e vice-versa.

E se o Loop Guard estiver habilitado por padrão e você configurar o Root Guard em uma porta, o Loop Guard será desativado nessa porta. Apenas um deles pode estar ativo por vez em cada porta. Certo?
