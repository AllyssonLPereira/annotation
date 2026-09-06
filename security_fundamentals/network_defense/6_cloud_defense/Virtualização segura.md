
## Introdução 

A virtualização segura é definida por organizações como IBM e NIST como um conjunto de práticas e tecnologias que garantem que a camada de abstração entre o hardware físico e os sistemas operacionais convidados (Guest OS) - hipervisor- permaneça íntegra e isolada. Diferente da virtualização convencional, que foca na eficiência e consolidação de recursos, a vertente segura prioriza o isolamento lógico rigoroso. 

O Hipervisor, ou Monitor de Máquina Virtual (VMM), atua como o núcleo de confiança do sistema. Ele é responsável por interceptar todas as chamadas de hardware feitas pelas máquinas virtuais (VMs), garantindo que nenhuma instância acesse áreas de memória ou ciclos de processamento que não lhe foram explicitamente atribuídos. A segurança nesse nível depende da robustez do Hipervisor em resistir a tentativas de subversão de suas funções de controle.

## TCB

- Melhor fluidez do que está acima;
- Melhor definição do que é TCB.

Dentro da arquitetura de virtualização, o conceito de _Trusted Computing Base_ (TCB) é fundamental para estabelecer a confiabilidade do sistema. O TCB engloba todos os componentes de hardware, firmware e software que são essenciais para manter a política de segurança do ambiente. Em um sistema virtualizado, a diretriz técnica é manter o TCB o menor possível. 

Quanto menos linhas de código existirem no Hipervisor e nos drivers de gerenciamento, menor será a probabilidade estatística de existirem vulnerabilidades exploráveis. Instituições acadêmicas e fabricantes como a Cisco ressaltam que um Hipervisor "enxuto" — tipicamente os de Tipo 1 (Bare Metal), que rodam diretamente sobre o hardware — oferece uma superfície de ataque reduzida em comparação com Hipervisores de Tipo 2, que dependem de um sistema operacional hospedeiro completo. Isso simplifica a auditoria e o endurecimento (_hardening_) do sistema.

## Isolamento e abstração de recursos

O isolamento é a pedra angular da virtualização segura. Ele assegura que, embora múltiplas VMs compartilhem o mesmo processador físico e barramentos de memória, elas operem em domínios de proteção completamente distintos. Este processo é viabilizado por tecnologias de hardware, como as extensões de virtualização de CPU (Intel VT-x ou AMD-V), que permitem ao Hipervisor criar partições isoladas. 

A virtualização segura exige que esse isolamento não se limite apenas à CPU e memória, mas se estenda à entrada e saída (I/O) e à rede virtual. Ao abstrair os recursos físicos, o Hipervisor impede que uma VM comprometida utilize técnicas de varredura de barramento para interceptar dados de outras máquinas, estabelecendo uma fronteira lógica que deve ser intransponível sem a mediação explícita da camada de controle.

## Redução da superfície de ataque

A interface de gerenciamento do ambiente virtualizado é frequentemente o ponto mais crítico de exposição em toda a arquitetura. Para que a virtualização seja considerada tecnicamente segura, o acesso a essas ferramentas de controle deve ser segregado da rede de dados convencional. 

A Fortinet enfatiza que a superfície de ataque deve ser minimizada através da desativação de funcionalidades e serviços desnecessários no Hipervisor. Além disso, o software de orquestração e as APIs de gerenciamento devem ser protegidos por controles de autenticação rigorosos e sistemas de logs de auditoria imutáveis. 

A integridade de toda a estrutura virtualizada depende da premissa de que o plano de controle está blindado, pois qualquer comprometimento no nível de gestão pode anular as proteções de isolamento implementadas no nível do hardware.

## Segurança e controle On-Premise

Em infraestruturas locais, a organização detém o controle absoluto sobre toda a pilha tecnológica, desde o hardware físico e o cabeamento até as aplicações que rodam nas máquinas virtuais. Entretanto, essa autonomia exige uma responsabilidade proporcional e integral. De acordo com a visão técnica da Cisco, um dos maiores erros em ambientes locais é a dependência excessiva de firewalls de borda para proteger o tráfego que entra e sai da rede (tráfego Norte-Sul). 

No contexto da virtualização, a maior ameaça reside no tráfego Leste-Oeste, que ocorre internamente entre máquinas virtuais dentro do mesmo servidor físico ou cluster. Sem controles de microssegmentação, uma VM comprometida pode servir de ponto de apoio para que um atacante se mova lateralmente por toda a rede interna, muitas vezes sem que os sistemas de segurança perimetrais detectem qualquer anomalia. 

A defesa local, portanto, exige que a segurança seja aplicada no nível do hipervisor e das interfaces virtuais, tratando cada carga de trabalho como se estivesse em uma rede potencialmente hostil.

## Responsabilidade compartilhada na nuvem

A transição para a nuvem altera fundamentalmente a dinâmica da segurança, introduzindo o conceito de Modelo de Responsabilidade Compartilhada, amplamente documentado pela IBM e por grandes provedores. Nesse cenário, existe uma divisão clara de deveres: o provedor de nuvem é responsável pela segurança "da" nuvem — o que inclui a proteção física dos data centers, o hardware do servidor e a integridade do hipervisor proprietário. 

O cliente, por sua vez, detém a responsabilidade pela segurança "na" nuvem. Isso abrange a configuração correta do sistema operacional da instância virtual, o gerenciamento de identidades e acessos (IAM), a criptografia de dados e a segurança das aplicações. 

A falha mais comum nesse ambiente não é uma vulnerabilidade no provedor, mas a má configuração por parte do usuário, que pode expor inadvertidamente portas de gerenciamento ou volumes de armazenamento para a internet pública, anulando as proteções de infraestrutura oferecidas pelo provedor.

## Visibilidade e consistência em ambientes híbridos

A complexidade aumenta significativamente quando as organizações operam em modelos híbridos, onde cargas de trabalho virtuais coexistem em servidores locais e em múltiplas nuvens públicas. A Fortinet destaca que a falta de visibilidade unificada é um dos principais vetores de risco nessas arquiteturas. Políticas de segurança configuradas manualmente em silos diferentes tendem a divergir, criando lacunas de proteção. 

Uma virtualização segura em ambiente híbrido exige a implementação de uma "malha de segurança" (Security Fabric) que permita aplicar políticas idênticas e centralizadas, independentemente de onde a máquina virtual esteja residindo fisicamente. 

O objetivo técnico é garantir que a postura de segurança seja centrada na carga de trabalho (Workload-centric), acompanhando a VM em todo o seu ciclo de vida, desde o provisionamento até a desativação, mantendo a conformidade e a proteção de dados de forma consistente através das fronteiras da infraestrutura física e virtual.

## Ameaças comuns de VMs

### VM Escape

O _VM Escape_ é considerado a ameaça mais crítica em ambientes virtualizados, pois representa a quebra completa do isolamento entre o sistema convidado e o hospedeiro. 

Nesta modalidade de ataque, um invasor utiliza um código malicioso dentro de uma máquina virtual para explorar uma vulnerabilidade no hipervisor, permitindo a execução de comandos diretamente no sistema operacional do host ou na camada de gerenciamento. Uma vez que o atacante "escapa" da VM, ele ganha visibilidade e controle sobre todas as outras máquinas virtuais que compartilham o mesmo hardware. 

Instituições de cibersegurança ressaltam que esta falha anula a premissa de multi-inquilinato (_multi-tenancy_), tornando-se um risco sistêmico especialmente grave em nuvens públicas onde diferentes empresas compartilham o mesmo servidor físico.

### Remanência de dados

A remanência de dados refere-se à persistência de informações sensíveis em componentes de hardware — como memória RAM ou discos de armazenamento — após uma máquina virtual ter sido encerrada ou movida. Como o hipervisor gerencia a alocação dinâmica desses recursos, existe o risco técnico de que um novo sistema virtual receba um bloco de memória que anteriormente continha chaves de criptografia, senhas ou dados confidenciais de outro usuário.

A IBM enfatiza que a virtualização segura exige processos rigorosos de "limpeza de recursos" (_resource scrubbing_), onde o hipervisor deve obrigatoriamente sobrescrever os bits de memória com zeros ou dados aleatórios antes de disponibilizá-los para uma nova instância, evitando a coleta passiva de informações por novos ocupantes do hardware.

### Escalonamento de privilégios e controle do Hipervisor

O escalonamento de privilégios no contexto virtual ocorre quando um atacante, após obter acesso limitado a uma máquina virtual ou a uma conta de usuário no console de gerenciamento, explora falhas de configuração para elevar seu nível de autoridade. Diferente do escalonamento em sistemas convencionais, aqui o objetivo costuma ser o controle das APIs do hipervisor.

Se um invasor obtém privilégios administrativos sobre a orquestração virtual, ele pode alterar políticas de segurança, desativar logs de auditoria ou criar clones de discos virtuais para análise offline. A Cisco aponta que a falta de uma política rigorosa de Menor Privilégio (PoLP) nas interfaces de gerenciamento é um dos principais facilitadores para que uma intrusão inicial se transforme em um comprometimento total da infraestrutura virtual.

### Vulnerabilidades em migração de VMs (Live Migration)

A migração ao vivo é a capacidade de mover uma máquina virtual de um servidor físico para outro sem interrupção do serviço. Contudo, este processo introduz riscos significativos se a rede de gerenciamento não for adequadamente protegida. 

Durante a migração, todo o conteúdo da memória RAM da VM — o que inclui estados de aplicações, credenciais ativas e chaves de sessão — é transmitido através da rede. Segundo estudos acadêmicos e documentação da Fortinet, se esse tráfego não for criptografado e isolado em uma rede dedicada, um atacante pode realizar um ataque de _Man-in-the-Middle_ (MitM) para capturar os dados em trânsito ou até mesmo injetar código malicioso no arquivo da VM antes que ele chegue ao destino. A segurança da migração, portanto, depende da integridade do canal de comunicação entre os hosts físicos.