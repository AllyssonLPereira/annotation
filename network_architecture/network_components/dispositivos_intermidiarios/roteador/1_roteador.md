---
tags:
  - arquivo
---
### O que é?

[Um roteador é um dispositivo de rede que conecta várias redes IP de Camada 3]. Na camada de distribuição da rede, os roteadores [direcionam o tráfego e realizam outras funções essenciais em uma operação de rede eficiente]. Os roteadores, como switches, conseguem decodificar e ler as mensagens que são enviadas para eles. 

Mas, ao contrário dos switches, que tomam uma decisão de encaminhamento com base no endereço MAC da Camada 2, os roteadores fundamentam suas decisões de encaminhamento com base no endereço IP da Camada 3.

---
### Roteamento

Roteamento é o processo de identificação do melhor caminho até um destino.


- [Primeiro caso]:

	Digamos que um dispositivo, h1, queira enviar um pacote para h2. 

	Então, h1 irá construir uma [quadro ethernet (ethernet frame)] com seu endereço IPv4 como origem e o endereço IPv4 de h2 como destino.

	Ele verifica se o endereço IPv4 de h2 está na mesma rede, utilizando sua máscara de sub-rede para fazer a comparação.

	Caso o host de destino esteja na mesma rede, ele envia o pacote diretamente para o host de destino, lembrando do protocolo ARP. 


- [Segundo caso]:

	Caso o endereço IPv4 de h2 esteja em outra rede, h1 irá enviar o pacote IPv4 para o gateway padrão, o roteador. 

	O roteador receberá e aceitará o quadro baseado no endereço MAC. Então, ele desencapsula o quadro ethernet, lê a porção de rede do endereço IP de destino e a utiliza para descobrir qual das redes conectadas é a melhor forma de encaminhar a mensagem para o destino, ele vê por qual porta envia de acordo com o IP de destino.

	Descoberto o caminho a ser enviado, ele constrói um novo quadro ethernet, dessa vez com o endereço MAC de origem sendo seu NIC e, então, envia o pacote.


> [!NOTE] Ethernet frame
> O formato do pacote contém os endereços IP dos hosts de destino e de origem, assim como os dados da mensagem que está sendo enviada entre eles.

Quando um roteador recebe um quadro em uma interface, ele remove do quadro o cabeçalho com as informações de camada 2. ***Ele verifica a tabela de roteamento para determinar qual interface usar para enviar o pacote ao seu destino. 

Uma vez que a interface é conhecida, o pacote é encapsulado com um novo cabeçalho de quadro contendo diferentes endereços MAC de origem e destino.

---
### Roteadores como Gateways


O roteador fornece um [gateway (porta de entrada, entrada, acesso)] pelo qual os hosts de uma rede podem se comunicar com hosts de diferentes redes. *Cada interface em um roteador está conectada a uma rede separada.

Na comunicação de dados, o dispositivo de gateway padrão é envolvido apenas quando um host precisa se comunicar com hosts em outra rede. O endereço de gateway padrão identifica um dispositivo de rede que um dispositivo host usa para se comunicar com dispositivos em outras redes. 

> [!NOTE] Gateway
> O dispositivo de gateway padrão não é usado quando um host se comunica com hosts na mesma rede.

O endereço IPv4 atribuído à interface identifica a rede local que está diretamente conectada a ele.

Todo host de uma rede deve usar o roteador como um gateway para outras redes. Portanto, cada host deve conhecer o endereço IPv4 da interface do roteador conectada à rede na qual o host está conectado. 

Esse endereço é conhecido como [endereço de gateway padrão]. Ele pode ser configurado estaticamente no host ou recebido dinamicamente por DHCP.

Quando um roteador sem fio está configurado para ser um servidor DHCP da rede local, ele envia automaticamente o endereço IPv4 correto da interface para os hosts como o endereço de gateway padrão. 

Dessa forma, todos os hosts na rede podem usar o endereço IPv4 para encaminhar mensagens aos hosts localizados no ISP e obter acesso a hosts na Internet. _Os roteadores sem fio geralmente são definidos para serem servidores DHCP por padrão._

---
### Roteadores como limites entre redes


O endereço IPv4 padrão configurado na interface do roteador local sem fio geralmente é o primeiro endereço de host naquela rede. Os hosts internos devem receber endereços dentro da mesma rede do roteador sem fio, sejam eles configurados estaticamente ou através do DHCP. 

Muitos ISPs usam um servidor DHCP para fornecer endereços IPv4 do lado de Internet do roteador sem fio localizado nas instalações de clientes. A rede atribuída ao lado de Internet do roteador sem fio é conhecida como [rede externa].

Quando um roteador sem fio está conectado a um ISP, ele atua como um cliente DHCP para receber o endereço IPv4 correto de rede externa para a interface de Internet. 

Os ISPs normalmente fornecem um endereço roteável pela Internet, o que permite que os hosts conectados ao roteador sem fio tenham acesso à Internet.

*O roteador sem fio serve como limite entre a rede interna local e a Internet externa.

---
### Tabela de Roteamento


Os roteadores movem informações entre redes locais e remotas. Para fazer isso, eles têm que usar [tabelas de roteamento] para armazenar informações. As tabelas de roteamento não estão relacionadas aos endereços de hosts individuais. _[Tabelas de roteamento contêm endereços de redes e o melhor caminho para acessar essas redes]_. 

As entradas podem ser feitas na tabela de roteamento de duas maneiras: [atualizadas dinamicamente por informações recebidas de outros roteadores] na rede ou [inseridas manualmente por um administrador de rede]. 

***Os roteadores usam as tabelas de roteamento para determinar qual interface deve ser usada para encaminhar uma mensagem para o destino desejado.***

Se o roteador não conseguir determinar para onde encaminhar uma mensagem, ele a descartará. Porém, os administradores de rede podem configurar uma [rota padrão] que é inserida na tabela de roteamento para evitar que o pacote seja descartado pelo fato do caminho para a rede de destino não estar na tabela de roteamento. 

***Essa rota padrão normalmente se conecta a outro roteador que pode encaminhar o pacote para a rede de destino final.

- Exemplo:

| Tipo | Rede          | Porta           |
| ---- | ------------- | --------------- |
| C    | 10.0.0.0/8    | FastEthernet0/0 |
| C    | 172.16.0.0/16 | FastEthernet0/1 |

- **Tipo -** O tipo de conexão - C, que significa *diretamente conectado*;
- **Rede -** O endereço de rede;
- **Porta -** Interface usada para encaminhar pacotes para a rede.