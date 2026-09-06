---
tags:
  - arquivo
---
## Diamond Model of Intrusion Analysis

#### Overview

O *Modelo Diamond de Análise de Intrusão* é composto por quatro partes. O modelo representa um incidente ou evento de segurança. 

No Modelo Diamond, um evento é uma atividade limitada ao tempo que é restrita a uma etapa específica em que um adversário usa uma capacidade sobre a infraestrutura para atacar uma vítima para alcançar um resultado específico.

Os quatro principais recursos de um evento de intrusão são adversário, capacidade, infraestrutura e vítima:

- *Adversary*

	Estas partes são responsáveis pela intrusão.

- *Funds*

	Esta é uma ferramenta ou técnica que o adversário usa para atacar a vítima.

- *Infrastructure*

	Este é o caminho ou caminhos de rede que os adversários usam para estabelecer e manter o comando e o controle sobre suas capacidades.

- *Victim*

	Este é o alvo do ataque. No entanto, uma vítima pode ser o alvo inicialmente e, em seguida, usada como parte da infraestrutura para lançar outros ataques.


O adversário usa recursos sobre infraestrutura para atacar a vítima. O modelo pode ser interpretado como dizendo: “O adversário usa a infraestrutura para se conectar à vítima. O adversário desenvolve capacidade de explorar a vítima.” 

> *Por exemplo, um recurso como malware pode ser usado na infraestrutura de e-mail por um adversário para explorar uma vítima.*

Os meta recursos expandem o modelo ligeiramente para incluir os seguintes elementos importantes:

- *Timestamp*

	Isso indica a hora de início e parada de um evento e é parte integrante do agrupamento de atividades mal-intencionadas.

- *Phase*

	Isso é análogo às etapas da cadeia Cyber Kill. A atividade maliciosa inclui duas ou mais etapas executadas sucessivamente para alcançar o resultado desejado.

- *Result*

	Isso delineia o que o adversário ganhou com o evento. Os resultados podem ser documentados como um ou mais dos seguintes: confidencialidade, integridade e disponibilidade comprometidas.

- *Direction*

	Indica a direção do evento em todo o Modelo Diamond. Elas incluem infraestrutura adversária, infraestrutura para vítima, vítima para infraestrutura e infraestrutura para adversário.

- *Method*

	Ela é usada para classificar o tipo geral de evento, como varredura de portas, phishing, ataque de entrega de conteúdo, syn flood, etc.

- *Funds*

	Estes são um ou mais recursos externos usados pelo adversário para o evento de intrusão, como software, conhecimento do adversário, informações (por exemplo, nome de usuário/senhas) e ativos para realizar o ataque (hardware, fundos, instalações, acesso à rede).

![[Pasted image 20250918212644.png]]

---
## Characterization of the diamond model of an exploration

Como analista de segurança cibernética, você pode ser chamado a usar o Modelo Diamond de Análise de Intrusão para diagramar uma série de eventos de intrusão. O Modelo Diamond é ideal para ilustrar como o adversário vai de um evento para o outro.

> *Por exemplo, na figura, um funcionário relata que seu computador está agindo de forma anormal. Uma verificação de host feita pelo técnico de segurança indica que o computador está infectado com malware...* 
> 
> *... uma análise do malware revela que o malware contém uma lista de nomes de domínio CNC. Estes nomes de domínio resolvem para uma lista de endereços IP. Esses endereços IP são então usados para identificar o adversário, bem como investigar registros para determinar se outras vítimas na organização estão usando o canal CNC.*

---
## The diamond model and the Cyber ​​Kill chain

#### Examples of Activity Topics

Os adversários não operam em apenas um evento. Em vez disso, os eventos são encadeados na qual cada evento deve ser concluído com êxito antes do próximo evento. Este segmento de eventos pode ser mapeado para a *Cyber Kill Chain*.

O exemplo a seguir, mostrado na figura, ilustra o processo de ponta a ponta de um adversário à medida que eles atravessam verticalmente a *Cyber Kill Chain*, usam um host comprometido para girar horizontalmente para outra vítima e, em seguida, iniciar outro segmento de atividade:

1. O adversário realiza uma pesquisa na web para a empresa vítima Gadgets, Inc. recebendo como parte dos resultados o nome de domínio `gadgets.com`.

2. O adversário usa o domínio recém descoberto `gadets.com` para uma nova pesquisa “administrador de rede gadget.com” e descobre postagens de fóruns de usuários que afirmam ser administradores de rede do gadget.com. Os perfis de usuário revelam seus endereços de e-mail.

3. O adversário envia e-mails de phishing com um cavalo de Tróia anexado aos administradores de rede do `gadget.com`.

4. Um administrador de rede (NA1) do `gadget.com` abre o anexo malicioso. Isso executa a exploração fechada, permitindo a execução de código adicional.

5. O host comprometido do NA1 envia uma mensagem HTTP Post para um endereço IP, registrando-a com um controlador CNC. O host comprometido do NA1 recebe uma resposta HTTP em troca.

6. É revelado pela engenharia reversa que o malware tem endereços IP adicionais configurados que atuam como um backup se o primeiro controlador não responder.

7. Através de uma mensagem de resposta CNC HTTP enviada para o host do NA1, o malware começa a agir como um proxy da web para novas conexões TCP.

8. Através de informações do proxy que está sendo executado no host da NA1, Adversary faz uma pesquisa na web para “pesquisa mais importante de sempre” e encontra Victima 2, Interessante Research Inc.

9. Adversary verifica a lista de contatos de e-mail da NA1 para qualquer contato da Interessante Research Inc. e descobre o contato para o Diretor de Pesquisa Interessante da Inc.

10. O Diretor de Pesquisa da Interessante Research Inc. recebe um e-mail spear-phish do endereço de e-mail da Gadget Inc. enviado do host da NA1 com a mesma carga útil observada no Evento 3.

O adversário agora tem duas vítimas comprometidas, das quais ataques adicionais podem ser lançados. Por exemplo, o adversário poderia explorar os contatos de e-mail do Diretor de Pesquisa para as vítimas potenciais adicionais. O adversário também pode configurar outro proxy para exfiltrar todos os arquivos do Diretor de Pesquisa.

> [!NOTE]
> Este exemplo é uma modificação do exemplo do Departamento de Defesa dos EUA na publicação “O modelo Diamante de analises de intrusão”.

![[Pasted image 20250918212852.png]]