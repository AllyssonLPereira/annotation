
Você já conhece os estados de bloqueio (blocking) e encaminhamento (forwarding), mas existem também alguns estados de transição entre eles, bem como temporizadores que determinam quando o switch muda de um estado para outro. 

Vou mostrar a você a BPDU (Bridge Protocol Data Unit) do Spanning Tree, quais campos estão incluídos nela e qual é a finalidade deles. Depois, veremos alguns recursos opcionais do STP, às vezes chamados de "kit de ferramentas" do Spanning Tree — recursos adicionais que você pode ativar para aprimorar o protocolo; abordaremos alguns deles brevemente.

Por fim, trataremos das configurações do Spanning Tree. O Spanning Tree é executado por padrão, então você não precisa realmente fazer nenhuma configuração, mas é importante saber como alterar qual switch se torna o switch raiz (root switch) e coisas do tipo, para garantir que o tráfego siga o melhor caminho.

## Estados das portas

Primeiro, vamos analisar os estados de porta do Spanning Tree. Você já conhece dois deles: BLOCKING (Bloqueio) e FORWARDING (Encaminhamento), mas existem outros dois: LISTENING (Escuta) e LEARNING (Aprendizado). 

BLOCKING e FORWARDING são os dois estados "estáveis". As portas Root (raiz) e Designated (designada) permanecem estáveis ​​no estado Forwarding, e as portas Non-designated (não designadas) permanecem estáveis no estado Blocking. 

Observe que elas só permanecem estáveis ​​enquanto não houver alterações na topologia da rede. Se um novo dispositivo for adicionado, uma interface for desativada ou ocorrer uma falha de hardware em algum ponto, elas podem precisar mudar de estado. 

Mas, como eu disse, enquanto a rede estiver estável, cada interface do Spanning Tree estará estável em um desses estados. 

Agora, existem também dois estados de transição. Listening (Escuta) e Learning (Aprendizado) são estados de transição pelos quais se passa quando uma interface é ativada, ou quando uma porta em estado de Blocking (Bloqueio) precisa transitar para um estado de Forwarding (Encaminhamento) devido a uma mudança na topologia da rede.

Na verdade, existe mais um estado sobre o qual você pode ouvir falar: o estado disabled (desativado). Isso se refere simplesmente a uma interface que está administrativamente desativada, ou seja, desligada (*shutdown*). Não falaremos muito sobre o estado desativado porque ele não desempenha nenhum papel no Spanning Tree; a interface está desligada. 

Ok, vamos dar uma olhada nesses estados, começando pelo estado de Blocking (Bloqueio).

### Estados de Porta STP - Blocking (Bloqueio)

Portas não designadas (*non-designated*) estão em estado de Blocking. Interfaces em estado de Blocking estão efetivamente desativadas para evitar loops.

É isso que faz o Spanning Tree funcionar: desativar interfaces redundantes para evitar loops.

Interfaces em estado de Blocking não enviam nem recebem tráfego de rede comum. Qualquer tráfego comum que chegue a uma interface em estado de Blocking será simplesmente descartado.

No entanto, interfaces em estado de Blocking recebem BPDUs do STP. Elas precisam receber e processar BPDUs para estarem cientes da topologia do Spanning Tree e estarem prontas para transitar para um estado de encaminhamento, se necessário. 

Mas interfaces em estado de Blocking NÃO encaminham BPDUs do STP.

Finalmente, interfaces em estado de Blocking NÃO aprendem endereços MAC. Se tráfego comum chegar à interface, ele é descartado sem adicionar o endereço MAC à tabela de endereços MAC.

### Estados de Porta STP - Listening (Escuta)

Após o estado de Blocking, interfaces com a função Designated (Designada) ou Root (Raiz) entram no estado de Listening.

O estado de Listening (Escuta) tem duração padrão de 15 segundos. Isso é determinado por um temporizador chamado "Forward delay" (Atraso de encaminhamento).

Você verá em breve que esse temporizador não é usado apenas para o estado de Listening. De qualquer forma, lembre-se de que o padrão é 15 segundos.

Uma interface no estado de Listening APENAS encaminha/recebe BPDUs do Spanning Tree.

Ela NÃO envia nem recebe tráfego comum. Se um quadro unicast comum for recebido em uma porta no estado Listening (Escuta), ele será descartado.

Uma interface no estado Listening também NÃO aprende endereços MAC a partir do tráfego comum que chega à interface. Eu disse a mesma coisa sobre o estado Blocking (Bloqueio), mas deixe-me explicar.

Como você já sabe bem, quando um quadro chega a uma interface de switch, o switch usa o campo de endereço MAC de origem para "aprender" esse endereço MAC e atualiza a tabela de endereços MAC com as informações de endereço MAC, interface e VLAN. 

No entanto, se uma interface estiver no estado Listening do Spanning Tree, ela não fará isso.

O tráfego é simplesmente descartado, e o processo de aprendizado de endereços MAC não ocorre.

### Estados de Porta STP - Learning (Aprendizado)

Após o estado Listening, uma porta Designada ou Root (Raiz) entrará no estado Learning.

O estado Learning dura 15 segundos por padrão. Isso é determinado pelo temporizador "Forward delay" (atraso de encaminhamento); portanto, o mesmo temporizador é usado tanto para o estado Listening quanto para o estado Learning, o que significa que, por padrão, leva-se um total de 30 segundos para passar por ambos os estados e entrar em um estado de encaminhamento.

Assim como no estado Listening, uma interface no estado Learning APENAS envia ou recebe BPDUs do protocolo Spanning Tree. 

Além disso, ela NÃO envia nem recebe tráfego comum.

No entanto, aqui está a diferença entre os estados Listening e Learning. Uma interface no estado Learning aprende endereços MAC a partir do tráfego comum que chega à interface.

Assim, uma interface no estado Learning está se preparando para encaminhar tráfego ao construir parte de sua tabela de endereços MAC antecipadamente. 

Finalmente, temos o estado Forwarding (Encaminhamento).

### Estados de Porta STP - Forwarding (Encaminhamento)

Portas Root e Designadas ficam no estado Forwarding quando estão estáveis. Uma porta no estado Forwarding opera normalmente. 

Então, o que isso significa? Uma porta no estado de encaminhamento (*Forwarding*) envia e recebe BPDUs.

Ela envia e recebe tráfego normal. Além disso, aprende endereços MAC a partir dos quadros que chegam até ela e os adiciona à tabela de endereços MAC. Ou seja, é uma porta de switch operando normalmente.

Agora, vamos falar sobre cada um dos temporizadores usados ​​no Spanning Tree.

## Temporizadores STP

Já mencionei os temporizadores Hello e Forward Delay, mas ainda não falei sobre o Max Age. Primeiramente, vamos analisar mais detalhadamente o temporizador Hello.

### Hello

Ele determina com que frequência a *root bridge* (ponte raiz) envia BPDUs do tipo Hello; por padrão, ela os envia a cada 2 segundos. 

Outros switches na rede não geram seus próprios BPDUs, mas encaminham os que recebem. No entanto, há algo que não mencionei antes: os switches só encaminham BPDUs através de suas PORTAS DESIGNADAS (*Designated Ports*). Vamos ver como isso funciona. 

Para começar, mostrei este slide no vídeo do dia 20. Supondo que todos esses switches entrem em operação ao mesmo tempo, cada um assume que é a *root* *bridge* e envia BPDUs por todas as suas interfaces. 

No entanto, uma vez que a rede tenha convergido e todos os switches e portas estejam estabilizados em suas funções, apenas a *root bridge* (ponte raiz) envia BPDUs.

Então, os outros switches encaminham esses BPDUs por suas portas designadas, atualizando informações como o custo até a *root bridge*, o ID da ponte de origem, o ID da porta de origem, etc.

Em seguida, dois segundos depois, a *root bridge* envia BPDUs novamente, e os outros switches encaminham novamente esses BPDUs por suas portas designadas. 

Observe que eles não encaminham os BPDUs por suas portas raiz ou portas não designadas, apenas por suas portas designadas. Então, esse é o temporizador *hello*.

A seguir, o temporizador *forward delay* (atraso de encaminhamento). 
### Forward Delay

Essa é a duração dos estados de transição *Listening* (Escuta) e *Learning* (Aprendizado) pelos quais uma porta passa quando transita para o estado de encaminhamento (*forwarding*). 

Observe que essa é a duração de cada um dos estados, não a duração total de ambos combinados. Assim, com o temporizador *forward delay* padrão de 15 segundos, leva-se um total de 30 segundos para que a porta do switch passe por ambos os estados e encaminhe tráfego

Então, o temporizador final, sobre o qual ainda não falei, é o temporizador *max age* (idade máxima).

### Max Age

Esse temporizador indica quanto tempo uma interface aguardará para alterar a topologia *spanning tree* após deixar de receber BPDUs.

Portanto, isso precisará de mais algumas explicações. Vamos dar uma olhada.

Lembre-se de que cada domínio de colisão possui uma porta designada, e os BPDUs são encaminhados a partir das portas designadas. Assim, todas as portas raiz e as portas não designadas esperam receber BPDUs.

A bridge raiz, SW3, envia BPDUs, e então SW1 e SW4 os encaminham a partir de suas portas designadas. Para demonstrar o temporizador Max Age, vamos focar na interface G0/1 do SW2.

Ela acabou de receber um BPDU, então o temporizador Max Age é reiniciado para 20. Ele faz a contagem regressiva para 19... 18... e, então, a bridge raiz envia BPDUs devido ao temporizador "hello" de 2 segundos;

eles são encaminhados pelos outros switches, e o SW2 reinicia seu temporizador Max Age para 20... 19... 18... Mas e se ocorrer uma falha na conexão entre SW1 e SW2?

A bridge raiz enviará BPDUs, e outros switches encaminharão os BPDUs, mas a interface G0/0 do SW1 está inativa (down), então o SW2 não recebe mais um BPDU em sua interface G0/1.

Assim, o temporizador Max Age continua a contagem regressiva. 17... 16... 15... e se a falha não for corrigida e o SW2 não receber mais BPDUs em sua interface G0/1, o temporizador Max Age do SW2 chegará a 0.

O que acontece então? Primeiramente, se outro BPDU for recebido antes que o temporizador Max Age chegue a 0, o tempo será reiniciado para 20 segundos e nenhuma alteração ocorrerá. 

No entanto, se outro BPDU não for recebido, o temporizador Max Age chega a 0 e o switch reavaliará suas escolhas de STP, incluindo a bridge raiz, a porta raiz local, as portas designadas e as portas não designadas.

Após essas decisões, se uma porta não designada for selecionada para se tornar uma porta designada ou uma porta raiz, ela fará a transição do estado de bloqueio para o estado de escuta (por 15 segundos), para o estado de aprendizado (novamente por 15 segundos) e, finalmente, para o estado de encaminhamento.

Portanto, pode levar um total de 50 segundos para que uma interface em bloqueio transite para o encaminhamento.

Por que isso demora tanto? Bem, esses temporizadores e estados de transição servem para garantir que loops não sejam criados acidentalmente pela mudança de uma interface para o estado de encaminhamento cedo demais. Mostrei na aula anterior o quão perigoso um loop de Camada 2 pode ser.

É por isso que o protocolo Spanning Tree é muito cauteloso ao mudar uma interface para o estado de encaminhamento.

No entanto, uma interface em encaminhamento pode mudar diretamente para o estado de bloqueio, pois não há preocupação quanto à criação de um loop ao bloquear uma interface. Mas, como acabei de dizer, uma interface em bloqueio não pode mudar diretamente para o estado de encaminhamento. Ela deve passar pelos estados de escuta e aprendizado.

Então, vamos prosseguir para examinar o BPDU (Bridge Protocol Data Unit) do Spanning Tree.

## STP BPDU (captura de pacotes no Wireshark)

Primeiramente, na seção do cabeçalho Ethernet, observe o destino. O PVST+ da Cisco utiliza o endereço MAC de destino 0100.0ccc.cccd para seus BPDUs.

Recomendo memorizar isso; é uma informação que você pode precisar saber para a prova.

Mencionei o PVST na aula anterior, mas o que é o PVST+? Bem, o PVST é uma versão mais antiga que suporta apenas o ISL da Cisco para encapsulamento de trunk.

O PVST+ é uma versão mais recente que suporta o padrão 802.1Q (dot1q). Às vezes posso usar o termo "PVST", mas na verdade quero dizer PVST+, pois o ISL praticamente não é mais utilizado. Aliás, já que mencionei o endereço MAC: o Spanning Tree padrão — ou seja, não o da Cisco, como o PVST ou PVST+ — utiliza o endereço MAC de destino 0180.c200.0000.

Novamente, é bom lembrar desse detalhe para o exame. 

Agora, vamos passar para o BPDU do Spanning Tree propriamente dito.

Não acho que você precise memorizar o BPDU para o CCNA, mas quero apenas apresentar o que está incluído nele.

Os três primeiros campos são:

- O identificador de protocolo (Protocol Identifier), que é sempre o valor hexadecimal 0000 para o Spanning Tree. 

- O identificador de versão do protocolo (Protocol Identofier Version) é definido como 0 para o Spanning Tree clássico; você verá um valor diferente aqui quando analisarmos o Rapid Spanning Tree Protocol.

- Por fim, o tipo de BPDU (BPDU Type) é o valor hexadecimal 00 para o chamado "BPDU de configuração".

Existem outros tipos de BPDUs, mas não precisamos nos aprofundar tanto nisso para o CCNA.

A seguir, temos algumas flags; elas são usadas para sinalizar alterações de topologia a outros switches. Novamente, não acho necessário nos aprofundarmos nelas para o CCNA.

Depois, temos o identificador da raiz (root identifier), que fornece a prioridade da bridge e o ID estendido do sistema, que corresponde ao ID da VLAN — 10, neste caso — e o ID do sistema da bridge, que é o endereço MAC da bridge raiz. 

Neste exemplo, defini o endereço MAC como apenas a letra "A" repetida.

O próximo campo é o custo do caminho até a raiz (root path cost). Ele é 0 neste caso, indicando que esta é a bridge raiz. Você também pode identificar que esta é a *root bridge* observando este campo. 

As informações no campo de identificador da *bridge* são iguais às do campo de identificador da *root bridge*, o que significa que esta é a *root bridge*.

Em seguida, temos o identificador da porta, ou seja, a interface que enviou o BPDU. O valor hexadecimal é 8002. Em hexadecimal, 80 equivale a 128, e 02 é o número da própria porta.

Finalmente, os temporizadores. A idade da mensagem (*message age*) é algo que ainda não mencionei, mas ela começa em 0 na *root bridge* (ponte raiz) e aumenta em 1 cada vez que é encaminhada por outro switch. 

Esse valor é subtraído da idade máxima (*max age*) quando um switch recebe a BPDU; então, por exemplo, se a BPDU passar por 5 switches, quando chegar à sexta ponte, ela reduzirá imediatamente seu temporizador de idade máxima para 15, o que significa que, sempre que receber uma BPDU, sua idade máxima será redefinida para 15 em vez de 20, mesmo que o temporizador de idade máxima seja 20. 

No entanto, não acho que esse seja um tópico importante para o CCNA; é algo um pouco mais avançado.

Depois disso, temos os três temporizadores de que falamos: *max age*, *hello* e *forward delay*.

Aliás, os temporizadores do Spanning Tree na *root bridge* determinam os temporizadores do Spanning Tree para o restante dos switches na rede, mesmo que eles estejam configurados de forma diferente.

## Kit de Ferramentas STP

A seguir, vamos falar sobre alguns recursos opcionais do Spanning Tree, às vezes chamados de "kit de ferramentas do Spanning Tree".

São recursos que podem ser habilitados para melhorar, de alguma forma, a funcionalidade do protocolo Spanning Tree.

O primeiro deles chama-se PortFast. Ele resolve um problema do Spanning Tree. 

### PortFast

O PortFast pode ser habilitado em interfaces conectadas a hosts finais, como a G0/2 interface em cada um desses switches. Essas são portas designadas, em estado de encaminhamento (*forwarding*).

No entanto, quando são ligadas ou conectadas aos PCs pela primeira vez, elas precisam passar pelos estados de *Listening* (escuta) e *Learning* (aprendizado) antes de começarem a encaminhar tráfego.

Quanto tempo isso leva? 15 segundos para *Listening* (Escuta) e 15 segundos para *Learning* (Aprendizado), totalizando 30 segundos.

Eu expliquei por que o Spanning Tree passa por esse processo antes de colocar uma porta no estado de *forwarding*: é porque loops de Camada 2 são tão perigosos para uma rede que o switch quer ter certeza absoluta de que nenhum loop será formado antes de encaminhar dados por aquela interface.

No entanto, apenas interfaces conectadas a outro switch podem formar um loop de Camada 2. Não há risco de formar um loop com um dispositivo final (*end host*). Então, não seria ótimo se essas portas conectadas a dispositivos finais pudessem começar a encaminhar imediatamente, sem ter que esperar 30 segundos para passar de *listening* para *learning* e depois para *forwarding*? 

Bem, é isso que o PortFast faz.

O PortFast permite que uma porta vá imediatamente para o estado de *Forwarding*, ignorando os estados de *Listening* e *Learning*.

Se utilizado, deve ser habilitado apenas em portas conectadas a dispositivos finais. Se habilitado em uma porta conectada a outro switch, isso pode causar um loop de Camada 2.

O objetivo dos estados de *listening* (escuta) e *learning* (aprendizado) é evitar a criação de loops; portanto, ignorá-los é arriscado quando a conexão é feita com outro switch.

Ainda não analisamos outras configurações do Spanning Tree, pois ele opera por padrão, mesmo sem configuração.

Vamos ver a configuração geral do Spanning Tree, mas primeiro vamos examinar o PortFast.

#### Configuração do PortFast

O PortFast é habilitado no nível da interface com o comando `spanning-tree portfast`.

Em seguida, recebemos um aviso sobre o que acabei de mencionar: você só deve habilitar o PortFast em portas conectadas a um dispositivo final (*end host*).

Há também uma mensagem informando que, embora o PortFast tenha sido configurado, ele só entrará em vigor se a interface não estiver em modo *trunk* — ou seja, se for uma porta de acesso.

Isso ocorre porque portas *trunk* geralmente são conectadas a outros switches. Você ainda pode configurar o PortFast em uma porta *trunk*, mas a configuração simplesmente não terá efeito.

Você também pode habilitar o PortFast usando o seguinte comando no modo de configuração global: `spanning-tree portfast default`. Isso habilita o PortFast em todas as portas de acesso, mas não nas portas *trunk*.

Portanto, o PortFast é um recurso excelente para colocar rapidamente em operação uma porta de switch conectada a um dispositivo final, sem precisar esperar 30 segundos.

No entanto, ainda pode haver riscos. E se um funcionário conectar outro switch à rede, como neste exemplo?

Esse funcionário não tem necessariamente uma intenção maliciosa; ele pode simplesmente não saber exatamente o que está fazendo. Como o PortFast coloca essas interfaces em estado de encaminhamento (*forwarding*), um loop de Camada 2 é formado. 

O PortFast também pode causar loops se o cabeamento da rede for alterado sem a devida cautela; por exemplo, se um host for movido para uma porta de switch diferente e um switch for conectado à sua porta antiga.

De qualquer forma, o ponto principal é que existe um risco ao usar o PortFast.

No entanto, existe um recurso opcional adicional do Spanning Tree que podemos ativar para proteger contra esses loops. Ele se chama BPDU Guard.

### BPDU Guard

Se uma interface com o BPDU Guard ativado receber um BPDU de outro switch, a interface será desativada (shutdown) para impedir a formação de um loop. 

O BPDU Guard é muito simples de configurar.

No modo de configuração de interface, use o comando `spanning-tree bpduguard enable`. É isso.

Assim como no PortFast, também existe uma opção para ativá-lo por padrão. É este comando aqui. No modo de configuração global, use o comando `spanning-tree portfast bpduguard default`.

Isso ativa o BPDU Guard em todas as interfaces com o PortFast ativado.

Observe que os comandos são um pouco diferentes: para ativá-lo diretamente na interface, usa-se `spanning-tree bpduguard enable`, sem mencionar o PortFast. No entanto, para ativá-lo globalmente, é preciso incluir "portfast" no comando: `spanning-tree portfast bpduguard default`. 

Tirei esta captura de tela no Packet Tracer, então o esquema de cores da CLI é um pouco diferente do anterior, mas conectei um switch a uma interface com BPDU Guard ativado e, agora, você pode ver o que acontece quando um BPDU chega a uma porta com BPDU Guard ativado.

A porta é desativada; ela entra efetivamente em estado de *shutdown*. E se você quiser reativar a porta? Para reativar uma porta que foi desativada pelo BPDU Guard, basta executar os comandos SHUTDOWN e, em seguida, NO SHUTDOWN na interface. 

Você verá que a interface volta a ficar ativa. No entanto, se você não tiver realmente resolvido o problema e ela ainda estiver conectada a um switch, poderá ver aqui que a interface será imediatamente desativada novamente assim que o próximo BPDU chegar.

Portanto, certifique-se de realmente resolver o problema antes de tentar reativar a interface.

Existem muitos outros recursos opcionais que podem ser habilitados, mas deixe-me apresentar rapidamente outros dois cujos nomes e finalidades básicas você deve, pelo menos, conhecer. 

São eles o Root Guard e o Loop Guard. 

### Root Guard/Loop Guard

### Root Guard

Se você habilitar o Root Guard em uma interface, mesmo que ela receba um BPDU superior (com um Bridge ID menor) nessa interface, o switch não aceitará o novo switch como Root Bridge.

A interface será desativada. Isso ajuda a manter a topologia Spanning Tree caso alguém conecte outro switch à rede, seja com más intenções ou, talvez, sem saber o impacto de sua ação.

### Loop Guard

Se você habilitar o Loop Guard em uma interface, mesmo que ela pare de receber BPDUs, ela não começará a encaminhar tráfego. A interface será desativada.

Isso evita loops que podem ocorrer se uma interface falhar em apenas uma direção, causando o que se chama de "link unidirecional" — que não consegue receber dados, mas ainda é capaz de encaminhá-los, ou vice-versa. 

Portanto, esses são outros dois recursos opcionais do Spanning Tree.

Finalmente, vamos ver algumas configurações básicas do Spanning Tree, começando pelo modo.

## Configuração de STP

### Modo

Você pode configurar o modo Spanning Tree que o switch utiliza com o comando SPANNING-TREE MODE, e então verá que existem três opções. O MST (Multiple Spanning Tree) 

O PVST é o Spanning Tree clássico, mas com a adição do conceito "por VLAN" da Cisco — aquele que temos estudado até agora. 

O Rapid-PVST é uma versão aprimorada sobre a qual falarei na próxima aula.

Os switches Cisco modernos executam o Rapid-PVST por padrão e, geralmente, não há motivo para alterá-lo. No entanto, se você quiser experimentar o Spanning Tree clássico em seu laboratório, como fiz nestas demonstrações, pode habilitá-lo com este comando: SPANNING-TREE MODE PVST.

### Root Bridge

Você também pode configurar manualmente a Root Bridge manipulando a prioridade de bridge de um switch.

Com esses endereços MAC e os valores de prioridade padrão, o SW1 é a Root Bridge. No entanto, poderíamos configurar o SW3 para ser a Root Bridge. Também podemos configurar algo chamado de *root bridge* "secundária", que será a próxima da fila para se tornar a  bridge raiz caso a bridge raiz atual falhe. Vamos ver como configurar isso.

É assim que se configura a bridge raiz, chamada de bridge raiz "primária" (*primary*): `spanning-tree vlan`, seguido pelo número da VLAN e, então, `root primary`.

Agora você pode ver que esta bridge se tornou a raiz. Esse comando define a prioridade do STP como 24576. Se outro switch já tiver uma prioridade menor que 24576, ele define a prioridade deste switch para um valor 4096 unidades menor que a prioridade do outro switch. 

Assim, ele faz com que este switch tenha a menor prioridade, tornando-o a bridge raiz.

Se você verificar a configuração em execução (*running-config*), verá que o comando realmente aplicado neste caso é `spanning-tree vlan 1 priority 24576`.

Portanto, esse comando instrui o switch a aplicar o comando de prioridade do spanning-tree, seja com a prioridade 24576 ou com um valor 4096 menor que a menor prioridade atual.

O comando para definir a bridge raiz secundária — a bridge com a segunda menor prioridade — é basicamente o mesmo: `spanning-tree vlan`, número da VLAN, `root secondary`.

Agora a prioridade foi definida como 28672. Assim, esse comando define a prioridade do spanning-tree para esta VLAN como 28672.

No entanto, assim como no comando *root primary*, o comando efetivamente aplicado é o comando de prioridade do spanning-tree. Então, para ambos os comandos, você poderia, na verdade, usar o comando `spanning-tree priority`

### Balanceamento de Carga STP

Como você vê aqui — para configurar a *root bridge*; o comando `spanning-tree root` é apenas uma maneira simples de fazer isso sem precisar lembrar dos diferentes incrementos de 4096.

Você deve se lembrar, da aula anterior, que a prioridade da *bridge* deve ser definida em incrementos de 4096; portanto, o comando `root` é mais fácil de usar.

Então, esta é a nossa topologia agora. A interface entre o SW1 e o SW2 está desativada porque o SW1 está bloqueando sua interface G0/0.

Esta topologia está executando o PVST+ da Cisco; portanto, na verdade, esta é apenas a topologia para a VLAN 1. Talvez exista outra VLAN, a VLAN 2, nesta topologia; como será a topologia para ela? Ela será assim — a topologia padrão —, porque as configurações de *root bridge* que definimos aplicam-se apenas à VLAN 1. 

Na VLAN 2, a conexão entre o SW1 e o SW2 NÃO será desativada; em vez disso, a conexão entre o SW2 e o SW3 será desativada. Isso permite o que chamamos de balanceamento de carga do *spanning tree*.

Se você tiver várias VLANs em sua rede, bloquear a mesma interface em cada VLAN é um desperdício de largura de banda da interface. Essa conexão não fará nada, apenas aguardará a falha de outra conexão para poder começar a encaminhar tráfego. 

No entanto, se você configurar uma *root bridge* diferente para VLANs diferentes, VLANs diferentes desativarão interfaces diferentes. 


### Cost and Port Priority

Como você pode ver neste comando, ambos são configurados por VLAN, assim como a prioridade da bridge. 

Para recapitular: o que é o custo? É o custo para a raiz (root cost); lembra-se da tabela que mostrei no dia 20? FastEthernet tem custo 19, Gigabit Ethernet tem custo 4, etc.

Ele é usado principalmente para determinar a porta raiz (root port) e também serve como critério de desempate na seleção de portas designadas e não designadas. 

E quanto à prioridade? Lembra-se para que ela serve? Bem, ela compõe a primeira metade do ID da porta, que é o critério final de desempate para determinar a porta raiz. 

Por que você iria querer alterar algum desses valores? Para modificar o resultado do processo de seleção da porta raiz ou da porta designada.




 
