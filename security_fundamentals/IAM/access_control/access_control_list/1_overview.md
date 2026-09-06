---
aliases:
tags:
  - arquivo
---
## What is an ACL?

Os roteadores tomam decisões de roteamento com base nas informações no cabeçalho do pacote. O tráfego que entra na interface do roteador é roteado apenas com base nas informações da tabela de roteamento. 

O roteador compara o endereço IP de destino com as rotas na tabela de roteamento para encontrar a melhor correspondência e, em seguida, encaminha o pacote com base na melhor rota de correspondência. Esse mesmo processo pode ser usado para filtrar tráfego usando uma lista de controle de acesso.

Uma ACL é uma série de comandos do IOS usados para filtrar pacotes com base nas informações encontradas no cabeçalho do pacote. Por padrão, um roteador não tem nenhuma ACLs configurada. 

Entretanto, quando uma ACL for aplicada a uma interface, o roteador executará a tarefa adicional de avaliar todos os pacotes de rede que passam pela interface para determinar se o pacote pode ser enviado.

Uma ACL usa uma lista sequencial de instruções de permissão ou negação, conhecidas como entradas de controle de acesso — ACEs.

> [!NOTE]
> As ACEs também são comumente chamadas de "declarações da ACL".

Quando o tráfego da rede passa através de uma interface configurada com uma ACL, o roteador compara as informações no pacote com cada ACE, em ordem sequencial, para determinar se o pacote corresponde a uma das ACEs. Esse processo é chamado de filtragem de pacote.

Temos alguns benefícios com isso, são eles:

- *Limitam o tráfego e aumentam o desempenho da rede;*
- *Fornecer controle de fluxo de tráfego;*
- *Fornecer um nível básico de segurança para acesso à rede;*
- *Filtrar o tráfego com base no tipo de tráfego;*
- *Screen hosts para permitir ou negar acesso aos serviços de rede;*
- *Fornecer prioridade a determinadas classes de tráfego de rede.*

---
## Inbound and outbound ACL

Uma ACL de entrada filtra pacotes antes de serem roteados para a interface de saída. Uma ACL de entrada é eficiente porque salva a sobrecarga de pesquisas de roteamento se o pacote é descartado. Se o pacote for permitido pela ACL, ele será processado para roteamento. 

> *As ACLs de entrada são mais usadas para filtrar pacotes quando a rede conectada a uma interface de entrada é a única origem dos pacotes que precisa ser examinada.*

Uma ACL de saída filtra pacotes após seu roteamento, independentemente da interface de entrada. Pacotes de entrada são roteados para a interface de saída e são processados através da ACL de saída. 

> *As ACLs de saída são mais usadas quando o mesmo filtro é aplicado aos pacotes que vêm de várias interfaces de entrada antes de saírem da mesma interface de saída.*


> [!NOTE] 
> A última instrução ACE de uma ACL é sempre uma negação implícita que bloqueia todo o tráfego. Por padrão, essa instrução é automaticamente implícita no final de uma ACL, mesmo que esteja oculta e não exibida na configuração.

---
## Joker mask


Uma máscara curinga é semelhante a uma máscara de subrede, na qual está também usa o processo de *`ANDing`* para identificar quais bits em um endereço IPV4 devem corresponder.

No entanto, eles diferem na forma como trabalham. Na máscara de subrede, o binário 1 é verdadeiro e o binário 0 é falso, em outras palavras, o 1 é uma correspondência e o 0 é uma não correspondêncial. Agora, na máscara curinga, é o inverso.

Elas usam a seguinte regra:

- Bit 0 — corresponde, ou seja, é verdadeiro;
- Bit 1 — não corresponde, ou sej,a é falso.

#### Types of Joker Mask

- *Joker to match a host*

	Neste exemplo, a máscara curinga é usada para corresponder a um endereço IPv4 de host específico. 

	Suponha que a ACL 10 precisa de uma ACE que permita apenas o host com endereço IPv4 *`192.168.1.1`*. Para corresponder a um endereço IPv4 de host específico, é necessária uma máscara curinga que consiste em todos os zeros — *`0.0.0.0`*.

	A tabela lista em binário, o endereço IPv4 do host, a máscara curinga e o endereço IPv4 permitido.

	A máscara curinga *`0.0.0.0`* estipula que cada bit deve corresponder exatamente. Portanto, quando a ACE é processada, a máscara curinga permitirá apenas o endereço *`192.168.1.1`*. A ACE resultante na ACL 10 seria access-list 10 permit *`192.168.1.1`* *`0.0.0.0`*.


	![[wildcard_to_match_a_host.png]]


- *Joker mask to match an IPv4 subnet*

	Neste exemplo, a ACL 10 precisa de uma ACE que permita todos os hosts na rede *`192.168.1.0/24`*. A máscara curinga 0.0.0.255 estipula que os três primeiros octetos devem corresponder exatamente, mas o quarto octeto não.

	A tabela lista em binário, o endereço IPv4 do host, a máscara curinga e os endereços IPv4 permitidos.

	Quando processado, a máscara curinga *`0.0.0.255`* permite todos os hosts na rede `192.168.1.0/24`. A ACE resultante na ACL 10 seria a lista de acesso 10 permitir *`192.168.1.1`* *`0.0.0.255`*.

	![[wildcard_mask_to_match_an_IPv4_subnet.png]]


- *Joker mask to match a range of IPv4 addresses*

	Neste exemplo, a ACL 10 precisa de uma ACE que permita todos os hosts nas redes *`192.168.16.0/24`*, *`192.168.17.0/24`*, ..., *`192.168.31.0/24`*. A máscara curinga *`0.0.15.255`* filtraria corretamente esse intervalo de endereços.

	A tabela lista em binário o endereço IPv4 do host, a máscara curinga e os endereços IPv4 permitidos.

	Os bits de máscara curinga realçados identificam quais bits do endereço IPv4 devem corresponder. Quando processada, a máscara curinga *`0.0.15.255`* permite que todos os hosts nas redes *`192.168.16.0/24`* a *`192.168.31.0/24`*. A ACE resultante na ACL 10 seria access-list 10 permit *`192.168.16.0`* *`0.0.15.255`*.

	![[wildcard_mask_to_match_a_range_of_IPv4_addresses.png]]



> [!NOTE] Cálculo da máscara curinga
> Calcular as máscaras curinga pode ser um desafio. Um método de atalho é subtrair a máscara de sub-rede de *`255.255.255.255`*. Consulte os exemplos para saber como calcular a máscara curinga usando a máscara de sub-rede.

---
## Joker Mask Keywords

Trabalhar com representações decimais de bits binários de máscara curinga pode ser entediante. Para simplificar esta tarefa, o Cisco IOS fornece duas palavras-chave para identificar os usos mais comuns do mascaramento de curinga. As palavras-chave reduzem os pressionamentos de teclas da ACL, mas, mais importante, as palavras-chave facilitam a leitura da ACE.

As duas palavras-chave são:

- *`host`* — Esta palavra-chave substitui a máscara *`0.0.0.0`*. Essa máscara indica que todos os bits do endereço IPv4 precisam corresponder para filtrar apenas um endereço de host;

- *`any`* — Esta palavra-chave substitui a máscara *`255.255.255.255`*. Essa máscara instrui o sistema a ignorar todo o endereço IPv4 ou a aceitar qualquer endereço.

Por exemplo, na saída do comando, duas ACLs são configuradas. A ACL 10 ACE permite apenas o host *`192.168.10.10`* e a ACL 11 ACE permite todos os hosts.

``` shell
R1(config)# access-list 10 permit 192.168.10.10  0.0.0.0
R1(config)# access-list 11 permit  0.0.0.0 255.255.255.255
R1(config)#
```

Alternativamente, as palavras-chaves *`host`* e *`any`* poderiam ter sido usadas para substituir a saída realçada.

Os comandos a seguir realizam a mesma tarefa que os comandos anteriores.

``` shell
R1(config)# access-list 10 permit  host  192.168.10.10
R1(config)# access-list 11 permit  any
R1(config)#
```
