---
tags:
  - arquivo
---
## Firewalls

Um firewall é um sistema ou grupo de sistemas que aplica uma política de controle de acesso entre redes.

#### Common Firewall Properties

Os firewalls são resistentes a ataques de rede. Além disso, firewalls são o único ponto de trânsito entre redes corporativas internas e redes externas porque *todo o tráfego flui através do firewall*, reforçando a política de controle de acesso.

#### Benefits of firewall

Firewalls impedem a exposição de hosts, recursos e aplicações sensíveis a usuários não confiáveis. Também, eles sanitizam o fluxo do protocolo, o que impede a exploração de falhas no protocolo.

Eles bloqueiam dados maliciosos de servidores e clientes, e reduzem a complexidade do gerenciamento de segurança descarregando a maior parte do controle de acesso à rede para alguns firewalls na rede.

---
## Firewall Types

É importante entender os diferentes tipos de firewalls e suas capacidades específicas para que o firewall correto seja usado para cada situação.

#### 1. Packet filtering firewall — stateless

Um firewall sem estado é um sistema de segurança que filtra pacotes de rede de forma isolada. Ele não armazena informações sobre o contexto das conexões ou o histórico de comunicações anteriores. Cada pacote de dados é tratado como uma entidade única e independente.

O controle é realizado através de **Listas de Controle de Acesso (ACLs)**. O firewall examina o cabeçalho de cada pacote individual e o compara com regras estáticas predefinidas. Se o pacote não atender aos critérios exatos, ele é bloqueado.

Os critérios de filtragem comuns incluem:

- Endereço IP de origem e destino.
- Número da porta de origem e destino.
- Tipo de protocolo (TCP, UDP, ICMP).

| **Vantagens**                                                                                  | **Desvantagens**                                                                                                    |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Velocidade:** Processamento rápido, pois não exige análise de contexto ou memória de estado. | **Baixa Segurança:** Vulnerável a ataques que exploram a falta de contexto (ex: falsificação de pacotes).           |
| **Baixo Consumo de Recursos:** Exige menos memória e CPU do hardware.                          | **Regras Complexas:** Exige regras manuais para o tráfego de entrada e saída (tráfego de retorno não é automático). |
| **Escalabilidade:** Eficiente em redes com volumes massivos de tráfego simples.                | **Incapacidade de Inspeção:** Não consegue identificar ameaças dentro da carga útil (payload) do pacote.            |
#### 2. Stateful Firewall

O firewall de segunda geração, conhecido como **Stateful Inspection** (Inspeção com Estado), evoluiu a partir da filtragem de pacotes simples ao adicionar a capacidade de monitorar o contexto das conexões de rede. Ele não analisa apenas pacotes isolados, mas o fluxo completo da comunicação.

A principal característica técnica é a **Tabela de Estados** (_State Table_). Quando um pacote inicia uma conexão, o firewall armazena os detalhes dessa sessão, incluindo:

- Endereços IP (origem e destino).
- Portas (origem e destino).
- Números de sequência do protocolo (TCP).
- Estado da conexão (ex: SYN_SENT, ESTABLISHED).


Ao receber pacotes subsequentes, o firewall verifica se eles pertencem a uma conexão já registrada na tabela. Se pertencerem, o tráfego é permitido automaticamente, ignorando a reavaliação completa das regras de segurança, o que otimiza o processamento.
#### 3. Application Gateway Firewall

*Um firewall de gateway de aplicação (firewall proxy), filtra as informações nas camadas 3, 4, 5 e 7 do modelo de referência OSI. 

*A maior parte do controle e filtragem do firewall é feita em software*. Quando um cliente precisa acessar um servidor remoto, ele se conecta a um servidor proxy. 

O servidor proxy se conecta ao servidor remoto em nome do cliente. Portanto, o servidor só vê uma conexão do servidor proxy.

#### 4. Next-generation firewall

Os firewalls de última geração (NGFW) vão além dos firewalls de estado, fornecendo:

- Prevenção de intrusão integrada;
- Reconhecimento e controle de aplicativos para ver e bloquear aplicativos arriscados;
- Caminhos de atualização para incluir futuros feeds de informações;
- Técnicas para lidar com ameaças de segurança em evolução.

Outros métodos de implementação de firewalls incluem:

#### 5. Host-based firewall — server and staff

Um PC ou servidor com software de firewall em execução.

Firewalls baseados em host podem usar um conjunto de políticas predefinidas, ou perfis, para controlar pacotes que entram e saem de um computador. 

Eles também podem ter regras que podem ser diretamente modificadas ou criadas para controlar o acesso com base em endereços, protocolos e portas. Aplicativos de firewall baseados em host também podem ser configurados para emitir alertas aos usuários se um comportamento suspeito for detectado. 

Eles podem então oferecer ao usuário a capacidade de permitir que um aplicativo ofensivo seja executado ou ser impedido de ser executado no futuro.

Uma abordagem para a prevenção de intrusões é o uso de firewalls distribuídos. Os firewalls distribuídos combinam recursos de firewalls baseados em host com gerenciamento centralizado. 

A função de gerenciamento envia regras para os hosts e também pode aceitar arquivos de log dos hosts.

Independentemente de serem instalados completamente no host ou distribuídos, os firewalls baseados em host são uma camada importante de segurança de rede, juntamente com firewalls baseados em rede. 

- *Firewall transparente -* Filtra o tráfego IP entre um par de interfaces em modo bridge.
- *Firewall híbrido -* Uma combinação dos vários tipos de firewalls. Por exemplo, um firewall de inspeção de aplicações combina um firewall com estado com um firewall de gateway de aplicativo.


