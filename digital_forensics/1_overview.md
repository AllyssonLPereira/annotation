---
tags:
  - arquivo
---
## Forensic Process of Digital Evidence

É importante que uma organização desenvolva processos e procedimentos bem documentados para análise forense digital. A conformidade regulamentar pode exigir esta documentação, e essa documentação pode ser inspecionada pelas autoridades em caso de investigação pública.

A publicação especial do *Guia para integração de tecnicas forenses para resposta a incidentes NIST 800-86* é um recurso valioso para organizações que precisam de orientação no desenvolvimento de planos forenses digitais. 

> *Por exemplo, ele recomenda que a computação forense seja realizada usando o processo de quatro fases.*

A seguir, descreve as quatro fases básicas do processo forense de evidências digitais.

- *Etapa 1 — Collection*

	Esta é a identificação e aquisição de potenciais fontes de dados forenses, além do manuseio e armazenamento desses dados. Este estágio é crítico porque deve-se ter especial cuidado para não danificar, perder ou omitir dados importantes.

- *Etapa 2 — Examination*

	Isto implica avaliar e extrair informações relevantes dos dados recolhidos. Isso pode envolver descompactação ou descriptografia dos dados. 

	As informações irrelevantes para a investigação podem ter de ser removidas. Identificar evidências reais em grandes coleções de dados pode ser muito difícil e demorado.

- *Etapa 3 — Analysis*

	A fase de análise envolve o uso dos dados coletados para comprovar ou refutar um caso construído pelos examinadores. Aqui estão as perguntas-chave que os examinadores precisam responder para todos os itens de dados relevantes:

	- Quem criou os dados?
	- Quem editou os dados?
	- Como os dados foram criados?
	- Quando essas atividades ocorrem?

	Além de fornecer as informações acima, os examinadores também determinam como as informações se relacionam com o caso.

- *Etapa 4 — Reporting*

	Isso implica preparar e apresentar informações resultantes da análise. Os relatórios devem ser imparciais e devem ser apresentadas explicações alternativas, se for o caso. Limitações da análise e problemas encontrados devem ser incluídos. Também devem ser feitas sugestões para uma investigação mais aprofundada e para os próximos passos.

---
## Tipos de evidencias

Em processos judiciais, as provas são geralmente classificadas como:

- *Provas diretas* 

	Essas são provas que estavam indiscutivelmente na posse do acusado, ou são testemunhas oculares de alguém que observou diretamente o comportamento criminoso.

- *Provas indiretas*

	Esta é a evidência que, em combinação com outros fatos, estabelece uma hipótese. Isso também é conhecido como *evidência circunstancial*. 

	Por exemplo, a evidência de que um indivíduo cometeu crimes semelhantes pode apoiar a afirmação de que a pessoa cometeu o crime de que é acusado.

- *Melhor evidência*

	Esta é a evidência que está em seu estado original. Essas evidências podem ser dispositivos de armazenamento usados por um acusado, ou arquivos que podem ser comprovados como inalterados.

- *Provas corroborantes*

	Esta é uma evidência que suporta uma afirmação que é desenvolvida a partir da melhor evidência.

---
## Evidence Collection Order

A *`IETF RFC 3227`* fornece diretrizes para a coleta de evidências digitais. Ela descreve uma ordem para o recolhimento de provas digitais com base na volatilidade dos dados. 

Os dados armazenados na RAM são os mais voláteis, e serão perdidos quando o dispositivo for desligado. Além disso, dados importantes na memória volátil podem ser substituídos por processos de rotina da máquina. Portanto, a coleta de evidências digitais deve começar com a evidência mais volátil e avançar para a menos volátil.

Um exemplo da ordem de coleta de evidências mais volátil a menos volátil é o seguinte:

*1.* Registros de memória, caches;
*2.* Tabela de roteamento, cache ARP, tabela de processo, estatísticas de kernel, RAM;
*3.* Sistemas de arquivos temporários;
*4.* Meios não voláteis, fixos e removíveis;
*5.* Dados de registro e monitoramento remotos;
*6.* Interconexões físicas e topologias;
*7.* Mídia de arquivamento, fita ou outros backups.

Detalhes dos sistemas a partir dos quais as provas foram recolhidas, incluindo quem tem acesso a esses sistemas e a que nível de permissões devem ser registadas. Essas informações devem incluir configurações de hardware e software para os sistemas a partir dos quais os dados foram obtidos.

---
## Chain of Custody

Embora possam ter sido recolhidas provas de fontes que apoiam a atribuição de um crime a um indivíduo acusado, pode-se argumentar que a evidência poderia ter sido alterada ou fabricada após a coleta. Para contrariar este argumento, deve ser definida e seguida uma rigorosa cadeia de custódia.

A cadeia de custódia envolve a *coleta*, *manuseio* e *armazenamento seguro* de evidências. Devem ser conservados registos pormenorizados dos seguintes elementos:

- Quem descobriu e recolheu as provas?
- Todos os detalhes sobre o tratamento de evidências, incluindo horas, locais e pessoal envolvido.
- Quem tem a principal responsabilidade pelas provas, quando a responsabilidade foi atribuída e quando a custódia mudou?
- Quem tem acesso físico à evidência enquanto foi armazenada? O acesso deve ser limitado apenas ao pessoal mais essencial.

#### Data integrity and preservation

Ao coletar dados, é importante que eles sejam preservados em sua condição original. O carimbo de data/hora — *timestamp* — dos arquivos deve ser preservado. Por esta razão, a prova original deve ser copiada e a análise deve ser realizada apenas em cópias do original. 

Isto é para evitar perda acidental ou alteração da evidência. Como os carimbos de data/hora podem fazer parte da evidência, abrir arquivos da mídia original deve ser evitado.

O processo utilizado para criar cópias dos elementos de prova utilizados no inquérito deve ser registado. Sempre que possível, as cópias devem ser cópias diretas em nível de bits dos volumes de armazenamento originais. 

Deve ser possível comparar a imagem do disco arquivado e a imagem do disco investigada para identificar se o conteúdo do disco investigado foi adulterado. Por esta razão, é importante arquivar e proteger o disco original para mantê-lo em sua condição original, sem adulteração.

Memória volátil pode conter evidências forenses, então ferramentas especiais devem ser usadas para preservar essa evidência antes que o dispositivo seja desligado e as evidências sejam perdidas. Os usuários não devem desconectar da tomada ou desligar máquinas infectadas, a menos que explicitamente instruído pelo pessoal de segurança.

Seguir estes processos garantirá que qualquer evidência de delito será preservada, e quaisquer indicadores de comprometimento podem ser identificados.

---
## The MITRE ATT&CK framework

Uma maneira de atribuir um ataque é modelar o comportamento do ator de ameaça. O *`MITRE Adversary Tactics and Techniques & Common Knowledge Framework — ATT&CK —`* permite detectar táticas, técnicas e procedimentos do atacante — TTP — como parte da defesa contra ameaças e atribuição de ataques. 

Isso é feito mapeando os passos em um ataque para uma matriz de táticas generalizadas e descrevendo as técnicas que são usadas em cada tática. 

> *As táticas consistem nos objetivos técnicos que um atacante deve realizar para executar um ataque e as técnicas são o meio pelo qual as táticas são realizadas. Por último, os procedimentos são as acções específicas tomadas pelos intervenientes ameaçadores nas técnicas identificadas. Os procedimentos são o uso documentado de técnicas no mundo real por atores ameaçadores.*

O *MITRE ATT&CK Framework* é uma base de conhecimento global do comportamento do ator de ameaças. Baseia-se na observação e análise de explorações do mundo real com o objetivo de descrever o comportamento do atacante, não o ataque em si. 

Ele foi projetado para permitir o compartilhamento automatizado de informações, definindo estruturas de dados para o intercâmbio de informações entre sua comunidade de usuários e MITRE.

A figura mostra uma análise de uma exploração de ransomware a partir da excelente sandbox online *ANY.RUN*. As colunas mostram as táticas de matriz de ataque corporativo, com as técnicas usadas pelo malware organizadas sob as colunas. Clicar na técnica, em seguida, lista detalhes dos procedimentos que são usados pela instância de malware específica com uma definição, explicação e exemplos da técnica.

![[any.run.png]]