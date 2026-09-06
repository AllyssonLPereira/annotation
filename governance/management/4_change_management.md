---
tags:
  - arquivo
---
Você precisa garantir um processo robusto de gerenciamento de mudanças e testar em ambientes modelos antes de fazer qualquer alteração em um ambiente de produção.

Mesmo com planejamento e testes extensivos, às vezes, há consequências indesejadas. Portanto, você deve garantir que haja um *plano de reversão*. Uma reversão consiste em restaurar o sistema ao estado em que se encontrava antes da alteração, a ponto de sabermos que estava funcionando corretamente.

Antes de introduzirmos alterações no ambiente, precisamos garantir que revisamos e testamos todos os patches e que podemos restaurar a configuração anterior.

Manter um ambiente de teste separado pode ser um desafio logístico para muitas organizações. Muitas não possuem ambientes de produção e teste separados para verificar adequadamente todos os patches e atualizações do sistema. 

Nesse caso, elas podem contar com testes de terceiros do fornecedor para certificar um novo software lançado com base em um conjunto genérico de dados.

> *O plano de reversão é importante em todos os ambientes, mas é absolutamente crítico para aqueles que não conseguem testar completamente uma alteração.*

---
## Change Management Components in the Workplace

A gestão de mudanças ocorre em um ciclo. Não há um ponto de parada real, ela é contínua. Isso significa que deve haver monitoramento contínuo desse ambiente.

Portanto, se você ou qualquer pessoa solicitar uma mudança, ela precisa passar pelas aprovações apropriadas e a organização deve estar preparada para reversão, se necessário.

Ou seja, se uma mudança específica não funcionar, precisamos ser capazes de reverter para o sistema legado.

Embora a gestão de mudanças seja um processo que abrange toda a organização, frequentemente cabe aos profissionais de segurança da informação coordenar o esforço e, talvez, fornecer supervisão e governança, dependendo do tamanho da organização.

Também pode se enquadrar em uma área de TI ou desenvolvimento em organizações que possuem um departamento de qualidade ou gestão de riscos. Também seria uma ótima opção para qualquer uma dessas áreas. 

O tema comum é que a gestão de mudanças reconhece e incorpora as contribuições dos usuários finais, bem como de todas as áreas de TI: desenvolvimento, segurança da informação e, principalmente, gestão, para garantir que todas as mudanças sejam devidamente testadas, aprovadas e comunicadas antes de serem implementadas.

---
## Change Management Components

O processo de gestão de mudanças inclui os seguintes componentes:

- *Documentation*:

	Todas as principais práticas de gestão de mudanças abordam um conjunto comum de atividades principais que começam com uma solicitação de mudança — RFC — e passam por vários estágios de desenvolvimento e teste até que a mudança seja liberada para os usuários finais. 

	Do primeiro ao último, cada etapa está sujeita a alguma forma de gerenciamento e tomada de decisão formalizados; cada etapa produz lançamentos contábeis ou de log para documentar seus resultados.

- *Approval*:

	Esses processos normalmente incluem: avaliar a integralidade das RFCs, atribuir ao processo de autorização de mudança adequado com base em práticas organizacionais e de risco, revisões das partes interessadas, identificação e alocação de recursos, aprovações ou rejeições apropriadas e documentação da aprovação ou rejeição.

- *Rollback*:

	Dependendo da natureza da mudança, uma variedade de atividades pode precisar ser concluída. 

	Geralmente, elas incluem: agendar a mudança, testar a mudança, verificar os procedimentos de reversão, implementar a mudança, avaliar a mudança para uma operação adequada e eficaz e documentar a mudança no ambiente de produção.

	A autoridade de reversão geralmente seria definida no plano de reversão, que pode ser imediato ou agendado como uma mudança subsequente se o monitoramento da mudança sugerir desempenho inadequado.