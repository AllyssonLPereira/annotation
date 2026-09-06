---
tags:
  - arquivo
---
### Decisão de Encaminhamento do Host

Com IPv4 e IPv6, os pacotes são sempre criados no host de origem. O host de origem deve ser capaz de direcionar o pacote para o host de destino. Para fazer isso, [os hosts criam suas próprias tabelas de roteamento].

Outra função da camada de rede é direcionar pacotes entre hosts. Um host pode enviar um pacote para o seguinte:

- **[Ele mesmo]** - um host pode executar ping em si mesmo enviando um pacote para um endereço IPv4 especial 127.0.0.1 ou um endereço IPv6 :: / 1, conhecido como interface de loop back. *O ping na interface de loop back testa a pilha de protocolos do TCP/IP no host.

- **[Host local]** - este é um host de destino que está na mesma rede local que o host de envio. *Os hosts de origem e destino compartilham o mesmo endereço de rede.

- **[Host remoto]** - este é um host de destino em uma rede remota. *Os hosts de origem e destino não compartilham o mesmo endereço de rede.


O host de origem determina se o endereço IP de destino está na mesma rede em que ele está. O método de determinação varia de acordo com a versão IP:

- **[Em IPv4]** - o host de origem usa sua própria máscara de sub-rede junto com seu próprio endereço IPv4 e o endereço IPv4 de destino para fazer essa determinação.

- **[Em IPv6]** - o roteador local anuncia o endereço da rede local (*prefixo de rede*) para todos os dispositivos da rede.

Em uma rede doméstica ou comercial, você pode ter vários dispositivos com e sem fio interconectados usando um host intermediário, como um switch LAN ou um ponto de acesso sem fio (WAP). 

Este host intermediário fornece interconexões entre hosts locais na LAN. Os hosts locais podem interagir entre si e compartilhar informações sem a necessidade de hosts adicionais. 

Se um host estiver enviando um pacote para um dispositivo configurado com a mesma rede IP que o host de destino, o pacote será simplesmente encaminhado para fora da interface do host remetente, através do host intermediário e diretamente ao dispositivo de destino.

Obviamente, na maioria das situações, queremos que nossos dispositivos possam se conectar além do segmento de rede local, como em outras residências, empresas e na Internet. 

Os dispositivos que estão além do segmento de rede local são conhecidos como hosts remotos. Quando um dispositivo de origem envia um pacote a um dispositivo de destino remoto, é necessária a ajuda de roteadores e do roteamento. 

*O roteamento é o processo de identificação do melhor caminho até um destino. O roteador conectado ao segmento de rede local é conhecido como gateway padrão.

---
### Tabela de roteamento

Uma tabela de roteamento de host normalmente inclui um gateway padrão. No IPv4, o host recebe o endereço IPv4 do gateway padrão dinamicamente do DHCP (Dynamic Host Configuration Protocol) ou configurado manualmente. 

No IPv6, o roteador anuncia o endereço de gateway padrão ou o host pode ser configurado manualmente.

A configuração do gateway padrão cria uma rota padrão na tabela de roteamento do computador. *Uma rota padrão é a rota ou o caminho que o computador usa quando tenta entrar em contato com uma rede remota.


> [!NOTE] 
> Em um host do Windows, o comando **route print** ou o comando **netstat-r** pode ser usado para exibir a tabela de roteamento do host. Os dois comandos geram o mesmo resultado.


