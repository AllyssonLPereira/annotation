---
tags:
  - arquivo
---
## Physical Access Controls

Controles de acesso físico são barreiras reais implantadas para evitar o contato direto com os sistemas. A meta é *prevenir que usuários não autorizados acessem fisicamente as instalações, equipamentos e outros ativos organizacionais.

Por exemplo, o controle de acesso físico determina *quem* pode entrar, *onde* podem entrar ou *quando* podem entrar.

---
## Logical Access Controls

Controles de acesso lógico são as soluções de hardware e software usadas para gerenciar o acesso aos recursos e sistemas. 

Essas soluções baseadas em tecnologia incluem ferramentas e protocolos que os sistemas de computador utilizam para identificação, autenticação, autorização e contabilização.

---
## Administrative Access Controls

Os controles de acesso administrativo são as políticas e procedimentos definidos pelas empresas para implementar e aplicar todos os aspectos de controle de acesso.

Os controles administrativos se concentram nas seguintes práticas de pessoal e negócios.

- *Políticas* são ideias ou ações aprovadas que orientam o comportamento.

- *Procedimentos* são as etapas detalhadas necessárias para realizar uma atividade.

- As *práticas de contratação* definem as etapas que uma organização adota para encontrar funcionários qualificados.

- As *verificações de antecedentes* são um tipo de triagem de funcionários que inclui a verificação de empregos anteriores, histórico de crédito e histórico criminal.

- A *classificação de dados* categoriza os dados com base em sua sensibilidade.

- O *treinamento de segurança* educa os funcionários sobre as políticas de segurança em uma organização.

- As *revisões* avaliam o desempenho no trabalho de um funcionário.

- ##### Authentication, authorization and accounting — *AAA*

	O conceito de controles de acesso administrativo envolve três serviços de segurança: autenticação, autorização e contabilidade — *AAA*.

	Esses serviços fornecem a estrutura principal para controlar o acesso, impedindo o acesso não autorizado a um computador, rede, banco de dados ou outro recurso de dados.

---
## Privileged Access Management

O gerenciamento de acesso privilegiado fornece o primeiro e talvez o mais familiar caso de uso. Considere uma identidade de usuário humano que recebe vários privilégios de criação, leitura, atualização e exclusão em um banco de dados.

Sem o gerenciamento de acesso privilegiado, o controle de acesso do sistema teria esses privilégios atribuídos ao usuário administrativo de forma estática, efetivamente "ativos" 24 horas por dia, todos os dias.

A segurança dependeria do processo de login para evitar o uso indevido dessa identidade. O gerenciamento de acesso privilegiado *`just-in-time`*, por outro lado, inclui subconjuntos de privilégios específicos baseados em funções que só se tornam ativos em tempo real quando a identidade solicita o uso de um recurso ou serviço.

> Este cenário ilustra a importância do gerenciamento de acesso privilegiado: 
> 
> *"A ABC, Inc. possui um pequeno departamento de TI responsável pelo provisionamento de usuários e pela administração de sistemas. 
> 
> Para economizar tempo, os funcionários do departamento de TI adicionaram seus IDs ao grupo Administradores de Domínio, efetivamente concedendo-lhes acesso a tudo dentro do ambiente de servidor e estação de trabalho Windows. 
> 
> Ao analisar uma fatura recebida por e-mail, eles abriram um e-mail com um anexo malicioso que iniciou um ataque de ransomware.
> 
> Como eles usam privilégios de Administrador de Domínio, o ransomware conseguiu criptografar todos os arquivos em todos os servidores e estações de trabalho. 
> 
> Uma solução de gerenciamento de acesso privilegiado poderia limitar os danos causados por esse ransomware se os privilégios de administrador fossem usados apenas ao executar uma função que exija esse nível de acesso. 
> 
> Operações de rotina, como tarefas diárias de e-mail, são realizadas sem um nível de acesso mais alto."*

#### Measures for privileged accounts

Medidas típicas utilizadas para moderar o potencial de riscos elevados decorrentes do uso indevido ou abuso de contas privilegiadas incluem o seguinte:

- *Registros mais extensos e detalhados do que contas de usuários comuns*. 

	O registro de ações privilegiadas é de vital importância tanto como um *impedimento* — para titulares de contas privilegiadas que possam ser tentados a se envolver em atividades indesejáveis — quanto como um *controle administrativo* — os registros podem ser auditados e revisados para detectar e responder a atividades maliciosas.

- *Controle de acesso mais rigoroso do que contas de usuários comuns*. 

	Mesmo usuários sem privilégios devem ser obrigados a usar métodos de MFA para obter acesso aos sistemas e redes organizacionais. 

	Usuários privilegiados — ou, mais precisamente, usuários altamente confiáveis com acesso a contas privilegiadas — devem ser obrigados a passar por uma autenticação adicional ou mais rigorosa antes de obter esses privilégios. 

	A identidade *just-in-time* também deve ser considerada uma forma de restringir o uso desses privilégios a tarefas específicas e aos horários em que o usuário as executa.

- *Verificação de confiança mais profunda do que em contas de usuários comuns*. 

	Titulares de contas privilegiadas devem estar sujeitos a verificações de antecedentes mais detalhadas, acordos de confidencialidade mais rigorosos e políticas de uso aceitável, além de estarem dispostos a serem submetidos a investigações financeiras. 

	Atualizações periódicas ou acionadas por eventos dessas verificações de antecedentes também podem ser necessárias, dependendo da natureza das atividades da organização e dos riscos que ela enfrenta.

- *Mais auditoria do que em contas de usuários comuns*. 

	A atividade de contas privilegiadas deve ser monitorada e auditada em uma frequência e extensão maiores do que o uso regular.

#### Least Privilege

Para preservar a confidencialidade das informações e garantir que elas estejam disponíveis apenas para pessoas autorizadas a visualizá-las, utilizamos o *`privileged access management`*, que se baseia no princípio do *`least privilege`*.

Isso significa que *cada usuário tem acesso apenas aos itens de que necessita e nada mais*. Por exemplo, apenas pessoas que trabalham com faturamento terão permissão para visualizar dados financeiros de consumidores, e um número ainda menor de pessoas terá autoridade para alterar ou excluir esses dados.

Isso mantém a confidencialidade e a integridade, ao mesmo tempo em que permite a disponibilidade, fornecendo acesso administrativo com uma senha ou login apropriado que comprove que o usuário possui as permissões necessárias para acessar esses dados.

Às vezes, é necessário permitir que os usuários acessem as informações por meio de um *acesso temporário/limitado*, por exemplo, por um período específico ou apenas dentro do horário comercial normal. Ou as regras de acesso podem limitar os campos aos quais os indivíduos podem ter acesso.

Um exemplo é um ambiente de saúde. Alguns profissionais podem ter acesso aos dados dos pacientes, mas não aos seus dados médicos. Médicos individuais podem ter acesso apenas aos dados relacionados aos seus próprios pacientes. Em alguns casos, isso é regulamentado por lei, como a HIPAA nos Estados Unidos e por leis de privacidade específicas em outros países.

Os sistemas frequentemente monitoram o acesso a informações privadas e, se os registros indicarem que alguém tentou acessar um banco de dados sem as devidas permissões, isso acionará automaticamente um alarme.

O administrador de segurança registrará o incidente e alertará as pessoas apropriadas para que tomem as medidas necessárias. Quanto mais informações críticas uma pessoa tiver acesso, maior deverá ser a segurança em torno desse acesso. Elas devem, definitivamente, ter autenticação multifator, por exemplo.

#### Mandatory Access Control in the Workplace

O *`Mandatory Access Control`* é determinado pelo proprietário dos ativos, *de forma abrangente*, com pouca tomada de decisão individual sobre quem obtém acesso.

Por exemplo, em certas agências governamentais, os funcionários precisam ter um determinado tipo de autorização de segurança para acessar determinadas áreas. Em geral, esse *nível de acesso é definido por políticas* governamentais e não por um indivíduo que concede permissão com base em seu próprio julgamento.

Frequentemente, isso é acompanhado pela separação de funções, em que o escopo do trabalho é limitado e os usuários não têm acesso a informações que não lhes dizem respeito. Essa separação de funções também é facilitada pelo *`Role-Based Access Control`*.

Um *`Mandatory Access Control`* é aplicada uniformemente a todos os sujeitos e objetos dentro dos limites de um sistema de informação.

Em termos mais simples, isso significa que apenas administradores de segurança devidamente designados, como sujeitos confiáveis, podem modificar quaisquer regras de segurança estabelecidas para sujeitos e objetos dentro do sistema.

Isso também significa que, para todos os sujeitos definidos pela organização — ou seja, conhecidos por seu sistema integrado de gerenciamento de identidade e controle de acesso, a organização atribui um subconjunto de privilégios totais para um subconjunto de objetos, de forma que o sujeito seja impedido de realizar qualquer uma das seguintes ações:

- Passar informações para sujeitos ou objetos não autorizados;
- Conceder seus privilégios a outros sujeitos;
- Alterar um ou mais atributos de segurança em sujeitos, objetos, no sistema de informação ou em componentes do sistema;
- Escolher os atributos de segurança a serem associados a objetos recém-criados ou modificados;
- Alterar as regras que regem o controle de acesso.

Embora o MAC soe muito semelhante ao DAC, a principal diferença é quem pode controlar o acesso.

Com o *`Mandatory Access Control`*, é obrigatório que os administradores de segurança atribuam direitos ou permissões de acesso; já com o *`Discretionary Access Control`*, fica a critério do proprietário do objeto.

Controles preventivos
Os controles de segurança preventiva impedem que atividades indesejadas e não autorizadas ocorram e / ou aplicam restrições a usuários autorizados.

Por exemplo, atribuir privilégios de usuário específico em um sistema é um controle preventivo, pois coloca limites para impedir que determinados usuários acessem e executem ações não autorizadas. Um firewall que bloqueia o acesso a uma porta ou um serviço que criminosos virtuais podem explorar também é um controle preventivo.

---
## Functional safety controls

#### Controles dissuasivos

Um impedimento tem como objetivo desencorajar que algo aconteça. Os profissionais e empresas de segurança digital usam as dissuasões para limitar ou mitigar uma ação ou comportamento, mas as dissuasões não os impedem.

As dissuasões de controle de acesso desencorajam os criminosos virtuais a obter acesso não autorizado aos sistemas de informações e dados confidenciais. Eles podem ser eficazes para desencorajar muitos tipos diferentes de ataques a sistemas, além de roubo de dados e disseminação de códigos mal-intencionados.

#### Controles de detecção

As detecções de controle de acesso identificam diferentes tipos de atividade não autorizada. Os controles de detetive não são uma medida preventiva e, em vez disso, concentram-se na descoberta de uma violação de segurança depois que ela ocorre.

Todos os sistemas de detetive têm várias coisas em comum. Eles buscam atividades incomuns ou proibidas e podem ser muito simples, como um detector de movimento ou agente de segurança, ou complexos, como um sistema de detecção de invasão. Também fornecem métodos para gravar ou alertar os operadores do sistema sobre um possível acesso não autorizado.

#### Controles corretivos

Os controles corretivos restauram o sistema ao estado de confidencialidade, integridade e disponibilidade. Eles também podem restaurar os sistemas ao estado normal, após ocorrer atividade não autorizada.

As empresas implementam controles de acesso corretivos após o sistema passar por uma ameaça. Sistemas de detecção de invasão, portas de segurança (mantraps), planejamento de negócios contínuo, antivírus, alarmes e políticas de segurança são exemplos de controles de acesso por correção.

#### Controles de recuperação

Os controles de acesso de recuperação restauram os recursos, funções e capacidades após uma violação de uma política de segurança. Os controles de recuperação podem reparar danos, além de deter qualquer dano adicional. Esses controles têm mais recursos avançados em controles de acesso corretivos.

Operações de backup e restauração, sistemas de acionamento de tolerância a falhas, clusters de servidores, cópias de sombra de banco de dados e software antivírus são exemplos de controles de acesso por recuperação.

#### Controles de compensação

Os controles de acesso compensatórios fornecem opções a outros controles para aumentar o reforço relacionado à sustentação de uma política de segurança.

Um controle compensatório também pode substituir um controle que não pode ser usado devido às circunstâncias. Por exemplo, se uma empresa não pode ter um cão de guarda, em vez disso, ela implementa um detector de movimento com um holofote e um som de latidos.

Exemplos de controles de segurança compensatórios incluem políticas de segurança, supervisão de pessoal, monitoramento e procedimentos de tarefas de trabalho que são usados na ausência do controle ideal que uma empresa teria implantado.


