---
tags:
  - arquivo
---
##### User Datagram Protocol (UDP)

O UDP é um [protocolo de camada de transporte mais simples] do que o TCP. [Ele não fornece confiabilidade e controle de fluxo], o que significa que requer menos campos de cabeçalho. 

Como o remetente e os processos UDP receptor não precisam gerenciar confiabilidade e controle de fluxo, isso significa que datagramas UDP podem ser processados mais rápido do que segmentos TCP. 

O UDP fornece as funções básicas para fornecer datagramas entre os aplicativos apropriados, com [muito pouca sobrecarga e verificação de dados].

> [!NOTE]
> O UDP divide os dados em datagramas que também são chamados de segmentos.

UDP é um [protocolo sem conexão]. Como o UDP não fornece confiabilidade ou controle de fluxo, ele não requer uma conexão estabelecida. Como o UDP não controla informações enviadas ou recebidas entre o cliente e o servidor, o UDP também é conhecido como um [protocolo sem estado].

UDP também é conhecido como um [protocolo de entrega de melhor esforço porque não há confirmação de que os dados são recebidos no destino]. Com o UDP, não há processo de camada de transporte que informe ao remetente se a entrega foi bem-sucedida.

O UDP é como colocar uma carta regular, não registrada, no correio. [O remetente da carta não tem conhecimento se o destinatário está disponível para receber a carta]. Nem a agência de correio é responsável por rastrear a carta ou informar ao remetente se ela não chegar ao destino final.

---
##### Recursos UDP

UDP é um protocolo de transporte de melhor esforço. 

O UDP é um protocolo de transporte leve que oferece a mesma segmentação de dados e remontagem que o TCP, mas sem a confiabilidade e o controle de fluxo do TCP.

O UDP é um protocolo simples, normalmente descrito nos termos do que ele não faz em comparação ao TCP.

Os recursos UDP incluem o seguinte:

- Os dados são reagrupados na ordem em que são recebidos.
- Quaisquer segmentos perdidos não são reenviados.
- Nenhum estabelecimento de seção.
- O envio não é informado sobre a disponibilidade do recurso.

> [!NOTE]
> Para obter mais informações sobre o UDP, pesquise na Internet o RFC.

---
##### Cabeçalho UDP

UDP é um protocolo sem estado, o que significa que nem o cliente nem o servidor rastreiam o estado da sessão de comunicação. Se a confiabilidade for necessária ao usar o UDP como protocolo de transporte, ela deve ser tratada pela aplicação.

Um dos requisitos mais importantes para transmitir vídeo ao vivo e voz sobre a rede é que os dados continuem fluindo rapidamente. Vídeo ao vivo e aplicações de voz podem tolerar alguma perda de dados com efeito mínimo ou sem visibilidade e são perfeitos para o UDP.

Os blocos de comunicação no UDP são chamados de datagramas ou segmentos. Esses datagramas são enviados como o melhor esforço pelo protocolo da camada de transporte.

O cabeçalho UDP é muito mais simples do que o cabeçalho TCP porque só tem quatro campos e requer 8 bytes (ou seja, 64 bits).

![[UDP-Header.webp]]

|Campos de Cabeçalho UDP|Descrição|
|---|---|
|Porta de origem|Um campo de 16 bits usado para identificar o aplicativo de origem por número de porta.|
|Porta de destino|Um campo de 16 bits usado para identificar o aplicativo de destino pelo número da porta.|
|Comprimento|Um campo de 16 bits que indica o comprimento do cabeçalho do datagrama UDP.|
|Checksum|Um campo de 16 bits usado para verificação de erros do cabeçalho e dos dados do datagrama.|

---
##### Aplicações que usam UDP

Há três tipos de aplicações que são mais adequadas para o UDP:

- **[Aplicações de vídeo e multimídia ao vivo]** - Esses aplicativos podem tolerar a perda de dados, mas requerem pouco ou nenhum atraso. Os exemplos incluem VoIP e transmissão de vídeo ao vivo.

- **[Aplicações de solicitação e resposta simples]** - Aplicativos com transações simples em que um host envia uma solicitação e pode ou não receber uma resposta. Os exemplos incluem DNS e DHCP.

- **[Aplicativos que lidam com a confiabilidade]** - Comunicações unidirecionais em que o controle de fluxo, a detecção de erros, as confirmações e a recuperação de erros não são necessários ou podem ser gerenciados pela aplicação. Os exemplos incluem SNMP e TFTP.


Embora por padrão DNS e SNMP usem UDP, ambos podem usar TCP. O DNS usará o TCP se a solicitação ou resposta de DNS for maior que 512 bytes, como quando uma resposta de DNS inclui muitas resoluções de nome. 

Da mesma forma, em algumas situações o administrador de redes pode querer configurar o SNMP para usar o TCP.


> [!NOTE]
> Como uma sessão não precisa ser estabelecida para UDP, o cliente seleciona uma porta de origem aleatória para iniciar uma conexão. O número de porta aleatória selecionado é inserido no campo de porta de origem do cabeçalho UDP.

---
##### Reagrupamento do Datagrama UDP

Como ocorre com segmentos TCP, quando múltiplos datagramas UDP são enviados a um destino, eles geralmente tomam caminhos diferentes e chegam na ordem errada. O UDP não rastreia os números de sequência da forma que o TCP faz. O UDP não tem como reordernar os datagramas na sua ordem de transmissão.

Portanto, o UDP simplesmente remonta os dados na ordem que eles foram recebidos e os encaminha para a aplicação. Se a sequência de dados for importante para a aplicação, a aplicação deverá identificar a sequência apropriada e determinar como os dados devem ser processados.

---
##### Processos e Solicitações do Servidor UDP

Do mesmo modo que aplicações baseadas em TCP, as aplicações de servidor baseadas em UDP recebem números de portas bem conhecidas ou registradas.

Quando as aplicações ou processos estão sendo executados, eles aceitarão os dados correspondentes ao número de porta atribuído. Quando o UDP recebe um datagrama destinado a uma destas portas, ele encaminha os dados à aplicação apropriada com base em seu número de porta.

---
##### Processos UDP em Servidores

Assim como o TCP, a comunicação cliente servidor é iniciada por uma aplicação cliente que requisita dados de um processo em um servidor. O processo no cliente UDP seleciona dinamicamente um número de porta a partir de uma faixa de números de portas e a usa como a porta de origem para a conversa. 

A porta de destino será geralmente o número de porta muito conhecida ou registrada atribuído ao processo no servidor.

Depois que um cliente seleciona as portas de origem e de destino, o mesmo par de portas é usado no cabeçalho de todos os datagramas na transação. Para dados que retornam para o cliente vindos do servidor, os números da porta de origem e de destino no cabeçalho do datagrama são invertidos.