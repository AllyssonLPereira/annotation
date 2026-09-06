---
tags:
  - arquivo
---
##### Introdução

Existem outros protocolos específicos da camada de aplicativo que foram projetados para facilitar a obtenção de endereços para dispositivos de rede. 

Esses serviços são essenciais porque seria muito demorado lembrar endereços IP em vez de URLs ou configurar manualmente todos os dispositivos em uma rede média a grande.

---
##### Nomes de domínio

Em redes de dados, os dispositivos são rotulados com endereços IP numéricos para enviar e receber dados pelas redes. *Os nomes de domínio foram criados para converter o endereço numérico em um nome simples e reconhecível.

Na internet, [nomes de domínio totalmente qualificados (FQDNs)], como [https://www.cisco.com], são muito mais fáceis de lembrar do que 198.133.219.25, que é o endereço numérico real para este servidor. 

Se a Cisco decidir alterar o endereço numérico de [www.cisco.com], é transparente para o usuário porque o nome de domínio permanece o mesmo. 

O novo endereço é simplesmente vinculado ao nome de domínio atual e a conectividade é mantida.

---
##### Definição do DNS


O protocolo DNS define um serviço automatizado que [compara nomes de recursos com o endereço de rede numérico requisitado]. Ele inclui o formato para consultas, respostas e dados. As comunicações do protocolo DNS utilizam um único [formato], chamado de [mensagem]. 

Este formato de mensagem é utilizado para todos os tipos de consultas de cliente e respostas de servidor, mensagens de erro e transferência de informações de registro de recursos entre servidores.

---
##### Formato de Mensagem DNS


O servidor DNS armazena diferentes tipos de registros de recursos usados ​​para resolver nomes. Esses registros contêm o nome, endereço e tipo de registro. Alguns desses [tipos de registro] são os seguintes:

- **[A]** - Um endereço IPv4 do dispositivo final
- **[NS]** - Um servidor de nomes autoritativo
- **[AAAA]** - Um endereço IPv6 de dispositivo final (pronuncia-se quad-A)
- **[MX]** - Um registro de troca de e-mail

Quando um cliente faz uma consulta, o processo DNS do servidor primeiro examina seus próprios registros para resolver o nome. Se não conseguir resolver o nome usando seus registros armazenados, ele entrará em contato com outros servidores para resolver o nome. 

Quando uma correspondência é encontrada e retornada ao servidor requisitante original, o servidor temporariamente armazena o número do endereço em questão, no caso do mesmo nome ser requisitado outra vez.

O serviço eficiente de DNS nos PCs com Windows também armazena nomes resolvidos anteriormente na memória. O comando **ipconfig /displaydns** exibe todas as entradas DNS em cache.

Conforme mostrado na tabela, o DNS usa o mesmo formato de mensagem entre servidores, consistindo em uma pergunta, resposta, autoridade e informações adicionais para todos os tipos de consultas de cliente e respostas de servidor, mensagens de erro e transferência de informações de registro de recursos.

|                |                                                     |
| -------------- | --------------------------------------------------- |
| Pergunta       | A pergunta para o servidor de nomes                 |
| Resposta       | Registros de recursos respondendo a pergunta        |
| Autoridade     | Registros de recursos apontando para uma autoridade |
| Crescimento do | Registros de recursos com informações adicionais    |

---
##### Hierarquia DNS

O protocolo DNS usa um [sistema hierárquico] para criar um banco de dados para fornecer resolução de nomes. [O DNS usa os nomes de domínio para formar a hierarquia].

A estrutura de nomenclatura é dividida em zonas pequenas, gerenciáveis. Cada servidor DNS mantém um arquivo de banco de dados específico e só é responsável por gerenciar os mapeamentos de nome para IP para essa pequena parte da estrutura DNS. 

Quando um servidor DNS recebe uma requisição para a conversão de um nome que não faça parte da sua zona DNS, o servidor DNS a encaminha para outro servidor DNS na zona apropriada para a tradução. 

O DNS é escalável porque a resolução do nome do host está espalhada por vários servidores.

Os diferentes [domínios de nível superior] representam o tipo de organização ou país de origem. Exemplos de domínios de nível superior são os seguintes:

- **[.com]** - uma empresa ou indústria
- **[.org]** - uma organização sem fins lucrativos
- **[.au]** - Australia
- **[.co]** - Colombia

---
##### O Comando nslookup


Ao configurar um dispositivo de rede, são fornecidos um ou mais endereços de servidor DNS que o cliente DNS pode usar para resolução de nomes. 

Normalmente, o ISP fornece os endereços a serem usados nos servidores DNS. Quando um aplicativo de usuário solicita a conexão a um dispositivo remoto por nome, o cliente DNS solicitante consulta o servidor de nomes para resolver o nome para um endereço numérico.

Os sistemas operacionais dos computadores também têm um utilitário chamado nslookup que permite que o usuário consulte manualmente os servidores de nome para resolver um nome de host específico. 

Este utilitário também pode ser usado para corrigir problemas de resolução de nomes e verificar o status atual dos servidores de nomes.

``` shell
C:\Users> nslookup

Default Server:  dns-sj.cisco.com
Address:         171.70.168.183

> www.cisco.com

Server:     dns-sj.cisco.com
Address:    171.70.168.183
Name:       origin-www.cisco.com
Addresses:  2001:420:1101:1::a
            173.37.145.84

Aliases:  www.cisco.com

> cisco.netacad.net

Server:   dns-sj.cisco.com
Address:  171.70.168.183
Name:     cisco.netacad.net
Address:  72.163.6.223

>
```