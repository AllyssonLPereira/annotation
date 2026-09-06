---
tags:
  - arquivo
---
## Introduction

Embora os profissionais de segurança se esforcem para proteger os sistemas de ataques maliciosos ou descuido humano, nevitavelmente, as coisas dão errado. Por esse motivo, os profissionais de segurança também desempenham o papel de socorristas. Uma compreensão da resposta a incidentes começa com o conhecimento dos termos usados para descrever diversos ataques cibernéticos.

#### Breach

Perda de controle, comprometimento, divulgação não autorizada, aquisição não autorizada ou qualquer ocorrência semelhante em que: uma pessoa que não seja um usuário autorizado acesse ou potencialmente acesse informações pessoalmente identificáveis; ou um usuário autorizado acesse informações pessoalmente identificáveis para uma finalidade diferente da autorizada. *NIST SP 800-53 Rev. 5*.

#### Event

Qualquer ocorrência observável em uma rede ou sistema. NIST SP 800-61 Rev 2.

#### Exploit

Um ataque específico. É chamado assim porque esses ataques exploram vulnerabilidades do sistema.

#### Incident

Um evento que real ou potencialmente coloca em risco a confidencialidade, integridade ou disponibilidade de um sistema de informação ou das informações que o sistema processa, armazena ou transmite.

#### Intrusion

Um evento de segurança, ou combinação de eventos, que constitui um incidente de segurança deliberado no qual um intruso obtém, ou tenta obter, acesso a um sistema ou recurso do sistema sem autorização. IETF RFC 4949 Ver 2.

#### Threat

Qualquer circunstância ou evento com o potencial de impactar negativamente as operações organizacionais (incluindo missão, funções, imagem ou reputação), ativos organizacionais, indivíduos, outras organizações ou a nação por meio de um sistema de informação devido um acesso não autorizado, destruição, divulgação, modificação de informações e/ ou negação de serviço. NIST SP 800-30 Rev 1.

#### Vulnerability

Fraqueza em um sistema de informação, procedimentos de segurança do sistema, controles internos ou implementação que podem ser explorados por uma fonte de ameaça. NIST SP 800-30 Rev 1.

#### Zero day

Uma vulnerabilidade de sistema previamente desconhecida com potencial de exploração sem risco de detecção ou prevenção porque em geral, não se enquadra em padrões, assinaturas ou métodos reconhecidos.

---
## The Goal of Incident Response

*Toda organização deve estar preparada para incidentes*. Apesar dos melhores esforços das equipes de gestão e segurança de uma organização para evitar ou prevenir problemas, é inevitável que eventos adversos ocorram com o potencial de afetar a missão ou os objetivos da empresa.

A prioridade de qualquer resposta a incidentes é proteger a *vida, a saúde e a segurança*. Ao tomar qualquer decisão relacionada a prioridades, sempre priorize a segurança.

*O principal objetivo da gestão de incidentes é estar preparado*. A preparação requer uma política e um plano de resposta que conduzam a organização durante a crise. Algumas organizações usam o termo "gestão de crise" para descrever esse processo.

Um evento é qualquer ocorrência mensurável, e a maioria dos eventos é inofensiva. No entanto, se o evento tiver o potencial de interromper a missão da empresa, ele é chamado de incidente. *Toda organização deve ter um plano de resposta a incidentes que ajude a preservar a viabilidade e a sobrevivência do negócio*.

O processo de resposta a incidentes visa reduzir o impacto de um incidente para que a organização possa retomar as operações interrompidas o mais rápido possível. O planejamento de resposta a incidentes é um subconjunto da disciplina maior de `business continuity management — BCM`.

---
## Components of the Incident Response Plan

A política de resposta a incidentes deve fazer referência a um plano de resposta a incidentes que todos os funcionários seguirão, dependendo de sua função no processo. O plano pode conter diversos procedimentos e padrões relacionados à resposta a incidentes. É uma representação viva da política de resposta a incidentes de uma organização.

A visão, a estratégia e a missão da organização devem moldar o processo de resposta a incidentes. Os procedimentos para implementar o plano devem definir os processos técnicos, técnicas, listas de verificação e outras ferramentas que as equipes utilizarão ao responder a um incidente.

![[components_of_the_incident_response_plan.png]]

#### Preparation

- Desenvolver uma política aprovada pela gerência;
- Identificar dados e sistemas críticos e quaisquer pontos únicos de falha;
- Treinar a equipe em resposta a incidentes;
- Implementar uma equipe de resposta a incidentes;
- Praticar a Identificação de Incidentes — primeira resposta;
- Identificar funções e responsabilidades;
- Planejar a coordenação da comunicação entre as partes interessadas;
- Considerar a possibilidade de que um método primário de comunicação possa não estar disponível.

#### Detection & Analysis

- Monitore todos os vetores de ataque possíveis;
- Analise o incidente usando dados conhecidos e inteligência de ameaças;
- Priorize a resposta a incidentes;
- Padronize a documentação do incidente.

#### Containment

- Reúna evidências;
- Escolha uma estratégia de contenção apropriada;
- Identifique o agressor;
- Isole o ataque.

#### Post-Incident Activity

- Identificar evidências que possam precisar ser retidas;
- Documentar as lições aprendidas.
- Realizar uma retrospectiva de:

	- Preparação;
	- Detecção e Análise;
	- Contenção, Erradicação e Recuperação;
	- Atividade Pós-incidente.


Então, a primeira parte da preparação é identificar as informações críticas que precisam de proteção e evitar qualquer ponto único de falha. Isso significa que, se temos algo particularmente importante, mas está protegido por apenas uma porta, criamos várias camadas de proteção para reduzir a probabilidade de um ataque bem-sucedido.

Falaremos mais adiante sobre o princípio da defesa em profundidade, mas como uma fortaleza. Quanto mais camadas de defesa tivermos, mais difícil será para os invasores que tentarem invadir.

É importante treinar a equipe em resposta a incidentes para que todos saibam o que fazer. O treinamento pode incluir simulações e cenários. Assim, as equipes podem praticar sua resposta e aprender a coordenar a comunicação entre os diferentes stakeholders da organização, que incluem colegas, superiores, proprietários das informações e clientes.

Precisamos considerar quais tipos de comunicação estarão disponíveis, pois não podemos comunicar as mesmas informações para todos. Alguns materiais serão confidenciais e outros serão úteis apenas para determinadas pessoas e não para a imprensa ou indivíduos externos.

Quando se trata de detecção e análise, precisamos monitorar os vetores de ataque, como o ataque foi realizado e qual tecnologia foi utilizada.

É importante padronizar a documentação de incidentes porque, em um grupo de pessoas, cada uma terá sua própria ideia de como registrar atividades e procedimentos para a consistência da organização e nossa responsabilidade com os proprietários dos dados. Precisamos ter uma resposta padronizada a incidentes, onde cada pessoa saiba exatamente o que precisa ser feito.

E em que sequência? Isso facilita a priorização da resposta, pois cada pessoa tem suas próprias tarefas e sabe como cuidar de suas próprias responsabilidades, comunicando-se adequadamente com os demais envolvidos.

Em seguida, precisamos encontrar a estratégia de contenção apropriada, identificar os invasores e como eles penetraram em nossas defesas e isolar o ataque, garantindo que ele não avance nem cause danos adicionais após o incidente.

Identificamos evidências que podem precisar ser retidas. Em seguida, frequentemente, há uma auditoria interna do ocorrido.

Uma investigação externa também pode ser necessária, especialmente em grandes ataques cibernéticos envolvendo a aplicação da lei. As lições aprendidas devem ser documentadas. Talvez se descubra que respondemos melhor do que em um ataque anterior, mas ainda precisamos aprimorar a preparação ou a análise de detecção.

Frequentemente, essas atividades pós-incidente estão sujeitas a requisitos regulatórios e determinada documentação deve ser apresentada. Isso é especialmente importante se o sistema estiver comprometido.

---
## Incident Response Team

Uma equipe de resposta a incidentes devidamente formada e treinada pode ser eficiente, dedicada ou uma combinação dos dois, dependendo
dos requisitos da organização.

Muitos profissionais de TI são classificados como socorristas em incidentes. Eles são os primeiros a chegar ao local e sabem diferenciar problemas típicos de TI de incidentes de segurança.

Eles são semelhantes aos socorristas médicos, que possuem as habilidades e o conhecimento para prestar assistência médica em locais de acidentes e ajudar a levar os pacientes às instalações médicas quando necessário. Os socorristas médicos têm treinamento específico para ajudá-los a distinguir entre ferimentos leves e graves. Além disso, eles sabem o que fazer quando se deparam com um ferimento grave.

Da mesma forma, os profissionais de TI precisam de treinamento específico para distinguir entre um problema típico que precisa ser solucionado e um incidente de segurança que precisam ser relatados e abordados em um nível superior.

Uma equipe de resposta a incidentes típica é um grupo multifuncional de indivíduos que representam as áreas de responsabilidade gerencial, técnica e funcional mais diretamente impactadas por um incidente de segurança.

Possíveis membros da equipe incluem:

- Representante(s) da alta gerência;
- Profissionais de segurança da informação;
- Representantes legais;
- Representantes de relações públicas/comunicações;
- Representantes de engenharia (sistema e rede).

Os membros da equipe devem receber treinamento sobre resposta a incidentes e sobre o plano de resposta a incidentes da organização. 

Normalmente, os membros da equipe auxiliam na investigação do incidente, na avaliação dos danos, na coleta de evidências, no relato do incidente e no início dos procedimentos de recuperação. Eles também participam das etapas de remediação e lições aprendidas, além de auxiliar na análise da causa raiz.

Muitas organizações agora têm uma equipe dedicada responsável por investigar quaisquer incidentes de segurança de computadores que ocorram. Essas equipes são comumente conhecidas como equipes de resposta a incidentes de computadores (CIRTs) ou equipes de resposta a incidentes de segurança de computadores (CSIRTs).

Quando ocorre um incidente, a equipe de resposta tem quatro responsabilidades principais:

- Determinar a quantidade e o escopo dos danos causados pelo incidente;

- Determinar se alguma informação confidencial foi comprometida durante o incidente;

- Implementar os procedimentos de recuperação necessários para restaurar a segurança e se recuperar dos danos relacionados ao incidente;

- Supervisionar a implementação de quaisquer medidas de segurança adicionais necessárias para melhorar a segurança e evitar a recorrência do incidente.