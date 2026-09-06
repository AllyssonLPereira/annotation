---
tags:
  - arquivo
---
## What is distributed computing?

Computação distribuída corresponde ao método de fazer vários computadores trabalharem juntos para resolver um problema comum. Isso faz com que uma rede de computadores pareça um único computador poderoso que fornece recursos em grande escala para lidar com desafios complexos.

---
## What are the advantages of distributed computing?


- *`Scalability`* — os sistemas distribuídos podem crescer com suas workloads e requisitos. 

- *`Availability`* — o sistema de computação distribuído não sofrerá impacto se um dos computadores falhar.

- *`Consistency`* — os computadores em um sistema distribuído compartilham informações e duplicam dados entre eles, mas o sistema gerencia automaticamente a consistência de dados em todos os computadores.

- *`Transparency`* — os sistemas de computação distribuída fornecem separação lógica entre o usuário e os dispositivos físicos.

- *`Efficiency`* — os sistemas distribuídos oferecem uma performance mais rápida com uso otimizado dos recursos do hardware subjacente.

---
## Types of distributed computing architecture

- Arquitetura client/server;
- Arquitetura três camadas;
- Arquitetura multicamadas;
- Arquitetura ponto a ponto.

---
## How does distributed computing work?

A computação distribuída funciona por computadores que transmitem mensagens entre si dentro da arquitetura dos sistemas distribuídos. 

Os protocolos ou regras de comunicação criam uma dependência entre os componentes do sistema distribuído. Essa interdependência é chamada de acoplamento e existem dois tipos principais de acoplamentos.


- *Weak coupling*:

	No qual os componentes são parcialmente conectados para que as alterações em um componente não afetem outros. Por exemplo, os computadores cliente e servidor podem ter um acoplamento fraco pela ação do tempo. 
	
	As mensagens do cliente são adicionadas a uma fila do servidor e o cliente pode continuar a executar outras funções até que o servidor responda à sua mensagem.

- *Strong coupling*:

	Agora, sistemas distribuídos de alta performance geralmente usam acoplamento forte. As redes locais rápidas normalmente conectam vários computadores, o que cria um cluster. Na computação em cluster, cada computador é configurado para executar a mesma tarefa. 
	
	Os sistemas de controle central, chamados de middleware de cluster, controlam e agendam as tarefas, bem como coordenam a comunicação entre os diferentes computadores.
