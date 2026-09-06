---
tags:
  - arquivo
---
## High availability

O termo "alta disponibilidade" descreve sistemas concebidos para evitar períodos de inatividade. A disponibilidade contínua de sistemas de informação é imprescindível, não só para as empresas, mas para a vida moderna, já que todos nós usamos e dependemos de computadores e sistemas de informação mais do que nunca.

Sistemas de alta disponibilidade normalmente incluem estes três princípios de projeto.

- *Eliminar pontos únicos de falha*

	O primeiro princípio que define os sistemas de alta disponibilidade começa com a identificação de todos os dispositivos e componentes do sistema cuja falha resultaria em falha em todo o sistema. Os métodos para eliminação de pontos únicos de falhas incluem dispositivos de *hot standby*, componentes redundantes e várias conexões ou caminhos.


> [!NOTE] 
> *Hot Standby*
> 
> O Hot Standby é uma estratégia de redundância utilizada em sistemas de computadores e redes para garantir a disponibilidade contínua de serviços e minimizar o tempo de inatividade em caso de falhas. Essa técnica consiste em manter um sistema de backup, chamado de standby, que está sempre pronto para assumir as funções do sistema principal caso ocorra algum problema.
> 
> *Como funciona o Hot Standby?*
> 
> No Hot Standby, o sistema principal e o standby estão conectados e sincronizados em tempo real. O standby monitora constantemente o sistema principal e mantém uma cópia atualizada de todos os dados e configurações. Dessa forma, caso o sistema principal falhe, o standby pode assumir imediatamente as operações sem interrupções significativas.
> 
> Para garantir a sincronização contínua, o standby recebe atualizações constantes do sistema principal. Isso pode ser feito por meio de replicação de dados, onde as alterações feitas no sistema principal são automaticamente replicadas no standby, ou por meio de um sistema de espelhamento, onde todas as operações realizadas no sistema principal são simultaneamente executadas no standby.


- *Fornecer transição confiável*

	Fontes de alimentação redundantes, sistemas de energia de backup e sistemas de comunicação de backup proporcionam transição confiável.

- *Detectar falhas à medida que ocorrem*

	O monitoramento ativo do dispositivo e do sistema detecta vários tipos de eventos, incluindo falhas do dispositivo e do sistema. Os sistemas de monitoramento podem até acionar o sistema de backup em caso de falha.

À medida que as redes evoluem, aprendemos que há quatro características básicas que os arquitetos de rede devem atender para corresponder às expectativas do usuário:

- Tolerância a falhas;
- Escalabilidade;
- Qualidade de serviço — *`QoS`*;
- Segurança.

---
## Fault Tolerance

Uma rede tolerante a falhas é aquela que limita o número de dispositivos afetados durante uma falha. Ela foi desenvolvida para permitir uma recuperação rápida quando ocorre uma falha. 

Essas redes dependem de vários caminhos entre a origem e o destino de uma mensagem. Se um caminho falhar, as mensagens serão instantaneamente enviadas por um link diferente. Ter vários caminhos para um destino é conhecido como *redundância*.

A implementação de uma *rede comutada por pacotes* é uma das maneiras pelas quais redes confiáveis *fornecem redundância*. A comutação de pacotes divide os dados do tráfego em pacotes que são roteados por uma rede compartilhada. Uma única mensagem, como um e-mail ou stream de vídeo, é dividido em vários blocos, chamados pacotes. 

Cada pacote tem as informações de endereço necessárias da origem e do destino da mensagem. Os roteadores na rede alternam os pacotes com base na condição da rede no momento. Isso significa que todos os pacotes em uma única mensagem podem seguir caminhos muito diferentes para o mesmo destino.

- *Boas práticas*:

	- *Redundância*: Implementar caminhos alternativos e dispositivos redundantes para garantir que o tráfego possa ser redirecionado em caso de falha.

	- *Monitoramento Contínuo*: Utilizar ferramentas de monitoramento para detectar falhas rapidamente e acionar mecanismos de recuperação.

	- *Planos de Recuperação*: Ter um plano de recuperação de desastres documentado e testado regularmente.

---
## Scalability

Uma rede escalável se expande rapidamente para oferecer suporte a novos usuários e aplicativos. Ela faz isso sem degradar o desempenho dos serviços que estão sendo acessados por usuários existentes. 

As redes são escaláveis porque os projetistas seguem padrões e protocolos aceitos. Isso permite que os fornecedores de software e hardware se concentrem em melhorar produtos e serviços sem precisar criar um novo conjunto de regras para operar na rede.

---
### Quality of Service

A *Quality of Service* — *`QoS`* — é um requisito crescente das redes atualmente. Novos aplicativos disponíveis para usuários em redes, como transmissões de voz e vídeo ao vivo, criam expectativas mais altas em relação à qualidade dos serviços entregues. 

O *`QoS`* se torna um mecanismo essencial para gerenciar os congestionamentos e garantir a entrega confiável do conteúdo para todos os usuários.

O congestionamento acontece quando a demanda por largura de banda excede a quantidade disponível. A largura de banda é medida pelo número de bits que podem ser transmitidos em um único segundo, ou bits por segundo — bps. 

Ao tentar uma comunicação simultânea pela rede, a demanda pela largura de banda pode exceder sua disponibilidade, criando um congestionamento na rede.

Quando o volume de tráfego é maior do que o que pode ser transportado pela rede, os dispositivos retêm os pacotes na memória até que os recursos estejam disponíveis para transmiti-los. 

Com uma política de *`QoS`* configurada, o roteador é capaz de gerenciar o fluxo do tráfego, priorizando certas comunicações se a rede ficar congestionada. O foco do *`QoS`* é priorizar o tráfego sensível ao tempo. O tipo de tráfego, e não o conteúdo, é o que é importante.

---
## Network security

A infraestrutura da rede, os serviços e os dados contidos nos dispositivos conectados à rede são recursos pessoais e comerciais críticos. Os administradores de rede devem abordar dois tipos de preocupações de segurança de rede: segurança da infraestrutura de rede e segurança da informação.

Proteger a infraestrutura de rede inclui proteger fisicamente os dispositivos que fornecem conectividade de rede e impedir o acesso não autorizado ao software de gerenciamento que reside neles.

Os administradores de rede também devem proteger as informações contidas nos pacotes transmitidos pela rede e as informações armazenadas nos dispositivos conectados à rede. Para atingir os objetivos de segurança de rede, existem três requisitos principais.

- *Confidencialidade*;
- *Integridade*;
- *Disponibilidade*.

---
## They are not the only ones...

As quatro características básicas mencionadas — *tolerância a falhas, escalabilidade, qualidade de serviço e segurança* — são fundamentais para o design de redes eficazes, mas não são as únicas. 

Existem outras características e considerações que também podem ser relevantes dependendo do contexto e das necessidades específicas de uma rede. Algumas dessas características adicionais incluem:

- *Gerenciamento de Rede*: A capacidade de monitorar e gerenciar a rede de forma eficaz, garantindo que problemas possam ser identificados e resolvidos rapidamente.

- *Interoperabilidade*: A habilidade de diferentes sistemas e dispositivos trabalharem juntos em uma rede, independentemente de suas plataformas ou fabricantes.

- *Desempenho*: Refere-se à eficiência geral da rede em termos de latência, largura de banda e throughput.

- *Flexibilidade*: A capacidade da rede de se adaptar a novas tecnologias ou mudanças nas demandas dos usuários.

---
## Rules and Regulations

Além disso, existem várias normas e regulamentações que orientam as práticas relacionadas a essas características:

- *ISO/IEC 27001*: Norma internacional para gestão da segurança da informação, que fornece requisitos para estabelecer, implementar, manter e melhorar um sistema de gestão da segurança da informação — SGSI.

- *NIST SP 800 Series*: Publicações do *Instituto Nacional de Padrões e Tecnologia* dos EUA que fornecem diretrizes sobre segurança cibernética, incluindo gerenciamento de risco e proteção da informação.

- *IEEE 802.1Q*: Padrão que define a implementação do VLAN tagging em redes Ethernet, importante para *`QoS`*.

- *ITIL — Information Technology Infrastructure Library*: Um conjunto de práticas para gerenciamento de serviços de TI que inclui diretrizes sobre gerenciamento de incidentes, problemas e mudanças.

---
## The Five Nines

Toda empresa quer poder operar ininterruptamente, mesmo em condições extremas, como durante um ataque.

Dentre as práticas mais populares de alta disponibilidade estão os *`Five Nines`*. Ela recebe esse nome pelo objetivo de atingir uma taxa de disponibilidade de *99,999%*, ou seja, cinco noves em seguida. Isso significa que o período de inatividade é menos de 5,26 minutos por ano.


- *Sistemas padronizados*

	A padronização dos sistemas propicia que os sistemas usem os mesmos componentes. Os inventários de peças são mais fáceis de manter, e é possível trocar componentes durante uma emergência.

	Nas instalações com sistema de informação altamente seguro, guardas controlam o acesso a áreas confidenciais da empresa. O benefício do uso de guardas é que eles podem se adaptar mais do que sistemas automatizados. Guardas podem aprender e distinguir muitas condições e situações diferentes e tomar decisões imediatamente.

- *Clustering*

	*Clusters* de vários dispositivos agrupados proporcionam um serviço que parece ser uma única entidade para um usuário. Se um dispositivo falhar, os outros dispositivos permanecem disponíveis.

- *Sistemas de componente compartilhado*

	Os sistemas são criados para que um sistema completo possa substituir um que falhou.

---
## N + 1 redundancy

A redundância N+1 garante a disponibilidade do sistema, no caso de falha de um componente. Os componentes — N —  precisam ter, no mínimo, um componente de backup — +1 .

Uma boa maneira de pensar sobre isso é que, no caso de um piso plano, um carro tem quatro pneus — N —  e um sobressalente — +1 —  no porta-malas.

Embora um sistema N + 1 contenha equipamento redundante, não é um sistema totalmente redundante.

Em um data center, a redundância N + 1 significa que o design do sistema pode suportar a perda de um componente.

Por exemplo, um data center inclui servidores, fontes de alimentação, switches e roteadores. A redundância de N + 1 em um data center que consiste nos elementos acima significa que temos um servidor, uma fonte de alimentação, um switch e um roteador em standby, prontos para entrar em linha se algo acontecer com o servidor principal, a fonte de alimentação principal, switch ou roteador.

---
## RAID

![[RAID.png]]

#### How does it work?

O RAID é uma tecnologia usada para aumentar o desempenho e/ou a confiabilidade do armazenamento de dados. 

A abreviatura significa *`Redundant Array of Inexpensive Disks — Conjunto Redundante de Discos Baratos`*. Com o tempo, numa tentativa de dissociar o conceito de "discos baratos", a indústria reviu o acrônimo para *`Redundant Array of Independent Disks — Conjunto Redundante de Discos Independentes`*.

Um sistema RAID consiste em duas ou mais unidades trabalhando em paralelo. Estes discos podem ser discos rígidos, mas há uma tendência para também usar a tecnologia para SSD (drives de estado sólido). 

O RAID oferece segurança e confiabilidade por meio da adição de redundância. Se um disco falhar, o outro continua funcionando normalmente e o usuário nem percebe diferença. O administrador é avisado pelo sistema e substitui o disco que falhou. 

Apesar disso, o RAID não protege contra *falhas de energia* ou *erros de operação* ou contra a *falha simultânea dos dois discos*. Falhas de energia, código errado de núcleo ou erros operacionais podem danificar os dados de forma irrecuperável. *Por este motivo, mesmo usando-se o RAID não se dispensa a tradicional cópia de backup*.

Existem diferentes níveis de RAID, cada um otimizado para uma situação específica. Estes não são padronizados por um grupo de indústria ou comitê de padronização. E isso explica por que as empresas às vezes vêm com seus próprios números únicos e implementações próprias. Segue alguns tipos de RAID:

- RAID 0 — striping;
- RAID 1 — espelhamento;
- RAID 5 — distribuição com paridade;
- RAID 6 — distribuição com paridade dupla;
- RAID 10 — combinando espelhamento e striping.

O software para executar a funcionalidade RAID e controlar as unidades pode ser localizado em uma placa controladora separada (um controlador RAID de hardware) ou pode ser simplesmente um driver. 

No tipo de implementação por *software*, todo o processamento necessário para o gerenciamento do RAID é feito pela CPU. Toda movimentação de dados (leitura e escrita) é feita por uma camada de software que faz a abstração entre a operação lógica (RAID) e os discos físicos, e é controlada pelo sistema operacional.

> *Algumas versões do Windows, como o Windows Server 2012, bem como o Mac OS X, incluem funcionalidade RAID de software. Controladores RAID de hardware custam mais do que software puro, mas também oferecem melhor desempenho, especialmente com RAID 5 e 6.*

Sistemas RAID podem ser usados com várias interfaces, incluindo SCSI, IDE, SATA ou FC — Fiber chanel. Existem sistemas que usam discos SATA internamente, mas que possuem uma interface FireWire ou SCSI para o sistema host.


> [!NOTE] Falso RAID
> A implementação via software geralmente não possui uma fácil configuração. Já na implementação via hardware as controladoras tem um preço muito elevado. Então foi criada uma "controladora barata" que em vez de um chip controlador RAID você utiliza uma combinação de funções especiais na BIOS da placa e drivers instalados no sistema operacional.


Às vezes, os discos em um sistema de armazenamento são definidos como JBOD, que significa *`Just a Bunch Of Disks`*. Isso significa que esses discos não usam um nível RAID específico e atuam como discos autônomos. Isso geralmente é feito para unidades que contêm arquivos de swap ou dados de spool.

Abaixo está uma visão geral dos níveis de RAID mais populares:

#### RAID 0 — Striping

![[raid_0.png]]

No *`striping`*, ou distribuição, os dados são subdivididos em segmentos consecutivos — *`stripes`*, ou faixas — que são escritos sequencialmente através de cada um dos discos de um array.

Usando vários discos — pelo menos 2 — ao mesmo tempo, isso oferece desempenho superior de I/O. Este desempenho pode ser melhorado ainda mais usando vários controladores, idealmente um controlador por disco.

- *Vantagens*

	O RAID 0 oferece ótimo desempenho, tanto em operações de leitura quanto de gravação. Não há sobrecarga causada por controles de paridade.

	Toda a capacidade de armazenamento é usada, e não há sobrecarga. Além disso, a tecnologia é fácil de implementar.

- *Desvantagens*

	O RAID 0 não é tolerante a falhas. Se uma unidade falhar, todos os dados na matriz RAID 0 se tornarão inutéis por terem um pedaçinho faltando. Portanto, ele não deve ser usado para sistemas de missão crítica.

	O RAID 0 não só não garante a tolerância a falhas, mas aumenta as suas chances de acontecerem. Pois, a fracionar os dados e coloca-los em discos diferentes, no caso de um dos discos falharem, os dados nos demais discos se tornarão inúteis. *A única razão para usá-lo é a sua velocidade, porque, quando temos 2 controladores funcionando ao invés de 1 só, o acesso aos dados é muito mais rápido.*

#### RAID 1 — Espelhamento

![[raid_1.png]]
Os dados são armazenados duas vezes, gravando-os tanto na unidade de dados quanto na unidade espelhada. 

Se uma unidade falhar, o controlador usa a unidade de dados ou a unidade espelhada para recuperação de dados e continua a operação.

- *Vantagens*

	O RAID 1 oferece uma excelente velocidade de leitura e uma velocidade de gravação que é comparável à de uma única unidade.

- *Desvantagens*

	A principal desvantagem é que a capacidade de armazenamento eficaz é apenas metade da capacidade total da unidade porque todos os dados são escritos duas vezes.

	Soluções RAID 1 de software nem sempre permitem a troca a quente de uma unidade com falha. Isso significa que a unidade com falha só pode ser substituída após desligar o computador ao qual ele está conectado. Para servidores que são usados simultaneamente por muitas pessoas, isso pode não ser aceitável. Esses sistemas normalmente usam controladores de hardware que suportam hot swapping.

#### RAID 5

![[raid_5.png]]

RAID 5 é o nível RAID seguro mais comum. Ele requer pelo menos 3 unidades, mas pode trabalhar com até 16. 

Os blocos de dados são listados através das unidades e em uma unidade uma *soma de verificação de paridade* de todos os dados do bloco é escrito. Os dados de paridade não são gravados em uma unidade fixa, eles são espalhados por todas as unidades, como mostra o desenho. 

Usando os dados de paridade, o computador pode recalcular os dados de um dos outros blocos de dados, caso esses dados não estejam mais disponíveis. Isso significa que uma matriz RAID 5 pode resistir a uma única falha de unidade sem perder dados ou acessar dados. 

Embora RAID 5 pode ser alcançado em software, um controlador de hardware é recomendado. Muitas vezes memória cache adicional é usada nesses controladores para melhorar o desempenho de gravação.

- *Vantagens*

	As transações de dados de leitura são muito rápidas enquanto as transações de dados de gravação são um pouco mais lentas — devido à paridade que deve ser calculada.

	Se uma unidade falhar, você ainda terá acesso a todos os dados, mesmo quando a unidade com falha está sendo substituída e o controlador de armazenamento reconstrói os dados na nova unidade.

- *Desvantagens*

	As falhas de unidade têm um efeito na taxa de transferência, embora isso ainda seja aceitável. Esta é uma tecnologia complexa. 

	Se um dos discos em uma matriz usando discos 4TB falhar e for substituído, restaurar os dados — o tempo de reconstrução — pode levar um dia ou mais, dependendo da carga na matriz e a velocidade do controlador. Se outro disco ficar ruim durante esse tempo, os dados serão perdidos para sempre.

#### RAID 6 — Striping com paridade dupla

RAID 6 é como RAID 5, mas os dados de paridade são gravados em duas unidades. Isso significa que requer pelo menos 4 unidades e pode suportar 2 drives morrendo simultaneamente. As chances de que duas unidades quebram exatamente no mesmo momento são, naturalmente, muito pequenas. 

No entanto, se uma unidade de um sistema RAID 5 morrer e for substituída por uma nova, demora horas ou até mais do que um dia para reconstruir a unidade trocada. Se outra unidade morrer durante esse tempo, você ainda perderá todos os seus dados. Com o RAID 6, o array RAID ainda sobreviverá a essa segunda falha.

- *Vantagens*

	Como com o RAID 5, as transações de dados de leitura são muito rápidas.

	Se duas unidades falharem, você ainda terá acesso a todos os dados, mesmo quando as unidades com falha estão sendo substituídas. Assim, o RAID 6 é mais seguro que o RAID 5.

- *Desvantagens*

	As transações de dados de gravação são mais lentas que o RAID 5 devido aos dados de paridade adicionais que devem ser calculados. Em um relatório eu li o desempenho de gravação foi 20% menor.

	As falhas de unidade têm um efeito na taxa de transferência, embora isso ainda seja aceitável. Esta é uma tecnologia complexa. Reconstruir uma matriz em que uma unidade falhou pode demorar muito tempo.

- *Uso ideal*

	RAID 6 é um bom sistema completo que combina armazenamento eficiente com excelente segurança e desempenho decente. É preferível ao RAID 5 em servidores de arquivos e aplicativos que usam muitas unidades grandes para armazenamento de dados.

#### RAID 10 — RAID 1 + 0

![[raid_10.png]]

É possível combinar as vantagens — e desvantagens — de RAID 0 e RAID 1 em um único sistema. Esta é uma configuração de RAID aninhada ou híbrida.

- *Vantagens*

	Se algo der errado com um dos discos em uma configuração RAID 10, o tempo de reconstrução é muito rápido, pois tudo o que é necessário é copiar todos os dados do espelho sobrevivente para uma nova unidade.

- *Desvantagens*

	Metade da capacidade de armazenamento vai para espelhamento, por isso em comparação com grande RAID 5 ou RAID 6 arrays, esta é uma maneira cara de ter redundância.

#### RAID 50 — RAID 5 + 0

![[raid_50.png]]

O RAID 50, também conhecido como RAID 5 + 0, combina a *paridade distribuída* — RAID 5 — com *striping* — RAID 0. Requer um mínimo de seis unidades . Esse nível de RAID oferece melhor desempenho de gravação, maior proteção de dados e recriações mais rápidas do que o RAID 5. 

O desempenho não diminui tanto quanto em um array RAID 5, porque uma única falha afeta apenas um array. Até quatro falhas de unidade podem ser superadas, desde que cada unidade com falha ocorra em um array RAID 5 diferente.

E quanto aos níveis RAID 2, 3, 4 e 7?

Esses níveis existem, mas não são comuns — RAID 3 é essencialmente como RAID 5, mas com os dados de paridade sempre gravados na mesma unidade.


> [!NOTE] RAID NÃO é substituto para back-up!
> 
> Todos os níveis de RAID exceto o RAID 0 oferecem proteção contra uma única falha de unidade. Um sistema RAID 6 ainda sobrevive a danificação de 2 discos simultaneamente. Para uma segurança completa, você ainda precisa fazer backup dos dados de um sistema RAID.
> 
> Esse backup será útil se todas as unidades falharem simultaneamente por causa de um pico de energia.
> 
> É uma salvaguarda quando o sistema de armazenamento é roubado.
> 
> Os back-ups podem ser mantidos fora do local em um local diferente. Isso pode ser útil se um desastre natural ou incêndio destrói seu local de trabalho.
> 
> O motivo mais importante para fazer backup de várias gerações de dados é o erro do usuário. Se alguém excluir acidentalmente alguns dados importantes e isso passar despercebido por várias horas, dias ou semanas, um bom conjunto de backups garante que você ainda pode recuperar esses arquivos

#### Data storage

Uma solução RAID pode ser baseada em software ou hardware. Uma solução baseada em hardware requer um controlador de hardware especializado, no sistema que contenha as unidades RAID.

Os termos a seguir descrevem as várias maneiras pelas quais o RAID pode armazenar dados na matriz de discos.

- *`Mirroring`* - Armazena dados duplicados em uma segunda unidade.
- *`Distribution`* - Grava dados em várias unidades para que segmentos consecutivos sejam armazenados em unidades diferentes.
- *`Parity`* - mais precisamente, tirar a paridade. Após a distribuição, as somas de verificação são geradas para verificar se não há erros nos dados distribuídos. Essas somas de verificação são armazenadas em uma terceira unidade.

Existem outras arquiteturas RAID, que combinam principalmente os elementos acima.

---
## Spanning Tree

A redundância aumenta a disponibilidade da infraestrutura da rede, protegendo-a de um ponto único de falha, como um cabo ou um switch com falha na rede.

Quando os designers projetam a redundância física em uma rede, pode haver loops e quadros duplicados. Os loops e quadros duplicados têm consequências graves para uma rede comutada.

O *`Spanning Tree Protocol`* — `STP` —  soluciona esses problemas. A função básica do STP é prevenir loops em uma rede, quando os switches se interconectarem por vários caminhos. O STP garante que os links físicos redundantes estejam livres de loop e que apenas um caminho lógico seja executado entre todos os destinos na rede. *Em resumo, STP bloqueia intencionalmente os caminhos redundantes que poderiam provocar um loop*.

Bloquear os caminhos redundantes é fundamental para evitar loops na rede. Os caminhos físicos ainda existirão para fornecer redundância, mas o STP desativa esses caminhos, de maneira lógica, para evitar que ocorram loops. Se um cabo ou switch da rede falhar, o STP recalculará os caminhos e desbloqueará as portas necessárias, para permitir que o caminho redundante se torne ativo.

1. O PC1 envia uma transmissão para a rede.
2. O trunk link entre S2 e S1 falha, resultando em interrupção do caminho original.
3. O S2 desbloqueia a porta anteriormente bloqueada do Tronco 2 e permite que o tráfego de broadcast siga o caminho alternativo na rede, permitindo que a comunicação continue.
4. Se o link entre S2 e S1 voltar a funcionar, o STP bloqueará novamente o link entre S2 e S3.
 

 ![[STP.png]]

---
## Router redundancy

O gateway padrão é normalmente o roteador que proporciona acesso dos dispositivos ao resto da rede ou à Internet. Se houver somente um roteador como gateway padrão, é um ponto único de falha. A empresa pode escolher instalar um roteador de standby adicional.

O roteador de encaminhamento e o roteador standby usam um protocolo de redundância para determinar qual roteador deve assumir o papel ativo na redundância. Cada roteador está configurado com um endereço IP físico e um endereço IP do roteador virtual. Dispositivos finais usam o endereço IP virtual como o gateway padrão.
![[1_router_redundancy.png]]

O roteador de encaminhamento e o roteador standby usam seus endereços IP físicos para trocar mensagens periódicas. O objetivo dessas mensagens é ter certeza de que os dois ainda estão on-line e disponíveis.

Se o roteador em espera parar de receber essas mensagens periódicas do roteador de encaminhamento, ele perceberá que é o único roteador disponível e assumirá a função de encaminhamento. 

Enquanto isso, como os PCs na rede ainda se comunicam com o roteador virtual em 192.0.2.100, eles permanecem on-line apesar de tudo o que aconteceu, já que o roteador virtual agora encaminha para o que era anteriormente o roteador de espera.

![[2_router_redundancy.png]]

A capacidade de uma rede de se recuperar dinamicamente da falha de um dispositivo que atua como um gateway padrão é conhecida como *`first hop redundancy`*.

O *`Virtual Redundancy Router Protocol`* — *`VRRP`* — é um protocolo de rede de computadores que permite a atribuição automática de roteadores IP disponíveis aos hosts participantes. Isso aumenta a disponibilidade e a confiabilidade dos caminhos de roteamento por meio de seleções automáticas do gateway padrão em uma sub-rede IP.

O protocolo consegue isso por meio da *criação de roteadores virtuais*, que são uma *representação abstrata de múltiplos roteadores*, ou seja, roteadores primários/ativos e secundários/em espera, atuando como um grupo. 

O roteador virtual é designado para atuar como um gateway padrão dos hosts participantes, em vez de um roteador físico. Se o roteador físico que está roteando pacotes em nome do roteador virtual falhar, outro roteador físico é selecionado para substituí-lo automaticamente. 

O roteador físico que está encaminhando pacotes em um determinado momento é chamado de roteador primário/ativo.

O *`VRRP`* fornece informações sobre o estado de um roteador, não sobre as rotas processadas e trocadas por ele. Além disso, cada instância de *`VRRP`* é limitada, em escopo, a uma única sub-rede. 

Ele não anuncia rotas IP além dessa sub-rede nem afeta a tabela de roteamento de forma alguma. O *`VRRP`* pode ser usado em redes Ethernet, MPLS e Token Ring com IPv4, bem como IPv6.

---
## Site redundancy

Uma empresa pode precisar pensar em redundância de local, dependendo de suas necessidades.

- *Synchronous replication*

	- Sincroniza os dois locais em tempo real;
	- Requer alta largura de banda;
	- Os locais devem ser próximos um do outro, para reduzir a latência.

- *Asynchronous replication*

	- Não sincronizados em tempo real, mas muito próximo disso;
	- Requer menos largura de banda;
	- Os sites podem estar mais distantes, pois a latência é o menor dos problemas.

- Point-in-time-Replication

	- Atualiza periodicamente a localização dos dados de backup;
	- Mais conservador em termos de largura de banda, pois não exige uma conexão constante.

O equilíbrio correto entre custo e disponibilidade determinará a escolha correta para uma empresa.

---
## Resilient design

Resiliência representa os métodos e configurações usados para tornarem um sistema ou rede tolerante a falhas.

- Exemplos:

	Uma rede pode ter links redundantes entre switches que executam o STP. Embora o STP proporcione um caminho alternativo pela rede se o link falhar, a transição pode não ser imediata, se a configuração não for ideal.

	Os protocolos de roteamento também proporcionam resiliência, mas o ajuste fino pode melhorar a transição, para que os usuários da rede não percebam. Os administradores devem investigar as configurações não padrão em uma rede de testes, para ver se podem melhorar os tempos de recuperação em uma rede.

	Como visto nos exemplos acima, o design resiliente é mais do que apenas adicionar redundância. É fundamental entender as necessidades comerciais da empresa e, em seguida, incorporar a redundância para criar uma rede resiliente.

	- *Application Resilience*:
	
		Resiliência de aplicativo é a capacidade do aplicativo reagir a problemas em um de seus componentes sem parar de funcionar. Um administrador precisará, eventualmente, desativar aplicativos para aplicações de patches, atualizações de versão ou para implantar novas funcionalidades.

		Alcançar a resiliência da infraestrutura de aplicativos significa evitar a perda de clientes, de funcionários ou de negócios devido a uma falha de aplicativo.

		Temos três soluções de disponibilidade para abordar a resiliência de aplicativos. À medida que o fator de disponibilidade de cada solução aumenta, a complexidade e os custos também aumentam.

		- *Hardware tolerante a falhas* — mais complexo e mais caro —  é um sistema projetado com a colocação de múltiplos componentes essenciais em um mesmo computador.  

		- Arquitetura de cluster é um grupo de servidores que funcionam como se fossem um único sistema.

		- Backup e restauração Cópias de backup de arquivos com a finalidade de poder restaurá-los se ocorrer perda de dados — menos complexo e menos caro .

	- *Resiliência do IOS*
	
		O IOS — Interwork Operating System, Sistema operacional Interwork —  para roteadores e switches Cisco incluem um atributo resiliente de configuração. Permite recuperação mais rápida se alguém, intencionalmente ou não, reformatar a memória flash ou apagar o arquivo de configuração de inicialização. 

		Este atributo mantém uma cópia de trabalho segura do arquivo de imagem do IOS do roteador e uma cópia do arquivo de configuração de execução. O usuário não pode remover esses arquivos seguros, também conhecidos como o bootset primário.

		Os comandos mostrados na figura protegem o arquivo de imagem IOS e o arquivo de configuração em execução.

---
## System and data backups

Uma empresa pode perder dados se os criminosos digitais o roubarem, se o equipamento falhar, ou se ocorrer um desastre ou outro erro, então é importante fazer backup dos dados regularmente.

Um backup dos dados armazena uma cópia das informações de um computador na mídia de backup removível. Quando essa mídia é removível, o operador armazena essa mídia de backup em um local seguro.

Fazer backup de dados é uma das formas mais eficazes de proteção contra perda de dados. Se houver falha no hardware do computador, o usuário pode restaurar os dados do backup, depois que o sistema estiver funcional.

Uma política de segurança sólida deve incluir backups de dados regulares. Os backups de dados são, normalmente, armazenados em outro local, para proteger a mídia de backup, se algo acontecer com a instalação principal.

- Frequency:

	Os backups podem levar muito tempo. Às vezes é mais fácil fazer um backup completo mensal ou semanal, e depois backups parciais frequentes de todos os dados que tiverem mudado, desde o último backup completo. No entanto, ter muitos backup parciais aumenta o tempo necessário para restaurar os dados.

- Storage:

	Para segurança adicional, os backups devem ser transportados para um local de armazenamento externo aprovado em uma rotação diária, semanal ou mensal, conforme estipulado pela política de segurança.

- Security:

	Proteja os backups com senhas. Em seguida, o operador digita a senha, antes de restaurar os dados na mídia de backup.

- Validation:

	Valide sempre os backups para garantir a integridade dos dados e

---
## Design a high availability system

A alta disponibilidade incorpora três grandes princípios para atingir a meta de acesso ininterrupto aos dados e serviços:

#### Elimination or reduction of single points of failure

É importante compreender as maneiras de abordar um ponto único de falha. Um ponto único de falha pode incluir roteadores centrais ou switches, serviços de rede e, até mesmo, uma equipe de TI altamente qualificada.

O que torna esses pontos únicos de falha é o fato de que uma perda ou falha desse sistema, processo ou pessoa teria um impacto muito disruptivo em todo o sistema, o que deve ser evitado. A chave é ter processos, recursos e componentes que reduzam os pontos únicos de falha.

Clusters de alta disponibilidade é uma maneira de proporcionar redundância. Esses clusters consistem em um grupo de computadores que têm acesso ao mesmo armazenamento compartilhado e têm configurações de rede idênticas. 

Todos os servidores participam no processamento de um serviço simultaneamente. Se um servidor dentro do cluster falhar, os outros servidores continuarão a processar o mesmo serviço que o dispositivo com falha.

#### Fault tolerance

Tolerância a falhas permite que um sistema continue funcionando, se um ou mais componentes falharem. Espelhamento de dados é um exemplo de tolerância a falhas. 

Se ocorrer uma "falha", causando interrupção de um dispositivo, como um controlador de disco, o sistema espelhado proporcionará os dados solicitados sem interrupção aparente no serviço para o usuário.

#### System resilience

Resiliência de sistemas refere-se à capacidade de manter a disponibilidade de dados e de processamento operacional, apesar de ataques ou de eventos de interrupção. 

Geralmente, isso requer sistemas redundantes, em termos de energia e de processamento, para que, se um sistema falhar, o outro possa assumir as operações, sem nenhuma interrupção no serviço. 

Resiliência do sistema é mais do que a blindagem de dispositivos. Requer que os dados e serviços estejam disponíveis, mesmo quando sob ataque.





