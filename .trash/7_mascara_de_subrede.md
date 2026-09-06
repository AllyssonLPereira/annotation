---
tags:
  - arquivo
---
##### Máscara de sub-rede

A máscara de sub-rede IPv4 é usada para diferenciar a parte da rede da parte do host de um endereço IPv4. Quando um endereço IPv4 é atribuído a um dispositivo, a máscara de sub-rede é usada para determinar o endereço de rede do dispositivo. O endereço de rede representa todos os dispositivos na mesma rede.

Para identificar as partes da rede e do host de um endereço IPv4, a máscara de sub-rede é comparada com o endereço IPv4 bit por bit, da esquerda para a direita.

[A máscara de sub-rede] não contém a parte da rede ou host de um endereço IPv4, [apenas informa ao computador onde procurar a parte do endereço IPv4 que é a parte da rede e qual parte é a parte do host].

O processo real usado para identificar a parte da rede e a parte de host é chamado de AND.

---
##### Comprimento do Prefixo

Expressar os endereços de rede e os endereços de host com o endereço da máscara de sub-rede em decimal com pontos pode ser complicado. Felizmente, existe um método alternativo para identificar uma máscara de sub-rede, um método chamado [comprimento do prefixo].

O comprimento do prefixo é o [número de bits definido como 1 na máscara de sub-rede]. Está escrito em "notação de barra", que é anotada por uma barra (/) seguida pelo número de bits definido como 1. Portanto, conte o número de bits da máscara de sub-rede e preceda-o com uma barra.

Consulte a tabela para exemplos. A primeira coluna lista várias máscaras de sub-rede que podem ser usadas com um endereço de host. A segunda coluna mostra o endereço binário de 32 bits convertido. A última coluna mostra o comprimento do prefixo resultante.

| Máscara de Sub-Rede | Endereço de 32 bits                 | Comprimento do Prefixo |
| ------------------- | ----------------------------------- | ---------------------- |
| 255.0.0.0           | 11111111.00000000.00000000.00000000 | /8                     |
| 255.255.0.0         | 11111111.11111111.00000000.00000000 | /16                    |
| 255.255.255.0       | 11111111.11111111.11111111.00000000 | /24                    |
| 255.255.255.128     | 11111111.11111111.11111111.10000000 | /25                    |
| 255.255.255.192     | 11111111.11111111.11111111.11000000 | /26                    |
| 255.255.255.224     | 11111111.11111111.11111111.11100000 | /27                    |
| 255.255.255.240     | 11111111.11111111.11111111.11110000 | /28                    |
| 255.255.255.248     | 11111111.11111111.11111111.11111000 | /29                    |
| 255.255.255.252     | 11111111.11111111.11111111.11111100 | /30                    |

> [!NOTE]
> Um endereço de rede também é conhecido como prefixo ou prefixo de rede. Portanto, o comprimento do prefixo é o número de 1 bits na máscara de sub-rede.

Ao representar um endereço IPv4 usando um comprimento de prefixo, o endereço IPv4 é gravado seguido do comprimento do prefixo sem espaços. Por exemplo, 192.168.10.10 255.255.255.0 seria gravado como 192.168.10.10/24.

---
##### Determinando a rede: "AND" lógico

Um AND lógico é uma das três operações booleanas usadas na lógica booleana ou digital. As outras duas são OR e NOT. A operação AND é usada para determinar o endereço de rede.

AND lógico é a comparação de dois bits que produz os resultados mostrados abaixo. Observe como somente 1 AND 1 produz um 1. Qualquer outra combinação resulta em um 0.

- 1 E 1 = 1
- 0 E 1 = 0
- 1 E 0 = 0
- 0 E 0 = 0

> [!NOTE]
> Na lógica digital, 1 representa Verdadeiro e 0 representa Falso. Ao usar uma operação AND, ambos os valores de entrada devem ser Verdadeiro (1) para que o resultado seja Verdadeiro (1).

Para identificar o endereço de rede de um host IPv4, é feito um AND lógico, bit a bit, entre o endereço IPv4 e a máscara de sub-rede. Quando se usa AND entre o endereço e a máscara de sub-rede, [o resultado é o endereço de rede].

Para ilustrar como AND é usado para descobrir um endereço de rede, considere um host com endereço IPv4 192.168.10.10 e máscara de sub-rede 255.255.255.0, conforme mostrado na figura:

- **[Endereço de host IPv4]** (192.168.10.10) - O endereço IPv4 do host em formato decimal com pontos e binário.

- **[Máscara de sub-rede]** (255.255.255.0) - A máscara de sub-rede do host nos formatos decimal com pontos e binário.

- **[Endereço de rede]** (192.168.10.0) - A operação lógica AND entre o endereço IPv4 e a máscara de sub-rede resulta em um endereço de rede IPv4 mostrado nos formatos decimal com pontos e binário.


Usando a primeira sequência de bits como exemplo, observe que a operação AND é executada no bit 1 do endereço do host com o bit 1 da máscara de sub-rede. Isso resulta em um bit 1 para o endereço de rede.

A operação AND entre um endereço de host IPv4 e uma máscara de sub-rede resulta no endereço de rede IPv4 para este host. 

Neste exemplo, a operação AND entre o endereço de host 192.168.10.10 e a máscara de sub-rede 255.255.255.0 (/24) resulta no endereço de rede IPv4 192.168.10.0/24. Esta é uma operação IPv4 importante, pois informa ao host a qual rede pertence.

> [!NOTE]
> A máscara de sub-rede identifica a parte de rede do endereço IP do host, não o próprio endereço IP da rede, e é por isso que dois hosts com a mesma máscara de sub-rede não estão necessariamente na mesma rede.