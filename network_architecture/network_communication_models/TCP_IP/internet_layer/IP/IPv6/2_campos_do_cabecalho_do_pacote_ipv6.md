---
tags:
  - arquivo
---
### Visão geral do IPv6

No início da década de 90, a Internet Engineering Task Force (IETF) tinha uma preocupação crescente a respeito dos problemas com o IPv4 e começou a procurar um substituto. Isso levou ao desenvolvimento do IP versão 6 (IPv6). 

O IPv6 supera as limitações do IPv4 e possui recursos que atendem às demandas atuais e previsíveis de rede.

As melhorias que o IPv6 fornece incluem o seguinte:

- **[Espaço de endereço aumentado]**

	Os endereços IPv6 são baseados no endereçamento hierárquico de 128 bits, em oposição ao IPv4 com 32 bits.

- **[Manipulação aprimorada de pacotes]**

	O cabeçalho IPv6 foi simplificado com menos campos.

- **[Elimina a necessidade de NAT]**

	Com um número tão grande de endereços IPv6 públicos, o NAT entre um endereço IPv4 privado e um IPv4 público não é necessário. Isso evita alguns dos problemas induzidos por NAT enfrentados por aplicativos que exigem conectividade de ponta a ponta.


O espaço de 32 bits de um endereço IPv4 fornece aproximadamente 4,294,967,296 endereços exclusivos. 

O espaço de endereço IPv6 fornece 340,282,366,920,938,463,463,374,607,431,768,211,456, ou 340 undecilhões de endereços. Isto é aproximadamente equivalente a cada grão de areia na Terra.

---
### Campos do cabeçalho do pacote IPv4 no cabeçalho do pacote IPv6

Uma das principais melhorias de design do IPv6 em relação ao IPv4 é o [cabeçalho IPv6 simplificado].

Por exemplo, o cabeçalho IPv4 consiste em um cabeçalho de comprimento variável de 20 octetos (até 60 bytes se o campo Opções for usado) e 12 campos de cabeçalho básicos, sem incluir o campo Opções e o campo Preenchimento.

Para o IPv6, alguns campos permaneceram os mesmos, alguns campos mudaram de nome e posição e alguns campos do IPv4 não são mais necessários, conforme destacado na figura.

![[cabecalho_do_pacote_IPv6.webp]]


Os campos no cabeçalho do pacote IPv6 incluem o seguinte:

- **[Versão]**

	Este campo contém um valor binário de [4 bits] definido como 0110 que identifica isso como um pacote IP versão 6.

- **[Classe de tráfego]**

	Este campo de [8 bits é equivalente ao campo DS] (Serviços diferenciados de IPv4).

- **[Etiqueta de fluxo]**

	Este campo de [20 bits] sugere que todos os pacotes com a mesma etiqueta de fluxo recebam o mesmo tipo de manipulação pelos roteadores, ou seja, manten o mesmo fluxo de pacotes por roteadores e switches.

- **[Comprimento da carga útil]**

	Este campo de [16 bits] indica o comprimento da parte dos dados ou da carga útil do pacote IPv6. Isso não inclui o comprimento do cabeçalho IPv6, que é um cabeçalho fixo de 40 bytes.

- **[Próximo cabeçalho]**

	Este campo de [8 bits] é equivalente ao campo Protocolo IPv4. Ele exibe o tipo de carga de dados que o pacote está carregando, permitindo que a camada de rede transfira os dados para o protocolo apropriado das camadas superiores.

- **[Limite de salto]**

	Este campo de [8 bits] substitui o campo TTL IPv4. Esse valor é subtraído de um por cada roteador que encaminha o pacote. 

	Quando o contador atinge 0, o pacote é descartado e uma mensagem de ICMPv6 com tempo excedido é encaminhada para o host de envio. 

	Ao contrário do IPv4, o IPv6 não inclui uma soma de verificação do cabeçalho IPv6, porque esta função é executada nas camadas inferior e superior. Isso significa que a soma de verificação não precisa ser recalculada por cada roteador quando diminui o campo Limite de Hop, o que também melhora o desempenho da rede.

- **[Endereço IPv6 de origem]**

	Este campo de 128 bits identifica o endereço IPv6 do host de envio.

- **[Endereço IPv6 de destino]**

	Este campo de 128 bits identifica o endereço IPv6 do host de recebimento.


Um pacote IPv6 pode conter também cabeçalhos de extensão (EH), que fornecem informações de camada de rede. Opcionais, os cabeçalhos de extensão ficam posicionados entre o cabeçalho IPv6 e a carga. Eles são usados para fragmentação, segurança, suporte à mobilidade e muito mais.

Ao contrário de IPv4, os roteadores não fragmentam os pacotes IPv6 roteados.