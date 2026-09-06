
## Version

O primeiro elemento contido no cabeçalho é o campo  Version, que ocupa quatro bits e serve para identificar o protocolo IP em uso, 0100 para IPv4 e 0110 para IPv6. 

## Internet Header Length

Logo em sequência, o campo _Internet Header Length_ (IHL), composto por quatro bits, específica o comprimento do cabeçalho.

O campo final do cabeçalho IPv4, Options, tem um comprimento variável. Portanto, o campo IHL se faz necessário para indicar o comprimento total do cabeçalho.

Este campo especifica o comprimento do cabeçalho em incrementos de quatro bytes. Por exemplo, se o valor neste campo for de 5, 5 vezes 4 bytes é igual a 20 bytes.

- O seu valor mínimo é cinco (20 bytes), o que equivale a um cabeçalho de sem o campo Options.

- Já o valor máximo é 15 (60 bytes).

## Differentied Services Code Point - DSCP

Para a aplicação de políticas de Qualidade de Serviço (QoS) e priorização de tráfego sensível a latência, utiliza-se o campo _Differentiated Services Code Point_ (DSCP) de seis bits. 

## Explicit Congestion Notification - ECN

O DSCP é acompanhado pelo campo _Explicit Congestion Notification_ (ECN) de dois bits, cuja função é sinalizar congestionamentos na rede diretamente entre as pontas da transmissão.

Normalmente, se uma rede está congestionada, isso é sinalizado pela perda de pacotes. O ECN oferece uma maneira de sinalizar que a rede está congestionada sem descartar pacotes.

Este é um campo opcional, exigindo que ambos os endpoints, bem como a infraestrutura de rede subjacente o suportem.
## Total Length

O campo de Comprimento Total (_Total Length_), de dezesseis bits, determina o tamanho em bytes de todo o pacote, somando o cabeçalho IPv4, o cabeçalho da camada 4 e os dados úteis encapsulados.

Seu tamanho mínino é de 20 bytes, que equivale a um cabeçalho IPv4 de tamanho mínimo sem dados encapsulados. Já seu valor máximo equivale a 65.535, que é o valor máximo de 16 bits binários, todos definidos como 1.

## Identification

Esse campo também possui dezesseis bits. Caso um pacote seja fragmentado por ser muito grande, este campo é usado para indicar a qual pacote o fragmento pertence, para que ele possa ser remontado e formar o pacote original.

Todos os fragmentos de um pacote terão seu cabeçalho IPv4 com o mesmo valor neste campo.

Os pacotes serão fragmentados se forem maiores que a MTU, Maximum Transmission Unit. A MTU geralmente é de 1500 bytes.

O tamanho máximo da carga útil de um quadro Ethernet é de 1500 bytes. Esses dois aspectos estão relacionados.
## Flags

O campo _Flags_ possui três bits, sendo utilizado para controlar e identificar fragmentos.

- O primeiro bit permanece reservado e sempre definido como 0;

- O segundo atua como o indicador _Don't Fragment_ (DF) para proibir a quebra do pacote, se seu valor for 1, quer dizer que o pacote não pode ser fragmentado;

- O terceiro funciona como o indicador _More Fragments_ (MF), apontando se ainda existem mais pedaços a serem recebidos ou se o bloco atual encerra a sequência. O valor é definido como 1 se houver mais fragmentos na pacote e, em seguida, como 0 para o último fragmento.

Se o pacote for inteiro e não fragmentado, o bit MF será sempre 0.

## Fragment Offset

Complementando, o campo _Fragment Offset_, que possui treze bits, aponta a posição numérica exata que cada fragmento ocupava no pacote original, permitindo a reconstrução correta do pacote mesmo se os fragmentos chegarem fora de ordem.

### Time To Live

O campo _Time to Live_ (TTL), de de oito bits, atua como um contador de saltos que sofre a redução de uma unidade por cada roteador que encaminha o pacote; ao atingir o valor zero, o pacote é descartado pelo roteador atual, a fim de evitar loops infinitos.

O TTL padrão recomendado atualmente é de 64.

## Protocol

O campo subsequente é o Protocol, também de oito bits, que indica qual protocolo da camada superior, PDU da camada 4, está encapsulado no payload do IP.

Veja alguns dos possíveis valores desse campo:

- 6 para TCP;
- 17 para UDP;
- 1 para ICMP;
- 89 para OSPF;
- etc.

## Header Checksum

O campo _Header Checksum_ de dezesseis bits, é usado para verificar erros no cabeçalho IPv4.

Quando um roteador recebe um pacote, ele calcula o checksum do cabeçalho e o compara ao checksum definido neste campo do cabeçalho. Se forem diferentes, significa que ocorreu algum erro de transmissão e o roteador descarta o pacote.

Esse campo é usado para verificar erros no cabeçalho IPv4, não nos dados encapsulados (isso é feito pelos protocolos da camada 4, que possuem o campo checksum deles).

## Source IP Address e Destination IP address

As porções finais do cabeçalho são os campos de Endereço IP de Origem (_Source IP Address_) e Endereço IP de Destino (_Destination IP Address_), onde cada possui trinta e dois bits. Eles registram os endereços lógicos do remetente e do destinatário final do fluxo de dados. 

## Options

Por fim, existe o campo de Opções, de tamanho variável (0 bits - 320 bits), cujo uso é raro nas redes modernas.

A existência desse campo é detectada pelos roteadores sempre que o campo de controle IHL exibe um valor superior a cinco, indicando que bytes extras contendo parâmetros adicionais de testes ou segurança foram inseridos logo após a terminação do endereço de destino.