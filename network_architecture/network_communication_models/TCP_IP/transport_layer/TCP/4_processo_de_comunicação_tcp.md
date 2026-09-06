---
tags:
  - arquivo
---
##### Processos em servidores TCP

Cada processo de aplicativo em execução em um servidor está configurado para usar um número de porta. O número da porta é atribuído automaticamente ou configurado manualmente por um administrador do sistema.

Um servidor individual não pode ter dois serviços atribuídos ao mesmo número de porta dentro dos mesmos serviços de camada de transporte. Por exemplo, um host executando um aplicativo de servidor web e um aplicativo de transferência de arquivos não pode ter os dois configurados para usar a mesma porta, como a porta TCP 80.

Um aplicativo de servidor ativo atribuído a uma porta específica é considerado aberto, o que significa que a camada de transporte aceita e processa os segmentos endereçados a essa porta. 

Qualquer solicitação de cliente que chega endereçada ao soquete correto é aceita e os dados são transmitidos à aplicação do servidor. Pode haver muitas portas abertas ao mesmo tempo em um servidor, uma para cada aplicação de servidor ativa.

---
##### Estabelecimento de Conexão TCP

Em algumas culturas, quando duas pessoas se encontram, elas costumam se cumprimentar apertando as mãos. Ambas as partes entendem o ato de apertar as mãos como um sinal para uma saudação amigável. As conexões de rede são semelhantes. 

Nas conexões TCP, o cliente host estabelece a conexão com o servidor usando o processo de handshake (aperto de mãos) de três vias.

1. [SYN]

	O cliente iniciador requisita uma sessão de comunicação cliente-servidor com o servidor.

2. [ACK e SYN]

	O servidor confirma a sessão de comunicação cliente-servidor e requisita uma sessão de comunicação de servidor-cliente.

3. [ACK]

	O cliente iniciador confirma a sessão de comunicação de servidor-cliente.


> [!NOTE]
> O handshake de três vias valida se o host de destino está disponível para comunicação.

---
##### Encerramento da Sessão

Para fechar uma conexão, o [flag de controle Finish] (FIN) deve ser ligado no cabeçalho do segmento. Para terminar cada sessão TCP de uma via, um handshake duplo, consistindo de um segmento FIN e um segmento ACK (Acknowledgment) é usado. 

Portanto, para terminar uma conversação única permitida pelo TCP, quatro trocas são necessárias para finalizar ambas as sessões. O cliente ou o servidor podem iniciar o encerramento.

1. [FIN]

	Quando o cliente não tem mais dados para enviar no fluxo, ele envia um segmento com um flag FIN ligado.

2. [ACK]

	O servidor envia ACK para confirmar o recebimento de FIN para encerrar a sessão do cliente com o servidor.

3. [FIN]

	O servidor envia um FIN ao cliente para encerrar a sessão do servidor-para-cliente.

4. [ACK]

	O cliente responde com um ACK para reconhecer o FIN do servidor.


Quando todos os segmentos tiverem sido confirmados, a conexão é encerrada.

---
##### Análise do Handshake Triplo do TCP

Os hosts mantêm o estado, rastreiam cada segmento de dados em uma sessão e trocam informações sobre quais dados são recebidos usando as informações no cabeçalho TCP. O TCP é um [protocolo full-duplex, em que cada conexão representa duas sessões de comunicação unidirecional].

Para estabelecer uma conexão, os hosts realizam um handshake triplo (three-way handshake). Os bits de controle no cabeçalho TCP indicam o progresso e o status da conexão.

Estas são as funções do handshake de três vias:

- Estabelece que o dispositivo de destino está presente na rede.

- Ele verifica se o dispositivo de destino possui um serviço ativo e está aceitando solicitações no número da porta de destino que o cliente inicial pretende usar.

- Ele informa ao dispositivo de destino que o cliente de origem pretende estabelecer uma sessão de comunicação nesse número de porta.


![[cabecalho_camada_de_transporte_tcp_ip.webp]]


Após a conclusão da comunicação, as sessões são fechadas e a conexão é encerrada. Os mecanismos de conexão e sessão ativam a função de confiabilidade do TCP.

Os seis bits no campo Bits de Controle do cabeçalho do segmento TCP são também conhecidos como flags. Um sinalizador é um pouco definido como ativado ou desativado.

Os seis bits de controle sinalizadores são os seguintes:

- **[URG]** - Campo de ponteiro urgente significativo
- **[ACK]** - Indicador de confirmação usado no estabelecimento de conexão e encerramento de sessão
- **[PSH]** - Função Push
- **[RST]** - Redefina a conexão quando ocorrer um erro ou exceder o tempo limite
- **[SYN]** - Sincronizar números de sequência usados no estabelecimento de conexão
- **[FIN]** - Não há mais dados do remetente e usados no encerramento da sessão

Pesquisar na Internet para saber mais sobre as bandeiras PSH e URG.