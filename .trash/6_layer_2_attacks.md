---
tags:
  - arquivo
---
### Ataques de Camada 2


A camada 2 refere-se à camada de link de dados no modelo de comunicação de dados Open Systems Interconnection (OSI).

Essa camada é usada para mover dados por uma rede física vinculada. Os endereços IP são mapeados para cada endereço de dispositivo físico (também conhecido como endereço de controle de acesso de mídia - MAC) na rede, usando um procedimento chamado protocolo de resolução de endereço (ARP). 

Em seus termos mais simples, o endereço MAC identifica o destinatário de um endereço IP enviado pela rede, e o ARP resolve endereços IP para endereços MAC para transmissão de dados. 

***Os invasores geralmente aproveitam as vulnerabilidades nessa segurança de camada 2.

---
### Tipos de ataques


###### Spoofing:

***[Spoofing é um ataque de representação e tira proveito de uma relação de confiança entre os dois sistemas].

- A falsificação de endereço MAC ocorre quando um invasor disfarça seu dispositivo como um dispositivo válido na rede e, portanto, pode ignorar o processo de autenticação. 

- O ARP spoofing envia mensagens ARP falsificadas através de uma LAN. Isso vincula o endereço MAC de um invasor ao endereço IP de um dispositivo autorizado na rede.

- A falsificação de IP envia pacotes IP de um endereço de origem falsificado para disfarçar a origem do pacote.
![[spoofing.png]]


###### Inundação de MAC

Os dispositivos em uma rede são conectados por um switch de rede usando o switching de pacote para receber e encaminhar dados para o dispositivo de destino. 

A inundação de MAC compromete os dados transmitidos para um dispositivo. ***[Um invasor inunda a rede com endereços MAC falsos, comprometendo a segurança do switch de rede].
![[inundacao_mac.png]]