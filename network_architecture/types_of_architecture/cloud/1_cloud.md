---
tags:
  - arquivo
---
## Types of Clouds


- *`Public clouds`*

	Os aplicativos e serviços baseados em nuvem oferecidos em uma nuvem pública são *disponibilizados à população em geral*.

- *`Private clouds`*

	Os aplicativos e serviços disponibilizados em uma nuvem privada são indicados para entidades ou empresas específicas, como o governo. 

	Uma nuvem privada pode ser configurada usando a rede privada de uma organização, embora isso possa ser caro para construir e manter. Uma nuvem privada também pode ser gerenciada por uma organização externa com segurança de acesso estrita.

- *`Hybrid clouds`*

	Uma nuvem híbrida é composta parte por um nuvem privada, parte por uma nuvem pública, onde em cada parte permanece um objeto separado, mas ambas são conectadas usando uma única arquitetura. 

- *`Community clouds`*

	Uma nuvem comunitária é criada para uso exclusivo de uma comunidade específica. As diferenças entre nuvens públicas e comunitárias são as necessidades funcionais que foram personalizadas para a comunidade. 

	Por exemplo, organizações de saúde devem manter a conformidade com políticas e leis — por exemplo, HIPAA — que exigem confidencialidade e autenticação especial.

---
## Cloud Computing and Virtualization

Os termos “computação em nuvem” e “virtualização” normalmente podem ser usados de forma intercambiável, no entanto, possuem significados diferentes. A virtualização é a base da computação em nuvem. Sem ela, a computação em nuvem, como é mais implantada, não seria possível.

A VMware desenvolveu uma tecnologia de virtualização que permitiu a um sistema operacional servidor suportar um ou mais sistemas operacionais clientes. 

A maioria das tecnologias de virtualização são baseadas, agora, nessa tecnologia. A transformação de servidores dedicados em servidores virtualizados foi adotada e está sendo feita rapidamente em data centers e em redes empresariais.

Virtualizar significa criar uma versão virtual, e não física, de um computador. Um exemplo seria a execução de um "computador Linux" no seu PC com Windows.

Para aproveitar totalmente a virtualização, primeiro é necessário entender um pouco do histórico da tecnologia de servidor. 

Historicamente, os servidores corporativos consistiam em um sistema operacional de servidor, como Windows Server ou Linux Server, instalado em hardware específico. Toda a RAM do servidor, poder de processamento e espaço no disco rígido foram dedicados ao serviço fornecido — por exemplo, web, serviços de e-mail, etc..

O maior problema com essa configuração é que quando um componente falha, o serviço que é fornecido por esse servidor se torna indisponível. Isso é conhecido como um único ponto de falha. 

Outro problema era que os servidores dedicados eram subutilizados. Os servidores dedicados geralmente ficavam ociosos por longos períodos, aguardando até que houvesse uma necessidade do serviço específico que eles forneciam. 

Esses servidores desperdiçavam energia e ocupavam mais espaço do que o garantido pela quantidade de serviço prestado. Isso é conhecido como expansão de servidores.

---
## Advantages of virtualization

Uma das principais vantagens da virtualização é o menor custo geral:

- *É necessário menos equipamento* - A virtualização permite a consolidação do servidor, o que requer menos dispositivos físicos e reduz os custos de manutenção.

- *Menos energia é consumida* - A consolidação de servidores reduz os custos mensais de energia e refrigeração.

- *Menos espaço é necessário* - A consolidação do servidor reduz a quantidade de espaço necessário.

- *Prototipagem mais fácil* - Laboratórios independentes, operando em redes isoladas, podem ser criados rapidamente para testes e implementações de prototipagem de rede.

- *Provisionamento de servidor mais rápido* - Criar um servidor virtual é muito mais rápido do que provisionar um servidor físico.

- *Maior tempo de atividade do servidor* - A maioria das plataformas de virtualização de servidor agora oferece recursos avançados de tolerância a falhas redundantes.

- *Recuperação de desastres aprimorada* - A maioria das plataformas de virtualização de servidores corporativos possui software que pode ajudar a testar e automatizar o failover antes que ocorra um desastre.

- *Suporte legado* - A virtualização pode estender a vida útil dos sistemas operacionais e aplicativos, proporcionando mais tempo para as organizações migrarem para soluções mais recentes.

---
## Hypervisors

O hypervisor é um programa, firmware ou hardware que adiciona uma camada de abstração ao hardware físico. 

A camada de abstração é usada para criar máquinas virtuais que têm acesso a todo o hardware da máquina física, como CPUs, memória, controladores de disco e NICs. 

Cada uma dessas máquinas virtuais executa um sistema operacional completo e separado. Com a virtualização, não é incomum que 100 servidores físicos sejam consolidados como máquinas virtuais sobre 10 servidores físicos que usam hipervisores.

#### Type 1 Hypervisor - “Bare Metal”

Os hypervisors tipo 1, também são chamados de abordagem "bare-metal", pois o hypervisor é instalado diretamente no hardware. Os hypervisors tipo 1 são geralmente usados em servidores corporativos e em dispositivos de rede de data center.

Com ele, o hypervisor é instalado diretamente no servidor ou no hardware de rede. Depois, as instâncias de um SO são instaladas no hypervisor. Os hypervisors tipo 1 têm acesso direto aos recursos de hardware e, portanto, são mais eficientes do que as arquiteturas hospedadas. Os hypervisors tipo 1 melhoram a escalabilidade, o desempenho e a robustez.

#### Type 2 hypervisor - “hosted”

Um hipervisor tipo 2 é um software que cria e executa instâncias VM. O computador, em que um hypervisor oferece suporte a uma ou mais VMs, é um computador host. 

Os hypervisors tipo 2 são também chamados hypervisors hospedados. Isso acontece porque o hypervisor está instalado no topo do SO atual, como Mac OS X, Windows ou Linux. Em seguida, uma ou mais instâncias de SO adicionais são instaladas no topo do hypervisor. 

Uma grande vantagem dos hipervisores tipo 2 é que o software do console de gerenciamento não é necessário.

*Observação*: É importante ter certeza de que a máquina de host seja robusta o suficiente para instalar e executar as VMs para que elas não fiquem sem recursos.