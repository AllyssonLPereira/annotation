## Introdução ao IPv4

A camada de rede, também conhecida como Camada 3 no modelo OSI (Open Systems Interconnection), desempenha um papel fundamental na comunicação de dados entre redes distintas. A sua principal função é o encapsulamento dos dados recebidos da camada de transporte em unidades chamadas pacotes, além do roteamento desses pacotes desde a origem até o destino final.

Para que esse processo ocorra de forma eficiente, a camada de rede necessita de um sistema de endereçamento lógico que identifique de maneira única cada dispositivo conectado à rede global. É nesse cenário que o Protocolo de Internet versão 4, ou IPv4, atua como o padrão mais difundido para essa finalidade.

O IPv4 foi projetado para fornecer um mecanismo de entrega de pacotes sem conexão, o que significa que ele não estabelece uma sessão prévia com o destino antes de enviar os dados, operando sob o princípio de "melhor esforço" (best-effort). Isso delega a responsabilidade de verificação de erros e controle de fluxo para as camadas superiores.

O papel central do IPv4 na Camada 3 é garantir que cada roteador no caminho consiga ler o endereço de destino contido no cabeçalho do pacote e tomar a decisão correta sobre qual rota o pacote deve seguir para alcançar o destino final.

## Estrutura de um endereço IPv4

Um endereço IPv4 é uma sequência numérica composta por exatamente 32 bits. Para facilitar a leitura e a manipulação por seres humanos, essa sequência binária é comumente representada no formato decimal separado por pontos. A estrutura é dividida em quatro partes iguais chamadas octetos, onde cada octeto representa um grupo de 8 bits. O valor decimal de cada octeto pode variar de 0 a 255, resultando em um formato padrão como, por exemplo, 192.168.1.1. 

A combinação total desses 32 bits permite a existência de $2^{32}$ endereços possíveis, o que equivale a aproximadamente 4,3 bilhões de endereços IP exclusivos.

Matematicamente, cada bit dentro de um octeto possui um peso baseado em potências de base 2. Quando todos os 8 bits de um octeto estão definidos como zero, o valor decimal é 0; quando todos estão definidos como um, o valor decimal atinge o limite máximo de 255. Por trás da representação decimal, os computadores e roteadores processam estritamente a forma binária para realizar as operações de rede.

Além da divisão em octetos, a anatomia de um endereço IPv4 é logicamente segmentada em duas porções principais: a identificação da rede (Network ID) e a identificação do host (Host ID). A porção de rede define a qual sub-rede específica o dispositivo pertence, permitindo que os roteadores localizem o segmento de rede correto. A porção de host identifica o dispositivo específico dentro daquela sub-rede. A demarcação exata de onde termina a porção de rede e onde começa a de host é determinada por uma máscara de sub-rede, um elemento complementar obrigatório para a correta interpretação do endereço IPv4.

## Classes de endereçamento

Inicialmente, a arquitetura do IPv4 foi estruturada sob o conceito de endereçamento com classes (classful addressing). Esse sistema dividia o espaço de endereçamento global em cinco classes distintas, denominadas A, B, C, D e E, com base nos bits iniciais do primeiro octeto.

- A Classe A, cujos endereços começam com o bit 0 no primeiro octeto (intervalo decimal de 0 a 127), foi projetada para grandes redes, reservando o primeiro octeto para a rede e os três restantes para hosts. 

- A Classe B, iniciando com os bits 10 (intervalo de 128 a 191), divide o endereço igualmente com dois octetos para rede e dois para hosts.

- A Classe C, iniciada pelos bits 110 (intervalo de 192 a 223), destina três octetos para a identificação da rede e apenas o último para hosts, sendo ideal para redes locais de menor porte.

- As classes D (224 a 239) e E (240 a 255) foram reservadas para transmissões multicast e propósitos experimentais ou de pesquisa, respectivamente.

![[Screenshot_20260605-122831_Brave 1.jpg]]

Dentro desse espaço global de endereçamento, determinados blocos de IPs foram estritamente reservados e não podem ser roteados na internet pública. 

A norma RFC 1918 definiu os escopos de endereços privados, amplamente utilizados em redes locais residenciais e corporativas: o bloco 10.0.0.0/8 na antiga Classe A, o intervalo de 172.16.0.0 a 172.31.255.255 na Classe B, e o bloco 192.168.0.0/16 na Classe C. Dispositivos configurados com esses IPs dependem de mecanismos como o NAT (Network Address Translation) para acessar redes externas.

Outro bloco reservado notável é o 127.0.0.0/8, destinado ao tráfego de loopback, que serve para testar a própria pilha de protocolos no dispositivo local, sendo o endereço 127.0.0.1 o mais conhecido. 

Há também o intervalo 169.254.0.0/16, utilizado pelo mecanismo APIPA (Automatic Private IP Addressing), que atribui automaticamente um endereço ao host quando este não consegue obter uma configuração IP por meio de um servidor DHCP.

## Máscaras de rede e CIDR

A máscara de sub-rede é o componente que define matematicamente quais bits de um endereço IP pertencem à rede e quais pertencem ao host. 

Ao realizar uma operação lógica AND bit a bit entre o endereço IP e a máscara, os roteadores conseguem isolar a identificação da rede. O modelo rígido de classes gerava um enorme desperdício de endereços, o que levou à criação do CIDR (Classless Inter-Domain Routing), ou Roteamento Interdomínios Sem Classes. 

O CIDR eliminou a dependência das classes fixas A, B e C, introduzindo a notação de barra, ou prefixo, que indica a quantidade exata de bits contínuos voltados à rede. Por exemplo, a notação /24 indica que os primeiros 24 bits representam a rede, independentemente de o endereço iniciar nos intervalos correspondentes às antigas classes.

## A Escassez de endereços IPv4

O crescimento exponencial da internet e a proliferação de dispositivos conectados superaram rapidamente as previsões iniciais dos projetistas do IPv4 na década de 1980.

Como o protocolo limita o espaço de endereçamento a exatamente 32 bits, o número máximo de combinações possíveis é de aproximadamente 4,3 bilhões de endereços. Esse montante tornou-se insuficiente para atender à demanda global de computadores, smartphones, servidores e dispositivos de Internet das Coisas (IoT). 

Diante do esgotamento oficial dos blocos de IPs centrais gerenciados pela IANA (Internet Assigned Numbers Authority) e pelos registros regionais, a comunidade técnica internacional precisou adotar estratégias de contenção para prolongar a vida útil do IPv4 enquanto a transição para o IPv6 — que possui um espaço de endereçamento virtualmente ilimitado — ocorre de forma gradual. 

A principal estratégia para mitigar essa escassez baseou-se na segregação de redes por meio de escopos de endereçamento públicos e privados.

Os endereços IP públicos são aqueles globalmente exclusivos e roteáveis na internet de forma direta. Cada servidor web, roteador de borda de provedor de internet ou serviço de computação em nuvem acessível publicamente deve possuir um endereço IP público único para que possa ser localizado por qualquer outro dispositivo no mundo.

Em contrapartida, os endereços IP privados são blocos específicos reservados para uso exclusivo dentro de redes locais corporativas ou residenciais. Múltiplas redes independentes ao redor do mundo reutilizam simultaneamente os mesmos intervalos de IPs privados, pois esses endereços não são roteados na infraestrutura global da internet; os roteadores públicos são configurados para descartar imediatamente qualquer pacote que possua um IP privado como destino ou origem. Isso isola o tráfego local, mas exige um mecanismo de conversão para que os hosts internos acessem recursos externos.

Com isso, abordamos o NAT (Tradução de Endereço de Rede), que é a tecnologia implementada em roteadores de borda que viabilizou a continuidade do funcionamento da internet sob o protocolo IPv4. A função primária do NAT é interceptar os pacotes gerados por dispositivos da rede interna (com IPs privados) e traduzir o endereço de origem para um único endereço IP público válido antes de enviar o pacote para a internet. 

O roteador mantém uma tabela de transações dinâmica para registrar qual dispositivo interno iniciou a comunicação. Quando a resposta do servidor externo retorna, o roteador consulta essa tabela, desfaz a tradução substituindo o IP público pelo IP privado do host correspondente e encaminha o dado ao destino correto dentro da rede local.

Na prática cotidiana, o NAT é configurado majoritariamente através de uma variação denominada PAT (Port Address Translation) ou NAT Overload. Nesse modelo, centenas de dispositivos de uma rede local conseguem compartilhar simultaneamente um único endereço IP público. Para diferenciar o tráfego de cada máquina interna, o roteador modifica e mapeia não apenas os endereços IP, mas também as portas de transporte (TCP ou UDP) de cada conexão. 

Esse método otimiza drasticamente a utilização dos recursos de endereçamento, permitindo que uma assinatura de internet residencial ou empresarial utilize apenas um IP público global para conectar todos os seus dispositivos internos à rede mundial.