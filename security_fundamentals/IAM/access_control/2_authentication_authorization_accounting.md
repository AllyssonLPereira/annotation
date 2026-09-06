---
tags:
  - arquivo
---
## What Is Authentication, Authorization, And Accounting — *AAA*?

Autenticação, Autorização e Contabilidade — *AAA* — é uma estrutura de segurança que controla o acesso aos recursos do computador, aplica políticas e audita o uso. 

A *AAA* e seus processos combinados desempenham um papel importante no gerenciamento de redes e na segurança cibernética, rastreando usuários e monitorando suas atividades enquanto estão conectados, alinhando-se aos princípios da tríade CIA para garantir a segurança dos dados.

---
## Authentication

A autenticação envolve o *fornecimento de informações sobre a identidade do usuário*. Os usuários apresentam credenciais de login que confirmam que são quem afirmam ser. 

Como uma ferramenta de gerenciamento de identidade e acesso — *Identity and Access Management (IAM)*, um servidor *AAA* compara as credenciais de um usuário com seu banco de dados de credenciais armazenadas, verificando se o nome de usuário, a senha e outras ferramentas de autenticação correspondem àquele usuário específico.

Os três tipos de autenticação incluem algo que você sabe, como uma senha; algo que você possui — como uma chave USB; e algo que você é, como sua impressão digital ou outros dados biométricos.

#### Authentication Management

O gerenciamento de autenticação tem como objetivo garantir a entrada segura, proporcionando facilidade de uso.

- Uma *`single sign-on solution`* — *`SSO`* — permite que o usuário use um conjunto de credenciais de login para autenticar em vários aplicativos. Dessa forma, o usuário só precisa lembrar uma senha forte. 

- *`OAuth`* é um padrão que permite que as informações da conta de um usuário sejam usadas por serviços de terceiros, como o Facebook ou o Google.  

- Um *`password vault`* pode proteger e armazenar as credenciais do usuário com uma única senha forte necessária para acessá-las.

- Muitas empresas implementam a *`knowledge-based authentication`* — *`KBA`* — para fornecer uma redefinição de senha caso um usuário esqueça sua senha. A KBA é baseada em informações pessoais conhecidas pelo usuário ou em uma série de perguntas.

#### Hash-based Message Authentication Code — HMAC

O *`Hash-based Message Authentication Code`* usa uma chave de criptografia com uma função de hash para autenticar um usuário da Web. Muitos serviços da Web usam a autenticação básica, que não criptografa o nome de usuário e a senha durante a transmissão. 

Usando o *`HMAC`*, o usuário envia um identificador com chave privada e um *`HMAC`*. O servidor procura a chave privada do usuário e cria um *`HMAC`*. O *`HMAC`* do usuário deve ser compatível com o calculado pelo servidor.

As VPNs que usam *`IPsec`* contam com as funções *`HMAC`* para autenticar a origem de cada pacote e fornecer a verificação de integridade de dados.

---
## Authorization

A autorização segue a autenticação. Durante a autorização, um usuário pode receber privilégios para acessar determinadas áreas de uma rede ou sistema. As áreas e os conjuntos de permissões concedidos a um usuário são armazenados em um banco de dados, juntamente com a identidade do usuário. 

Os privilégios do usuário podem ser alterados por um administrador. A autorização difere da autenticação, pois a autenticação verifica apenas a identidade do usuário, enquanto a autorização determina o que o usuário tem permissão para fazer.

Por exemplo, um membro da equipe de TI pode não ter os privilégios necessários para alterar as senhas de acesso de uma rede virtual privada — VPN — corporativa. No entanto, o administrador da rede pode optar por conceder privilégios de acesso ao membro, permitindo que ele altere as senhas de VPN de usuários individuais. 

Dessa forma, o membro da equipe será autorizado a acessar uma área da qual estava anteriormente bloqueado.

#### Separation of Duties

Um elemento central da autorização é o *princípio da separação de funções* — também conhecido como *`segregation of duties`*.

A separação de funções *baseia-se na prática de segurança de que nenhuma pessoa deve controlar uma transação de alto risco inteira, do início ao fim*. A separação de funções divide a transação em partes separadas e exige que uma pessoa diferente execute cada parte.

> *Por exemplo, um funcionário pode enviar uma fatura para pagamento a um fornecedor — ou para reembolso a si mesmo, mas ela deve ser aprovada por um gerente antes do pagamento; em outro caso, quase qualquer pessoa pode enviar uma proposta de alteração na configuração de um sistema, mas a solicitação deve passar por revisão técnica e gerencial e obter aprovação antes de ser implementada.*

Essas etapas podem *prevenir fraudes ou detectar um erro no processo* antes da implementação. Pode ser que o mesmo funcionário esteja autorizado a enviar faturas referentes a um conjunto de atividades, mas não as aprove, e ainda assim tenha autoridade de aprovação, mas não o direito de enviar faturas referentes a outro conjunto.

É possível, é claro, que dois indivíduos trabalhem juntos intencionalmente para contornar a separação de funções e cometer fraudes em conjunto. Isso se chama conluio. 

Outra implementação da separação de funções é o *`dual control`*.

Isso se aplicaria a um banco onde há duas fechaduras de combinação separadas na porta do cofre. Alguns funcionários conhecem uma das combinações e outros a outra, mas ninguém conhece ambas as combinações.

Duas pessoas devem trabalhar juntas para abrir o cofre; portanto, o cofre está sob controle duplo. 

Temos, aqui, o princípio do *`Two-person integrity`*. A regra de duas pessoas é uma estratégia de segurança que exige que no mínimo duas pessoas estejam juntas em uma área, impossibilitando que uma pessoa esteja sozinha na área.

Muitos sistemas de controle de acesso impedem que um titular de cartão entre em uma área de alta segurança selecionada, a menos que esteja acompanhado por pelo menos uma outra pessoa.

O uso da regra de duas pessoas pode ajudar a reduzir ameaças internas a áreas críticas, exigindo a presença de pelo menos duas pessoas a qualquer momento. Ela também é usada para a segurança de vidas dentro de uma área de segurança; se uma pessoa tiver uma emergência médica, haverá assistência presente.

---
## Accounting

A contabilidade monitora a atividade do usuário enquanto ele está conectado a uma rede, rastreando informações, como: por quanto tempo esteve conectado, os dados que enviou ou recebeu, seu endereço de Protocolo de Internet — IP, o Identificador Uniforme de Recursos — URI — que utilizou e os diferentes serviços que acessou.

A contabilidade pode ser usada para analisar tendências do usuário, auditar suas atividades e fornecer faturamentos mais precisos. Isso pode ser feito aproveitando os dados coletados durante o acesso do usuário. 

Por exemplo, se o sistema cobra dos usuários por hora, os registros de tempo gerados pelo sistema de contabilidade podem informar por quanto tempo o usuário esteve conectado ao roteador e dentro do sistema, e então cobrá-lo de acordo. 

#### Network Accounting

A contabilidade de rede captura informações para todas as sessões PPP (Point-to-Point Protocol), incluindo contagens de pacotes e bytes.

#### Connection Accounting

Contabilidade de conexão captura informações sobre todas as conexões de saída feitas a partir do cliente AAA, como por SSH.

#### EXEC Accounting

A contabilidade EXEC captura informações sobre sessões de terminal EXEC do usuário (shells do usuário) no servidor de acesso à rede, incluindo nome de usuário, data, horas de início e parada e o endereço IP do servidor de acesso.

#### System Accounting

A contabilidade do sistema captura informações sobre todos os eventos no nível do sistema (por exemplo, quando o sistema é reinicializado ou quando a contabilidade é ativada ou desativada).

#### Command Accounting

A contabilidade de comandos captura informações sobre os comandos do shell EXEC para um nível de privilégio especificado, bem como a data e hora em que cada comando foi executado e o usuário que o executou.

#### Resource Accounting

A implementação da Cisco de contabilidade AAA captura o suporte de registro de “iniciar” e “parar” para conexões que passaram pela autenticação do usuário. 

O recurso adicional de geração de registros de “parada” para conexões que falham na autenticação como parte da autenticação do usuário também é suportado. Esses registros são necessários para que os usuários que empregam registros contábeis gerenciem e monitorem suas redes.

---
## Why Is The AAA Framework Important In Network Security?

A *AAA* é uma parte crucial da segurança de redes porque limita quem tem acesso a um sistema e rastreia suas atividades. Dessa forma, agentes mal-intencionados podem ser mantidos afastados, e um agente presumivelmente bom que abusa de seus privilégios pode ter suas atividades rastreadas, o que fornece aos administradores informações valiosas sobre suas atividades.

Existem dois tipos principais de *AAA* para redes: acesso à rede e administração de dispositivos.

#### Network access

O acesso à rede envolve bloquear, conceder ou limitar o acesso com base nas credenciais de um usuário. A *AAA* verifica a identidade de um dispositivo ou usuário comparando as informações apresentadas ou inseridas com um banco de dados de credenciais aprovadas. Se as informações corresponderem, o acesso à rede é concedido.

#### Device administration

A administração de dispositivos envolve o controle do acesso a sessões, consoles de dispositivos de rede, shell seguro — SSH, e muito mais. Esse tipo de acesso é diferente do acesso à rede porque não limita quem tem permissão para entrar na rede, mas sim a quais dispositivos eles podem ter acesso.

---
## Types Of AAA Protocols

Existem vários protocolos que incorporam os elementos do *AAA* para garantir a segurança da identidade.

#### Remote authentication dial-In user service (RADIUS)

O *`RADIUS`* é um protocolo de rede que executa funções *AAA* para usuários em uma rede remota usando um modelo cliente/servidor. O *`RADIUS`* fornece simultaneamente autenticação e autorização aos usuários que tentam acessar a rede. O *`RADIUS`* também recebe todos os pacotes de dados *AAA* e os criptografa, proporcionando um nível extra de segurança.

O *`RADIUS`* funciona em três fases: o usuário envia uma solicitação a um servidor de acesso à rede — Network Access Service (NAS), e o NAS então envia uma solicitação de acesso ao servidor *`RADIUS`*, que responde à solicitação aceitando-a, rejeitando-a ou contestando-a, solicitando mais informações.

#### Diameter

O protocolo *`Diameter`* é um protocolo *AAA* que funciona com redes LTE — Long-Term Evolution — e multimídia. O *`Diameter`* é uma evolução do *`RADIUS`*, que tem sido usado há muito tempo em telecomunicações. No entanto, o *`Diameter`* é projetado sob medida para otimizar conexões LTE e outros tipos de redes móveis.

#### Terminal access controller access-control system plus (TACACS+)

Semelhante ao *`RADIUS`*, o *`TACACS+`* usa o modelo cliente/servidor para conectar usuários. No entanto, o *`TACACS+`* permite maior controle sobre as maneiras pelas quais os comandos são autorizados. O *`TACACS+`* funciona fornecendo uma chave secreta conhecida pelo cliente e pelo próprio sistema. Quando uma chave válida é apresentada, a conexão pode prosseguir.

O *`TACACS+`* separa os processos de autenticação e autorização, o que o diferencia do *`RADIUS`*, que os combina. Além disso, o *`TACACS+`*, assim como o *`RADIUS`*, criptografa seus pacotes *AAA*.

![[tacacs+_radius.png]]

---
## Authentication protocols and technologies

Um protocolo de autenticação autentica os dados entre duas entidades para impedir o acesso não autorizado. Um protocolo descreve o tipo de informação que precisa ser compartilhada para se autenticar e se conectar.

#### Extensible Authentication Protocol 

Uma senha do cliente é enviada usando um hash para o servidor de autenticação. O servidor de autenticação tem um certificado (o cliente não precisa de um certificado).

#### Password Authentication Protocol

Um nome de usuário e uma senha são enviados para um servidor de acesso remoto em texto sem formatação. A maioria dos servidores remotos de sistema operacional de rede é compatível com PAP.

#### Challenge Handshake Authentication Protocol

CHAP valida a identidade de clientes remotos usando uma função de hash unidirecional criada pelo cliente. O serviço também calcula o valor esperado de hash. O servidor os dois valores, se os valores corresponderem, a transmissão continua. O CHAP também verifica periodicamente a identidade do cliente durante a transmissão.

#### 802.1x

Uma empresa autentica sua identidade e autoriza o acesso à rede. Sua identidade é determinada com base em credenciais ou em um certificado confirmado por um servidor RADIUS.

#### RADIUS

Quando a autenticação simples de nome de usuário/senha for necessária, use RADIUS para aceitar ou negar acesso. RADIUS criptografa apenas a senha do usuário do cliente RADIUS para o servidor RADIUS. 

O nome de usuário, a contabilidade e os serviços autorizados são transmitidos em texto não criptografado. Quando o RADIUS é integrado a um produto, são necessárias medidas de segurança que protegem contra ataques de repetição.

#### TACACS+

TACACS + usa TCP como protocolo de transporte. TACACS + criptografa todos os dados (nome de usuário, senha, contabilidade e serviços autorizados) entre o cliente e o servidor. 

Como os administradores de rede podem definir ACLs, filtros e privilégios de usuário, TACACS + é a melhor escolha para redes corporativas que exigem etapas de autenticação mais sofisticadas e controle sobre atividades de autorização.

#### Kerberos

Kerberos usa criptografia forte, solicitando que um cliente comprove sua identidade para um servidor, com o servidor, por sua vez, se autenticando no cliente.

O servidor Kerberos contém IDs de usuário e senhas com hash para todos os usuários que terão autorizações para serviços de região. O servidor Kerberos também tem chaves secretas compartilhadas com todos os servidores aos quais concederá tíquetes de acesso. A base para a autenticação em um ambiente Kerberos é o tíquete. 

Os tíquetes são usados em um processo de duas etapas com o cliente. O primeiro tíquete é um tíquete de concessão de tíquete emitido pelo serviço de autenticação para um cliente solicitante. O cliente pode então apresentar esse tíquete ao servidor Kerberos com uma solicitação de tíquete para acessar um servidor específico. 

Esse tíquete do cliente para o servidor (também conhecido como tíquete de serviço) é usado para obter acesso ao serviço de um servidor. Como toda a sessão pode ser criptografada, isso elimina a transmissão inerentemente insegura de itens (como senhas) que podem ser interceptados na rede. Os tickets têm o carimbo de hora e expiram, portanto, qualquer tentativa de reutilização de um ticket não será bem-sucedida.

---
## Applications of Cryptographic Hash Functions

Como vimos anteriormente, as funções de hash de criptografia nos ajudam a garantir a integridade dos dados e verificar a autenticação. As funções de hash criptográfico são usadas nas seguintes situações:

- Para fornecer prova de autenticidade quando usado com uma chave de autenticação secreta simétrica, como segurança IP (IPsec) ou autenticação de protocolo de roteamento.

- Fornecer autenticação gerando respostas únicas e unidirecionais aos desafios nos protocolos de autenticação.

- Para fornecer prova de verificação de integridade da mensagem (como os usados em contratos assinados digitalmente) e certificados de infraestrutura de chave pública (PKI) (como os aceitos ao acessar um site seguro).

Ao escolher um algoritmo de hash, use o SHA-256 ou superior, pois são os mais seguros atualmente. Evite SHA-1 e MD5 devido a falhas de segurança que foram descobertas