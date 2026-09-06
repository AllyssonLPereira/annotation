
## Classes de Endereços IPv4  

Antes de entrar no assunto CIDR, vamos revisar as classes de endereços IPv4 para que possamos, então, compreender a necessidade do endereçamento IPv4 sem classes (*classless*).

Existem cinco classes de endereços IPv4: A, B, C, D e E. Os endereços de Classe A têm um primeiro octeto que começa com 0, e o restante dos bits pode ser 0 ou 1. Isso resulta em uma faixa decimal para o primeiro octeto de 0 a 127. 

Lembre-se de que um endereço IPv4 tem 32 bits; portanto, há 4 octetos — 4 grupos de 8 bits — em um endereço IPv4. Isso faz com que a faixa de endereços da Classe A vá de 0.0.0.0 até 127.255.255.255. Lembre-se de que existem alguns endereços especiais e reservados nessas faixas que não podem ser usados como endereços IP normais em um dispositivo, mas, para este vídeo, vamos incluir todos eles na Classe A.

Os endereços de Classe B têm um primeiro octeto que começa com 1 0, e os outros 6 bits podem ser 0 ou 1. Isso resulta em uma faixa para o primeiro octeto de 128 a 191. A faixa de endereços para a Classe B vai de 128.0.0.0 até 191.255.255.255. 

Os endereços de Classe C têm os três primeiros bits definidos como 1 1 0, e os outros podem ser 0 ou 1. Se você escrever essa faixa em decimal, ela vai de 192 a 223. Portanto, a faixa de endereços é de 192.0.0.0 até 223.255.255.255.

Os endereços de Classe D começam com 1 1 1 0 em binário, o que resulta em uma faixa de 224 a 239 para o primeiro octeto do endereço. Isso significa que a faixa de endereços para a Classe D vai de 224.0.0.0 a 239.255.255.255.

Por fim, os endereços de Classe E começam com 1 1 1 1 em binário; portanto, a faixa do primeiro octeto vai de 240 a 255 e, consequentemente, a faixa de endereços vai de 240.0.0.0 a 255.255.255.255.  

No entanto, apenas os endereços das Classes A, B e C podem ser atribuídos a um dispositivo como endereço IP, já que as Classes D e E possuem finalidades especiais que mencionei nos vídeos sobre endereçamento IPv4.

Os endereços de Classe A têm um comprimento de prefixo /8, o que significa que o primeiro octeto identifica a rede e os outros três octetos são usados para hosts individuais dentro da rede. 

Os endereços de Classe B têm um comprimento de prefixo /16; assim, os dois primeiros octetos identificam a rede, e os dois últimos octetos identificam hosts individuais dentro dessa rede. 

Os endereços de Classe C têm um comprimento de prefixo /24; portanto, os três primeiros octetos são usados para identificar a rede, e apenas o último octeto é usado para identificar hosts individuais dentro dessa rede.  

Os diferentes comprimentos de prefixo conferem características distintas a essas classes. Como você pode ver, existem poucas redes de Classe A disponíveis — apenas 128, ou na verdade menos que isso, pois algumas são reservadas, como a faixa 127.0.0.0/8, que, como você deve se lembrar, é usada para endereços de loopback. 

Como apenas o primeiro octeto de um endereço de classe A é usado para o ID da rede, há três octetos inteiros disponíveis para endereços dentro de cada rede de classe A; portanto, existem 16.777.216 endereços em cada rede de classe A. Isso equivale a 2 elevado à 24ª potência, pois são 3 octetos e 3 vezes 8 resulta em 24 bits.

Os endereços de classe B são diferentes: há mais redes de classe B — 16.384 —, mas menos endereços por rede — 65.536 —, o que ainda representa um número muito grande de endereços, é claro. 

Por fim, existem muitas redes de classe C — 2.097.152 redes —, mas apenas 256 endereços por rede.  

## Atribuição de Endereços IPv4  

Então, como uma empresa obtém sua própria rede para utilizar? Bem, os endereços IP são atribuídos a empresas ou organizações por uma corporação americana sem fins lucrativos chamada IANA, a Internet Assigned Numbers Authority (Autoridade para Atribuição de Números da Internet). 

A IANA atribui endereços IPv4 e redes às empresas com base em seu porte. Por exemplo, uma empresa de grande porte pode receber uma rede de classe A ou classe B — lembre-se de que há muitos endereços disponíveis para hosts em cada rede de classe A e de classe B —, enquanto uma pequena empresa pode receber uma rede de classe C, pois há menos endereços em cada rede de classe C: apenas 256.

No entanto, esse sistema gerava muito desperdício de endereços IP; por isso, foram criados vários métodos para aprimorá-lo. Deixe-me dar um exemplo de como esse sistema rígido de endereçamento pode levar ao desperdício de endereços IP.  

Aqui temos dois roteadores. Como você pode ver, o R1 tem três redes conectadas a ele. Lembre-se de que roteadores são usados para conectar redes diferentes; portanto, cada uma dessas conexões é distinta — redes de Camada 3, redes IP diferentes.

O R2 também tem três redes conectadas aqui. Talvez cada uma dessas redes tenha alguns switches, com muitos dispositivos finais, como PCs e servidores, conectados a esses switches. No entanto, há mais uma rede aqui.

É esta rede que conecta esses dois roteadores. Ela é conhecida como rede "ponto a ponto", o que significa que é uma rede que conecta dois pontos — neste caso, o R1 e o R2.

Por exemplo, essa pode ser uma conexão entre escritórios em cidades diferentes; digamos, São Francisco e Nova York.  

Então, como se trata de uma conexão ponto a ponto, não precisamos de um grande bloco de endereços, então vamos usar uma rede classe C, 203.0.113.0/24.

Como se trata de uma rede classe C, existem 256 endereços na rede. Menos 1 para o endereço de rede, 203.0.113.0, menos um para o endereço de broadcast, 203.0.113.255, menos um para o endereço do R1, que vou definir como 203.0.113.1, e menos 1 para o endereço do R2, que vou definir como 203.0.113.2.  

Isso totaliza 4 endereços utilizados e 252 endereços DESPERDIÇADOS. Claramente, esse não é um sistema ideal.  

Antes de apresentar o CIDR, aqui está outro exemplo rápido de desperdício de endereços. Uma empresa, a empresa X, precisa de endereçamento IP para 5.000 hosts finais. Isso é um problema. Por quê?

Uma rede classe C não fornece endereços suficientes, então é necessário atribuir uma rede classe B. Como uma rede classe B permite cerca de 65.000 endereços, isso resulta em aproximadamente 60.000 endereços desperdiçados.  

## CIDR  

Quando a Internet foi criada, seus idealizadores não previram que ela se tornaria tão grande quanto é hoje. Isso resultou em desperdício de espaço de endereçamento, como nos exemplos que mostrei a vocês, e há muitos outros exemplos que eu poderia apresentar. 

O espaço total de endereços IPv4 inclui mais de 4 bilhões de endereços, e isso parecia um número enorme de endereços quando o IPv4 foi criado; mas agora o esgotamento do espaço de endereçamento é um grande problema — não há endereços suficientes. Uma maneira de resolver ou remediar isso é o CIDR. 

A IETF (Internet Engineering Task Force) introduziu o CIDR em 1993 para substituir o sistema de endereçamento com classes (*classful*). Com o CIDR, as exigências de que "endereços de classe A devem usar uma máscara de rede /8, classe B deve usar /16 e classe C deve usar /24" foram eliminadas.

Isso permitiu que redes maiores fossem divididas em redes menores, proporcionando maior eficiência. Essas redes menores são chamadas de "sub-redes" (*subnets*). 

Vamos ver um exemplo de divisão de uma rede maior em uma rede menor para que você possa entender como isso funciona. Aqui está a mesma rede ponto a ponto que analisamos anteriormente. Antes, havia sido atribuído a ela o espaço de rede 203.0.113.0/24, mas isso resultava em muito desperdício de endereços. 

Vamos escrever isso em binário. Aqui está o binário, com a notação decimal pontuada logo abaixo. Agora, o comprimento do prefixo é /24; portanto, aqui está a máscara de rede — também conhecida como máscara de sub-rede: 255.255.255.0.  

Lembre-se: todos os dígitos "1" na máscara de sub-rede indicam que o bit correspondente no endereço faz parte da porção de rede. Neste caso, coloquei a porção de rede em azul, e a porção de host está em vermelho. Bem, quantos bits de host existem? 8, pois trata-se de um octeto.

Então, quantos hosts potenciais, ou quantos endereços utilizáveis existem? Bem, a fórmula é esta: 2 elevado à oitava potência, menos 2, é igual a 254 endereços utilizáveis. O que é esse 8? Bem, é o número de bits de host, que é 8 neste caso. E por que menos 2? Esses são o endereço de rede e o endereço de broadcast; não podemos atribuí-los a um dispositivo, então temos que subtraí-los do número de endereços utilizáveis.  

Portanto, temos 254 endereços utilizáveis, mas precisamos apenas de dois: um para o R1 e outro para o R2.  

### Número de endereços utilizáveis por sub-rede  
  
No entanto, o CIDR nos permite atribuir diferentes tamanhos de prefixo; não precisa ser /24. Vamos praticar o cálculo do número de hosts com diferentes tamanhos de prefixo. 

203.0.113.0/25, 203.0.113.0/26, 203.0.113.0/27, /28, /29, /30, /31 e, finalmente, /32. 

Eu coloquei /31 e /32 em vermelho porque são casos um pouco especiais; você verá quando tentar calculá-los. Então, pause o vídeo aqui e tente calcular quantos endereços utilizáveis existem em cada rede... ok, vamos conferir as respostas.  

Então, aqui temos o 203.0.113.0, mas desta vez com uma máscara /25. Observe que a parte de rede do endereço se estendeu até o primeiro bit do último octeto, e a máscara em notação decimal pontuada agora é escrita como 255.255.255.128.

Mudei a cor do bit extra para roxo, mas ele faz parte da porção de rede, a parte azul. Se você não se lembra de como converter de binário para decimal pontuado, certifique-se de revisar isso; é muito importante para a criação de sub-redes.  

Agora há 7 bits na parte de host do endereço, então o número de endereços utilizáveis é 2 elevado à sétima potência, menos 2, o que resulta em 126. Mais uma vez, precisamos de apenas 2 endereços, um para o R1 e outro para o R2, então desperdiçaremos 124 endereços.

Isso é melhor do que desperdiçar 252 endereços com um prefixo /24, mas ainda assim é um desperdício.  

Que tal um prefixo /26? Observe que agora ele é escrito como 255.255.255.192 em decimal pontuado, porque dois bits do último octeto agora fazem parte da porção de rede. 

Como existem 6 bits de host, agora há 62 endereços utilizáveis nesta rede. Se fôssemos usar uma máscara de rede /26 para a rede 203.0.113.0, desperdiçaríamos 60 endereços. Está ficando melhor, mas podemos tornar essa rede ainda menor.  

Agora que você entendeu a ideia, vamos acelerar o processo. Para um comprimento de prefixo /27, a máscara é escrita como 255.255.255.224 em notação decimal pontuada. Agora temos 5 bits de host, o que significa que existem 30 endereços utilizáveis. 

Como você pode ver, o espaço de endereçamento fica cada vez menor à medida que estendemos a máscara de rede. Para um comprimento de prefixo /28, a máscara é escrita como 255.255.255.240 em notação decimal pontuada. Agora há apenas 4 bits de host, o que significa que existem 14 endereços utilizáveis. 

Após atribuir endereços ao R1 e ao R2, isso resultaria em apenas 12 endereços desperdiçados. Mas podemos tornar esse espaço de endereçamento ainda menor, para tornar nosso endereçamento ainda mais eficiente.  

Se usarmos um comprimento de prefixo /29, a máscara é escrita como 255.255.255.248 em notação decimal pontuada. Agora temos apenas 3 bits de host, o que significa que existem apenas 6 endereços utilizáveis. Novamente, depois de atribuir endereços ao R1 e ao R2, haveria apenas 4 endereços desperdiçados.  

Se usarmos um comprimento de prefixo /30, a máscara é escrita como 255.255.255.252 em notação decimal pontuada. Agora há apenas 2 bits de host, o que significa 2 endereços utilizáveis. Então, isso é perfeito!  

Há um total de 4 endereços: o endereço de rede, o endereço de broadcast, o endereço do R1 e o endereço do R2. Isso significa zero endereços desperdiçados! 

Antes de passar para /31 e /32, deixe-me fazer um pequeno esclarecimento. Então, em vez de 203.0.113.0/24, usaremos 203.0.113.0/30, que é uma sub-rede daquela rede Classe C maior. O endereço 203.0.113.0/30 abrange a faixa de endereços de 203.0.113.0 a 203.0.113.3. Deixe-me mostrar isso em binário. 

Aqui está o 203.0.113.0 em binário, com a parte do host composta apenas por zeros. Aqui estão o 203.0.113.1, o 203.0.113.2 e o 203.0.113.3. Esses são os 4 endereços da rede, sendo que dois deles são os endereços utilizáveis, atribuídos ao R1 e ao R2. 

Então, utilizamos 4 endereços com esta sub-rede; e quanto aos outros endereços na faixa 203.0.113.0/24? Os endereços restantes no bloco de endereços — de 203.0.113.4 a 203.0.113.255 — agora estão disponíveis para serem usados em outras sub-redes! Essa é a mágica da divisão em sub-redes (subnetting). 

Em vez de usar 203.0.113.0/24 e desperdiçar 252 endereços, podemos usar /30 e não desperdiçar nenhum endereço. Ou será que existe outra maneira de tornar isso ainda mais eficiente? Vamos analisar. 

### CIDR: /31  

Se usarmos um comprimento de prefixo /31, a máscara é escrita como 255.255.255.254 em notação decimal pontuada. Agora existe apenas 1 bit de host, o que significa... 0 endereços utilizáveis. 2 elevado à potência de 1 é 2, menos 2 para os endereços de rede e de broadcast, resulta em 0 endereços que podemos atribuir a dispositivos.  

Então, antigamente não era possível usar prefixos de rede /31 por causa disso. NO ENTANTO, para uma conexão ponto a ponto como esta, na verdade é possível usar uma máscara /31. Vamos verificar isso.  

Aqui está a rede 203.0.113.0/31; o R1 é 203.0.113.0 e o R2 é 203.0.113.1. A rede 203.0.113.0/31 consiste nos endereços de 203.0.113.0 a 203.0.113.1... o que na verdade são apenas dois endereços. Aqui estão eles em binário: 203.0.113.0 e 203.0.113.1. 

Normalmente, isso seria um problema, pois não restariam endereços utilizáveis após subtrair os endereços de rede e de broadcast; mas para redes ponto a ponto como esta — uma conexão dedicada entre dois roteadores —, na verdade não há necessidade de um endereço de rede ou de um endereço de broadcast. 

Portanto, podemos quebrar as regras neste caso e atribuir os dois únicos endereços desta rede aos nossos roteadores. Observe que, se você tentar essa configuração em um roteador Cisco, receberá um aviso como este, lembrando-o de garantir que se trata de um link ponto a ponto; no entanto, é uma configuração totalmente válida.  

Então, mais uma vez: os endereços restantes no bloco 203.0.113.0/24 — ou seja, de 203.0.113.2 a 255 — agora estão disponíveis para uso em outras redes! Mas, desta vez, economizamos ainda mais endereços, utilizando apenas 2 em vez de 4 para essa conexão ponto a ponto.  

As pessoas ainda usam /30 para conexões ponto a ponto às vezes, mas as máscaras /31 são totalmente válidas e mais eficientes que as /30; por isso, recomendo esse método! 

### CIDR: /32  

Mas ainda não analisamos a máscara /32. Uma máscara /32 é escrita como 255.255.255.255 em notação decimal pontuada, fazendo com que todo o endereço corresponda à parte de rede; não há bits de host. 

Se você fizer o cálculo usando nossa fórmula, obterá -1 endereços utilizáveis... claramente, a fórmula não funciona nesse caso. Você não conseguirá usar uma máscara /32 nessa situação e provavelmente nunca usará uma máscara /32 para configurar uma interface real. 

No entanto, existem algumas aplicações para a máscara /32; por exemplo, quando você deseja criar uma rota estática não para uma rede, mas apenas para um host específico, pode usar uma máscara /32 para especificar exatamente esse host. 

De qualquer forma, falarei sobre isso mais adiante no curso; saiba apenas que as máscaras /32 são usadas em pontos, mas você não precisa se preocupar com eles por enquanto.  

## Notação CIDR  

Aqui está uma tabela simples mostrando as máscaras de sub-rede em formato decimal pontuado e seus equivalentes na notação CIDR. Isso mesmo: a forma de escrever um prefixo com uma barra seguida pelo comprimento do prefixo, como /25, /26, etc., é chamada de notação CIDR, pois foi introduzida com o sistema CIDR. 

Anteriormente, utilizava-se apenas o método decimal pontuado. Observe que até agora mostrei apenas como criar sub-redes em uma rede Classe C, mas também veremos redes Classe B e Classe A, com comprimentos de prefixo como /17, /11, /9, etc.  

## Cenário de Sub-rede

Dediquei bastante tempo a esse único exemplo, mas espero que você consiga perceber a utilidade da criação de sub-redes — dividir uma rede maior em redes menores, chamadas de sub-redes. Em vez de usar toda a rede 203.0.113.0/24 para a conexão ponto a ponto, podemos usar uma sub-rede /30 e utilizar apenas 4 endereços, ou, melhor ainda, usar uma sub-rede /31 e utilizar apenas 2 endereços.

Vou apresentar mais um exemplo de criação de sub-redes antes de encerrar este vídeo. No próximo vídeo, passarei alguns exercícios e os explicarei passo a passo para que você possa praticar a criação de sub-redes na prática.  

Então, aqui está um cenário. Há 4 redes conectadas ao R1, com muitos hosts conectados a cada switch. Há 45 hosts por rede; o R1 precisa de um endereço IP em cada rede para que seu endereço esteja incluído na faixa. 

Você recebeu a rede 192.168.1.0/24 e deve dividi-la em quatro sub-redes capazes de acomodar o número de hosts necessários. Primeiramente, será que a rede 192.168.1.0/24 possui endereços suficientes para isso? 

Precisamos de 45 hosts por rede, incluindo o R1; mas lembre-se também de que cada rede possui um endereço de rede e um de broadcast — ou seja, mais 2 endereços —, então precisamos de 47 endereços por sub-rede. 47 vezes 4 é igual a 188, portanto, não há problema quanto ao número de hosts.  

A 192.168.1.0/24 é uma rede classe C, totalizando 256 endereços; logo, poderemos criar 4 sub-redes para acomodar todos os hosts sem problemas. Certo, vamos ver como calcular as sub-redes necessárias.

Precisamos de quatro sub-redes de tamanhos iguais, com capacidade para pelo menos 45 hosts. Aqui, escrevi o endereço 192.168.1.0 com uma máscara /30 (255.255.255.252). Pulei as máscaras /32 e /31, pois, como não se trata de links ponto a ponto, não podemos usar /31 e, definitivamente, não podemos usar /32. 

Como há 2 bits de host, a fórmula para determinar o número de endereços utilizáveis é 2 elevado a 2, menos 2. 

2 elevado a 2 é 2 vezes 2, ou seja, 4. Isso significa que existem 2 endereços utilizáveis em uma rede /30. Claramente, não há espaço suficiente para acomodar os 45 hosts que temos. Que tal usarmos uma máscara /29 para criar essas sub-redes? Conseguimos acomodar os 45 hosts de que precisamos?

Há 3 bits de host, então a fórmula é 2 elevado à terceira potência menos 2. 2 elevado à terceira potência é 2 vezes 2 vezes 2, o que dá 8. Portanto, temos 6 endereços utilizáveis — insuficiente para 45 hosts. Que tal usarmos /28? 

Há 4 bits de host, então a fórmula é 2 elevado à quarta potência menos 2. 2 elevado à quarta potência é 2 vezes 2 vezes 2 vezes 2, o que dá 16. Isso significa que há 14 endereços utilizáveis; mais uma vez, insuficiente para 45 hosts. Que tal /27? 

Há 5 bits de host, então a fórmula é 2 elevado à quinta potência menos 2. E 2 elevado à quinta potência é 2 vezes 2 vezes 2 vezes 2 vezes 2, o que resulta em 32. Isso significa 30 endereços utilizáveis — novamente, insuficiente para 45 hosts. Que tal uma máscara de sub-rede /26? 

Agora temos 6 bits de host, então a fórmula é 2 elevado à sexta potência menos 2. 2 elevado à sexta potência é 2 vezes 2 vezes 2 vezes 2 vezes 2 vezes 2, o que resulta em 64. Isso significa que há 62 endereços utilizáveis. Então, parece que encontramos o número certo! 

/27 não oferece espaço de endereçamento suficiente. Uma máscara /26 oferece mais do que precisamos, mas temos que optar pela /26. Infelizmente, nem sempre conseguimos fazer com que as sub-redes tenham exatamente o número de endereços que você deseja. Pode haver algum espaço de endereçamento não utilizado.

Na verdade, isso não é problema, já que é bom ter uma margem para crescimento, de qualquer forma.

Se você encontrar o endereço de broadcast da sub-rede 1, o próximo endereço depois dele será o endereço de rede da sub-rede 2.  

Portanto, o endereço de rede da sub-rede 1192.168.1.0/26. Aqui está o 192.168.1.0 escrito em binário. Em azul temos a parte da rede, em vermelho a parte do host e em roxo a parte que "EMPRESTAMOS" da parte do host para adicionar à parte da rede.  

Isso nos permite dividir a rede maior /24 em múltiplas sub-redes menores. Para encontrar o endereço de broadcast desta sub-rede — que é o endereço mais alto na faixa de endereços da sub-rede —, defina todos os bits da parte do host como 1.  

Em seguida, vamos converter isso para o formato decimal pontuado. O resultado é 192.168.1.63. Esse é o endereço de broadcast. Então, o intervalo de endereços para a sub-rede 1 vai de 192.168.1.0 a 192.168.1.63.  

O endereço de rede da sub-rede 2 será 1 unidade superior ao endereço de broadcast. Isso significa que a sub-rede 2 será 192.168.1.64/26. Esse é o endereço de rede; aqui está ele em binário.  

Observe que alteramos para 1 um dos bits que pegamos emprestados da porção de host. Assim, o endereço de rede agora é 192.168.1.64, com todos os bits de host definidos como 0. Agora, vamos encontrar o endereço de broadcast. Alteramos todos os bits de host para 1 e, agora, vamos convertê-lo para o formato decimal pontuado. Portanto, o endereço de broadcast é 192.168.1.127.  

Esse é o intervalo para a sub-rede 2. Somamos 1 ao endereço de broadcast e obtemos o endereço de rede para a sub-rede 3. Isso significa que a sub-rede 3 é 192.168.1.128/26. Aqui está o endereço de rede em binário; note novamente que alteramos um dos bits roxos emprestados para 1, mas os bits de host são todos 0.  

Alteramos esses bits para 1 e aqui está o endereço de broadcast. Assim, o intervalo de endereços para esta sub-rede vai de 192.168.1.128 a 192.168.1.191. Agora podemos encontrar a última sub-rede, a sub-rede 4.  

A sub-rede 4 é 192.168.1.192/26. Aqui está o endereço de rede em binário; desta vez, os bits emprestados são todos 1, então esta é a nossa última sub-rede; não temos mais espaço para outras. Mude os bits de host para 1, e aqui está o endereço de broadcast.  

Portanto, o intervalo de endereços para a sub-rede 4 vai de 192.168.1.192 a 192.168.1.255.

Você pode notar algo sobre esses números. 0 mais 64 é igual a 64. 64 mais 64 é igual a 128, e 128 mais 64 é igual a 192.  

Eu disse no vídeo anterior que mostraria apenas o básico sobre sub-redes, sem truques especiais, mas deixe-me mostrar um que pode ajudar você a entender as coisas mais rapidamente.  

### Truque de Sub-rede  

Então, descobrimos que uma máscara de sub-rede /26 é adequada. Isso ocorre porque existem 6 bits de host, o que permite 62 hosts. Vamos traçar esta linha aqui.  

No lado esquerdo fica a parte da rede, e no lado direito, a parte do host. Como estamos analisando apenas o último octeto, vou ampliá-lo. Ok, então coloquei aqui embaixo a representação binária apenas do último octeto.  

Novamente, a parte vermelha é a parte do host, e a parte roxa são os bits que emprestamos para expandir a parte da rede. Você deve se lembrar do valor de cada bit binário, mas vou colocá-los aqui mesmo assim. Da direita para a esquerda: 1, 2, 4, 8, 16, 32, 64 e 128.  

Observe que o ÚLTIMO bit da parte de rede é 64. Isso significa que, para encontrar a próxima sub-rede, basta somar 64. Vamos ver.  

Somamos 64 e obtemos 192.168.1.64, que é o endereço de rede da sub-rede 2. Somamos 64 novamente e obtemos 192.168.1.128, que é o endereço de rede da sub-rede 3. Finalmente, somamos 64 mais uma vez e obtemos 192.168.1.192, que é o endereço de rede da sub-rede 4.  

Então, como você pode ver, ao somar 64 a cada passo, conseguimos encontrar os endereços de rede de cada sub-rede.  

## Subnetting de Redes Classe B

Agora, vamos finalmente analisar o subnetting de redes maiores, especificamente as de Classe B. Observando este gráfico novamente, você pode ver que há muito mais bits de host e, portanto, muito mais sub-redes possíveis que podem ser criadas com uma rede Classe B do que com uma rede Classe C.  

No entanto, o processo de subnetting é EXATAMENTE O MESMO. Então, vou apresentar alguns exemplos com redes Classe B e, depois, deixaremos as redes Classe A para o último vídeo desta série sobre subnetting. 

Foi fornecida a você a rede 172.16.0.0/16. Solicita-se que você crie 80 sub-redes para as várias LANs da sua empresa. Qual comprimento de prefixo você deve usar? Bem, esta é uma pergunta realmente simples, e podemos seguir exatamente o mesmo processo da última vez.  

Novamente, podemos simplesmente usar a fórmula 2 elevado a X, onde X é o número de bits emprestados. Se não emprestarmos nenhum bit, não poderemos criar sub-redes; teremos apenas uma grande rede /16. Se pegarmos emprestado um bit, podemos criar 2 sub-redes, pois 2 elevado à potência de 1 é 2.  

Isso nos dá um comprimento de prefixo /17 e, se escrevermos essa máscara de sub-rede em formato decimal pontuado, ela fica 255.255.128.0. Lembre-se: ao inserir comandos na CLI da Cisco, não é possível usar a notação CIDR como /17; é preciso inserir o formato decimal pontuado, como 255.255.128.0.  

De qualquer forma, 2 sub-redes não são suficientes para nossas necessidades, então vamos pegar mais um bit emprestado. Pegar 2 bits emprestados permite criar 4 sub-redes. Isso resulta em um comprimento de prefixo /18, e a máscara de sub-rede é escrita como 255.255.192.0 em formato decimal pontuado.  

Vamos pegar mais um bit emprestado. Pegar 3 bits emprestados nos dá 8 sub-redes e um comprimento de prefixo /19. A máscara de sub-rede é 255.255.224.0 em formato decimal pontuado.  

Ainda não temos sub-redes suficientes, então vamos pegar mais um bit emprestado. Pegar 4 bits emprestados nos permite criar 16 sub-redes e utiliza um comprimento de prefixo /20. A propósito, /20 equivale a 255.255.240.0 em formato decimal pontuado.  

Pegar 5 bits emprestados nos dá 32 sub-redes, e o comprimento do prefixo é /21, o que equivale a 255.255.248.0 em formato decimal pontuado. 

Pegar emprestados 6 bits nos dá 64 sub-redes. Estamos chegando perto. O comprimento do prefixo é /22, o que corresponde a 255.255.252.0 em notação decimal pontuada.  

Vamos pegar mais um bit emprestado; isso deve ser suficiente. Pegar emprestados 7 bits nos dá 128 sub-redes. O comprimento do prefixo é /23, o que corresponde a 255.255.254.0 em notação decimal pontuada. Então, esta é a resposta correta: devemos usar um comprimento de prefixo /23 para podermos criar as 80 sub-redes de que precisamos.  

128 sub-redes é mais do que precisamos, mas o /22 permite apenas 64, o que não é suficiente. Não vou mostrar todas as 80 sub-redes, é claro, mas vamos examinar algumas das sub-redes que podem ser criadas; a primeira é a 172.16.0.0/23, naturalmente.  


A próxima é a 172.16.2.0/23; note que mudei o último bit da parte de rede para 1. A seguir, temos a 172.16.4.0/23, depois a 172.16.6.0, 172.16.8.0, etc. Vamos fazer outra questão semelhante.  

Qual comprimento de prefixo é apropriado? Foi fornecida a você a rede 172.22.0.0/16. Você precisa dividir a rede em 500 sub-redes separadas. Qual comprimento de prefixo você deve usar? 

Então, a resposta correta é /25. Precisamos dividir essa rede de classe B em 500 sub-redes, o que significa que temos que pegar emprestados 9 bits, pois 2 elevado a 9 é igual a 512. Observe que você pode pegar bits emprestados até mesmo do último octeto; assim, pode usar /25, /26, /27, etc., mesmo com uma rede de classe B.  

Aqui está outra questão para praticar. Foi fornecida a rede 172.18.0.0/16. Sua empresa precisa de 250 sub-redes com o mesmo número de hosts por sub-rede. Qual comprimento de prefixo você deve usar? Desta vez, você precisa considerar tanto o número de sub-redes quanto o número de hosts.  

Então, a resposta é /24. Precisamos de 250 sub-redes, e pegar 8 bits emprestados nos permite criar 256 sub-redes. Também precisamos de 250 hosts por sub-rede, e ter 8 bits de host permite 254 hosts por sub-rede.  

Aqui está uma tabela, semelhante à que mostrei para endereços Classe C, exibindo o número de hosts por sub-rede (Classe B) de sub-redes disponíveis e o número de endereços de host disponíveis para cada comprimento de prefixo ao dividir uma rede Classe B em sub-redes.  

Não se preocupe, não é necessário memorizar esses números. Isso seria simplesmente um desperdício de esforço. Apenas conheça os padrões.

Para cada bit emprestado, o número de sub-redes dobra: 2, 4, 8, 16, 32, etc. Para cada bit de host, o número de endereços em cada sub-rede dobra; no entanto, você precisa subtrair 2 para identificar o número de endereços de host utilizáveis. Como eu disse, não decore isso; apenas conheça esses padrões para que você possa fazer os cálculos quando precisar.  

## Subnetting de Redes Classe A  

Observe o tamanho do campo de bits restante; essa é a parte do host. Há 24 bits de host dos quais podemos pegar emprestado, o que significa muito espaço para criar sub-redes.  

No entanto, deixe-me lembrá-lo de que o processo de subnetting para redes Classe A, Classe B e Classe C é exatamente o mesmo! Então, vamos fazer apenas 2 exercícios práticos de subnetting de redes Classe A e, depois, passar para VLSM.  

Exercício Prático 1 Foi fornecida a você a rede 10.0.0.0/8. Você deve criar 2.000 sub-redes que serão distribuídas para várias empresas. Qual comprimento de prefixo você deve usar? Quantos endereços de host, ou endereços utilizáveis, haverá em cada sub-rede? Vamos resolver essa questão assim como as outras.  

Aqui está o endereço 10.0.0.0/8 em binário e em decimal pontuado. É /8, portanto, apenas o primeiro octeto é a parte da rede, e temos 3 octetos inteiros dos quais podemos pegar emprestado para criar sub-redes.  

Observe que escrevi a máscara de sub-rede /8 aqui embaixo: 255.0.0.0. Atualmente, estamos pegando 0 bits emprestados, então não podemos criar nenhuma sub-rede. Em vez de passar por todo o processo de pegar emprestado 1 bit, 2 bits, 3 bits, etc., vamos ver se você consegue fazer isso de cabeça.  

Então, 2 elevado a que potência? Iguala-se a pelo menos 2.000? Lembre-se: cada bit que você pega emprestado dobra o número de sub-redes que você pode criar.

2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048. São 11 bits emprestados, então a resposta é 2 elevado à 11ª potência. Portanto, emprestar 11 bits nos permite criar as 2.000 sub-redes necessárias. Isso significa que usaremos um comprimento de prefixo /19. Agora, quantos hosts haverá em cada sub-rede?  

Bem, restam 13 bits de host, o que significa 8.190 hosts por sub-rede. Então, essas são as respostas. Usaremos um comprimento de prefixo /19 e haverá 8.190 endereços de host — ou seja, endereços utilizáveis — em cada sub-rede.  

Esse é o mesmo processo que usamos para redes de Classe B e Classe C; os números são apenas maiores.  


Vamos fazer mais uma questão de prática para uma rede de Classe A. O PC1 tem o endereço IP 10.217.182.223/11. Identifique o seguinte para a sub-rede do PC1:

1) Endereço de rede: ?
2) Endereço de broadcast: ?
3) Primeiro endereço utilizável: ?
4) Último endereço utilizável: ?
5) Número de endereços de host (ou utilizáveis):  ?

Aqui está o endereço escrito como um /8 padrão: 8 bits de rede e 24 bits de host. Mas não é /8, é /11, então há 3 bits emprestados. Para encontrar o endereço de rede, altere todos os bits de host para 0. Depois, converta-o de volta para o formato decimal pontuado.  

- Então, aí está o endereço de rede: 10.192.0.0. 

- Some 1 ao endereço de rede e você obtém o primeiro endereço utilizável, que é 10.192.0.1. 

- Altere todos os bits de host para 1 e você obtém o endereço de broadcast: 10.223.255.255. 

- Subtraia um do endereço de broadcast e você obtém o último endereço utilizável.  Finalmente, para determinar o número de endereços de host, conte o número de bits de host. São 21, o que significa 2.097.150 hosts por sub-rede. 

Então, aqui estão as respostas para cada parte da pergunta. 

Como eu disse antes, o processo de criação de sub-redes para redes Classe A é o mesmo que para redes Classe B e Classe C; você só precisa se acostumar com os números maiores. Além disso, espero que você já esteja se acostumando a converter entre binário e decimal pontuado, pois, como você provavelmente percebeu, isso é absolutamente essencial para a criação de sub-redes.  

## VLSM  

Então, vamos passar para um tópico muito importante: VLSM, que significa máscaras de sub-rede de tamanho variável.  
 
Até agora, praticamos a criação de sub-redes usando FLSM (Máscaras de Sub-rede de Tamanho Fixo). Isso significa que todas as sub-redes usam o mesmo comprimento de prefixo; por exemplo, dividir uma rede Classe C em 4 sub-redes usando /26.  

No entanto, VLSM (Máscaras de Sub-rede de Comprimento Variável) é o processo de criar sub-redes de diferentes tamanhos, para tornar o uso de endereços de rede mais eficiente.  

O VLSM é, de fato, mais complicado que o FLSM, mas torna-se fácil se você seguir os passos corretamente. Então, é isso que quero ensinar agora: os passos para dividir uma rede em sub-redes usando VLSM. 

Aqui está um exemplo de rede de uma pequena empresa. Há duas LANs em Tóquio e duas LANs em Toronto. 

- A LAN A de Tóquio tem 110 hosts;
- A LAN B de Tóquio tem 8 hosts;
- A LAN A de Toronto tem 29 hosts; e
- A LAN B de Toronto tem 45 hosts.  

Além disso, há uma conexão ponto a ponto entre os dois roteadores, para a qual devemos atribuir endereços IP.  

Recebemos a rede 192.168.1.0/24 e devemos dividi-la em 5 sub-redes para fornecer endereços IP para todos os hosts da rede corporativa. Se tentássemos fazer isso com máscaras de sub-rede de comprimento fixo, precisaríamos pegar emprestados 3 bits para criar sub-redes suficientes.  

Isso deixaria 5 bits para hosts. 5 bits para hosts permitem apenas 30 endereços de host. Então, isso não é suficiente de endereços para a LAN A de Tóquio ou para a LAN B de Toronto. No entanto, se usarmos VLSM, podemos atribuir tamanhos de sub-rede diferentes a cada LAN, o que nos permitirá garantir que cada LAN tenha endereços suficientes disponíveis.  

Então, quais são os passos para criar sub-redes usando VLSM?  

### Passos do VLSM  

Primeiro, atribua a maior sub-rede no início do espaço de endereçamento. Em seguida, atribua a segunda maior logo depois. E então repita o processo até que todas as sub-redes tenham sido atribuídas, da maior para a menor.  

Se você olhar para a nossa rede aqui, isso significa que atribuiremos as sub-redes nesta ordem. Primeiro, a LAN A de Tóquio, que requer 110 hosts. Depois, a LAN B de Toronto. Em seguida, a LAN A de Toronto, a LAN B de Tóquio e, finalmente, a conexão ponto a ponto entre os dois roteadores.  

Então, vamos fazer a LAN A de Tóquio. Quero que você pause o vídeo e descubra estes cinco valores por conta própria: endereço de rede, endereço de broadcast, primeiro endereço utilizável, último endereço utilizável e número total de endereços de host utilizáveis.  

Já praticamos muito isso, então sei que você consegue fazer sozinho. Pause o vídeo agora para encontrar as respostas... Ok, vamos conferir as respostas.  

Então, decidi usar um comprimento de prefixo /25. Por que isso? Bem, um comprimento de prefixo /25 deixa 7 bits para host, o que significa um total de 128 endereços, ou seja, 126 endereços de host utilizáveis. 

Precisamos de 110, então /25 é o comprimento de prefixo correto.  Isso significa que o endereço de rede é 192.168.1.0/25. Converta todos os bits de host para 1, e teremos o endereço de broadcast: 192.168.1.127. Então, agora temos as respostas para a LAN A de Tóquio. 

O primeiro endereço utilizável é o endereço de rede mais um, e o último endereço utilizável é o endereço de broadcast menos um. E, como acabei de mencionar, 7 bits de host permitem 126 endereços de host utilizáveis, o que é 2 elevado à sétima potência, menos 2.  
 
Assim, temos agora nossa primeira sub-rede, 192.168.1.0/25, para a LAN A de Tóquio. Essa sub-rede /25 consome metade do espaço de endereçamento da rede 192.168.1.0/24, mas isso não é problema.  

Usando VLSM, podemos atribuir sub-redes menores a essas outras LANs, e você verá que ainda sobra espaço de endereçamento suficiente. Então, a seguir, devemos configurar a LAN B de Toronto. 

O endereço 192.168.1.127 é o endereço de broadcast da LAN A de Tóquio. Se somarmos um a ele, obteremos o endereço de rede da próxima sub-rede, que será usada para a LAN B de Toronto. Portanto, 192.168.1.128 é o endereço de rede da LAN B de Toronto. 

Mas falta um ponto importante. Que comprimento de prefixo devemos usar para a LAN B de Toronto? Então, com essas informações, quero que você faça o mesmo para a Toronto LAN B. Pause o vídeo e encontre o comprimento do prefixo que devemos usar; depois, o endereço de broadcast, o primeiro e o último endereços utilizáveis e o número total de endereços de host utilizáveis para esta sub-rede. 

Pause o vídeo agora... ok, vamos conferir a resposta. Então, para acomodar os 45 hosts, usaremos um comprimento de prefixo /26. Isso deixa 6 bits de host, o que permite 62 endereços de host. Isso é mais do que precisamos, mas se criarmos uma sub-rede menor com um prefixo /27, só poderemos ter 30 hosts, o que não é suficiente.  
  
Portanto, o endereço de rede completo é 192.168.1.128/26. Mude todos os bits de host para 1 e você obterá o endereço de broadcast: 192.168.1.191. Aqui estão as respostas para a Toronto LAN B. Para a Tokyo LAN A e a Toronto LAN B, utilizamos o espaço de endereçamento de 192.168.1.0 a 191. Essas duas sub-redes ocupam três quartos do espaço de endereçamento, mas isso não é problema. Ainda há espaço para mais sub-redes, menores.

192.168.1.191 é o endereço de broadcast da LAN B de Toronto; portanto, 192.168.1.192 é o endereço de rede da LAN A de Toronto. No entanto, mais uma vez, precisamos determinar qual comprimento de prefixo usar para a LAN A de Toronto.  

Vamos realizar o mesmo processo utilizado com as outras LANs. Por favor, pause o vídeo agora para encontrar as informações restantes... ok, espero que você tenha encontrado as respostas; vamos conferir.  

A LAN A de Toronto requer 29 hosts, então devemos usar um comprimento de prefixo /27, o que deixa 5 bits para hosts e, consequentemente, 30 endereços de host. Assim, 192.168.1.192/27 é o endereço de rede, e 192.168.1.223 é o endereço de broadcast. Com essas informações, podemos determinar o primeiro e o último endereços utilizáveis.  

Aqui estão as respostas para a LAN A de Toronto. Vamos analisar a LAN B de Tóquio em seguida. Então, utilizamos o intervalo até 192.168.1.223, que é o endereço de broadcast da LAN A de Toronto. Não resta muito espaço de endereçamento, mas, com VLSM, conseguimos acomodar as duas últimas sub-redes nesse espaço.  

O endereço seguinte ao endereço de broadcast da LAN A de Toronto é o endereço de rede da LAN B de Tóquio. Mais uma vez, precisamos encontrar o comprimento de prefixo a ser usado para essa sub-rede.  
  
Então, por favor, pause o vídeo aqui para encontrar esses diferentes endereços para a LAN B de Tóquio. Certo, vamos conferir as respostas.  

Então, como a LAN B de Tóquio requer 8 hosts, devemos usar um prefixo /28.  Um erro possível aqui é usar um prefixo /29. Embora o /29 permita 8 endereços, lembre-se de que devemos subtrair dois para os endereços de rede e de broadcast; portanto, na verdade, o /29 permite apenas 6 endereços utilizáveis.  

Assim, devemos usar /26, que permite 14 endereços de host. Logo, o endereço de rede para a LAN B de Tóquio é 192.168.1.224/28. Alterando os bits de host para 1, o endereço de broadcast é 192.168.1.239. Aqui estão as respostas para a LAN B de Tóquio. 

Agora resta apenas uma sub-rede para atribuirmos: a conexão ponto a ponto entre esses dois roteadores. Já utilizamos o espaço de endereçamento até 192.168.1.239. Não sobra muito espaço, mas isso não é problema.  

Conexões ponto a ponto requerem apenas 2 endereços. 192.168.1.239 é o endereço de rede da LAN B de Tóquio; portanto, 192.168.1.240 é o endereço de rede da conexão ponto a ponto. Agora, qual prefixo devemos usar?  

Como mencionei no primeiro vídeo sobre sub-redes, é possível usar um prefixo /31 para uma sub-rede que requer apenas dois hosts. No entanto, para o exame CCNA, se lhe perguntarem qual comprimento de prefixo usar para uma sub-rede que requer dois hosts, recomendo NÃO usar um /31.  

Em vez disso, qual outro comprimento de prefixo permite 2 hosts? Pause o vídeo aqui e encontre as respostas... ok, vamos conferir. Então, um comprimento de prefixo /30 permite 2 hosts. 192.168.1.240 é o endereço de rede, e 192.168.1.243 é o endereço de broadcast. Aqui estão as respostas para as conexões ponto a ponto.  

Há apenas 2 endereços de host utilizáveis: 1 para o roteador de Tóquio e um para o de Toronto. roteador. Ok, então dividimos essa rede em sub-redes com sucesso usando VLSM, e ainda resta um pouco de espaço de endereçamento.  

Observe que cada sub-rede usa um comprimento de prefixo diferente. Se tentássemos usar o mesmo comprimento de prefixo para cada sub-rede, não haveria espaço de endereçamento suficiente, mas com VLSM conseguimos fazer isso e deixar algum espaço extra no final.  

Aqui está um lembrete das etapas do VLSM. Comece pela maior sub-rede e atribua-a ao início do espaço de endereçamento e, em seguida, passe para a segunda maior sub-rede, etc., e repita até ter atribuído todas as sub-redes necessárias.  

O VLSM é uma ótima maneira de usar o espaço de endereçamento de rede de forma mais eficiente.

