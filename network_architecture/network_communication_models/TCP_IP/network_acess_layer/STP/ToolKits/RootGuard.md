
Desta vez, o foco é o Root Guard. Como o nome sugere, o Root Guard protege a *root bridge* (ponte raiz) da LAN, garantindo que outro switch com um Bridge ID menor não assuma essa função. Ele é normalmente utilizado ao conectar seus switches a switches de terceiros sobre os quais você não tem controle direto. 

Por exemplo, se um provedor de serviços conecta seus switches à rede de um cliente, o provedor pode querer garantir que a *root bridge* permaneça na rede do próprio provedor. E o Root Guard pode ajudar nisso.

O Root Guard impede que uma porta se torne uma root port (porta raiz), desativando-a caso receba BPDUs superiores, garantindo assim a manutenção da *root bridge* atual. Como mencionei na introdução, isso pode ser muito útil ao conectar sua LAN a outra LAN sobre a qual você não tem controle direto. 

Então, por que é importante garantir que um switch específico permaneça como a *root bridge*? Antes de analisarmos o Root Guard, vamos ver por que ele é importante.

Como você sabe, o STP evita loops elegendo uma bridge raiz — o SW1 na rede acima — e garantindo que cada um dos outros switches tenha apenas um caminho válido para alcançá-la. Nesta rede, o SW2 tem um caminho ativo para chegar ao SW1: a conexão direta entre o SW2 e o SW1. O mesmo vale para o SW3; apenas seu link direto com o SW1 está ativo. 

O link entre o SW2 e o SW3 é desativado para evitar loops. Qualquer um desses três switches poderia ser a bridge raiz e o STP cumpriria seu papel de evitar loops. Mas você não deve selecionar a bridge raiz aleatoriamente.

A boa localização da bridge raiz é importante, e alguns aspectos a considerar incluem o fluxo ideal de tráfego. Por exemplo, você deve tentar minimizar a latência e o congestionamento na LAN. Latência significa apenas quanto tempo o tráfego leva para percorrer a LAN. E congestionamento refere-se ao nível de ocupação da rede. 

Se você tentar forçar a passagem de muita água por um cano pequeno de uma só vez, não será muito eficiente. O mesmo princípio se aplica às conexões de rede. 

Então, tendo isso em mente, por que selecionei o SW1 como a bridge raiz para esta LAN? Bem, na maioria das LANs como esta, os PCs — como aqueles conectados ao SW2 e ao SW3 — não se comunicam muito entre si. Geralmente, eles querem se comunicar com servidores fora da LAN: pela internet, pela rede de longa distância (WAN), etc. 

Portanto, queremos garantir que os PCs tenham um caminho eficiente para chegar ao R1, seu gateway para o mundo externo. E é por isso que selecionei o SW1 como a bridge raiz. O tráfego proveniente de hosts conectados ao SW2 utiliza o link SW2-SW1. E o tráfego proveniente de hosts conectados ao SW utiliza o link SW3-SW1. 

Esse é o caminho mais eficiente para que os quadros de cada host cheguem ao R1.

Outra consideração ao selecionar a *root bridge* (ponte raiz) é a estabilidade e a confiabilidade. Uma vez que você seleciona uma *root bridge* que oferece um caminho eficiente para o tráfego na LAN, você quer que esse switch permaneça ativo e operacional pelo maior tempo possível. 

Portanto, se você estiver usando vários tipos de switches na LAN, um dos switches mais avançados e confiáveis ​​deve ser a *root bridge*. Por exemplo, se você tiver orçamento apenas para comprar alguns switches novos, e os demais forem equipamentos velhos e obsoletos que você encontrou no armário, deve definir um dos novos switches como a raiz, pois provavelmente pode confiar que ele não falhará após algumas semanas de operação. 

Então, essas são algumas considerações ao selecionar a *root bridge*: fluxo de tráfego ideal, além de estabilidade e confiabilidade. Vamos nos concentrar no primeiro ponto e ver o que acontece se definirmos um switch diferente como a *root bridge*.

Agora, o SW3 é a *root bridge*. Qual é o problema disso? O tráfego dos hosts conectados ao SW3 segue o mesmo caminho, mas o tráfego dos hosts do SW2 agora precisa ir do SW2 para o SW3, e depois do SW3 para o SW1, antes de chegar ao R1. Isso adiciona um pouco de latência, já que os quadros estão percorrendo um caminho menos direto. 

Mas, para ser sincero, isso é insignificante na maioria dos casos: provavelmente menos de um milissegundo. O verdadeiro problema é que pode haver congestionamento no link SW3-SW1 se a rede estiver muito utilizada. Quando um link está congestionado, os quadros precisam aguardar sua vez para serem transmitidos; na pior das hipóteses, alguns quadros podem ser descartados, o que poderia afetar seriamente o desempenho da rede e a experiência do usuário. 

Ninguém gosta de uma rede lenta. Portanto, a seleção é importante e, depois de selecionarmos uma root bridge, geralmente queremos que ela permaneça estável.

## Root Guard: o problema

Vamos expandir a rede para mostrar como o Root Guard é útil. Dentro da sua própria LAN, você pode facilmente controlar a root bridge definindo sua prioridade como 0. Por exemplo, aqui está o bridge ID do SW1. A prioridade é 0, mais 1 referente ao VLAN ID. Lembre-se de que os switches Cisco executam o PVST+, então eles sempre adicionam o VLAN ID à prioridade. 

Supondo que o SW2 e o SW3 tenham a prioridade padrão, isso torna o SW1 a root bridge. E, para os três switches à direita, faremos o mesmo com o SW6, tornando-o a root bridge de sua LAN. No entanto, há casos em que você pode conectar sua LAN a outros switches que estão fora do seu controle direto. 

Por exemplo, talvez a LAN à esquerda seja controlada por um provedor de serviços e a LAN à direita seja controlada por um cliente. Este é um exemplo de situação em que switches controlados por organizações diferentes podem ser conectados. 

Um provedor de serviços oferecendo serviço Metro Ethernet a clientes. Metro Ethernet não é algo que você precise estudar para o exame CCNA, mas é frequentemente usado para conectar locais dentro de uma MAN (rede de área metropolitana), como conectar escritórios dentro da mesma cidade. 

Então, o que acontece quando o provedor de serviços e o cliente conectam suas redes neste exemplo? Bem, o SW2 e o SW3 enviarão BPDUs informando que o SW1 é a root bridge. Mas o SW4 e o SW5 também enviarão BPDUs informando que o SW6 é a root bridge. Então, quem está certo? Qual switch se torna a root bridge? 

SW1 e SW6 possuem o mesmo ID de bridge até este ponto: uma prioridade de 1 e um endereço MAC começando com 5254.001; no entanto, o próximo dígito para SW1 é "a" e o próximo dígito para SW6 é "8", portanto, o SW6 tem um ID de bridge menor. E isso significa que ele se tornará a bridge raiz. 

Assim, a lição aqui é que, mesmo que você defina a prioridade da sua bridge raiz como 0, sua função pode ser assumida por outro switch com um endereço MAC menor, como o SW6 neste caso.

Portanto, sem nenhuma medida de proteção para garantir que o SW1 permaneça como a bridge raiz, o SW1, o SW2 e o SW3 aceitam o SW6 como a bridge raiz, afetando a topologia STP do provedor de serviços. Tanto o link SW1-SW3 quanto o link SW2-SW3 são desativados. Assim, os quadros do SW3 para o SW1 precisam fazer um desvio através da LAN do cliente. 

Obviamente, esse não é um caminho de tráfego eficiente, mas o Root Guard pode ser usado para evitar uma situação como essa. O Root Guard pode ser configurado para proteger sua topologia STP, impedindo que seus switches aceitem BPDUs superiores provenientes de switches fora do seu controle.

E um BPDU superior é aquele que apresenta parâmetros melhores para o algoritmo STP. Por exemplo, um BPDU que reivindica um ID de bridge raiz melhor. Os BPDUs do SW6 reivindicam um ID de bridge raiz menor do que os do SW1; portanto, os do SW6 são superiores.

## Root Guard: a solução

Assim, se você quiser garantir que a bridge raiz permaneça em sua LAN, pode configurar o Root Guard nas portas conectadas a switches fora do seu controle. Estamos analisando este exemplo sob a perspectiva do provedor de serviços; ou seja, as portas G0/2 dos switches SW2 e SW3, que estão conectadaS aos switches do cliente. 

O comando para habilitar o Root Guard em uma porta é `spanning-tree guard root`, no modo de configuração de interface. Ao contrário do PortFast, BPDU Guard e BPDU Filter, não existe um comando para habilitá-lo por padrão a partir do modo de configuração global. Você só pode configurá-lo no modo de configuração de interface.

Agora que o Root Guard está habilitado nas portas G0/2 dos switches SW2 e SW3, o que acontece quando eles recebem BPDUs de SW4 e SW5 afirmando que SW6 é o root bridge? Se uma porta com Root Guard habilitado receber um BPDU, ela entrará no estado "broken" (quebrado) ou "root inconsistent" (inconsistência de root), desabilitando-a efetivamente. 

Veremos o significado desses termos ao analisar a CLI desses switches, mas, basicamente, isso significa que a porta não conseguirá encaminhar quadros e descartará quaisquer quadros que receber. Todo o tráfego é interrompido. E SW1, SW2 e SW3 não aceitarão SW6 como o root bridge. Portanto, embora as LANs do provedor de serviços e do cliente estejam fisicamente conectadas, elas não conseguem se comunicar. 

Antes de prosseguir, quero ressaltar que as portas G0/2 de SW2 e SW3, assim como as portas às quais elas se conectam em SW4 e SW5, são todas portas designadas. Normalmente, pode haver apenas uma porta designada por link, mas, neste caso, os switches discordam sobre qual é o root bridge.

Lembre-se apenas de que, em uma LAN com Spanning Tree funcional e normal, deve haver apenas uma porta designada por link. Mas este é um caso especial, porque o Root Guard está bloqueando o link. 

Certo, o Root Guard impediu que o cliente influenciasse a topologia STP do provedor de serviços, resolvendo o problema para o provedor. Mas isso também significa que o cliente não consegue se comunicar através da rede do provedor de serviços. Como podemos resolver isso? 

Para reativar uma porta desativada pelo Root Guard, você deve resolver o problema que causou a desativação da porta. Em outras palavras, a porta desativada precisa parar de receber BPDUs superiores. Para interromper os BPDUs superiores, o provedor de serviços deve instruir o cliente a aumentar a prioridade de seu switch. Então, o cliente aumenta a prioridade do SW6 para 4096, mais 1 referente ao ID da VLAN; e o que acontece depois?

Assim que os BPDUs superiores recebidos pelo SW2 e SW3 expirarem (atingirem o tempo limite), as portas serão automaticamente reativadas. E quanto tempo isso leva? Bem, como você já sabe, o *Max Age* (tempo máximo de vida) de um BPDU é de 20 segundos por padrão. Portanto, deve levar cerca de 20 segundos para que as portas G0/2 do SW2 e SW3 sejam reativadas.

E elas não serão apenas reativadas; o SW4, o SW5 e o SW6 também passarão a aceitar o SW1 como a *root bridge* (ponte raiz). E a topologia final do STP poderá ficar assim: o SW1 é a *root bridge*, todos os outros switches têm um caminho ativo para alcançar o SW1, e os links restantes ficam bloqueados. 

Portanto, o ponto importante aqui é que, para reativar uma porta desativada pelo Root Guard, você não precisa fazer nada na CLI do SW2 ou do SW3 — os switches que estão utilizando o Root Guard. Basta interromper o envio de BPDUs superiores, e as portas desativadas serão recuperadas automaticamente.

Neste caso, o provedor de serviços instruiu o cliente a modificar o *bridge ID* de seu switch, e o problema foi resolvido. 

## Root Guard: demonstração na CLI

Como o Root Guard requer apenas um comando para ser configurado, não há muito o que mostrar na CLI. Mas vamos voltar um pouco e observar esse processo novamente na CLI. 

Então, mais uma vez, a prioridade STP do SW6 é 1, tornando seu Bridge ID superior ao do SW1. Ativei o Root Guard na porta G0/2 do SW2 com o comando SPANNING-TREE GUARD ROOT. Estou mostrando apenas a CLI do SW2 aqui, mas fiz o mesmo no SW3 também.

Após executar o comando, uma mensagem é exibida informando que o Root Guard foi ativado na porta. Então, o que acontece quando o SW2 e o SW3 recebem BPDUs do SW4 e do SW5? Como diz esta mensagem de log, o Root Guard bloqueia as portas. Observe a saída do comando SHOW SPANNING-TREE.

A coluna de status da G0/2 indica BKN e, à direita, aparece ROOT_Inc. BKN significa "broken" (interrompida/inoperante) e ROOT_Inc significa Root Inconsistent (Inconsistência de Root). Uma porta "broken" está basicamente desativada; ela não consegue encaminhar ou receber quadros de dados. E o status Root Inconsistent nos diz por que a porta está nesse estado: ela foi desativada pelo Root Guard.

Vamos corrigir esse problema solicitando ao cliente que aumente a prioridade do SW6, que agora é 4097. Após cerca de 20 segundos, o SW2 exibe uma mensagem informando que a G0/2 foi desbloqueada. E, como você pode ver aqui, o status não é mais "broken" e a mensagem Root Inconsistent desapareceu.

Assim, a rede converge novamente com o SW1 atuando como root bridge. Antes de prosseguirmos para resumir este vídeo, quero apenas esclarecer onde você deve configurar o Root Guard. SW1, SW2 e SW3 pertencem a um provedor de serviços, e eles querem garantir que o SW1 permaneça como *root bridge*. 

Um switch de cliente não deve comprometer a topologia STP ao se tornar o *root bridge*. Portanto, o Root Guard é configurado nas portas que se conectam aos switches dos clientes, como a G0/2 do SW2 e a G0/2 do SW3. No entanto, observe que você nem sempre deve configurar o Root Guard em todas as portas conectadas a outra rede. 

Por exemplo, embora os switches do cliente se conectem ao provedor de serviços, o cliente não deve configurar o Root Guard em suas próprias portas. Se o cliente configurar o Root Guard nas portas do SW4 e SW5 que se conectam ao provedor, essas portas serão desativadas caso recebam BPDUs superiores, bloqueando esses links. 

E não faz sentido conectar-se a um provedor de serviços se você não conseguir se comunicar através da rede dele.

## Resumo

Certo, vamos resumir o Root Guard. Ao selecionar o *root bridge* de uma LAN, você deve considerar alguns aspectos, como um fluxo de tráfego ideal que minimize a latência e o congestionamento, bem como a estabilidade e a confiabilidade dos switches. O *root bridge* desempenha um papel fundamental no *spanning tree*, portanto, a escolha não deve ser aleatória. 

Em sua própria LAN, você pode controlar facilmente o *root bridge* definindo sua prioridade como 0. E se você tiver controle direto sobre todos os switches da rede, não há necessidade de configurar o Root Guard. Mas há casos em que você pode conectar seus switches a outros switches que estão fora do seu controle. O exemplo que usamos neste vídeo foi o de switches de um provedor de serviços conectando-se a switches de um cliente, o que pode ocorrer quando o provedor está oferecendo serviços Metro Ethernet, por exemplo. 

O Root Guard pode ser configurado em portas específicas para impedir que elas aceitem BPDUs superiores de outros switches. Por exemplo, os switches de um provedor de serviços geralmente não devem aceitar BPDUs superiores de um cliente. Você pode usar o comando `spanning-tree guard root` para ativar o Root Guard em uma porta, mas não existe um comando para ativá-lo por padrão a partir do modo de configuração global.

O PortFast pode ser ativado por padrão porque, na maioria dos casos, você deseja ativá-lo em todas as portas de acesso, já que elas geralmente se conectam a dispositivos finais (hosts). E o BPDU Guard e o Filter podem ser ativados por padrão em todas as portas com PortFast, pois esses recursos são frequentemente usados ​​em conjunto. 

Mas o Root Guard não é o tipo de recurso que você deseja ativar nas portas por padrão. Ele deve ser ativado apenas em portas específicas onde for necessário, e é por isso que não pode ser ativado no modo de configuração global. E o que exatamente o Root Guard faz?

Ele impede que uma porta se torne uma porta raiz (root port) caso receba um BPDU superior. Em vez disso, o status da porta passará a ser "broken" (interrompida) e "root inconsistent" (inconsistência de raiz). Basicamente, "broken" significa que a porta está bloqueada; ela não pode encaminhar quadros. E "Root Inconsistent" nos diz por que ela está interrompida: porque o Root Guard bloqueou a porta. 

Mas, se a porta parar de receber BPDUs superiores, ela se recuperará automaticamente. Você não precisa reativar a porta manualmente nem usar o recurso ErrDisable Recovery, como acontece com o BPDU Guard.