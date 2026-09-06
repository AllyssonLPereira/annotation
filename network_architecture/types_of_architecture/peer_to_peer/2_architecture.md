---
tags:
  - arquivo
---
Um sistema _peer-to-peer_ implementa uma rede abstrata sobreposta, em cima da topologia da rede. Essa sobreposição é utilizada para descobrir e indexar os pares da rede, tornando o sistema P2P funcional, independente da topologia da rede física. O conteúdo é trocado diretamente sobre o protocolo IP. 

> [!NOTE]
> Sistemas _peer-to-peer_ anônimos são exceções, pois implementam camadas extras de roteamento para ocultar sua identidade de origem ou de destino.

---
## Overlay

A rede _Overlay_ P2P consiste em uma forma em que todos os pares da rede funcionem como apenas um nó dessa. Existe uma ligação entre dois nós que se conhecem na rede. Isto é, um nó participante conhece a localização de outro nó da rede P2P. 

Então, existe uma aresta que liga o primeiro nó existente ao segundo na rede sobreposta. Com base em como os nós estão conectados na rede, podemos classificar a rede P2P como estruturada ou não estruturada.

Os pares são organizados de acordo com critérios e algoritmos, que realizam a sobreposição com topologias específicas.

A localização de nós e objetos é realizada na rede _overlay_ através de um algoritmo de roteamento distribuído. Esse algoritmo é implementado sobre a camada de aplicação, não tendo nenhuma ligação com o roteamento implementado pelos roteadores da camada de rede. 

É através desse algoritmo que as requisições dos clientes são roteadas para um hospedeiro que possui o objeto pela qual a requisição está endereçada.

---
## Structured P2P


Numa rede _peer-to-peer_ estruturada, a rede sobreposta é construída através de um procedimento determinístico. O procedimento mais utilizado, de longe, é organizar os processos através de uma tabela hash distribuída — DHT. 

Num sistema baseado em DHTs, os dados recebem uma chave aleatória de um extenso espaço de identificadores, tipicamente um identificador de 128 ou 160 bits. Os nodos da rede também recebem um identificador do mesmo espaço. 

O grande desafio num sistema baseado em DHT é implementar um esquema eficiente e determinístico que mapeia unicamente a chave de um item para o identificador do nodo responsável pelo item desejado. A partir disso, é possível retornar o endereço de rede do nodo responsável pelo item desejado, que pode ser contatado diretamente.


- _Peer-to-peer_ pura: toda rede consiste unicamente em pares equipotentes, existindo apenas uma camada de encaminhamento e nenhum sistema de infraestrutura especial.

- _Peer-to-peer_ centralizada: é utilizado um servidor central para indexar as informações e iniciar o sistema inteiro. As conexões entre pares não são gerenciadas por qualquer algoritmo.

- _Peer-to-peer_ híbrida: permite que os nós da infraestrutura coexistam.

---
## Unstructured P2P


Sistemas _peer-to-peer_ não estruturados geralmente se baseiam em algoritmos aleatorizados para a construção da rede sobreposta. A ideia principal é que cada nó mantenha uma lista de vizinhos, que é construída mais ou menos de forma aleatória. Da mesma forma, se assume que os dados são colocados de forma aleatória nos nodos. 

Assim, quando um nó necessita localizar um item específico, a única coisa que pode fazer é inundar a rede com uma busca. Uma desvantagem desse tipo de busca é que consultas podem não ser respondidas caso o cliente e o hospedeiro estejam muito afastados na rede. 

Isso acontece devido a mecanismos que impedem que mensagens se propaguem indefinidamente na rede — TTL. Outra desvantagem é que mecanismos de inundação geralmente causam grande tráfego de sinalização, o que, muitas vezes, torna esse tipo de busca lenta.

Muitos sistemas _peer-to-peer_ não estruturados constroem redes sobrepostas que remetem a um grafo aleatório. O modelo básico é que cada nó mantém uma lista com _c_ vizinhos, onde idealmente cada um desses representa um nodo escolhido aleatoriamente dentre o conjunto dos nodos "vivos". Essa lista de nós pode ser chamada de _visão parcial_.
