---
tags:
  - arquivo
---
##### O que é?

...

---
##### Destino em uma rede local

Às vezes, um host deve enviar uma mensagem, mas ele só sabe o endereço IP do dispositivo de destino. O host precisa saber o endereço MAC desse dispositivo, mas como ele pode ser descoberto? É aí que a resolução de endereços se torna crítica.

Dois endereços principais são atribuídos a um dispositivo em uma LAN Ethernet:

- **Endereço físico (o endereço MAC)** - Usado para comunicações de NIC para NIC na mesma rede Ethernet.
- **Endereço lógico (o endereço IP)** – Usado para enviar o pacote do dispositivo de origem para o dispositivo de destino. O endereço IP de destino pode estar na mesma rede IP que a origem ou pode estar em uma rede remota.

Os endereços físicos da camada 2 (ou seja, endereços MAC Ethernet) são usados para entregar o quadro de enlace de dados, contendo o pacote IP encapsulado, a partir de uma NIC para outra NIC que está na mesma rede. Se o endereço IP de destino estiver na mesma rede, o endereço MAC de destino será o do dispositivo de destino.

Considere o exemplo a seguir usando representações de endereço MAC simplificadas.

| MAC de destino | MAC de origem | IPv4 de origem | IPv4 de destino |
| -------------- | ------------- | -------------- | --------------- |
| 55-55-55       | aa-aa-aa      | 192.168.10.10  | 192.168.10.11   |

Neste exemplo, PC1 deseja enviar um pacote para PC2. A figura exibe os endereços MAC de destino e de origem da Camada 2 e o endereçamento IPv4 da Camada 3 que seriam incluídos no pacote enviado a partir do PC1.

O quadro Ethernet da camada 2 contém o seguinte:

- **Endereço MAC de destino** — Este é o endereço MAC simplificado de PC2, 55-55-55.
- **Endereço MAC de origem** — Este é o endereço MAC simplificado da NIC Ethernet em PC1, aa-aa-aa .

O pacote IP da camada 3 contém o seguinte:

- **Endereço IPv4 de origem** — Este é o endereço IPv4 de PC1, 192.168.10.10 .
- **Endereço IPv4 dedestino** — Este é o endereço IPv4 de PC2, 192.168.10.11.

---
##### Destino em uma rede remota

Quando o endereço IP de destino (IPv4 ou IPv6) estiver em uma rede remota, o endereço MAC de destino será o endereço do gateway padrão do host (ou seja, a interface do roteador).

Considere o exemplo a seguir usando uma representação de endereço MAC simplificada.

| MAC de  <br>destino | MAC de  <br>origem | IPv4 de origem | IPv4 de  <br>destino |
| ------------------- | ------------------ | -------------- | -------------------- |
| bb-bb-bb            | aa-aa-aa           | 192.168.10.10  | 10.1.1.10            |

Neste exemplo, PC1 deseja enviar um pacote para PC2. O PC2 está localizado na rede remota. Como o endereço IPv4 de destino não está na mesma rede local que PC1, o endereço MAC de destino é o do gateway padrão local, no roteador.

Os roteadores examinam o endereço IPv4 destino para determinar o melhor caminho para encaminhar o pacote IPv4. Quando o roteador recebe o quadro Ethernet, ele desencapsula as informações da Camada 2. 

Usando o endereço IPv4 de destino, ele determina o dispositivo do próximo salto e, em seguida, encapsula o pacote IPv4 em um novo quadro (da camada de enlace) para a interface de saída.

No nosso exemplo, o R1 agora encapsularia o pacote com novas informações de endereço da Camada 2, conforme mostrado na figura.

| MAC de  <br>destino | MAC de  <br>origem | IPv4 de origem | IPv4 de  <br>destino |
| ------------------- | ------------------ | -------------- | -------------------- |
| dd-dd-dd            | cc-cc-cc           | 192.168.10.10  | 10.1.1.10            |

O novo endereço MAC de destino seria o da interface G0/0/1 em R2 e o novo endereço MAC de origem seria o da interface G0/0/1 em R1.

Ao longo de cada link do caminho, um pacote IP é encapsulado em um quadro. O quadro é específico para a tecnologia do enlace associado a esse link, como Ethernet. Se o dispositivo do próximo salto for o destino final, o endereço MAC de destino será o da NIC Ethernet do dispositivo, conforme mostrado na figura.

| MAC de  <br>destino | MAC de  <br>origem | IPv4 de origem | IPv4 de  <br>destino |
| ------------------- | ------------------ | -------------- | -------------------- |
| 55-55-55            | ee-ee-ee           | 192.168.10.10  | 10.1.1.10            |

[Como os endereços IP dos pacotes IP em um fluxo de dados são associados aos endereços MAC em cada link ao longo do caminho até o destino?] Para pacotes IPv4, isso é feito através de um processo chamado [ARP] (Address Resolution Protocol). Para pacotes IPv6, o processo é [ICMPv6 Neighbor Discovery] (ND).