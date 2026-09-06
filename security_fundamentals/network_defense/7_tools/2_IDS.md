---
tags:
  - arquivo
---
## Intrusion Detection System — IDS

Uma intrusão ocorre quando um invasor consegue contornar ou frustrar mecanismos de segurança e obter acesso aos recursos de uma organização. 

A detecção de intrusão é uma forma específica de monitoramento que monitora informações gravadas e eventos em tempo real para detectar atividades anormais que indiquem um potencial incidente ou intrusão. 

Um sistema de detecção de intrusão automatiza a inspeção de logs e eventos do sistema em tempo real para detectar tentativas de intrusão e falhas do sistema. Um IDS é concebido como parte de um plano de segurança de defesa em profundidade. 

Ele funcionará com, e complementará, outros mecanismos de segurança, como firewalls, mas não os substituirá. Os IDSs podem reconhecer ataques que vêm de conexões externas, como um ataque da internet, e ataques que se espalham internamente, como um worm malicioso. 

Assim que detectam um evento suspeito, eles respondem enviando alertas ou disparando alarmes. O principal objetivo de um IDS é fornecer um meio para uma resposta rápida e precisa a intrusões.

A detecção e prevenção de intrusões referem-se a recursos que fazem parte do isolamento e proteção de um domínio/zona mais seguro/confiável de um menos confiável/menos seguro. 

Essas são funções naturais de se esperar de um firewall, por exemplo. Os tipos de IDS são comumente classificados como *`host-based`* e *`network-based`*. 

Um IDS baseado em host — HIDS — monitora um único computador ou host. Um IDS baseado em rede — NIDS — monitora uma rede observando padrões de tráfego de rede.

#### Host-based Intrusion Detection System

Um HIDS *monitora a atividade em um único computador*, incluindo chamadas de processo e informações registradas em logs de sistema, aplicativos, segurança e firewall baseado em host. 

Ele pode frequentemente examinar eventos com mais detalhes do que um NIDS e pode identificar arquivos específicos comprometidos em um ataque. Ele também pode rastrear processos empregados pelo invasor. 

Uma vantagem dos HIDSs em relação aos NIDSs é que os HIDSs podem detectar anomalias no sistema host que os NIDSs não conseguem detectar. Por exemplo, um HIDS pode detectar infecções onde um intruso se infiltrou em um sistema e o está controlando remotamente. 

Os HIDSs são mais caros de gerenciar do que os NIDSs porque exigem atenção administrativa em cada sistema, enquanto os NIDSs geralmente suportam administração centralizada. Um HIDS não consegue detectar ataques de rede em outros sistemas. 

#### Network Intrusion Detection System

Um NIDS monitora e avalia a atividade da rede para detectar ataques ou anomalias de eventos. Ele não consegue monitorar o conteúdo do tráfego criptografado, mas consegue monitorar outros detalhes dos pacotes. 

Um único NIDS pode monitorar uma grande rede usando sensores remotos para coletar dados em locais-chave da rede que enviam dados para um console de gerenciamento central. 

Esses sensores podem monitorar o tráfego em roteadores, firewalls, switches de rede que suportam espelhamento de portas e outros tipos de interceptação de rede. 

Um NIDS tem pouco efeito negativo no desempenho geral da rede e, quando implantado em um sistema de propósito único, não afeta negativamente o desempenho de nenhum outro computador. 

Um NIDS geralmente é capaz de detectar o início de um ataque ou ataques em andamento, mas nem sempre pode fornecer informações sobre o sucesso de um ataque. Eles não saberão se um ataque afetou sistemas específicos, contas de usuários, arquivos ou aplicativos. 

#### Security Information and Event Management

O gerenciamento de segurança envolve o uso de ferramentas que coletam informações sobre o ambiente de TI de diversas fontes distintas para examinar melhor a segurança geral da organização e otimizar os esforços de segurança. 

Essas ferramentas são geralmente conhecidas como soluções de gerenciamento de informações e eventos de segurança. 

A ideia geral de uma solução SIEM é coletar dados de log de várias fontes em toda a empresa para entender melhor possíveis preocupações com a segurança e alocar os recursos adequadamente. 

Os sistemas SIEM podem ser usados em conjunto com outros componentes — defesa em profundidade — como parte de um programa geral de segurança da informação.