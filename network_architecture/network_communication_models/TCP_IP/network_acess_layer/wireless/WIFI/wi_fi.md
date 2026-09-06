---
tags:
  - arquivo
---
## O que é uma rede sem fio ou Wi-Fi?

Uma rede sem fio refere-se a uma rede de computadores que faz uso de conexões de radiofrequência (Radio frequency, RF) entre nós na rede. As redes sem fio são uma solução popular para residências, empresas e redes de telecomunicações.

É comum que as pessoas se perguntem “o que é uma rede sem fio” porque, embora existam em quase todos os lugares onde as pessoas vivem e trabalham, como elas funcionam é frequentemente um mistério. Da mesma forma, as pessoas frequentemente presumem que toda a rede sem fio é Wi-Fi, e muitas se surpreenderiam ao descobrir que as duas não são sinônimos. 

Ambos usam RF, mas há muitos tipos diferentes de redes sem fio em uma variedade de tecnologias (Bluetooth, ZigBee, LTE, 5G), enquanto a Wi-Fi é específica para o protocolo sem fio definido pelo Instituto de engenheiros elétricos e eletrônicos (Institute of electrical and electronic engineers, IEEE) na especificação 802.11 e suas emendas.

## Rede com e sem fio: Qual é a diferença?

No mais óbvio, uma rede sem fio mantém os dispositivos conectados a uma rede, ao mesmo tempo em que lhes dá a liberdade de se mover, sem sobrecargas por fios. Uma rede com fio, por outro lado, faz uso de cabos que conectam dispositivos à rede. Esses dispositivos são frequentemente computadores desktop ou laptop, mas também podem incluir scanners e máquinas de ponto de venda.

Há diferenças tecnológicas mais sutis que entram em jogo entre redes com e sem fio.  A maioria das redes com fio modernas agora é “full duplex”, o que significa que elas podem transmitir/receber pacotes em ambas as direções simultaneamente.  Além disso, a maioria das redes com fio tem um cabo dedicado que se estende a cada dispositivo do usuário final.

Em uma rede Wi-Fi, o meio (a frequência de rádio sendo usada para a rede) é um recurso compartilhado, não apenas para os usuários da rede, mas também para outras tecnologias (a rede Wi-Fi opera nas chamadas bandas “compartilhadas”, onde muitos dispositivos eletrônicos diferentes são aprovados para operar).  Isso tem várias implicações: 

1) ao contrário de uma rede com fio, o wireless não pode falar e ouvir ao mesmo tempo, é “meio duplex” 
2) Todos os usuários estão compartilhando o mesmo espaço devem se revezar para falar 
3) todos podem “ouvir” todo o tráfego que está acontecendo. 

Isso forçou as redes Wi-Fi a implementar várias medidas de segurança ao longo dos anos para proteger a confidencialidade das informações transmitidas sem fio.

## Os componentes de uma rede sem fio

Vários componentes compõem a topologia de uma rede sem fio:

1. **Clientes**: O que tendemos a pensar como os dispositivos do usuário final são normalmente chamados de “clientes”.  À medida que o alcance do Wi-Fi se expande, uma variedade de dispositivos pode estar usando o Wi-Fi para conectar a rede, incluindo telefones, tablets, laptops, desktops e muito mais. Isso dá aos usuários a capacidade de se mover pela área sem sacrificar sua ponte para a rede. Em alguns casos, a mobilidade dentro de um escritório, armazém ou outra área de trabalho é necessária. Por exemplo, se os funcionários tiverem que usar scanners para registrar pacotes que devem ser enviados, uma rede sem fio oferece a flexibilidade necessária para se movimentar livremente pelo armazém.

2. **Ponto de acesso (Access point, AP)**: Um ponto de acesso (AP) consiste em um ponto de Wi-Fi que está anunciando um nome de rede (conhecido como Identificador do conjunto de serviços, Service Set Identifier, ou SSID).  Os usuários que se conectam a essa rede normalmente encontrarão seu tráfego em ponte para uma rede de área local (LAN) com fio [(como Ethernet)](https://www.fortinet.com/br/resources/cyberglossary/what-is-ethernet-switching) para comunicação com a rede maior ou até mesmo a internet.   


## Como funciona uma rede Wi-Fi?

Uma rede sem fio baseada em Wi-Fi envia sinais usando ondas de rádio (telefones celulares e rádios também transmitem por ondas de rádio, mas em frequências e modulação diferentes).

Em uma rede Wi-Fi típica, o ponto de acesso (Access Point, AP) anunciará a rede específica à qual ele oferece conectividade. Isso é chamado de Identificador do conjunto de serviços (Service Set Identifier, SSID) e é o que os usuários veem quando observam a lista de redes disponíveis em seus telefones ou laptops.  

O AP anuncia isso por meio de transmissões chamadas beacons.  O sinalizador pode ser visto como um anúncio dizendo: “Olá, tenho uma rede aqui, se for a rede que você está procurando, você pode entrar”.

Um dispositivo cliente recebe o beacon transmitido pelo AP e converte o sinal de RF em dados digitais, em seguida, esses dados são passados para o dispositivo para interpretação. 

Se o usuário deseja se conectar à rede, pode enviar mensagens para o ponto de acesso tentando entrar e (quando a segurança está habilitada) fornecendo as credenciais adequadas para comprovar que têm o direito de entrar.  Esses processos são conhecidos como Associação & Autenticação. 

Se qualquer um desses falhar, o dispositivo não entrará na rede com sucesso e não poderá se comunicar com o AP.

Supondo que tudo corra bem, chegamos à parte que é o objetivo final do usuário final: passar dados.  Os dados do cliente (ou do AP para o cliente) são convertidos de dados digitais em um sinal modulado por RF e transmitidos pelo ar.  Quando recebido, é demodulado, convertido de volta em dados digitais e, em seguida, encaminhado ao seu destino (geralmente a internet ou um recurso na rede interna maior).

A comunicação Wi-Fi só é aprovada para transmitir em frequências específicas. Na maioria das partes do mundo, essas são as bandas de frequência de 2,4 GHz e 5 GHz, embora muitos países também estejam adicionando frequências de 6 GHz. Essas bandas de frequência não são as mesmas que as redes celulares usam, portanto, telefones celulares e Wi-Fi não competem pelo uso das mesmas frequências.  

No entanto, isso não significa que não haja outras tecnologias que possam operar nessas bandas.  Na banda de 2,4 GHz, em particular, há muitos produtos, incluindo Bluetooth, ZigBee, teclados sem fio e equipamentos A/V, apenas para citar um pequeno subconjunto que usa as mesmas frequências e pode causar interferência.  

### Vários dispositivos em um AP

Se vários dispositivos Wi-Fi quiserem se conectar a uma rede, eles podem usar o mesmo AP. Isso oferece uma solução conveniente, tornando o Wi-Fi extensível em ambientes onde a cobertura para muitos usuários é necessária. No entanto, surgem problemas se muitas pessoas precisam de acesso ao mesmo tempo, todas necessitando de altos níveis de largura de banda. 

Por exemplo, se vários usuários estiverem assistindo a vídeos em alta definição ao mesmo tempo, eles podem experimentar quedas de desempenho devido à congestão na camada RF, o que torna difícil ou impossível para o ponto de acesso passar todos os pacotes necessários de maneira oportuna.


## Canais

Canais Wi-Fi são subdivisões da faixa de frequência (como 2,4 GHz ou 5 GHz) para organizar o tráfego e minimizar interferências entre redes vizinhas.

### Banda 2,4 GHz

Tem 13 canais disponíveis no Brasil (numerados 1 a 13), cada um com 20-22 MHz de largura, espaçados a cada 5 MHz. Porém, apenas **1, 6 e 11** são não sobrepostos (sem interferência mútua), ideais para uso — outros se "invadem", causando lentidão.

### Banda 5 GHz

Oferece até 25 canais não sobrepostos (ex: 36, 40, 44, 48, 149, 153, 157, 161), com larguras maiores (40/80/160 MHz) para mais velocidade. Menos interferência, mas alcance menor.

---
## Padrões de rede Wi-Fi

O padrão de rede usado pela arquitetura sem fio é IEEE 802.11. No entanto, esse padrão está em desenvolvimento contínuo e novas alterações surgem regularmente.  As emendas ao padrão são atribuídas a letras, e embora muitas emendas tenham sido lançadas, as mais conhecidas são:  

#### 802.11a

Esta emenda original adicionou suporte para a banda de 5 GHz, permitindo a transmissão de até 54 megabits de dados por segundo. O padrão 802.11a faz uso da multiplexação por divisão de frequência ortogonal (Orthogonal frequency-division multiplexing, OFDM). Ele divide o sinal de rádio em subsinais antes que eles cheguem a um receptor.  O 802.11a é um padrão mais antigo e foi amplamente substituído por tecnologia mais recente.  

#### 802.11b

O 802.11b adicionou taxas mais rápidas na banda de 2,4 GHz ao padrão original. Ele pode passar até 11 megabits de dados em um segundo. Ele usa modulação de codificação de código complementar (Complementary code keying, CCK) para alcançar melhores velocidades. O 802.11b é um padrão mais antigo e foi amplamente substituído por tecnologias mais novas.  

#### 802.11g

O 802.11g padronizou o uso da tecnologia OFDM usada no 802.11a na banda de 2,4 GHz.  Ele era compatível com versões anteriores do 802.11 e do 802.11b. O 802.11g é um padrão mais antigo e foi amplamente substituído por tecnologias mais novas.  

#### 802.11n

Em um determinado momento, o padrão mais popular, o 802.11n, foi a primeira vez que uma especificação unificada abrangeu tanto as bandas de 2,4 GHz quanto as de 5 GHz. Este protocolo oferece melhor velocidade quando comparado com aqueles que vieram antes dele, aproveitando a ideia de transmitir usando várias antenas simultaneamente (geralmente chamada de Multiple In Multiple Out ou tecnologia MIMO). 802.11n é um padrão mais antigo, mas alguns dispositivos mais antigos ainda podem ser encontrados em uso.  

#### 802.11ac

O 802.11ac foi especificado apenas para a banda de 5 GHz.  Ele se baseou nos mecanismos introduzidos em 802.11n.  Embora não tão revolucionário quanto o 802.11n, ele ainda estendeu as velocidades e capacidades na banda de 5 GHz.  A maioria dos dispositivos atualmente na natureza provavelmente são dispositivos 802.11ac.

A tecnologia 802.11ac foi lançada em dois grupos principais, geralmente chamados de “ondas”.  A principal diferença é que os dispositivos da Fase 2 têm mais alguns recursos técnicos quando comparados à Fase 1, mas tudo é interoperável.  

#### 802.11ax (Wi-Fi 6)

O 802.11ax (muito parecido com o 802.11n) unificou a especificação em todas as bandas de frequência aplicáveis.  Em nome da simplicidade, o setor começou a se referir a ele como Wi-Fi 6. O Wi-Fi 6 expandiu as tecnologias usadas para modulação para incluir OFDMA, que permite uma certa quantidade de paralelismo para a transmissão de pacotes dentro do sistema, fazendo uso mais eficiente do espectro disponível e melhorando a taxa de transferência geral da rede.  Wi-Fi 6 é a tecnologia mais recente e é o que a maioria dos novos dispositivos está utilizando.  

### 802.11be (Wi-Fi 7)


#### Outros padrões 802.11

Há muitas outras alterações que foram feitas nos padrões ao longo dos anos (a maioria das letras do alfabeto foi usada ao longo do tempo).  Padrões 802.11 adicionais têm se concentrado em coisas como melhor segurança, maior qualidade de serviço, bem como muitas outras melhorias.