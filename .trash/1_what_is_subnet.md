---
tags:
  - arquivo
---
## What is subnetting?

***[Uma sub-rede é simplesmente um intervalo de endereços IP]***. Todos os dispositivos na mesma sub-rede podem se comunicar diretamente uns com os outros sem passar por roteadores. No IPv4, uma interface de rede é conectada a apenas uma sub-rede e possui apenas um endereço IP. 

Meu laptop está em uma sub-rede que também inclui um servidor, uma impressora, algumas outras estações de trabalho e um roteador. Se eu quiser me comunicar com outro dispositivo na minha sub-rede, posso enviar pacotes diretamente para ele. 

Se não estiver na minha sub-rede, preciso encaminhar o pacote para um roteador primeiro. Esse roteador também precisa estar na minha sub-rede. *Meu computador sabe que outro dispositivo está na minha sub-rede observando meu próprio endereço IP e minha máscara de sub-rede.

Suponha que meu endereço IP seja `192.168.101.15` e minha máscara de sub-rede seja `255.255.255.0`. Há 32 bits no endereço IP e o mesmo número na máscara. Sempre escrevemos esses 32 bits como quatro números de 8 bits, frequentemente chamados de ***octetos***. 

*O que pode causar confusão é que usamos a notação decimal para cada um desses números de 8 bits, mas a mecânica da sub-rede, na verdade, acontece em binário.

Vejamos o endereço IP lado a lado com a máscara em notação decimal e binária:

$$[192.168.101.15] = 1100 0000 . 1010 1000 . 0110 0101 . 0000 1111$$
$$[255.255.255.0] = 1111 1111 . 1111 1111 . 1111 1111 . 0000 0000$$
 

A parte da rede é `192.168.101.xx` e a parte do host é `xx.xx.xx.15` - *para simplificar um pouco, sempre agrupamos todos os 1s à esquerda e todos os zeros à direita da máscara.

Qualquer outro dispositivo com a mesma parte da rede faz parte da minha sub-rede. Portanto, `192.168.101.1` faz parte da minha sub-rede e `192.168.101.100` faz parte da minha sub-rede, mas `192.168.102.15` não faz parte da minha sub-rede e preciso passar pelo roteador para alcançá-lo.

$$[192.168.101.0] = 1100 0000 . 1010 1000 . 0110 0101 . 0000 0000$$
$$[192.168.101.1] = 1100 0000 . 1010 1000 . 0110 0101 . 0000 0001$$
$$[192.168.101.15] = 1100 0000 . 1010 1000 . 0110 0101 . 0000 1111$$
$$[192.168.102.15] = 1100 0000 . 1010 1000 . 0110 0110 . 0000 1111$$
$$[255.255.255.0] = 1111 1111 . 1111 1111 . 1111 1111 . 0000 0000$$

Observe os dois últimos bits destacados do terceiro octeto no endereço `192.168.102.15`. Em vez de ser "*01100101*", é "*0110110*". Como essa diferença ocorre na parte "rede" do endereço - onde a máscara tem 1s em vez de 0s, este endereço está em uma sub-rede diferente.

---
## Special addresses and subnets

Agora, pense apenas na parte do host do endereço. Em nosso exemplo - `192.168.101.15/24`, a parte do host é `.15`. A máscara é `/24`. Isso significa que oito bits - `32 - 24 = 8` - estão disponíveis para especificar o host.

Se eu escrever `15` em binário, obtenho *0000 1111* - *É convencional escrever esses valores binários de 8 bits como dois grupos de quatro com um espaço entre eles, pois são mais fáceis de ler dessa forma.

O menor valor neste intervalo de sub-rede é *0000 0000*, que é o número decimal `0`. O maior é *1111 1111*, que é o número decimal `255`. É a isso que me refiro quando digo "todos 0" e "todos 1". 

Esses dois valores são reservados para o endereço de rede - *para se referir a toda a rede* - e *para transmissões locais na sub-rede*, respectivamente. Você não pode atribuí-los a nenhum host — embora haja exceções a essa regra, sobre as quais falarei em breve.

Como resultado, embora existam `256` valores possíveis para um número de 8 bits, há apenas `254` endereços de host permitidos em uma sub-rede `/24`.

Embora muitos de nós estejamos familiarizados com os intervalos especiais de endereços IP privados, como `10.0.0.0/8` e `192.168.0.0/16`, existem alguns outros endereços IP especiais que você também pode consultar e que são usados ​​para diversas finalidades.

---
## Subnet masks

*`/24` é um tamanho de sub-rede muito comum*. É fácil de entender porque a parte da rede do endereço corresponde aos três primeiros octetos e a parte do host corresponde ao último octeto.

Você pode simplesmente ler as informações da sub-rede. Quaisquer dois endereços com os mesmos três primeiros octetos estão na mesma sub-rede.

Eu realmente gosto de usar sub-redes `/24` justamente porque elas são muito fáceis de ler e lembrar. Uma das minhas regras pessoais de design de rede é que, quando alguém me liga às 3 da manhã para solucionar um problema, provavelmente é melhor não ter que pensar muito.

Mas existem alguns bons motivos para usar outros tamanhos de sub-redes. Por exemplo, você pode querer conservar endereços em uma sub-rede que você sabe que nunca terá muitos dispositivos. Ou pode precisar criar uma sub-rede com centenas de dispositivos. Em ambos os casos, você vai querer um tamanho de sub-rede diferente.

Se você tiver uma sub-rede com máscara `/25`, em vez de oito bits livres para a parte do host do endereço, você terá apenas sete bits - `32 - 25 = 7`. $2^7$ é 128. Assim como no caso `/24`,  na qual você não pode usar endereços de host 0 ou 1, isso deixa `126` endereços de host possíveis.

Eu Incluí os nomes de classe antigos na tabela, mas é importante saber que ***a internet não reconhece mais o conceito de classe***. É também por isso que o "C" na notação `CIDR` estilo "`/24`" significa "`Classless`" - *sem classe*.

Observe as duas últimas entradas, que violam as regras de que todos os endereços de host 0 e 1 são ilegais. *Antigamente, a única maneira de obter uma sub-rede ponto a ponto com dois dispositivos era usar uma sub-rede `/30`. 

Mas o problema com a sub-rede `/30` é que ela desperdiça metade do alcance, pois cada sub-rede `/30` tem quatro endereços de host, dos quais dois são todos 0 e todos 1, que são necessários como endereço de rede e endereço de broadcast.

Portanto, *a `RFC 3021` foi introduzida para permitir o uso de sub-redes `/31` especificamente para links ponto a ponto que não exigem broadcast local*. Nessas redes, qualquer pacote enviado por um nó deve ser destinado ao outro nó, pois não há outras possibilidades.

*A sub-rede `/32` é usada para coisas como endereços de loopback internos, onde há apenas um dispositivo em uma sub-rede*. Interfaces de loopback são frequentemente usadas por dispositivos de rede, como roteadores, para fornecer uma interface sempre ativa.

---
## Saving time with CIDR notation

Temos falado sobre a notação de máscara de rede tradicional. Mas antes de prosseguirmos, deixe-me falar sobre outra notação chamada `CIDR` - `Classless Inter-Domain Routing - Roteamento Inter-Domínio sem Classes` - https://www.techtarget.com/searchnetworking/definition/CIDR.

O problema com a notação de máscara de rede tradicional é que, olhando para ela, você pode pensar que pode ter uma sequência arbitrária de 1s e 0s. Então, você poderia tornar quaisquer dois endereços parte da mesma sub-rede. Isso seria extremamente confuso para um humano ler, mas não traria nenhum benefício em termos de roteamento ou de fornecer mais espaço de endereço, portanto, não é permitido.

Todos os 1s devem estar à esquerda e todos os 0s à direita. Portanto, o que realmente importa é quantos 1s existem. Você nem precisa contar os 0s separadamente, pois precisam ser 32 bits no total.

Em nosso exemplo, a máscara é `255.255.255.0`. São três grupos de oito 1s seguidos por oito 0s. Portanto, podemos dizer tudo o que há para saber sobre essa máscara simplesmente especificando que existem 24 1s - $3 × 8 = 24$, e escrevemos isso como `/24`. Na notação `CIDR`, nosso endereço de exemplo e as informações de sub-rede podem ser escritos como `192.168.101.15/24`.

Se você não gosta da notação `CIDR`, tudo bem. Eu também não gostei no começo, mas realmente economiza muito tempo e espaço ao escrever endereços.

---
## Determinando endereços em um intervalo de sub-rede

Até agora, espero que tudo pareça bem simples. Há apenas uma parte difícil em descobrir sub-redes: saber quais endereços estão incluídos em um intervalo específico. Existem alguns truques que podem ajudar e evitar conflitos de endereços IP.

O primeiro truque é que o endereço totalmente 0 é um número binário que necessariamente termina em zero, o que significa que é sempre um número par. Portanto, exceto para as sub-redes `/31` e `/32`, o primeiro endereço utilizável em qualquer intervalo é sempre um número ímpar. Da mesma forma, o endereço totalmente 1 é sempre um número ímpar. Portanto, o último endereço utilizável deve ser par.

O segundo truque é lembrar os números na coluna do meio da tabela acima, *as potências de dois*. Você realmente precisa se lembrar das potências de dois até $2^8$. Em seguida, você conta pela potência de dois apropriada - `1, 2, 4, 8, 16, 32, 64, 128, 256` – basta memorizá-los.

Eis o que quero dizer. Se estou usando uma sub-rede `/28`, primeiro subtraio 28 de 32, que é 4. Lembro que $2^4 = 16$. Isso me diz para contar de 1 em 16. A primeira sub-rede é `xx.xx.xx.0/28`. Para obter a segunda sub-rede, adiciono 16: `xx.xx.xx.16/28`, depois `xx.xx.xx.32/28` e `xx.xx.xx.48/28`, e assim por diante.

| Tipo             | Endereço                  |
| ---------------- | ------------------------- |
| Endereço de rede | 192.168.1.0 (não usável)  |
| Primeiro host    | 192.168.1.1 ✅             |
| ...              | ...                       |
| Último host      | 192.168.1.14 ✅            |
| Broadcast        | 192.168.1.15 (não usável) |

Esses valores me indicam o primeiro e o último host em cada intervalo. Para `xx.xx.xx.0/28`, são `.1` e `.14`. Para `xx.xx.xx.16/28`, são `.17` e `.30`, e assim por diante. Observe que o primeiro endereço é sempre ímpar e o último é sempre par.

| Bloco/Sub-rede    | Intervalo de IPs    | Hosts válidos       |
| ----------------- | ------------------- | ------------------- |
| `192.168.1.0/28`  | 192.168.1.*0 – 15*  | 192.168.1.*1 – 14*  |
| `192.168.1.16/28` | 192.168.1.*16 – 31* | 192.168.1.*17 – 30* |
| `192.168.1.32/28` | 192.168.1.*32 – 47* | 192.168.1.*33 – 46* |

***E quanto a intervalos maiores?***

Também podemos criar sub-redes maiores que os 254 endereços disponíveis em uma sub-rede `/24`.

Pense em `/23`. Há 32 bits no endereço, portanto, se a máscara tiver 23 bits, haverá 9 bits disponíveis para os hosts. Isso significa todos os bits do quarto octeto no endereço IP e um bit do terceiro. Na notação de máscara de rede, isso seria `255.255.254.0`. Vejamos um exemplo.

Suponha que nossa sub-rede seja `10.11.12.0/23`. O primeiro endereço neste intervalo é obviamente `10.11.12.1`, mas o último é, na verdade, `10.11.13.254`. Observe que o terceiro octeto é 13. Observe a representação binária do endereço e da máscara para entender por que isso é verdade.

$$10.11.12.0    = 0000 1010 . 0000 1011 . 0000 1100 . 0000 0000$$
$$10.11.13.0    = 0000 1010 . 0000 1011 . 0000 1101 . 0000 0000$$
$$255.255.254.0 = 1111 1111 . 1111 1111 . 1111 1110 . 0000 0000$$

Todos os endereços entre `10.11.12.1` e `10.11.13.254` estão incluídos nesta sub-rede. Isso inclui `10.11.12.255` e `10.11.13.0`, mas muitos administradores de rede evitam esses endereços por motivos supersticiosos, mesmo sendo endereços válidos. 

Não é totalmente supersticioso. Se você usar esses endereços e um ou mais hosts na rede estiverem configurados incorretamente para usar a máscara de sub-rede `/24`, mais comum, você poderá acabar vendo tráfego para esses dois hosts enviado como broadcasts em vez de pacotes unicast diretos.

Podemos criar sub-redes com intervalos ainda maiores, como `/22` ou `/11`. Mas a boa notícia é que você não precisa memorizar várias potências de 2 para elas. Em vez disso, basta aplicar as regras que discutimos acima para `/24 e /32`, mas em um octeto diferente do endereço.

Com isso, quero dizer que `/16` é como `/24`, mas no terceiro octeto. Da mesma forma, `/17` é como `/25`, e assim por diante. Por exemplo, se minha sub-rede fosse `10.12.0.0/20`, eu poderia pensar na análise que acabamos de fazer para `/28` - porque 20 bits são 4 a mais que 16, assim como 28 é 4 a mais que 24.

Então, onde determinamos que `/28` corresponde a uma máscara de `255.255.255.240`, recuamos um octeto para obter a máscara para `/20`, `255.255.240.0`. E, assim como contamos de 16 em 16 para obter as sub-redes para `/28`, contamos de 16 em 16 para obter as sub-redes para `/20`. Eles seriam `xx.xx.0.0/20`, `xx.xx.16.0/20`, `xx.xx.32.0/20` e assim por diante.

E nossos hosts em cada um desses intervalos seriam executados do primeiro valor ímpar ao último valor par: `xx.xx.0.1` a `xx.xx.15.254`. Isso é um pouco diferente de simplesmente copiar o quarto octeto de `/28` para o terceiro octeto de `/20`, porque podemos usar 0 e 15. Só não podemos usar o primeiro - `xx.xx.0.0` - e o último endereço - `xx.xx.15.255` - do intervalo.

---
## Você realmente precisa de sub-redes tão grandes?

É aqui que encontramos um dos aspectos interessantes do roteamento TCP/IP. Você provavelmente não quer lidar com uma sub-rede `/20` ou `/9`. Isso é simplesmente muitos hosts em um segmento. As transmissões para ARP em qualquer rede Ethernet criariam um sério problema de congestionamento. Mas você pode simplificar bastante as tabelas de roteamento usando a *sumarização*.

A sumarização funciona assim: suponha que eu esteja trabalhando com monitoramento de rede baseado em nuvem e tenha uma rede grande que usa apenas `10.0.0.0/8`. Mas suponha que eu tenha alocado meus endereços para que minha rede de Montreal use `10.1.4.0/24`, `10.1.5.0/24`, `10.1.6.0/24` e `10.1.7.0/24`. E suponha que minha rede de Toronto use `10.1.8.0/24` e `10.1.9.0/24`. *Um roteador central que precisa enviar tráfego para ambos os sites poderia ter todas essas seis sub-redes em sua tabela de roteamento, ou poderíamos resumir*.

Podemos notar que os 4 intervalos de Montreal são todos sub-redes de `10.1.4.0/22`, e os 2 intervalos de Toronto são sub-redes de `10.1.8.0/23`. Agora, preciso apenas de 2 entradas de rota.

E eu poderia subdividir ainda mais qualquer um desses intervalos. Por exemplo, `10.1.4.0/24` pode, na verdade, consistir em `10.1.4.8/28`, `10.1.4.16/28` e `10.2.4.252/30`. O resumo ainda funciona. Não preciso de mais entradas na tabela de roteamento no meu roteador central.

E é importante ressaltar que o TCP/IP tem uma maneira eficiente de lidar com exceções. Suponha que a rede de Toronto também tenha `10.1.4.248/30`. Neste caso, eu poderia deixar a rota resumida para Montreal, `10.1.4.0/22`, e adicionar apenas esta exceção para apontar para Toronto: `10.1.4.248/30`.

Ao rotear pacotes, um roteador sempre selecionará a "melhor" ou "mais longa" correspondência. Portanto, você pode ter uma rota `/22` como resumo e, em seguida, lidar com exceções individuais. Qualquer coisa que corresponda a uma das exceções com um número maior - maior número após a "/" - será roteada de acordo com essa regra.

Você já está familiarizado com este conceito de regras e exceções de resumo. O roteador tem uma rota resumida para tudo, chamada de "rota padrão", `0.0.0.0/0`. A rota padrão corresponde a todos os endereços possíveis. Normalmente, ela aponta para a Internet pública. Seus roteadores terão rotas mais específicas para todas as suas redes internas, e a rota padrão enviará todo o resto para a Internet.

Ok, então determinar endereços de sub-rede não é tão difícil assim. Se você pensar por um minuto no que está fazendo, verá que realmente não precisa de uma dessas calculadoras de sub-rede. E, na verdade, pensar no que está fazendo provavelmente é uma boa ideia de qualquer maneira.

---

``` shell
[Subnetting]
│
├── IP + Máscara = Rede + Host
│   └── Ex: 192.168.101.15/24 → Rede: 192.168.101.0
│
├── CIDR (/n)
│   └── Quantos bits 1 na máscara
│
├── Hosts disponíveis
│   └── 2^n - 2 (exceto /31 e /32)
│
├── Tamanho da sub-rede
│   └── Quanto menor o /n, mais hosts
│
└── Dicas
    ├── Lembrar potências de 2
    ├── Contar em saltos (16 em 16 para /28, etc.)
    └── Primeiro IP = ímpar, Último = par (em geral)

```
