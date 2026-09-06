---
tags:
  - arquivo
---
##### Unicast:

Unicast diz respeito à transmissão de pacotes [um para um], sendo que os endereços de host unicast IPv4 estão no intervalo de endereços de 1.1.1.1 a 223.255.255.255. Contudo, dentro desse intervalo há muitos endereços que já são reservados para fins especiais.


> [!NOTE] Title
> A máscara de subrede, por exemplo: 255.255.255.0, pode ser representada da seguinte maneira: /24. Isso se deve ao fato da máscara tida como exemplo possuir 24 bits.

---
##### Broadcast:

Broadcast diz respeito à transmissão de pacotes [um para todos], isto é, um host enviando para todos os outros na mesma rede e [todos processam o pacote] (os pacotes de transmissão usam recursos na rede que faz com que os hosts receptores processem o pacote).

Sua representação é: 255.255.255.255.

Um broadcast pode ser [direcionado] ou [limitado], o direcionado é quando um pacote é enviado para uma rede específica, já o limitado para todos (255.255.255.255).

> [!NOTE]
> Pacotes broadcast só existem com o IPv4, com o IPv6 não.

>[!NOTE]
>Por padrão, um router não encaminha o pacote por outras redes.


---
##### Multidcast:

Multicast diz respeito à transmissão de pacotes [um para muitos], isto é, um host enviando para todos na mesma rede, porém, apenas os selecionados processarão o pacote, o que diminui o tráfego.

Um pacote multicast é um pacote com um endereço IP de destino que é um endereço multicast. O IPv4 reservou os endereços 224.0.0.0 a 239.255.255.255 como intervalo de multicast.



