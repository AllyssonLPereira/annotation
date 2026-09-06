---
tags:
  - arquivo
---
Os analistas de segurança cibernética devem identificar os:

- *`Ativos`* — qualquer coisa de valor para uma organização que deve ser protegida, incluindo servidores, dispositivos de infraestrutura, dispositivos finais e o maior ativo, dados.

- *`Vulnerabilidades`* — Uma fraqueza em um sistema ou em seu design que pode ser explorada por um agente de ameaça.

- *`Ameaças`* — Qualquer perigo potencial para um ativo.

---
## Identify assets

Muitas organizações só têm uma ideia geral dos *`assets`* que precisam ser protegidos. A coleta de todos os dispositivos e informações de propriedade ou gerenciadas pela organização são ativos. 

Os *`assets`* constituem a *superfície de ataque que os atores da ameaça podem atingir*. Estes *`assets`* devem ser inventariados e avaliados quanto ao nível de proteção necessário para impedir potenciais ataques.

O gerenciamento de *`assets`* consiste em *inventários de todos os ativos* e, em seguida, *desenvolver políticas* e procedimentos para protegê-los e, então, *implementar essas políticas*. Essa tarefa pode ser assustadora, considerando que muitas organizações precisam proteger usuários e recursos internos, trabalhadores móveis e serviços virtuais e baseados em nuvem.

#### Asset Classification

Uma empresa pode adotar um sistema de rotulagem, de acordo com o valor, a confidencialidade e a importância das informações.

1. Determinar a categoria de identificação de *`assets`* adequada inclui:

	- *`assets`* de informações — dados;
	- *`assets`* de software;
	- *`assets`* físicos;
	- Serviços.

2. Depois de definir em que categoria ao *`assets`* se encontram, podemos estabelecer a responsabilização, identificando o proprietário de todos os *`assets`* de informações e de softwares de aplicativos:

	- Identificar o proprietário de todos os *`assets`* de informações;
	- Identificar o proprietário de todo o software de aplicação.

3. Agora, pode determinar os critérios de classificação:

	- Confidencialidade;
	- Valor;
	- Tempo;
	- Direitos de acesso;
	- Destruição.

4. Por fim, implemente um esquema de classificação:

	- Adotar uma maneira uniforme de identificação.

#### Asset Standardization

*Os padrões do ativo identificam produtos de hardware e software específicos usados e suportados pela empresa*.

Quando há uma falha, a ação imediata ajuda a manter o acesso e a segurança. Se uma empresa não padronizar sua seleção de hardware, provavelmente será difícil o pessoal encontrar um componente de reposição. 

Além de exigirem mais conhecimento para serem gerenciados, ambientes não padronizados aumentam o custo com contratos de manutenção e inventário.

#### Asset lifecycle stages

Para especialistas em segurança digital, parte do trabalho é gerenciar *`assets`* e sistemas relacionados durante todo o ciclo de vida do ativo.

- *Aquisição*:

	A empresa compra os *`assets`* de acordo com as necessidades identificadas nos dados coletados para justificar a compra.

	O ativo é adicionado ao inventário da empresa.

- *Implantação*:

	O ativo é montado e inspecionado para verificar se há falhas ou outros problemas. A equipe realiza testes e instala tags ou códigos de barras para fins de rastreamento.

	O ativo passa do inventário para o em uso.


- *Utilização*:

	Essa é a fase mais longa do ciclo. O desempenho do ativo é verificado continuamente. Atualizações, correções de patches, compras de novas licenças e auditorias de conformidade fazem parte do estágio de utilização.

- *Manutenção*:

	A manutenção ajuda a prolongar a vida produtiva de um ativo. Os funcionários podem modificar ou atualizar o recurso.


- *Eliminação*:

	Ao fim da vida produtiva do ativo, ele deve ser descartado. Todos os dados devem ser apagados do recurso. O descarte pode incluir a desmontagem de um ativo para peças. Quaisquer peças que possam causar riscos ambientais devem ser descartadas de acordo com as diretrizes locais.

---
## Defense in depth


As organizações devem usar uma abordagem de *defesa profunda* para identificar *threats* e proteger *`assets`* vulneráveis. Essa abordagem usa várias camadas de segurança na borda da rede, na rede e nos pontos de extremidade da rede.


- *Roteador de borda*:

	A primeira linha de defesa é conhecida como um roteador de borda. O roteador de borda tem um conjunto de regras especificando qual tráfego ele permite ou nega. Ele passa todas as conexões que se destinam à LAN interna para o firewall.

---
#### What Is Network Edge?

A borda da rede é a conexão ou interface entre um dispositivo ou rede local e a internet. A borda está próxima dos dispositivos com os quais se comunica e é o ponto de entrada da rede. A borda da rede é um limite de segurança crucial para o qual os administradores de rede devem fornecer soluções.

Dispositivos de Internet das Coisas (IoT) e infraestrutura de computadores se beneficiam de estar o mais próximo possível da fonte de dados, pois isso aumenta a taxa de transferência, o que, por sua vez, facilita uma operação mais eficiente e eficaz. 

A ameaça à segurança cibernética para dispositivos na fronteira de uma rede interconectada está crescendo à medida que criminosos cibernéticos criam novas maneiras de explorar vulnerabilidades em redes, aplicativos e dispositivos emergentes e pouco protegidos.

#### What is the difference between network edge and network core?

*A borda da rede refere-se aos endpoints*. É o primeiro passo entre os endpoints e o núcleo da rede. Isso inclui computadores pessoais (PCs), adaptadores, modems e os dispositivos que se conectam a eles. 

O núcleo da rede refere-se aos componentes que fornecem serviços para aqueles na borda. Isso inclui instalações que geralmente estão dentro de data centers, como servidores, e aquelas dentro da camada de enlace de dados.

###### IoT edge networks

Dispositivos de IoT permitem que dados sejam coletados e processados na borda externa de uma rede, pois interagem com pessoas, o ambiente, tarefas e outros dispositivos que coletam e transmitem dados para o núcleo. 

Uma infraestrutura de borda de IoT envolve a rede que transmite informações, como uma rede 4G ou 5G, o dispositivo de IoT e os modems e roteadores que transportam o sinal do dispositivo em direção ao núcleo da rede.

Cada dispositivo de IoT apresenta um potencial para vulnerabilidades de segurança únicas, portanto, o surgimento de dispositivos de IoT traz consigo uma necessidade crescente de medidas de segurança de borda mais rigorosas.

#### What Is Edge Computing And How Does It Differ From Network Edge?

A computação de borda envolve o processamento de dados em tempo real próximo à fonte dos dados. Isso é diferente da borda da rede, pois, embora possa ser um componente da borda, não inclui os outros dispositivos usados para transmitir dados da borda externa para o núcleo.

No entanto, com a computação de borda, você pode obter tempos de resposta aprimorados e economia de custos. O dispositivo de computação de borda, por estar mais próximo da fonte de dados, possibilita transmissões mais rápidas. 

Também pode reduzir os gastos relacionados à configuração e manutenção de dispositivos principais, pois grande parte da carga de trabalho computacional é gerenciada pelo dispositivo de computação de borda.

###### Edge devices

Um dispositivo de borda serve como ponto de entrada para o núcleo da rede de uma organização ou provedor de serviços. Inclui roteadores, switches, redes de longa distância (WANs), firewalls e dispositivos de acesso integrado (IADs).

###### Router

Um roteador transmite pacotes de dados entre duas redes diferentes. Esse tráfego inclui o conteúdo de sites, bem como comunicações como bate-papo por vídeo, e-mail e transmissões de Voz sobre Protocolo de Internet (VoIP). 

Os roteadores direcionam o tráfego na internet, enviando-o de um ponto a outro, permitindo que diferentes dispositivos de borda se comuniquem entre si.

###### Switch

Um switch de rede conecta dispositivos dentro de uma rede de computadores por meio de comutação de pacotes, que recebe dados e os encaminha para o dispositivo ao qual se destinam. Um switch permite que dispositivos de borda interajam e compartilhem recursos sem usar dispositivos no núcleo.

###### Wide-area network

Uma WAN consiste em redes locais (LANs) que se conectam entre si. Dessa forma, a borda da WAN conecta as bordas das LANs. Por exemplo, uma organização pode conectar três escritórios, cada um com sua própria LAN, usando uma WAN ou uma WAN definida por software (SD-WAN).

###### Firewall

Um firewall controla os dados que podem entrar e sair de uma infraestrutura de rede de acordo com regras predefinidas. 

Os firewalls inspecionam os pacotes de dados, procurando por qualquer coisa que levante suspeita e, em seguida, descartam quaisquer pacotes que contenham ameaças potenciais. Os firewalls são a principal linha de defesa na borda da rede, impedindo a entrada ou saída de ameaças.

###### Integrated access device

Um IAD converte diferentes tipos de entrada de dados e os renderiza em um formato comum. Por exemplo, um IAD é usado para converter sinais telefônicos analógicos e digitais em um sinal digital comum. Os IADs ajudam a simplificar as comunicações e permitem transmissões mais eficientes na borda.

![[network_edge.png]]

Os roteadores e firewalls não são os únicos dispositivos que são usados em uma abordagem de defesa profunda. Outros dispositivos de segurança incluem *IPS* — Intrusion Prevention Systems, *Proteção Avançada contra Malware* — AMP, WAF, IAM, NAC e muito mais.

*Na abordagem de segurança em camadas de defesa profunda, as diferentes camadas trabalham juntas para criar uma arquitetura de segurança na qual a falha de uma salvaguarda não afeta a eficácia das outras salvaguardas*.

---
## Defense in Depth Strategies


Se uma empresa tem apenas uma medida de segurança para proteger dados e informações, os criminosos digitais precisam passar por uma única defesa para roubar informações ou causar outros danos. 

Para garantir que as informações e os dados permaneçam disponíveis, uma empresa precisa criar diferentes camadas de proteção.


- *Sobreposição*:

	Um bom exemplo de camadas é uma empresa que armazena seus documentos ultra-secretos em um servidor protegido por senha em um prédio trancado e cercado por uma cerca elétrica.

	Uma abordagem em camadas oferece a proteção mais abrangente porque, mesmo que os criminosos cibernéticos penetrem em uma camada, eles ainda precisam enfrentar várias outras defesas. *Idealmente, cada camada deve ser mais complicada de superar*!

	A defesa em profundidade não fornecerá um escudo cibernético impenetrável, mas ajudará a empresa a minimizar riscos, mantendo-se um passo à frente dos criminosos virtuais.


- *Limitação*:

	Limitar o acesso aos dados e às informações reduz a possibilidade de uma ameaça. Uma empresa deve restringir o acesso para que os usuários tenham apenas o nível de acesso necessário para fazer o seu trabalho.

	Uma empresa deve ter as ferramentas e as configurações certas, como permissões de arquivo, para limitar o acesso, bem como as medidas processuais certas, que definem etapas específicas para fazer qualquer coisa que possa afetar a segurança. 


- *Diversidade*:

	Se todas as camadas protegidas fossem as mesmas, não seria muito difícil, para os criminosos virtuais, realizar um ataque bem-sucedido. 

	As camadas devem ser diferentes para que, se uma camada for penetrada, a mesma técnica não funcionará em todas as outras, o que comprometeria todo o sistema. 

	Uma empresa pode usar diferentes algoritmos de criptografia ou sistemas de autenticação para proteger os dados em diferentes estados.

	Para atingir o objetivo de diversidade nas defesas, as empresas podem usar produtos de segurança de diferentes empresas como diferentes fatores de autenticação, como um cartão de furto de uma empresa e um leitor de impressão digital fabricado por uma empresa diferente.

	Assim também, podem ter medidas de segurança variadas, como bloqueio de tempo nos armários e supervisão por um membro da equipe de segurança ao desbloqueá-lo.


- *Ofuscação*:

	A ofuscação de informações também pode proteger dados e informações. Uma empresa não deve revelar informações que os criminosos virtuais podem usar para descobrir a versão do sistema operacional em execução em um servidor ou o tipo de equipamento que ele usa.

	Por exemplo, as mensagens de erro não devem conter nenhum detalhe que os criminosos virtuais possam usar para determinar as vulnerabilidades que estão presentes. Ocultar certos tipos de informação dificulta ataques de criminosos virtuais a um sistema.


- *Simplicidade*:

	A complexidade não garante, necessariamente, a segurança. Se uma empresa implementar sistemas complexos que são difíceis de entender e de solucionar problemas, o “tiro pode sair pela culatra”. 

	Se os funcionários não entenderem como configurar uma solução complexa corretamente, pode ser tão fácil quando em uma solução mais simples para os criminosos virtuais comprometerem esses sistemas.

	*Para manter a disponibilidade, uma solução de segurança deve ser simples, do ponto de vista de dentro da empresa, mas complexa do ponto de vista externo*.

