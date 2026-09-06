---
tags:
  - arquivo
---
##### O que é?

**Rede mesh**, ou **rede de malha**, é uma alternativa de protocolo ao padrão 802.11 para diretrizes de tráfego de [dados] e [voz] além das [redes a cabo] ou infraestrutura [wireless].

Uma rede de infraestrutura é composta de AP's ([Access point] - Ponto de acesso) e clientes, os quais necessariamente devem utilizar aquele AP para trafegarem em uma rede. Uma rede _mesh_ é composta de vários [nós]/[roteadores], que passam a se comportar como uma única e grande rede, possibilitando que o cliente se conecte em qualquer um destes nós. 

Os nós têm a função de repetidores e cada nó está conectado a um ou mais dos outros nós. Desta maneira é possível transmitir mensagens de um nó a outro por diferentes caminhos. Já existem redes com cerca de 500 nós e mais de 400.000 usuários operando.

Redes do tipo _mesh_ possuem a desvantagem de possuir um alto custo, contudo têm a vantagem de serem redes de fácil implantação e bastante tolerantes a falhas. A esta característica tem-se dado o nome de "resiliência".

Nessas redes, roteadores sem fio são geralmente instalados no topo de edifícios e comunicam-se entre si usando protocolos como o [OLSR] em modo [ad hoc] através de múltiplos saltos de forma a encaminhar pacotes de dados aos seus destinos. 

Usuários nos edifícios podem se conectar à rede mesh de forma cabeada, em geral via [Ethernet], através de redes 802.11. 

Quando estiverem 100% definidos os parâmetros para padronização do protocolo mesh pelo [IEEE], este protocolo será denominado padrão 802.11s.

---
##### Funcionamento

O segredo do sistema mesh está no [protocolo de roteamento], que faz a varredura das diversas possibilidades de rotas de fluxo de dados, com base numa tabela dinâmica, onde o equipamento [seleciona qual a rota mais eficiente a seguir] para chegar ao seu objetivo, levando em conta a maior rapidez, com menor perda de pacotes, ou o acesso mais rápido à [Internet], além de outros. 

Esta varredura é feita diversas vezes por segundo ou intervalo de tempo, sendo transparente ao usuário mesmo quando ocorre alteração de rota de acesso aos gateways, que são os nós que possuem acesso direto à internet. Por exemplo, quando o nó que estava sendo utilizado para de funcionar, o sistema se rearranja automaticamente, desviando o nó defeituoso, sem que usuário perceba ou perca a conexão.

Outra característica importante das redes mesh é o [roaming], também conhecido como "fast hand-off", característica das redes que [permitem ao usuário o trânsito entre nós da rede sem perder a conexão no momento da troca]. A consequência prática é a mobilidade geográfica que o sistema permite.

Outro ponto interessante é que [apenas um ou mais destes nós precisam estar conectados à Internet]. Os outros precisam apenas de alimentação de energia. O sistema sempre saberá quais saltos serão necessários para que a requisição de um cliente em qualquer ponto da rede chegue da forma mais eficiente possível à Internet.

Devido às características da topologia em malha, pode-se dizer que a mesma [consiste em uma rede ad-hoc], sendo normalmente empregada em redes _wireless_. 

Na ad-hoc, [cada nó opera como um roteador, recebendo um pacote e encontrando o melhor caminho dentro da rede] para alcançar o destino. Como consequência desta propriedade, as redes ad-hoc possuem a habilidade de se auto-organizar, nesse sentido, caso aconteça uma falha em um dos nós da rede, a mesma continuará operando ao encontrar uma nova configuração para manter sua operacionalidade.

---
##### Aplicações Industriais

As redes do tipo _mesh_ também possuem um interessante campo de aplicação que são as redes sem fio para monitoramento e controle de variáveis na área industrial. Um ambiente industrial, assim como uma área urbana, possui uma arquitetura complexa, com muitos obstáculos fixos ou móveis que, dependendo da aplicação, dificultam ou inviabilizam a aplicação de enlaces sem fio tradicionais, quer sejam baseados do IEEE 802.11 ou proprietários.

Com o advento das redes _mesh_ e a sua característica principal de roteamento dinâmico, autor-recuperação da rede em caso de perda de algum equipamento, algumas aplicações industriais puderam ser viabilizadas, tornando possível o monitoramento e controle de variáveis ao longo de uma planta industrial.

---
##### Redes mesh off-line

São redes mesh com a mesma característica de funcionamento da anterior, porém [sem acesso à internet]. Com propósitos de utilização do sistema de roaming e agilidade de implantação, foi utilizada, por exemplo, na guerra do golfo, onde os nós eram os veículos de combate, que se comunicavam e permitiam que informações trafegassem através de distâncias muito maiores.

Também em campo de guerra, foram criadas redes mesh instantâneas, com pequenos nós alimentados por baterias, inclusos em pequenas cápsulas estanques, e que eram jogados a partir de aviões e entravam em funcionamento tão logo se comunicavam com os nós vizinhos.

---
##### Problemas

O grande problema das redes mesh hoje consiste no [excesso de informações sobre o roteamento que deve ser transportado junto com os pacotes de dados]. Esta situação é chamada de "overhead". O resultado prático deste problema é a [queda de desempenho das redes].

Existem basicamente duas linhas de desenvolvimento de protocolos mesh: o [reativo] e o [pró-ativo]:

- O [reativo] somente reage quando surge um evento que demande a necessidade de ajuste no roteamento. 

- O [pró-ativo] faz buscas periódicas e se antecipa aos problemas, respondendo mais rapidamente. A consequência prática é que, apesar de mais eficiente, o _overhead_ é muito maior no sistema pró-ativo.

Outro problema é a [perda de desempenho por número de saltos]. O termo salto aqui é utilizado para descrever a situação onde um determinado emissor não consegue acessar diretamente o receptor e necessita do repasse das informações por nós intermediários. 

Um salto, nesse contexto, consiste no evento que representa o repasse dos pacotes entre dois nós para alcançar o receptor. A realização de um salto na rede implica em um custo computacional e quanto mais saltos forem necessários, maior será o custo total da comunicação.

Não existe na prática uma limitação para o número de saltos que uma informação pode dar numa rede mesh, mas existe uma degradação de _performance_ que vai aumentando conforme aumenta o número de saltos.

Em equipamentos com apenas um rádio 802.11g de um fabricante dos EUA, a _performance_ que pode chegar a 7 Mbps no primeiro salto, não passa de 1 Mbps a partir do quinto salto.

Equipamentos mais sofisticados com múltiplos rádios 802.11n podem diminuir drasticamente estes problemas. O padrão em Malha incentiva a conexão de todos os dispositivos entre si.

O modelo é usado até mesmo em operações maiores, mas quanto maior o número de dispositivos, maior a complexidade da instalação e o custo em si.

Cabear e conectar todos os dispositivos de uma rede entre si é uma tarefa que exige um nível de planejamento considerável. Ainda que o diagnóstico de erros seja facilitado nesse padrão, a implementação inicial é bastante custosa e complicada.