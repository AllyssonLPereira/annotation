---
tags:
  - arquivo
---
Se você já foi responsável pela atribuição de endereços IP, já se deparou com os termos ``classful`` e ``classless`` addressing. Caso contrário, a principal diferença entre endereçamento ``classful`` e ``classless`` está no comprimento da sub-rede: 


> [!NOTE] Definição
> *O endereçamento **`classful`** usa máscaras de sub-rede de **comprimento fixo**, enquanto o **`classless`** usa máscaras de sub-rede de **comprimento variável** - `VLSM` - Variable Length Subnet Masks -*.

Vamos analisar mais detalhadamente o endereçamento ``classful`` e ``classless``, a história e o propósito por trás deles, e as razões pelas quais o endereçamento `classless` realmente prevaleceu.

---
## O que é endereçamento `classful`?

O endereçamento `classful` é uma arquitetura de endereçamento IPv4 que divide os endereços em cinco grupos.

Antes do endereçamento `classful`, os primeiros oito bits de um endereço IP definiam a rede da qual um determinado host fazia parte. Isso teria o efeito de limitar a internet a apenas 254 redes. Cada uma dessas redes continha `16.777.216` endereços IP diferentes. 

À medida que a internet crescia, a ineficiência de alocar endereços IP dessa maneira se tornou um problema. Afinal, existem muito mais do que 254 organizações que precisam de endereços IP e muito menos redes que precisam de 16,7 milhões de endereços IP para si mesmas.

Simplificando: precisávamos de uma maneira de alocar endereços de forma mais eficiente. Em 1981, a `RFC791` e o endereçamento `classful` surgiram para ajudar a resolver esse problema. Com os endereços `classful`, passamos de apenas 254 redes disponíveis para 2.113.664 redes disponíveis.

Como?

---
## Como funciona o endereçamento `classful`

*O endereçamento `classful` divide o espaço de endereços IPv4 - `0.0.0.0` - `255.255.255.255` - em 5 classes: `A, B, C, D e E`*. No entanto, apenas A, B e C são usados ​​para hosts de rede. A Classe D, que abrange o intervalo de endereços IP `224.0.0.0` - `239.255.255.255`, *é reservada para multicast*, e a Classe E - `240.0.0.0` - `255.255.255.255` - *é reservada para "uso futuro"*.

A tabela abaixo detalha a máscara de rede padrão - máscara de sub-rede, os intervalos de endereços IP, o número de redes e o número de endereços por rede de cada classe de endereço.

![[table_ipv4_address_class.png]]

Como podemos ver, a Classe A continua a usar os primeiros 8 bits de um endereço e pode ser adequada para redes muito grandes. A Classe B é para redes muito menores que a Classe A, mas ainda assim grandes por si só. Os endereços da Classe C são adequados para redes pequenas.

---
## Quais são as limitações do endereçamento IP `classful`?

Como você provavelmente pode imaginar, a internet está ávida por endereços IP. Embora o endereçamento IP `classful` fosse muito mais eficiente do que o antigo método dos "primeiros 8 bits" de dividir o espaço de endereços IPv4, ainda não era suficiente para acompanhar o crescimento.

À medida que a popularidade da internet continuou a crescer após 1981, ficou claro que alocar blocos de 16.777.216, 65.536 ou 256 endereços simplesmente não era sustentável. Endereços estavam sendo desperdiçados em blocos muito grandes, e estava claro que chegaria um ponto crítico em que ficaríamos sem espaço para endereços IP.

Uma das melhores maneiras de entender por que isso era um problema é considerar uma organização que precisava de uma rede um pouco maior do que uma Classe C. Por exemplo, suponha que nossa organização de exemplo precise de 500 endereços IP. 

Mudar para uma rede Classe B significa desperdiçar 65.034 endereços - 65.534 endereços de host Classe B utilizáveis ​​menos 500. Da mesma forma, se precisasse de apenas 2 endereços IP públicos, uma rede Classe C desperdiçaria 252, 254 endereços utilizáveis ​​– 2.

De qualquer forma, os endereços IP sob o protocolo IPv4 estavam se esgotando, seja por desperdício ou pelos limites superiores do sistema.

> [!NOTE] Você sabia?
> Há um limite calculado de *4.294.967.296 endereços IPv4*, e eles se esgotaram em 21 de abril de 2017.

---
## O que é endereçamento `classless`?

O endereçamento `classless` é uma arquitetura de endereçamento IPv4 que *utiliza mascaramento de sub-rede de comprimento variável*.

A solução viria em 1993, quando o `Classless Inter-Domain Rotation` - `CIDR` - introduziu o conceito de endereçamento `classless`. *Veja bem, com o endereçamento `classful`, o tamanho das redes é **fixo***. 

*Cada intervalo de endereços tem uma máscara de sub-rede padrão*. O endereçamento `classless`, no entanto, desvincula os intervalos de endereços IP de uma máscara de sub-rede padrão, permitindo o mascaramento de sub-rede de comprimento variável - ``VLSM``.

Usando o endereçamento `classless` e o `VLSM`, os endereços podem ser alocados com muito mais eficiência. Isso ocorre porque os administradores de rede podem escolher máscaras de rede e, por sua vez, blocos de endereços IP com o tamanho certo para qualquer finalidade.

---
## Como funciona o endereçamento `classless`?

*Em um nível mais amplo, o endereçamento `classless` funciona permitindo que endereços IP recebam máscaras de rede arbitrárias, independentemente da "classe"*. Isso significa que as máscaras de rede `/8` - `255.0.0.0`, `/16` - `255.255.0.0` - e `/24` - `255.255.255.0` - podem ser atribuídas a qualquer endereço que tradicionalmente estaria na faixa de Classe A, B ou C. 

*Além disso, isso significa que não estamos mais presos a `/8`, `/16` e `/24` como nossas únicas opções, e é aí que o endereçamento `classless` se torna muito interessante*.

Voltando à nossa organização de exemplo, se precisarmos de 500 endereços IP, usar uma calculadora de sub-rede nos diz que um bloco `/23` é muito mais eficiente do que uma alocação de Classe B. `/23` nos dá 510 endereços de host utilizáveis. 

Isso significa que, ao mudar para o endereçamento `classless`, evitamos o desperdício de mais de 65.000 endereços. Da mesma forma, se precisarmos apenas dos dois hosts, um `/30` economiza 250 endereços.

![[classless-vs-classful-comparison-addresses.png]]

---
## O que é "sub-rede `classless`" e qual a diferença?

Você frequentemente ouvirá as pessoas se referirem ao termo "sub-rede `classless`" de forma intercambiável com "endereçamento `classless`", já que os termos geralmente se referem à mesma coisa. Sub-rede `classless` é simplesmente o uso de `VLSM` para sub-redes em suas redes.

Há também a questão da classe e da sub-rede. A diferença fundamental entre sub-rede `classless` e sub-rede `classful` é: *as máscaras de rede devem ser definidas explicitamente na sub-rede `classless`, enquanto as máscaras de rede são implícitas na sub-rede `classful`*. O que isso significa exatamente?

Considere o endereço IP `192.168.11.11`. Com o endereçamento IP `classful`, você sabe que é um endereço de Classe C. Isso significa que você também sabe que a máscara de rede é `255.255.255.0` - `/24`. *Em um endereço `classful`, o formato do endereço IP implica a máscara de rede. Não há opção*.

No entanto, com o endereçamento `classless`, saber apenas o endereço IP não significa que você tenha a máscara de rede. *Você precisa ser explicitamente informado sobre ela*.

---
## Quais são as vantagens do endereçamento `classless`?

Em uma palavra, o endereçamento `classless` pode ser resumido como: ***eficiente***.

Especificamente, como podemos ver na `RFC4632`, o endereçamento `classless` ajudou a resolver três problemas principais e oferece as seguintes vantagens:

- *Mais alocações de endereços IP*. 

	Hoje, sabemos que o IPv6 é nossa solução de longo prazo para o problema de esgotamento de endereços IP. No entanto, o IPv6 ainda não é amplamente utilizado. No início da década de 1990, estava claro que esgotaríamos rapidamente o espaço de endereços IPv4 se nada mudasse. 

	Como resultado, o endereçamento `classless` foi usado como uma solução de médio prazo para nos ajudar a estender a vida útil do IPv4.


* *Uso mais equilibrado dos intervalos de endereços IP*. 

	O endereçamento `classless` desvinculou a relação entre o tamanho da rede e o endereço IP e permitiu o uso equilibrado entre o que costumava ser os intervalos de Classe A, B e C. 


- *Muito menos endereços desperdiçados. Roteamento mais eficiente*.

	`VLSM` e sub-redes possibilitam agregação de rotas e protocolos de roteamento `classless`. Com a agregação de rotas - às vezes chamada de sumarização de rotas ou super-redes, as tabelas de roteamento podem ser menores, reduzindo o consumo de recursos em roteadores e economizando largura de banda. 

	Além disso, a inclusão de máscaras de rede em protocolos de roteamento permite que rotas mais específicas sejam anunciadas. Por exemplo, `198.51.100.0/29` nos diz mais do que `198.51.100.0` - com um `/24` implícito.

É claro que, como qualquer pessoa que tenha estudado para obter uma certificação em redes pode dizer, há um aumento significativo na complexidade entre o endereçamento `classful` e o `classless`. 

Com o endereçamento `classful`, você sempre pode inferir a sub-rede a partir do endereço IP. Com o endereçamento `classless` e o `VLSM`, as máscaras de rede devem ser definidas explicitamente. 

Da mesma forma, existem complexidades com o roteamento `classless` que não existem com o roteamento `classful`. Com o roteamento `classful`, uma tabela de roteamento pode ter várias correspondências para um único endereço IP. No geral, há muito mais para aprender e manter em ordem.

No entanto, as vantagens do endereçamento `classless` superam em muito as compensações de complexidade. Como resultado, o endereçamento `classless` tornou-se uma parte fundamental do funcionamento das sub-redes — e até mesmo da internet.