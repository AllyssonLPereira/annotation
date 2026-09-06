
Como engenheiros de rede, somos responsáveis ​​por uma infraestrutura crítica para os negócios; portanto, temos que garantir que essa infraestrutura seja o mais resiliente possível a falhas.

Primeiro, aqui está uma rede mal projetada. Há muitos pontos de falha aqui que poderiam interromper a conectividade. Por exemplo, se esta conexão for interrompida devido a uma falha de hardware, toda esta rede perde a conectividade com a Internet. 

Ou, se esta conexão for interrompida devido a uma falha de hardware, estes hosts perdem a conectividade dentro da LAN e com a Internet. Certo, esses são apenas dois exemplos; vamos analisar um projeto de rede melhor.

Esta rede aqui tem um projeto muito melhor. Se este PC quiser acessar a Internet, ele pode usar este caminho em uma situação normal. No entanto, mesmo que este roteador apresente uma falha de hardware e pare de funcionar completamente, o PC pode acessar a Internet por meio deste ou de outro caminho alternativo. 

Talvez o tráfego para este outro PC na LAN geralmente siga este caminho até o destino.

E se este switch falhar? Isso não é um problema, pois este caminho alternativo está disponível. Então, acho que você consegue perceber a vantagem de projetar redes redundantes.

No entanto, você pode estar se perguntando: e se este switch falhar? Bem, se esse for o caso, todos os hosts conectados a esse switch perderiam a conectividade. Infelizmente, a maioria dos PCs possui apenas uma placa de rede (NIC), portanto, eles só podem ser conectados a um único switch.

No entanto, servidores importantes geralmente possuem múltiplas NICs, permitindo que sejam conectados a vários switches para garantir redundância. Abordaremos muitos protocolos usados ​​para habilitar a redundância de rede ao longo deste curso, e o Spanning Tree é um deles. 

Aliás, o Spanning Tree é um protocolo de Camada 2; ele viabiliza redes de Camada 2 redundantes, ou seja, dentro da LAN — sem roteamento para a Internet ou entre redes na Camada 3.

Acabei de mostrar os benefícios de uma LAN redundante: ter múltiplos caminhos entre esses switches oferece rotas alternativas caso uma conexão falhe. No entanto, sem o Spanning Tree, surge um problema GRAVE que pode destruir sua rede.

Então, onde está o problema? Deixe-me apresentar o conceito de "tempestades de broadcast" (broadcast storms).

Usarei uma topologia de rede simplificada para demonstrar a questão. O PC1 é 10.0.0.1, o PC2 é 10.0.0.2 e o PC3 é 10.0.0.3. Você já sabe o que um switch faz com um quadro de broadcast ou um quadro unicast desconhecido. 

Digamos, por exemplo, que o PC1 queira enviar tráfego para o PC2. Para isso, ele precisa saber o endereço MAC do PC2. Então, suponha que o PC1 envie um quadro de solicitação ARP — que é um quadro de broadcast; ele utiliza o endereço de broadcast com seu endereço MAC como origem e endereço MAC composto apenas por "F"s como seu endereço de destino.

Quando o SW1 recebe o quadro, o que ele faz? Como eu disse, você já sabe o que um switch faz com quadros de broadcast e unicast desconhecido. Ele os encaminha (faz o *flood*) por todas as interfaces, exceto aquela pela qual o quadro foi recebido.

Assim, tanto o SW2 quanto o SW3 recebem uma cópia do quadro. Eles então fazem a mesma coisa: encaminham o quadro por todas as interfaces, exceto aquela pela qual ele foi recebido. Então, o PC2 recebe a solicitação ARP e responde com uma resposta ARP unicast.

### Loop infinito

Tudo certo? Na verdade, não; nem tudo está certo. Embora o PC2 tenha recebido a solicitação ARP e enviado sua resposta, esses quadros de broadcast ainda permanecem na rede. Limpei as setas para que você possa visualizar isso mais facilmente.

Como acabei de dizer, o PC2 recebeu a solicitação ARP e enviou a resposta, mas e quanto a esses quadros de broadcast na rede? Os switches continuarão a encaminhá-los (*flooding*). Então, o que acontecerá depois disso?

O SW1 acabou de receber dois quadros de broadcast em duas interfaces diferentes. Ele irá encaminhá-los novamente. Deixe-me limpar a imagem novamente. O SW2 e o SW3 acabaram de receber quadros de broadcast; o que eles farão?

Eles irão encaminhá-los. Acho que você entendeu a ideia. Isso continuará para SEMPRE.

Você se lembra do campo TTL, ou tempo de vida (*time to live*), do cabeçalho IP? Ele é usado para evitar loops infinitos na Camada 3. Mas o cabeçalho Ethernet não possui um campo TTL.

Esses quadros de broadcast circularão pela rede indefinidamente. Se um número suficiente desses broadcasts em loop se acumular na rede, ela ficará congestionada demais para permitir o tráfego legítimo. Isso é chamado de tempestade de broadcast (*broadcast storm*).

Com o tempo, sua rede ficará assim: tão cheia de quadros de broadcast em loop que nenhum tráfego comum conseguirá passar por ela. As setas vermelhas representam o loop no sentido horário entre os três switches, e as setas roxas representam o loop no sentido anti-horário.

### MAC Address Flapping

No entanto, o congestionamento da rede não é o único problema. Toda vez que um quadro chega a uma porta do switch, o switch usa o campo de endereço MAC de origem para "aprender" o endereço MAC e atualizar sua tabela de endereços MAC.

Quando quadros com o mesmo endereço MAC de origem chegam repetidamente a interfaces diferentes, o switch atualiza continuamente a interface em sua tabela de endereços MAC.

Isso é conhecido como *MAC Address Flapping* (oscilação de endereço MAC).

Então, como podemos projetar uma rede com caminhos redundantes que não resulte em loops de Camada 2?

Bem, o protocolo Spanning Tree é uma resposta para esse problema. Então, vamos dar uma olhada no protocolo Spanning Tree — o que agora chamamos de "protocolo Spanning Tree clássico"

## Introdução ao STP

O Spanning Tree Protocol é um protocolo padrão da indústria, o IEEE 802.1D. Esse é o tipo de STP no qual focaremos no vídeo de hoje; focaremos no Rapid STP, que é mais recente, mais adiante.

Como é tão importante evitar loops de Camada 2, switches de TODOS os fabricantes executam o STP por padrão.

Portanto, você não encontrará o STP apenas em switches Cisco. O STP evita loops de Camada 2 colocando portas redundantes em um estado de bloqueio, essencialmente desativando a interface.

Essas interfaces atuam como backups que podem entrar em estado de encaminhamento se uma interface ativa — ou seja, uma interface que está encaminhando tráfego no momento — falhar. 

Interfaces em estado de encaminhamento comportam-se normalmente. Elas enviam e recebem todo o tráfego normal. No entanto, interfaces em estado de bloqueio apenas enviam ou recebem mensagens STP (chamadas de BPDUs, ou *Bridge Protocol Data Units*) e alguns outros tipos específicos de tráfego.

### Bridge ou Switch?

Antes de nos aprofundarmos mais, deixe-me falar sobre a palavra "bridge" (ponte).

Hubs, bridges e switches. Hubs eram usados ​​antes da invenção dos switches e, em vez de aprenderem endereços MAC para encaminhar quadros ao destino correto, eles simplesmente propagavam (faziam *flood*) de quadros por todas as interfaces.

Mas, na verdade, antes dos switches, existia outro tipo de dispositivo chamado *bridge* (ponte).

Você não precisa saber sobre *bridges* para o CCNA — é uma tecnologia antiga —, mas elas representam uma etapa de transição entre o hub e o switch.

No entanto, o motivo pelo qual estou falando sobre *bridges* é que o protocolo Spanning Tree (STP) ainda utiliza esse termo. Contudo, quando usamos o termo "*bridge*", na verdade estamos nos referindo a um switch. 

*Bridges* não são utilizadas em redes modernas. Portanto, nesta aula — e sempre que eu falar sobre STP —, você me ouvirá usar o termo "*bridge*", mas ele significa, na verdade, switch.

Assim, se olharmos novamente para esta topologia, talvez estas interfaces estejam em estado de encaminhamento (*forwarding*), enquanto esta interface específica no SW3 está em estado de bloqueio (*blocking*), desativando efetivamente a conexão entre o SW2 e o SW3.

Na prática, é como se aquele link não existisse, e esta passa a ser a nossa topologia.

Se o PC1 enviar aquele mesmo quadro de broadcast de solicitação ARP, ele será propagado desta forma; não haverá mais loops. No entanto, se em algum momento outra interface falhar — talvez esta aqui, os switches ajustarão automaticamente a topologia, e o quadro de broadcast será propagado desta maneira; novamente, sem loops.

Então, essa é apenas uma visão geral básica da finalidade do Spanning Tree Protocol. Agora, vamos nos aprofundar um pouco mais em como o Spanning Tree Protocol funciona.

## Funcionamento

Ao selecionar quais portas estão encaminhando tráfego e quais estão bloqueando, o STP cria um único caminho de ida e volta para cada ponto da rede. Isso evita loops de Camada 2.

Existe um processo definido que o STP utiliza para determinar quais portas devem encaminhar tráfego e quais devem bloquear. É esse processo que abordaremos a seguir. 

Switches com STP habilitado enviam BPDUs do tipo "Hello" por todas as interfaces; o temporizador padrão é de 2 segundos, portanto, o switch enviará um BPDU "Hello" por cada interface a cada 2 segundos.

Se um switch recebe um BPDU "Hello" em uma interface, ele sabe que essa interface está conectada a outro switch, pois roteadores, PCs, etc., não utilizam STP e, portanto, não enviam BPDUs "Hello".

Então, voltando à nossa topologia aqui, esses switches enviarão BPDUs por cada interface. Eles usam esses BPDUs para anunciar sua presença a outros switches e para obter informações sobre outros switches. Agora, para que exatamente esses BPDUs são usados

Primeiramente, os switches utilizam um campo no BPDU do STP — o campo Bridge ID — para eleger uma *root bridge* (ponte raiz) para a rede. O switch com o menor Bridge ID torna-se a *root bridge*. Falarei sobre o Bridge ID no próximo slide.

TODAS as portas da *root bridge* são colocadas em estado de encaminhamento, e os outros switches na topologia devem ter um caminho para alcançar a *root bridge*. 

Assim, como mencionei anteriormente, o STP coloca as portas em estado de bloqueio ou de encaminhamento para evitar loops de Camada 2 na rede. No entanto, como acabei de dizer, na bridge raiz, todas as portas estão no estado de encaminhamento (*forwarding*), e todos os outros switches devem ter um caminho para alcançar a bridge raiz. 

Tradicionalmente, o campo de ID da bridge no BPDU do Spanning Tree tinha este formato:

- Há um campo de prioridade da bridge (bridge priority), com 16 bits de tamanho; e

- Depois, há o endereço MAC do switch, que, como você já sabe, tem 48 bits.

A prioridade padrão da bridge é 32768 em todos os switches; portanto, por padrão, o endereço MAC é usado como critério de desempate. 

Como mencionei anteriormente, o switch com o menor ID de bridge torna-se a bridge raiz; logo, por padrão, o switch com o menor endereço MAC torna-se a bridge raiz.

Aqui está aquela topologia novamente; anotei a prioridade e o endereço MAC de cada switch. Como você sabe, endereços MAC possuem 12 dígitos hexadecimais, mas eu os reduzi para três.

Também adicionei indicadores luminosos às interfaces para mostrar se elas estão encaminhando ou bloqueando tráfego.

A interface G0/2 de cada switch está conectada a um PC; como ela não está recebendo nenhum BPDU, o switch sabe que é seguro entrar no modo de encaminhamento — não há risco de criar um loop de Camada 2 —, então essas luzes de porta estão todas verdes. 

Agora, todos os três switches têm a prioridade padrão de 32768; portanto, para saber qual deles será a bridge raiz, teremos que comparar os endereços MAC. Lembre-se: o MENOR ID de bridge vence.

Qual desses endereços MAC é o menor? Bem, o valor hexadecimal A é igual a 10, B é igual a 11 e C é igual a 12; logo, o SW1 tem o menor endereço MAC. Portanto, o SW1 se tornará a *root bridge* (ponte raiz) desta rede.

Todas as portas na *root bridge* tornam-se portas designadas, em estado de encaminhamento (*forwarding*). Esse é, então, o *Bridge ID* tradicional.

## PVST, Extended System ID

No entanto, o *Bridge ID* foi, na verdade, atualizado, isso para Switches Cisco, para ficar assim. Na realidade, a prioridade da ponte foi atualizada para consistir em duas partes: a prioridade da ponte — que tem 4 bits — e o "Extended System ID" (ID de sistema estendido), que é simplesmente o ID da VLAN, o qual possui 12 bits, pois, como você sabe, um número de VLAN tem 12 bits de comprimento.

Por que incluir um ID de VLAN na prioridade da ponte? Bem, os switches Cisco utilizam uma versão do STP chamada PVST, que significa *Per-VLAN Spanning Tree*. 

O PVST executa uma "instância" do STP separada em cada VLAN; assim, em cada VLAN, diferentes interfaces podem estar encaminhando ou bloqueando tráfego. Uma interface pode estar encaminhando na VLAN 1, mas bloqueando na VLAN 2, por exemplo.

Ao adicionar o ID da VLAN à prioridade da ponte, o switch terá um *Bridge ID* diferente em cada VLAN. Vamos analisar mais a fundo o campo de prioridade da ponte.

Você pode ter se perguntado por que 32768 é a prioridade padrão da ponte. Bem, isso ocorre porque esse campo total tem 16 bits de comprimento e o bit mais significativo é definido como 1 por padrão. 

Portanto, a prioridade padrão da ponte ERA 32768. No entanto, com a adição do *Extended System ID* — incorporando o número do ID da VLAN à prioridade da ponte —, isso mudou. Então, o ID da VLAN padrão é 1; portanto, a prioridade da bridge, no total, na verdade NÃO é 32768, é 32769. 

Na VLAN padrão 1, a prioridade da bridge padrão é, na verdade, 32769, ou seja, 32768 + 1. Agora, eis uma questão: se você quiser aumentar a prioridade da bridge do switch sem alterar os números de VLAN: qual é a unidade mínima de incremento/decremento?

A prioridade da bridge + o ID de sistema estendido formam um campo único do ID da bridge; no entanto, o ID de sistema estendido é fixo e não pode ser alterado, pois é determinado pelo ID da VLAN.

Portanto, você só pode alterar a prioridade total da bridge (ou seja, a prioridade da bridge + o ID de sistema estendido) em unidades de 4096, que é o valor do bit menos significativo da parte referente à prioridade da bridge.

Vou demonstrar. Atualmente, a prioridade da bridge aqui é 32769. Vamos reduzi-la para tornar este switch a bridge raiz. Se eu quiser reduzi-la apenas um pouco, posso reduzi-la para 28673, que é 16384 mais 8192 mais 4096 mais 1.

Eu poderia reduzi-la mais, é claro, mas o ponto principal é este: a prioridade da bridge no STP só pode ser alterada em unidades de 4096. Assim, os valores válidos que você pode configurar estão listados aqui, começando em 0 e aumentando em unidades de 4096. 

O ID de sistema estendido será então somado a esse número para compor o valor total da prioridade da bridge.

## Root Bridge

Então, vamos analisar esta topologia novamente. Vamos analisar a topologia STP para uma única VLAN, a VLAN1; portanto, a prioridade para cada switch é 32769. 

Mas, se houver múltiplas VLANs — digamos, VLAN1, VLAN2 e VLAN3 — nesta rede, a prioridade seria 32770 para a VLAN2, 32771 para a VLAN3, e assim por diante.

Também poderíamos alterar a prioridade da bridge nos switches para uma VLAN específica; assim, por exemplo, o SW1 seria a root bridge na VLAN1, o SW2 poderia ser a root bridge na VLAN2 e o SW3 poderia ser a root bridge na VLAN3. 

Falarei sobre como fazer isso no próximo vídeo; quero apenas apresentar algumas das possibilidades.

Então, aqui na VLAN1, o SW1 é a root bridge. Todas as interfaces na root bridge são portas designadas, e portas designadas estão em estado de encaminhamento (*forwarding*).

"Porta designada" é uma das funções de porta no Spanning Tree. Existem outras funções de porta; vou apresentá-las em breve.

Certo, mais alguns pontos sobre a root bridge. Quando um switch é ligado, ele assume que é a root bridge. Ele só abrirá mão dessa posição se receber um BPDU "superior" — e "superior" significa um BPDU proveniente de um switch com um Bridge ID menor.

Uma vez que a topologia tenha convergido e todos os switches concordem sobre qual é a root bridge, apenas a root bridge envia BPDUs. O motivo pelo qual todos os switches enviam BPDUs inicialmente é que todos pensam ser a root bridge.

Outros switches na rede encaminharão os BPDUs da root bridge, mas não gerarão seus próprios BPDUs originais. 

## Seleção de função de porta STP (seleção de Root Port via Root Cost)

Até agora, abordamos a primeira etapa do processo do Spanning Tree para criar LANs de Camada 2 livres de loops.

Etapa 1: o switch com o menor Bridge ID é eleito como root bridge. Todas as portas na root bridge são portas designadas (designated ports); portanto, estão em estado de encaminhamento (forwarding).

É importante que essa seja a primeira etapa realizada pelo Spanning Tree, pois as etapas seguintes dependem de saber qual switch é a root bridge.

Agora, vamos para a etapa 2. Todos os outros switches selecionarão UMA de suas portas para ser sua "root port" (porta raiz). Isso significa que há uma root port em cada switch da rede, EXCETO na root bridge.

A interface com o menor "root cost" (custo raiz) será a root port. As portas raiz também estão em estado de encaminhamento.

Agora, vamos falar sobre o que é esse "custo raiz" (root cost). 

### Root Cost - Custo Raiz

Cada interface possui um "custo" associado ao Spanning Tree.

- Uma interface Ethernet comum, com velocidade de 10 megabits por segundo, tem um custo de 100.
- A Fast Ethernet, com 100 megabits por segundo, tem um custo de 19.
- A Gigabit Ethernet tem um custo de 4, e 
- A 10 Gigabit Ethernet tem um custo de 2.

Então, estas são portas Gigabit Ethernet; logo, todas elas têm um custo de 4. O root cost é o custo total das interfaces de saída ao longo do caminho até o root bridge.

O SW1 é a root bridge, portanto, ele tem um custo de 0 em todas as interfaces.

São interfaces Gigabit Ethernet, mas não se conta o custo da interface de recepção, apenas o da interface de envio, ou seja, a interface de saída.

Assim, o SW1 anuncia seu custo de raiz (root cost) de 0 em seus BPDUs.

O SW2 receberá o BPDU e adicionará o custo de sua interface de saída, a G0/1, que é 4, ao propagar (fazer o flood de) esses BPDUs por suas interfaces. O SW3 fará o mesmo.

Então, qual porta você acha que o SW2 escolherá como sua porta raiz (root port)? Aqui está a lógica: foi anunciado um custo de 0 em sua interface G0/1; no entanto, o custo da própria interface é 4, portanto, o custo total até a raiz via G0/1 é 4.

Foi anunciado um custo de 4 na G0/0, vindo do SW3. Porém, a interface dele também tem um custo de 4, então o custo total até a raiz via G0/0 é 8. Assim, ele selecionará a G0/1 como a porta raiz.

A lógica do SW3 segue o mesmo processo. Ele tem um custo total de 4 via G0/0 e um custo total de 8 via G0/1; portanto, selecionará a G0/0 como sua root port. Nesse caso, as portas diretamente opostas a cada porta raiz pertencem à root bridge, então elas já são portas designadas. 

No entanto, lembre-se de que a porta conectada à porta raiz de outro switch DEVE ser uma porta designada. Como a porta raiz é o caminho do switch para a root bridge, outro switch não deve bloqueá-la.

Certo, então atualizei nosso resumo do spanning-tree aqui. 

- Primeiro, um switch é eleito como a *root bridge* (ponte raiz). Todas as portas na *root bridge* são portas designadas. Há apenas uma etapa na seleção da *root bridge*: trata-se do switch com o menor bried ID. 

- Em seguida, cada switch restante selecionará UMA de suas interfaces para ser sua root port, a qual também estará em estado de encaminhamento (*forwarding*). As portas opostas à porta raiz — ou seja, as portas conectadas a ela — são sempre portas designadas.

	- O primeiro critério para a seleção da root port é a porta com o menor custo de raiz (*root cost*). No entanto, e se um switch tiver várias portas com o mesmo custo de raiz?
	
	- Nesse caso, a interface conectada ao vizinho com o menor bridge ID será selecionada como a porta raiz. 
	
	- NO ENTANTO, existe MAIS UM critério de desempate que pode ser necessário para selecionar a porta raiz.
	
	- E se dois switches tiverem duas conexões entre si, de modo que tanto o custo até a raiz quanto o Bridge ID do vizinho sejam iguais? Então chegamos ao critério de desempate final: a interface conectada à interface no switch vizinho que tiver o menor Port ID se tornará a porta raiz. 

### Port ID

 Certo, deixe-me explicar brevemente o Port ID. Aqui está a saída do comando SHOW SPANNING-TREE; falaremos mais sobre isso em um vídeo futuro, quando analisarmos a configuração do Spanning Tree. 

 Quero apenas mostrar esta seção: ela lista o Port ID do Spanning Tree de cada interface no switch. Observe que o título da coluna é "Prio. Nm".

 Cada porta tem uma prioridade padrão de 128 e um número de porta exclusivo: 1 para a G0/0, 2 para a G0/1, e assim por diante neste switch. Portanto, o Port ID do STP é igual à prioridade da porta mais o número da porta. 

Assim como no ID da bridge, onde o endereço MAC é usado como critério de desempate caso as prioridades sejam iguais, neste caso, o número da porta é usado como critério de desempate se as prioridades forem iguais.

Não vou me aprofundar mais na explicação sobre o ID da porta; geralmente, você não precisa se preocupar com isso nem alterá-lo, então pode focar apenas no número da porta. Por exemplo, G0/0 é menor que G1/0, ou G0/3 é menor que G1/2.
