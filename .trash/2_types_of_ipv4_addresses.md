---
tags:
  - arquivo
---
##### Public and private IPv4 addresses:

Endereços IPv4 públicos são todos aqueles que podem ser roteados globalmente, que podem ser usados na internet. Já os privados (que não faz parte da intenet) são endereços atribuídos a hosts internos (eles não são exclusivos, podendo ser usados internamente em qualquer rede).


Private IPv4 addresses:

| Endereço de rede e prefixo | RFC 1918 intervalo de endereços privados |
| -------------------------- | ---------------------------------------- |
| 10.0.0.0/8                 | 10.0.0.0 - 10.255.255.255                |
| 172.16.0.0/12              | 172.16.0.0 - 172.31.255.255              |
| 192.168.0.0/16             | 192.168.0.0 - 192.168.255.255            |
 

---

##### Special-Use IPv4 Addresses:

- **[Endereços de loopback]**: 

	Os endereços de loopback (127.0.0.0/8 ou 127.0.0.1 a 127.255.255.254) são usados pelos hosts para direcionar o tráfego para eles mesmos.

- **[Endereços locais de link]**:

	Os endereços locais de link (169.254.0.0/16 ou 169.254.0.1 a 169.254.255.254), também chamados de endereços auto-atribuídos. 

	Ele é usado por um cliente Windows para se autoconfigurar caso não consiga um endereço IP por outros métodos.

---

##### Legacy Classful Addressing:

Em 1981, os endereços IPv4 foram atribuídos usando o endereço classful, conforme definido na RFC 790. Os hosts receberam um endereço de rede com base em uma das três classes: A, B ou C. A RFC dividiu os [intervalos de unicast em classes específicas] da seguinte maneira:

- **[Classe A (0.0.0.0/8 to 127.0.0.0/8)]** – Projetado para suportar redes extremamente grandes com mais de 16 milhões de endereços de host. A Classe A usou um prefixo fixo /8 com o primeiro octeto para indicar o endereço de rede e os três octetos restantes para endereços de host.

- **[Classe B (128.0.0.0/16 to 191.255.0.0/16)]** - Projetada para oferecer suporte às necessidades de redes de tamanho moderado a grande com até aproximadamente 65.000 endereços de host. A Classe B usou um prefixo fixo /16 com os dois octetos de alta ordem para indicar o endereço de rede e os dois octetos restantes para endereços de host.

- **[Classe C (192.0.0.0/24 to 223.255.255.0/24)]** - Projetado para oferecer suporte a pequenas redes com no máximo 254 hosts. A Classe C usou um prefixo fixo / 24 com os três primeiros octetos para indicar a rede e o octeto restante para os endereços de host.


> [!NOTE]
> Há também um bloco multicast Classe D consistindo de 224.0.0.0 a 239.255.255.255 e um bloco de endereço experimental Classe E consistindo de 240.0.0.0 - 255.0.0.0.


Em meados da década de 1990, com a introdução da World Wide Web (WWW), o endereçamento clássico foi obsoleto para alocar de forma mais eficiente o espaço de endereços IPv4 limitado. [A alocação de endereço de classe foi substituída por endereçamento sem classe, que é usado hoje]. 

O endereçamento sem classe ignora as regras das classes (A, B, C). Endereços de rede IPv4 públicos (endereços de rede e máscaras de sub-rede) são alocados com base no número de endereços que podem ser justificados.
