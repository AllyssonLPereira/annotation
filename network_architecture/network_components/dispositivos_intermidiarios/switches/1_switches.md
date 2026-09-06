

Um switch Ethernet da camada 2 usa endereços MAC da camada 2 para tomar decisões de encaminhamento. Ele desconhece completamente os dados (protocolos) que estão sendo transportados na parte de dados do quadro, como um pacote IPv4, uma mensagem ARP ou um pacote ND IPv6. 

[O switch toma decisões de encaminhamento com base apenas nos endereços MAC Ethernet da camada 2].

Um switch Ethernet examina sua tabela de endereços MAC para tomar uma decisão de encaminhamento para cada quadro, ao contrário dos hubs Ethernet herdados que repetem bits em todas as portas, exceto a porta de entrada.

> [!NOTE]
> A tabela de endereços MAC às vezes é chamada de tabela de memória endereçável de conteúdo (CAM). Embora o termo "tabela CAM" seja muito comum

---
### Aprendizado e Encaminhamento

O switch cria a tabela de endereços MAC [dinamicamente examinando o endereço MAC de origem] dos quadros recebidos em uma porta. 

O switch encaminha quadros procurando uma correspondência entre o endereço MAC de destino no quadro e uma entrada na tabela de endereços MAC.

- Como funciona o aprendizado?

	Todo quadro que entra em um switch é verificado quanto ao aprendizado de novas informações. Isso é feito examinando o endereço MAC de origem do quadro e o número da porta em que o quadro entrou no comutador. 

	Se o endereço MAC de origem não existe, é adicionado à tabela juntamente com o número da porta de entrada. 

	Se o endereço MAC de origem existir, o switch atualizará o cronômetro de atualização para essa entrada na tabela. *Por padrão, a maioria dos switches Ethernet mantém uma entrada na tabela por 5 minutos.

	Temos, ainda, a forma estática (na qual o endereço é configuraxo e não mais tirado) e o estático persistente (na qual o endereço é excluido com o reset do switch).

- Como funciona o encaminhamento?

	Se o endereço MAC de destino for um endereço unicast, o switch procurará uma correspondência entre o endereço MAC de destino do quadro e uma entrada em sua tabela de endereços MAC. 

	Se o endereço MAC de destino estiver na tabela, ele encaminhará o quadro pela porta especificada. 

	Se o endereço MAC de destino não estiver na tabela, o switch encaminhará o quadro por todas as portas, exceto a de entrada. Isso é chamado de [unicast desconhecido].

	Se o endereço MAC de destino for um broadcast ou multicast, o quadro também inundará todas as portas, exceto a porta de entrada.

- Segurança:

	- 802.1x
	- mac flooding
	- espelhamento de porta (monitorar a porta e verificar o tráfego)
	- colocar num lugar seguro, fisicamente falando
	- limitar o número de endereços MAC por porta
	- ACLs para filtrar endereços.