---
tags:
  - arquivo
---
### Hexadecimal numbering system

Antes de abordar o endereçamento IPv6, é importante que você saiba que os endereços IPv6 são representados usando números hexadecimais. Este sistema numérico, de base dezesseis, usa os dígitos de 0 a 9 e as letras de A a F:

	0 1 2 3 4 5 6 7 8 9 A B C D E F

Nos endereços IPv6, esses 16 dígitos são representados por hextetos (discutidos a seguir), permitindo representar esses endereços enormes em um formato muito mais legível.

---
### IPv6 Addressing Formats

O primeiro passo para aprender sobre IPv6 em redes é entender a forma como um endereço IPv6 é escrito e formatado. Os endereços IPv6 são muito maiores do que os endereços IPv4, razão pela qual é improvável que fiquemos sem eles.

Os endereços IPv6 têm 128 bits e são escritos como uma sequência de valores hexadecimais. [Cada 4 bits são representados por um único dígito hexadecimal, totalizando 32 valores hexadecimais]. *Os endereços IPv6 não diferenciam maiúsculas e minúsculas.

---
### Preferred format

Como mostrado, o formato preferencial para escrever um endereço IPv6 é [x: x: x: x: x: x: x: x], com cada “x” consistindo em quatro algarismos hexadecimais.

No IPv6, um [hexteto] é o termo não oficial usado para se referir a um [segmento de 16 bits ou quatro algarismos hexadecimais]. Cada “x” é um único hexteto de 16 bits ou quatro dígitos hexadecimais.

"Formato preferencial" significa que o endereço IPv6 é gravado usando todos os 32 dígitos hexadecimais. Isso não significa necessariamente que é o método ideal para representar o endereço IPv6. 

Existem duas regras que ajudam a reduzir o número de dígitos necessários para representar um endereço IPv6.


``` shell
2001 : 0db8 : 0000 : 1111 : 0000 : 0000 : 0000: 0200
2001 : 0db8 : 0000 : 00a3 : abcd : 0000 : 0000: 1234
2001 : 0db8 : 000a : 0001 : c012 : 9aff : fe9a: 19ac
2001 : 0db8 : aaaa : 0001 : 0000 : 0000 : 0000: 0000
fe80 : 0000 : 0000 : 0000 : 0123 : 4567 : 89ab: cdef
fe80 : 0000 : 0000 : 0000 : 0000 : 0000 : 0000: 0001
fe80 : 0000 : 0000 : 0000 : c012 : 9aff : fe9a: 19ac
fe80 : 0000 : 0000 : 0000 : 0123 : 4567 : 89ab: cdef
0000 : 0000 : 0000 : 0000 : 0000 : 0000 : 0000: 0001
0000 : 0000 : 0000 : 0000 : 0000 : 0000 : 0000: 0001
```

---
### Regra 1 - Omitir zeros à esquerda

A primeira regra para ajudar a reduzir a notação de endereços IPv6 é omitir os 0s (zeros) à esquerda de qualquer seção de 16 bits ou hexteto. Aqui estão quatro exemplos de maneiras de omitir zeros à esquerda:

- 01AB pode ser representado como 1AB
- 09f0 pode ser representado como 9f0
- 0a00 pode ser representado como a00
- 00ab pode ser representado como ab

Essa regra se aplica somente aos 0s à esquerda, e NÃO aos 0s à direita. Caso contrário, o endereço ficaria ambíguo. Por exemplo, o hexteto “abc” poderia ser “0abc” ou “abc0”, mas essas duas representações não se referem ao mesmo valor.

| Tipo              | Formato                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------- |
| Preferencial      | 2001   :   **0**db8   :   **000**0   :   1111   :   **000**0   :   **000**0   :   **000**0   :   **0**200  |
| Sem 0s à esquerda | 2001   :     db8   :         0   :   1111   :         0   :         0   :         0   :     200            |
|                   |                                                                                                            |
| Preferencial      | 2001   :   **0**db8   :   **000**0   :   **00**a3   :   ab00   :   **0**ab0   :   **00**ab   :   1234      |
| Sem 0s à esquerda | 2001   :     db8   :         0   :       a3   :   ab00   :     ab0   :       ab   :   1234                 |
|                   |                                                                                                            |
| Preferencial      | 2001   :   **0**db8   :   **000**a   :   **000**1   :   c012   :     90ff   :    fe90   :   **000**1       |
| Sem 0s à esquerda | 2001   :     db8   :         a   :         1   :   c012   :     90ff   :    fe90   :        1              |
|                   |                                                                                                            |
| Preferencial      | 2001   :   **0**db8   :   aaaa   :   **000**1   :   **000**0   :    **000**0   :   **000**0   :   **000**0 |
| Sem 0s à esquerda | 2001   :     db8   :    aaaa  :         1   :         0    :         0   :         0   :         0         |

---
### Regra 2- Dois pontos duplos

A segunda regra para ajudar a reduzir a notação de endereços IPv6 é que dois pontos duplos (::) podem substituir qualquer string única e contígua de um ou mais hextetos de 16 bits consistindo em zeros.

Os dois-pontos duplos (::) só podem ser usados uma vez dentro de um endereço, caso contrário, haveria mais de um endereço resultante possível. 

Quando associada à técnica de omissão dos 0s à esquerda, a notação do endereço IPv6 pode ficar bastante reduzida. [É o chamado formato compactado].

Aqui está um exemplo do uso incorreto dos dois pontos duplos: 2001:db8::abcd::1234.

Os dois pontos duplos são usados duas vezes no exemplo acima. Aqui estão as possíveis expansões possíveis deste endereço de formato compactado incorretamente:

- 2001:db8::abcd:0000:0000:1234
- 2001:db8::abcd:0000:0000:0000:1234
- 2001:db8:0000:abcd::1234
- 2001:db8:0000:0000:abcd::1234

Se um endereço tiver mais de uma string contígua de hextetos com zero, a melhor prática é usar dois pontos duplos (::) na string mais longa. Se as strings forem iguais, a primeira string deve usar dois pontos duplos (::).

| Tipo               | Formato                                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Preferencial       | 2001   :   **0**db8   :   **000**0   :   1111   :   **000**0   :   **000**0   :   **000**0   :   **0**200         |
| Compactado/espaços | 2001   :     db8   :         0   :   1111   :                                            :     200                |
| Compactado         | 2001:db8:0:1111::200                                                                                              |
|                    |                                                                                                                   |
| Preferencial       | 2001   :   **0**db8   :   **000**0   :   **000**0   :   ab00   :   **0000**   :   **0000**   :   **0000**         |
| Compactado/espaços | 2001   :     db8   :         0   :         0   :   ab00   : :                                                     |
| Compactado         | 2001:db8:0:0:ab00::                                                                                               |
|                    |                                                                                                                   |
| Preferencial       | **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **000**1 |
| Compactado/espaços | ::                                                                                                             1  |
| Compactado         | ::1                                                                                                               |
|                    |                                                                                                                   |
| Preferencial       | **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000**   :   **0000** |
| Compactado/espaços | ::                                                                                                                |
| Compactado         | ::                                                                                                                |
