---
tags:
  - arquivo
---
São muitos os serviços que acessamos pela Internet ao longo do dia. DNS, Web, E-mail, FTP, Mensagem instantânea e VoIP são apenas alguns desses serviços que são disponibilizados por sistemas cliente/servidor em todo o mundo. 

Eles podem ser fornecidos por um único servidor ou por vários servidores em grandes datacenters.

Quando uma mensagem é entregue usando o TCP ou o UDP, os protocolos e os serviços são identificados por um número de porta. 

Uma porta é um identificador numérico dentro de cada segmento que é usado para rastrear conversas específicas entre um cliente e um servidor. Cada mensagem que um host envia contém uma porta origem e destino.

---
##### Funcionamento

Quando uma mensagem é recebida por um servidor, é necessário que o servidor consiga determinar qual serviço está sendo solicitado pelo cliente. [Os clientes são pré-configurados para usar uma porta de destino que foi registrada na Internet para cada serviço]. 

Um exemplo disso são os clientes de navegador da Web, que são configurados previamente para enviar solicitações para servidores da Web pela porta 80 (a porta usada normalmente para serviços da Web em HTTP).

As portas são atribuídas e gerenciadas por uma organização conhecida como ICANN (Internet Corporation for Assigned Names and Numbers, Corporação da Internet para Atribuição de Nomes e Números). As portas foram divididas em três categorias e variam em número de 1 a 65.535.

- **[Portas bem conhecidas] –** As portas de destino que estão associadas a aplicativos de rede comuns são identificadas como portas bem conhecidas. Elas estão no intervalo de 1 a 1.023.

- **[Portas registradas] –** As portas 1.024 a 49.151 podem ser usadas como portas de destino ou de origem. Elas podem ser usadas por empresas para registrar aplicativos específicos, como os de mensagem instantânea.

- **[Portas privadas] –** As portas de 49.152 a 65.535 são geralmente utilizadas como portas de origem. Elas podem ser usadas por qualquer aplicativo.

A tabela exibe alguns números de porta conhecidos comuns e seus aplicativos associados.

| Número da Porta | Protocolo de aplicação                               | Transporte |
| --------------- | ---------------------------------------------------- | ---------- |
| 20              | Protocolo de Transferência de Arquivos (FTP) - Dados | TCP        |
| 21              | FTP - Controle                                       | TCP        |
| 22              | Secure Shell (Shell seguro) - SSH                    | TCP        |
| 23              | Telnet                                               | TCP        |
| 25              | SMTP                                                 | TCP        |
| 53              | DNS                                                  | UDP, TCP   |
| 67              | DHCP - Servidor                                      | UDP        |
| 68              | DHCP - Cliente                                       | UDP        |
| 69              | Protocolo de Transferência Trivial de Arquivo (TFTP) | UDP        |
| 80              | HTTP                                                 | TCP        |
| 110             | POP3 (Post Office Protocol - Protocolo dos Correios) | TCP        |
| 143             | IMAP                                                 | TCP        |
| 161             | Protocolo de Gerenciamento Simples de Rede (SNMP)    | UDP        |
| 443             | HTTPS                                                | TCP        |

Algumas aplicações podem usar tanto TCP quanto UDP. Por exemplo, o DNS usa o protocolo UDP quando os clientes enviam requisições a um servidor DNS. Contudo, a comunicação entre dois servidores DNS sempre usa TCP.

Pesquise no site da IANA o registro de portas para visualizar a lista completa de números de portas e aplicativos associados.

---
##### Pares de soquetes

As portas origem e destino são colocadas no segmento. Os segmentos são encapsulados em um pacote IP. O pacote IP contém o endereço IP de origem e destino. A combinação do endereço IP de origem e o número de porta de origem, ou do endereço IP de destino e o número de porta de destino é conhecida como um [socket].

Por exemplo, a solicitação FTP gerada por um PC inclui os endereços MAC da Camada 2 e os endereços IP da Camada 3. A solicitação também identifica o número da porta de origem 1305 (ou seja, gerado dinamicamente pelo host) e a porta de destino, identificando os serviços de FTP na porta 21. 

O host também solicitou uma página da Web do servidor usando os mesmos endereços de Camada 2 e Camada 3. No entanto, ele está usando o número da porta de origem 1099 (ou seja, gerado dinamicamente pelo host) e a porta de destino identificando o serviço Web na porta 80.

O socket é usado para identificar o servidor e o serviço que está sendo solicitado pelo cliente. Um socket do cliente pode ser assim, com 1099 representando o número da porta de origem: [192.168.1.5:1099]. Já o soquete em um servidor da web pode ser [192.168.1.7:80].

Juntos, esses dois sockets se combinam para formar um par de sockets: 192.168.1.5:1099, 192.168.1.7:80

Os sockets permitem que vários processos em execução em um cliente se diferenciem uns dos outros, e várias conexões com um processo no servidor sejam diferentes umas das outras.

Este número de porta age como um endereço de retorno para a aplicação que faz a solicitação. A camada de transporte rastreia essa porta e a aplicação que iniciou a solicitação, de modo que quando uma resposta é retornada, ela pode ser encaminhada para a aplicação correta.

---
##### O Comando netstat

Conexões TCP desconhecidas podem ser uma ameaça de segurança maior. Elas podem indicar que algo ou alguém está conectado ao host local. Às vezes é necessário conhecer quais conexões TCP ativas estão abertas e sendo executadas em um host de rede. 

O netstat é um utilitário de rede importante que pode ser usado para verificar essas conexões. Como mostrado abaixo, digite o comando **netstat** para listar os protocolos em uso, o endereço local e os números de porta, o endereço externo e os números de porta e o estado da conexão.

``` shell
C:∖> netstat

Active Connections  

Proto    Local Address          Foreign Address           State  

TCP      192.168.1.124:3126     192.168.0.2:netbios-ssn   ESTABLISHED  
TCP      192.168.1.124:3158     207.138.126.152:http      ESTABLISHED  
TCP      192.168.1.124:3159     207.138.126.169:http      ESTABLISHED  
TCP      192.168.1.124:3160     207.138.126.169:http      ESTABLISHED  
TCP      192.168.1.124:3161     sc.msn.com:http           ESTABLISHED  
TCP      192.168.1.124:3166     www.cisco.com:http        ESTABLISHED
(output omitted)
C:∖>
```

Por padrão, o comando **netstat** tentará resolver os endereços IP para os nomes de domínio e os números de porta para aplicações bem conhecidas. A opção **-n** pode ser usada para exibir endereços IP e números de porta em sua forma numérica.