---
tags:
  - arquivo
---
### Decisão de Encaminhamento de Pacotes no Roteador

Quando um host envia um pacote para outro host, ele consulta sua tabela de roteamento para determinar para onde enviar o pacote. Se o host de destino estiver em uma rede remota, o pacote será encaminhado para o gateway padrão, que geralmente é o roteador local.

O que acontece quando um pacote chega na interface do roteador?

O roteador examina o endereço IP de destino do pacote e pesquisa sua tabela de roteamento para determinar para onde encaminhar o pacote. *A tabela de roteamento contém uma lista de todos os endereços de rede conhecidos (prefixos) e para onde encaminhar o pacote. 

[Essas entradas são conhecidas como entradas de rota ou rotas]. *O roteador encaminhará o pacote usando a melhor (mais longa) rota correspondente.

---
### Tabela de Roteamento do Roteador IP

*A tabela de roteamento do roteador contém entradas de rota de rede listando todos os possíveis destinos de rede conhecidos.

A tabela de roteamento armazena três tipos de entradas de rota:

- **[Redes conectadas diretamente]**

	Essas entradas de rota de rede são interfaces de roteador ativas. *Os roteadores adicionam uma rota diretamente conectada quando uma interface está [configurada com um endereço IP] e está [ativada]. 

	Cada interface do roteador está conectada a um segmento de rede diferente.

- **[Redes remotas]**

	Essas entradas de rotas de rede são conectadas a outros roteadores.

	Os roteadores aprendem sobre redes remotas sendo explicitamente configurados por um administrador ou trocando informações de rota usando um protocolo de roteamento dinâmico. 

- **[Rota padrão]**

	Como um host, a maioria dos roteadores também inclui uma entrada de rota padrão, um gateway de último recurso.

	A rota padrão é usada quando não há correspondência melhor (mais) na tabela de roteamento IP.

---
### Roteamento estático

Rotas estáticas são entradas de rota configuradas manualmente. *A rota estática inclui o endereço de rede remota e o endereço IP do roteador de salto seguinte.

O R1 é configurado manualmente com uma rota estática para alcançar a rede 10.1.1.0/24. Se esse caminho mudar, R1 exigirá uma nova rota estática.

Se houver uma alteração na topologia da rede, a rota estática não será atualizada automaticamente e deverá ser reconfigurada manualmente. Por exemplo, R1 tem uma rota estática para alcançar a rede 10.1.1.0/24 via R2. 

Se esse caminho não estiver mais disponível, R1 precisaria ser reconfigurado com uma nova rota estática para a rede 10.1.1.0/24 via R3. Portanto, o roteador R3 precisaria ter uma entrada de rota em sua tabela de roteamento para enviar pacotes destinados a 10.1.1.0/24 para R2.

![[roteamento_estatico.png]]

O roteamento estático tem as seguintes características:

- Uma rota estática deve ser configurada manualmente.

- O administrador precisa reconfigurar uma rota estática se houver uma alteração na topologia e se a rota estática não for mais viável.

- Uma rota estática é apropriada para uma rede pequena e quando há poucos ou nenhum vínculo redundante.

---
### Roteamento dinâmico

*Um [protocolo de roteamento dinâmico] permite que os roteadores aprendam automaticamente sobre redes remotas, incluindo uma rota padrão, de outros roteadores. 

Os roteadores que usam protocolos de roteamento dinâmico compartilham automaticamente informações de roteamento com outros roteadores e compensam qualquer alteração de topologia sem envolver o administrador da rede. 

Se houver uma alteração na topologia de rede, os roteadores compartilham essas informações usando o protocolo de roteamento dinâmico e atualizam automaticamente suas tabelas de roteamento.

Os protocolos de roteamento dinâmico incluem [OSPF] e [Enhanced Interior Gateway Routing Protocol (EIGRP)]. A figura mostra um exemplo de roteadores R1 e R2 compartilhando automaticamente informações de rede usando o protocolo de roteamento OSPF.

![[roteamento_dinamico.png]]


A configuração básica requer apenas que o administrador de rede habilite as redes conectadas diretamente dentro do protocolo de roteamento dinâmico. O protocolo de roteamento dinâmico fará automaticamente o seguinte:

- Descobrir redes remotas
- Manter as informações de roteamento atualizadas
- Escolha o melhor caminho para as redes de destino
- Tentar encontrar um novo melhor caminho se o caminho atual não estiver mais disponível

Quando um roteador é configurado manualmente com uma rota estática ou aprende sobre uma rede remota dinamicamente usando um protocolo de roteamento dinâmico, o endereço de rede remota e o endereço de próximo salto são inseridos na tabela de roteamento IP. 

***Se houver uma alteração na topologia de rede, os roteadores ajustarão automaticamente e tentarão encontrar um novo melhor caminho.


> [!NOTE] 
> É comum que alguns roteadores usem uma combinação de rotas estáticas e um protocolo de roteamento dinâmico.

---
### Introdução a uma tabela de roteamento IPv4

Observe na figura que R2 está conectado à internet. Portanto, o administrador configurou R1 com uma rota estática padrão enviando pacotes para R2 quando não há nenhuma entrada específica na tabela de roteamento que corresponda ao endereço IP de destino. 

R1 e R2 também estão usando roteamento OSPF para anunciar redes conectadas diretamente.

![[roteamento_ipv4.png]]

``` shell
R1# show ip route

Codes: 

L  - local, 
C  - connected, 
S  - static, 
R  - RIP, 
M  - mobile, 
B  - BGP,
D  - EIGRP, 
EX - EIGRP external, 
O  - OSPF, 
IA - OSPF inter area,
N1 - OSPF NSSA external type 1, 
N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, 
E2 - OSPF external type 2,
i  - IS-IS, 
su - IS-IS summary, 
L1 - IS-IS level-1, 
L2 - IS-IS level-2,
ia - IS-IS inter area, 
*  - candidate default, 
U  - per-user static route,
o  - ODR, 
P  - periodic downloaded static route, 
H  - NHRP, 
l  - LISP,
a  - application route,
+  - replicated route, 
%  - next hop override, 
p  - overrides from PfR

Gateway of last resort is 209.165.200.226 to network 0.0.0.0

S*    0.0.0.0/0 [1/0] via 209.165.200.226, GigabitEthernet0/0/1
	  10.0.0.0/24 is subnetted, 1 subnets

O     10.1.1.0 [110/2] via 209.165.200.226, 00:02:45, GigabitEthernet0/0/1
      192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks

C     192.168.10.1/24  is directly connected, GigabitEthernet0/0/0
L     192.168.10.1/32  is directly connected, GigabitEthernet0/0/0
	  209.165.200.0/24 is variably subnetted, 2 subnets, 2 masks

C     209.165.200.224/30 is directly connected, GigabitEthernet0/0/1
L     209.165.200.225/32 is directly connected, GigabitEthernet0/0/1

R1#
```


O comando de modo EXEC privilegiado `show ip route` é usado para exibir a tabela de roteamento IPv4 em um roteador Cisco IOS.

O exemplo mostra a tabela de roteamento IPv4 do roteador R1. No início de cada entrada de tabela de roteamento é um código que é usado para identificar o tipo de rota ou como a rota foi aprendida. As fontes comuns de rotas (códigos) incluem:

- **L** - Endereço IP da interface local diretamente conectado
- **C** - Rede diretamente conectada
- **S** - A rota estática foi configurada manualmente por um administrador
- **O** - OSPF
- **D** - EIGRP

A tabela de roteamento exibe todas as rotas de destino IPv4 conhecidas para R1.

Uma rota diretamente conectada é criada automaticamente quando uma interface do roteador é configurada com informações de endereço IP e é ativada. 

O roteador adiciona duas entradas de rota com os códigos **C** (ou seja, a rede conectada) e **L** (ou seja, o endereço IP da interface local da rede conectada). 

As entradas de rota também identificam a interface de saída a ser usada para alcançar a rede. As duas redes diretamente conectadas neste exemplo são 192.168.10.0/24 e 209.165.200.224/30.

Os roteadores R1 e R2 também estão usando o protocolo de roteamento dinâmico OSPF para trocar informações do roteador. 

Na tabela de roteamento de exemplo, R1 tem uma entrada de rota para a rede 10.1.1.0/24 que aprendeu dinamicamente do roteador R2 por meio do protocolo de roteamento OSPF.

Uma rota padrão tem um endereço de rede de todos os zeros. Por exemplo, o endereço de rede IPv4 é 0.0.0.0. Uma entrada de rota estática padrão na tabela de roteamento começa com um código de **S***, conforme destacado no exemplo.