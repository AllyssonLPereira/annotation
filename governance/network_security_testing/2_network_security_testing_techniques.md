---
tags:
  - arquivo
---
## Operations security

A segurança das operações se preocupa com as práticas diárias necessárias para primeiro implantar e depois manter um sistema seguro. Todas as redes estão vulneráveis a ataques se o planejamento, implementação, operações e manutenção da rede não seguirem as práticas de segurança operacional.

A segurança das operações começa com o processo de planejamento e implementação de uma rede. Durante essas fases, a equipe de operações analisa projetos, identifica riscos e vulnerabilidades e faz as adaptações necessárias. 

As tarefas operacionais reais começam depois que a rede é configurada e incluem a manutenção contínua do ambiente. Essas atividades permitem que o ambiente, os sistemas e os aplicativos continuem a funcionar de maneira correta e segura.

Algumas técnicas de teste de segurança são predominantemente manuais, e outras são altamente automatizadas. Independentemente do tipo de teste, a equipe que configura e realiza os testes de segurança deve ter conhecimento significativo em segurança e rede nestas áreas:

- Sistemas operacionais;
- Programação básica;
- Protocolos de rede, como TCP/IP;
- Vulnerabilidades de rede e mitigação de riscos;
- Hardening do dispositivo;
- Firewalls;
- IPS's.

---
## Testing and Evaluating Network Security

A eficácia de uma solução de segurança de operações pode ser testada sem esperar que uma ameaça real ocorra. Os testes de segurança de rede tornam isso possível. 

O teste de segurança de rede é executado em uma rede para garantir que todas as implementações de segurança estejam operando conforme o esperado. Normalmente, os testes de segurança da rede são conduzidos durante os estágios de implementação e operacional, após o sistema ter sido desenvolvido, instalado e integrado.

Os testes de segurança fornecem informações sobre várias tarefas administrativas, como análise de risco e planejamento de contingência. É importante documentar os resultados dos testes de segurança e disponibilizá-los para a equipe envolvida em outras áreas de TI.

Durante a fase de implementação, os testes de segurança são realizados em partes específicas da rede. Depois que uma rede estiver totalmente integrada e operacional, é realizado um Teste e Avaliação de Segurança — *`ST&E`*. Um *`ST&E`* é um exame das medidas de proteção que são colocadas em uma rede operacional.

Os objetivos da *`ST&E`* incluem o seguinte:

- Descubrir falhas de design, implementação e operação que poderiam levar à violação da política de segurança.
- Determinar a adequação de mecanismos de segurança, garantias e propriedades do dispositivo para aplicar a política de segurança.
- Avaliar o grau de consistência entre a documentação do sistema e sua implementação.

Os testes devem ser repetidos periodicamente e sempre que for feita uma alteração no sistema. Para sistemas de segurança que protegem informações críticas ou protegem hosts que estão expostos a ameaças constantes, os testes de segurança devem ser realizados com mais frequência.

---
## Types of network tests

Depois que uma rede estiver operacional, você deve acessar seu status de segurança. Muitos testes de segurança podem ser realizados para avaliar o status operacional da rede:

- *`Pentest`* — Testes de penetração de rede simulam ataques de fontes maliciosas. O objetivo é determinar a viabilidade de um ataque e as possíveis consequências se um ocorrer. Alguns testes de penetração podem envolver o acesso às instalações de um cliente e o uso de habilidades de engenharia social para testar sua postura geral de segurança.

- *`Network scanning`* — Inclui software que pode fazer ping em computadores, verificar portas TCP de escuta e exibir quais tipos de recursos estão disponíveis na rede. Alguns softwares de varredura também podem detectar nomes de usuários, grupos e recursos compartilhados. Os administradores de rede podem usar essas informações para fortalecer suas redes.

- *`Vulnerability scanning`* — Inclui software que pode detectar fraquezas potenciais nos sistemas testados. Esses pontos fracos podem incluir configuração incorreta, senhas em branco ou padrão ou alvos potenciais para ataques DoS. Alguns softwares permitem que os administradores tentem travar o sistema através da vulnerabilidade identificada.

- *`Password Cracking`* — Isso inclui software usado para testar e detectar senhas fracas que devem ser alteradas. As políticas de senha devem incluir diretrizes para evitar senhas fracas.

- *`Log review`* — Os administradores de sistema devem revisar os logs de segurança para identificar ameaças de segurança em potencial. O software de filtragem para varrer arquivos de log longos deve ser usado para ajudar a descobrir atividades anormais a serem investigadas.

- *`Integrity checkers`* — Um sistema de verificação de integridade detecta e gera relatórios sobre mudanças no sistema. A maior parte do monitoramento concentra-se no sistema de arquivos. No entanto, alguns sistemas de verificação podem relatar atividades de login e logout.

- *`Virus detection`* — O software de detecção de vírus ou antimalware deve ser usado para identificar e remover vírus de computador e outros malwares.

> [!NOTE]
> Outros testes, incluindo Wardialing e Witders, são considerados legados, mas ainda devem ser contabilizados em testes de rede.
> 

#### Applying Network Test Results

Os resultados dos testes de segurança de rede podem ser usados de várias maneiras:

- Para definir atividades de mitigação para abordar vulnerabilidades identificadas;
- Como referência para rastrear o progresso de uma organização em atender aos requisitos de segurança;
- Avaliar o estado de implementação dos requisitos de segurança do sistema;
- Realizar análises de custos e benefícios para melhorias na segurança da rede;
- Melhorar outras atividades, como avaliações de risco, certificação e autorização e esforços de melhoria de desempenho;
- Como ponto de referência para a ação corretiva.
