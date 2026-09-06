---
tags:
  - arquivo
---
Há dois tipos básicos de modelos para descrever as funções que devem ocorrer para que as comunicações de rede sejam bem-sucedidas: [modelos de protocolo] e [modelos de referência].

- **[Modelo de referência]**

	Este tipo de modelo descreve as funções que devem ser concluídas em uma determinada camada, ou seja, [o que deve ser gerado pela camada. Mas não especifica exatamente como] uma função deve ser realizada. 

	Um modelo de referência não deve fornecer um nível suficiente de detalhes para definir com precisão como cada protocolo deve trabalhar em cada camada. 

	[A principal finalidade] de um modelo de referência [é ajudar a entender melhor as funções e os processos necessários para as comunicações de rede].


O modelo de referência internetwork mais conhecido foi criado pelo projeto [Open Systems Interconnection (OSI)] da ISO (Organização Internacional de Padronização). [Ele é usado para projeto de redes de dados, especificações de operação e solução de problemas]. Esse modelo costuma ser chamado de *modelo OSI*.

Segundo Tanenbaum, o Modelo OSI [não é uma arquitetura de redes], pois não especifica os serviços e protocolos exatos que devem ser usados em cada camada. Ele apenas informa o que cada camada deve fazer.

| Camada de modelo OSI | Descrição                                                                                                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7 - Aplicação        | Contém protocolos usados para comunicações processo a processo.                                                                                                                                         |
| 6 - Apresentação     | Fornece a representação comum de dados transferidos entre serviços da camada de aplicação.                                                                                                              |
| 5 - Sessão           | Fornece serviços à camada de apresentação para organizar o diálogo e gerenciar a troca de dados.                                                                                                        |
| 4 - Transporte       | Define serviços para segmentar, transferir e reagrupar os dados para comunicações individuais entre os dispositivos finais.                                                                             |
| 3 - Rede             | Fornece serviços para trocar dados individuais pela rede entre dispositivos finais identificados.                                                                                                       |
| 2 - Enlace de dados  | Os protocolos nessa camada descrevem métodos para a troca de quadros de dados entre os dispositivos em um meio físico comum.                                                                            |
| 1 - Físico           | Os protocolos aqui descrevem os meios mecânicos, elétricos, funcionais e procedimentais para ativar, manter e desativar conexões físicas para uma transmissão de bits de e para um dispositivo de rede. |

> [!NOTE] 
> Enquanto o Modelo de Referência OSI é útil para discutir conceitos de rede, muitos protocolos de rede não seguem de perto o modelo OSI.

---
### PDU e SDU

De acordo com o padrão X.200, existem sete camadas, de 1 a 7, onde cada camada é conhecida de forma genérica como "[camada N]". Somente a entidade N+1 (camada acima de N) pode solicitar serviços de uma "entidade N". 

Essa interação entre camadas ocorre através da transmissão da *"Unidade de Protocolo de Dados" (PDU), [bloco de dados dividido em três partes: cabeçalho (header), carga útil (SDU) e rabeira (tail)].*

A [Unidade de Dados de Serviço (SDU)] é uma unidade específica de dados que foram passados ​​de uma camada OSI para uma camada inferior, e que a camada inferior ainda não encapsulou em uma unidade de dados de protocolo (PDU) seu. Uma [SDU é um conjunto de dados que são enviados por um usuário dos serviços de uma determinada camada], e é transmitida semanticamente inalterada a um usuário do serviço peer.

Com efeito, a SDU é a "carga útil" de uma dada PDU. Isto é, o processo de alteração de um SDU a uma PDU é constituído por um [processo de encapsulamento], realizada pela camada inferior. Ou seja, uma camada inferior recebe um SDU e altera ela num processo de encapsulamento.

Todos os dados contidos no SDU fica encapsulado dentro do PDU. A camada de N-1 adiciona cabeçalhos ou rodapés, ou ambos, para a SDU, transformando-a numa PDU de camada N-1. 

Os cabeçalhos ou rodapés adicionados fazem parte do processo utilizado para tornar possível a obtenção de dados de uma fonte para um destino.

---
### Camadas


- **[Camada física]**

A camada física se refere ao [meio físico de comunicação e às tecnologias para transmitir dados por esse meio]. 

Em sua essência, a comunicação de dados é a transferência de sinais digitais e eletrônicos por meio de vários canais físicos, como cabos de fibra óptica, cabos de cobre e ar. 

Essa camada inclui o equipamento físico envolvido na transferência de dados, como cabos e switches. Essa também é a camada em que os dados são convertidos em um fluxo de bits, que é uma sequência de 1s e 0s. 

A camada física de ambos os dispositivos também precisa aceitar, de comum acordo, uma convenção de sinais para que se possa distinguir os 1s dos 0s em ambos os dispositivos.

A camada física inclui padrões para tecnologias e métricas estreitamente relacionadas aos canais, como Bluetooth, NFC e velocidades de transmissão de dados.

![[camada_fisica.png]]
***Cloudflare***


- **[Camada de enlace de dados]**

A camada de enlace de dados [se refere às tecnologias usadas para conectar duas máquinas em uma rede onde a camada física já existe]. 

A camada de enlace de dados é muito semelhante à camada de rede, a não ser pelo fato de que a camada de enlace de dados facilita a transferência de dados entre dois dispositivos na mesma rede. 

A camada de enlace de dados pega os pacotes da camada de rede e os divide em pedaços menores denominados "[frames]". 

Como a camada de rede, a camada de enlace de dados também é responsável pelo [controle de fluxo e pelo controle de erros na comunicação intra-rede] (a camada de transporte faz o controle de fluxo e o controle de erros para comunicações inter-rede).

A camada de enlace de dados geralmente é dividida em duas subcamadas: [a camada Media Access Control (MAC) e a camada Logical Link Control (LLC)]. 

![[camada_enlace_de_dados.png]]
***Cloudflare***


- **[Camada de rede]**

A camada de rede se preocupa com conceitos como [roteamento, encaminhamento e endereçamento] em uma rede dispersa ou em várias redes conectadas. 

A camada de rede é responsável por facilitar a transferência de dados entre duas redes diferentes.

[Se os dois dispositivos que estão se comunicando estiverem na mesma rede, a camada de rede será desnecessária]. 

A camada de rede divide os segmentos da camada de transporte em unidades menores denominadas [pacotes] no dispositivo remetente e remonta esses pacotes no dispositivo receptor.

A camada de rede também pode gerenciar o controle de fluxo. Na Internet, o IPv4 e o IPv6 são usados ​​como os principais protocolos da camada de rede.
***Cloudflare***


- **[Camada de transporte]**

O foco principal da camada de transporte é [garantir que os pacotes de dados cheguem na ordem correta, sem perdas nem erros], ou que possam ser recuperados sem complicações, se necessário. 

Em outras palavras, a camada 4 é responsável pela comunicação de ponta a ponta entre os dois dispositivos. Isso inclui pegar os dados da camada de sessão e dividi-los em porções chamadas [segmentos] antes de enviá-los para a camada 3.

A camada de transporte também é [responsável pelo controle de fluxo e pelo controle de erros]. 

O controle de fluxo determina uma velocidade de transmissão ideal para garantir que um remetente com uma conexão rápida não sobrecarregue um receptor com uma conexão lenta, por exemplo. 

A camada de transporte executa o controle de erros no lado do receptor, garantindo que os dados recebidos estejam completos e solicitando uma retransmissão caso não estejam ***(quebra cabeça faltando uma peça)***.

O controle de fluxo, em conjunto com o controle de erros, é frequentemente um foco na camada de transporte. Nessa camada, os protocolos comumente usados ​​incluem o Transmission Control Protocol (TCP), um protocolo baseado em conexão quase sem perdas, e o User Datagram Protocol (UDP), um protocolo sem conexão com perdas. 

![[camada_transporte.png]]
***Cloudflare***


- **[Camada de sessão]**

A camada de sessão é responsável pela [coordenação de rede entre duas aplicações separadas em uma sessão]. Uma sessão gerencia o início e o término de uma conexão individual de aplicações e gerenciando os conflitos de sincronização. 

A camada de sessão também [sincroniza a transferência de dados com pontos de verificação]. Por exemplo, se um arquivo de 100 megabytes estiver sendo transferido, a camada de sessão poderá definir um ponto de verificação a cada 5 megabytes. 

No caso de uma desconexão ou falha após a transferência de 52 megabytes, a sessão pode ser retomada a partir do último ponto de verificação, o que significa que apenas mais 50 megabytes de dados precisam ser transferidos. [Sem os pontos de verificação, a transferência inteira teria que começar novamente do zero].

O [Network File System (NFS) e o Server Message Block (SMB)] são protocolos comumente usados na camada de sessão.

![[camada_sessao.png]]
***Cloudflare***


- **[Camada de apresentação]**

A camada de apresentação [se preocupa principalmente com a sintaxe dos próprios dados para as aplicações enviarem e consumirem]. 

Dois dispositivos de comunicação que se comunicam podem usar métodos de codificação diferentes, por isso, a camada 6 é responsável pela [tradução dos dados de entrada em uma sintaxe que a camada de aplicação do dispositivo receptor possa entender].

Por exemplo, Hypertext Markup Language (HTML), JavaScript Object Notation (JSON) e Comma Separated Values (CSV) são todas linguagens de modelagem para descrever a estrutura de dados na camada de apresentação. 

![[camada_apresentacao.png]]
***Cloudflare***


- **[Camada de aplicação]**

A camada de aplicação [se preocupa com o tipo específico da aplicação em si e seus métodos de comunicação padronizados].

Os softwares aplicativos, como navegadores web e clientes de e-mail, dependem da camada de aplicação para iniciar as comunicações. 

É preciso deixar claro que [os softwares aplicativos clientes não fazem parte da camada de aplicação], que, na verdade, é responsável pelos protocolos e manipulação de dados dos quais o software depende para apresentar dados significativos ao usuário.

Por exemplo, navegadores podem se comunicar usando Hyper Text Transfer Protocol Secure (HTTPS), e clientes de e-mail podem se comunicar usando POP3 (Post Office Protocol versão 3) e SMTP (Simple Mail Transfer Protocol).

![[camada_aplicacao.png]]
***Cloudflare***


![[modelo_osi.png]]
***IBM***

> [!NOTE]
> Nem todos os sistemas que usam o modelo OSI implementam todas as camadas.

---
### Como ocorre as comunicações?

Ao encadear todas essas camadas e protocolos, as comunicações de dados complexas podem ser enviadas de uma aplicação de alto nível para outra. O processo funciona da seguinte forma:

1. A camada de aplicação do remetente transmite a comunicação de dados para a próxima camada inferior.

2. Cada camada adiciona seus próprios cabeçalhos e endereçamentos aos dados antes de transmiti-los.

3. A comunicação de dados se desloca para baixo pelas camadas até que seja finalmente transmitida pelo meio físico.

4. Na outra extremidade desse meio, cada camada processa os dados de acordo com os cabeçalhos relevantes naquele nível. 

5. Na extremidade receptora, os dados sobem na camada e são gradualmente descompactados até que a aplicação na outra extremidade os receba.

---
### Referências

https://www.cloudflare.com/pt-br/learning/ddos/glossary/open-systems-interconnection-model-osi/
https://www.ibm.com/docs/pt-br/aix/7.3?topic=management-network-communication-concepts
https://aws.amazon.com/pt/what-is/osi-model/
https://pt.wikipedia.org/wiki/Modelo_OSI

