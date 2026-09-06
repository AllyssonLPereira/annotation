---
tags:
  - arquivo
---
## Resumo

O Protocolo de Transferência de Hipertexto - HTTP - é um protocolo de nível de aplicação sem estado para sistemas de informação de hipertexto distribuídos e colaborativos. Este documento descreve a arquitetura geral do HTTP, estabelece uma terminologia comum e define aspectos do protocolo que são compartilhados por todas as versões. 

Esta definição inclui os elementos principais do protocolo, os mecanismos de extensibilidade e os esquemas de Identificador Uniforme de Recursos - URI - "http" e "https".

Quando um cliente Web recebe o endereço IP de um servidor Web, o navegador do cliente usa esse endereço IP e a porta 80 para solicitar serviços da Web. Essa solicitação é enviada para o servidor com o ***[Hyper Text Transfer Protocol (HTTP)]***.

> [!NOTE] O que é ***Hyper Text***?
> Refere-se a um sistema de escrita e leitura não linear, onde os *textos estão interconectados por meio de links*. O Hyper Texto permite que os usuários naveguem de um texto para outro de forma não sequencial, seguindo os links que conectam os diferentes conteúdos.


O conteúdo de informações de uma página Web é codificado por meio de linguagens de marcação especializadas. A codificação Hyper Text Markup Language (HTML) informa ao navegador o modo de formatação da página Web, além de gráficos e fontes a serem usados. *HTML é a linguagem mais usada.

Porém, é importante ressaltar que o protocolo HTTP não é um protocolo seguro, as informações podem ser facilmente interceptadas por outros usuários à medida que os dados são enviados pela rede. Para oferecer segurança aos dados, o HTTP pode ser usado com protocolos de transporte seguros. 

As solicitações de HTTP seguro são enviadas para a porta 443. Essas solicitações usam **[HTTPS]** no endereço do site no navegador, em vez de HTTP.

Existem muitos servidores web e clientes web diferentes disponíveis. Os padrões de HTML e do protocolo HTTP fazem com que esses servidores e clientes de diversos fabricantes trabalhem em conjunto sem dificuldades.

---
## Introdução

- ##### Objetivo:

O Protocolo de Transferência de Hipertexto - HTTP - é:

- Uma família de protocolos de solicitação/resposta *sem estado - **`stateless`** - o que significa que cada requisição é independente e não depende das anteriores -*;
- De ***`nível de aplicação`***;
- Que compartilham uma ***`interface genérica`** - um jeito padrão de comunicação;
- Ela possui ***`semântica extensível`** - pode ser estendido para diferentes usos*;
- ***`Mensagens autodescritivas`*** para permitir uma interação flexível com sistemas de informação de hipertexto baseados em rede.


O HTTP ***[oculta os detalhes de como um serviço é implementado]***, apresentando aos clientes uma interface uniforme, independente dos tipos de recursos fornecidos. 

Em outras palavras, O HTTP esconde como o serviço é implementado atrás dessa interface padrão. Para o cliente, tudo parece igual, não importa se o servidor está usando um banco de dados, arquivos ou outro sistema para entregar a informação. 

> Isso facilita o uso do protocolo em muitos tipos diferentes de sistemas, pois o cliente só precisa saber como falar HTTP, não como o servidor funciona por dentro.

Da mesma forma, ***os servidores não precisam estar cientes da finalidade de cada cliente***: uma solicitação pode ser considerada isoladamente, em vez de ser associada a um tipo específico de cliente ou a uma sequência predeterminada de etapas da aplicação. 

Isso permite que implementações de propósito geral sejam usadas efetivamente em diversos contextos, reduz a complexidade da interação e permite a evolução independente ao longo do tempo.

O HTTP também foi projetado para uso como um `protocolo de intermediação`, no qual proxies e gateways podem traduzir sistemas de informação não HTTP em uma interface mais genérica.

Uma consequência dessa flexibilidade é que o protocolo não pode ser definido em termos do que ocorre por trás da interface. Em vez disso, estamos limitados a definir a sintaxe da comunicação, a intenção da comunicação recebida e o comportamento esperado dos destinatários. 

Isto é, por causa dessa flexibilidade, o protocolo não define o que acontece "por trás da interface" - ele só define a forma da comunicação - ***`sintaxe`*** -, o que a comunicação quer dizer - ***`intenção`*** - e `como os destinatários devem se comportar`. *Ou seja, o HTTP não se importa com a implementação interna, apenas com o que é enviado e recebido.

Se a comunicação for considerada isoladamente, as ações bem-sucedidas devem ser refletidas em alterações correspondentes na interface observável fornecida pelos servidores. No entanto, como vários clientes podem atuar em paralelo e talvez com propósitos opostos, não podemos exigir que tais alterações sejam observáveis ​​além do escopo de uma única resposta.

---
## História e Evolução

O HTTP tem sido o principal protocolo de transferência de informações para a World Wide Web desde sua introdução em 1990. Começou como um mecanismo trivial para solicitações de baixa latência, com um único método - `GET` - para solicitar a transferência de um suposto documento de hipertexto identificado por um determinado caminho. 

A medida que a Web cresceu, o HTTP foi expandido para incluir solicitações e respostas em mensagens, transferir formatos de dados arbitrários usando tipos de mídia do tipo MIME e rotear solicitações por meio de intermediários. Esses protocolos foram eventualmente definidos como HTTP/0.9 e HTTP/1.0.

O HTTP/1.1 foi projetado para refinar os recursos do protocolo, mantendo a compatibilidade com a sintaxe de mensagens de texto existente, melhorando sua interoperabilidade, escalabilidade e robustez na Internet. 

Isso incluiu delimitadores de dados baseados em comprimento para conteúdo fixo e dinâmico - fragmentado -, uma estrutura consistente para negociação de conteúdo, validadores opacos para solicitações condicionais, controles de cache para melhor consistência do cache, solicitações de intervalo para atualizações parciais e conexões persistentes padrão. 

O HTTP/1.1 foi introduzido em 1995 e publicado no Standards Track em 1997 [RFC2068], revisado em 1999 [RFC2616] e revisado novamente em 2014 - [RFC7230] a [RFC7235].

O HTTP/2 introduziu uma camada de sessão multiplexada sobre os protocolos TLS e TCP existentes para a troca de mensagens HTTP simultâneas com compressão de campo eficiente e push de servidor. O HTTP/3 proporciona maior independência para mensagens simultâneas, utilizando o QUIC como um transporte multiplexado seguro sobre UDP em vez de TCP.

Elas não se tornaram obsoletas umas às outras, pois cada uma possui benefícios e limitações específicos, dependendo do contexto de uso. Espera-se que as implementações escolham a sintaxe de transporte e mensagens mais apropriada para seu contexto específico.

---
## Semântica Central

O HTTP fornece uma interface uniforme para interagir com um recurso — independentemente de seu tipo, natureza ou implementação — enviando mensagens que manipulam ou transferem representações.

Cada mensagem é uma solicitação ou uma resposta. Um cliente constrói mensagens de solicitação que comunicam suas intenções e as encaminha para um servidor de origem identificado. 

Um servidor escuta as solicitações, analisa cada mensagem recebida, interpreta a semântica da mensagem em relação ao recurso de destino identificado e responde a essa solicitação com uma ou mais mensagens de resposta. 

O cliente examina as respostas recebidas para verificar se suas intenções foram executadas, determinando o que fazer em seguida com base nos códigos de status e no conteúdo recebido.

> [!NOTE]
> A semântica HTTP inclui as ***intenções*** definidas por cada método de solicitação, ***extensões a essas semânticas*** que podem ser descritas nos campos de cabeçalho da solicitação, ***códigos de status*** que descrevem a resposta e ***outros dados de controle e metadados de recursos*** que podem ser fornecidos nos campos de resposta.
> 
> A semântica também inclui ***metadados de representação*** que descrevem como o conteúdo deve ser interpretado por um destinatário, ***campos de cabeçalho da solicitação*** que podem influenciar a seleção de conteúdo e os ***diversos algoritmos de seleção*** que são coletivamente chamados de "negociação de conteúdo".



