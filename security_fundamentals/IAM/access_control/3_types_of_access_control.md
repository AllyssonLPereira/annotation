---
tags:
  - arquivo
---
## DAC — Discretionary Access Control

O *`Discretionary Access Control`* é um tipo específico de política de controle de acesso aplicada a todos os sujeitos e objetos em um sistema de informação.

No DAC, a política especifica que um sujeito que recebeu acesso à informação *PODE* realizar uma ou mais das seguintes ações:

- Passar as informações para outros sujeitos ou objetos;
- Conceder seus privilégios a outros sujeitos;
- Alterar atributos de segurança em sujeitos, objetos, sistemas de informação ou componentes do sistema;
- Escolher os atributos de segurança a serem associados a objetos recém-criados ou revisados;
- Alterar as regras que regem o controle de acesso; controles de acesso obrigatórios restringem essa capacidade.

Steve e Aidan, por exemplo, são dois usuários (sujeitos) em um ambiente UNIX operando com DAC em vigor. Normalmente, os sistemas criam e mantêm uma tabela que mapeia sujeitos a objetos, como mostrado na imagem.

![[dac.png]]

Em cada intersecção está o conjunto de permissões que um determinado sujeito possui para um objeto específico. Muitos sistemas operacionais, como o Windows e toda a árvore genealógica do Unix, incluindo Linux, e iOS, usam esse tipo de estrutura de dados para tomar decisões rápidas e precisas sobre a autorização ou negação de uma solicitação de acesso.

Observe que esses dados podem ser visualizados como linhas ou colunas:

- A lista de controle de acesso de um objeto mostra o conjunto total de sujeitos que possuem alguma permissão para aquele objeto específico;

- A lista de capacidades de um sujeito mostra cada objeto no sistema para o qual o sujeito possui alguma permissão.

Essa metodologia depende da discrição do proprietário do objeto de controle de acesso para determinar os direitos específicos do sujeito de controle de acesso.

Portanto, a segurança do objeto fica literalmente a critério do proprietário do objeto. DACs não são muito escaláveis; eles dependem das decisões de controle de acesso tomadas por cada proprietário individual do objeto, e pode ser difícil encontrar a origem dos problemas de controle de acesso quando ocorrem problemas.

---
## MAC — Mandatory Access Control

O *`Mandatory Access Control`* é determinado pelo administrador de segurança, *de forma abrangente*, com pouca tomada de decisão individual sobre quem obtém acesso.

Por exemplo, em certas agências governamentais, os funcionários precisam ter um determinado tipo de autorização de segurança para acessar determinadas áreas. Em geral, esse *nível de acesso é definido por políticas* governamentais e não por um indivíduo que concede permissão com base em seu próprio julgamento.

Frequentemente, isso é acompanhado pela separação de funções, em que o escopo do trabalho é limitado e os usuários não têm acesso a informações que não lhes dizem respeito. Essa separação de funções também é facilitada pelo *`Role-Based Access Control`*.

Um *`Mandatory Access Control`* é aplicada uniformemente a todos os sujeitos e objetos dentro dos limites de um sistema de informação.

Em termos mais simples, isso significa que apenas administradores de segurança devidamente designados, como sujeitos confiáveis, podem modificar quaisquer regras de segurança estabelecidas para sujeitos e objetos dentro do sistema.

Isso também significa que, para todos os sujeitos definidos pela organização — ou seja, conhecidos por seu sistema integrado de gerenciamento de identidade e controle de acesso, a organização atribui um subconjunto de privilégios totais para um subconjunto de objetos, de forma que o sujeito seja *IMPEDIDO* de realizar qualquer uma das seguintes ações:

- Passar informações para sujeitos ou objetos não autorizados;
- Conceder seus privilégios a outros sujeitos;
- Alterar um ou mais atributos de segurança em sujeitos, objetos, no sistema de informação ou em componentes do sistema;
- Escolher os atributos de segurança a serem associados a objetos recém-criados ou modificados;
- Alterar as regras que regem o controle de acesso.

---
## RBAC — Role-Based Access Control

O *`role-based access control`* concede a cada funcionário privilégios com base na função que ele desempenha na organização.

> *Por exemplo:
> 
> - Apenas o Recursos Humanos tem acesso aos arquivos de pessoal; 
> - Apenas o Financeiro tem acesso às contas bancárias; 
> - Cada gerente tem acesso aos seus próprios subordinados diretos e ao seu próprio departamento;
> - Administradores de sistema de alto nível podem ter acesso a tudo; 
> - Novos funcionários teriam acesso muito limitado, o mínimo necessário para realizar suas tarefas.*

Monitorar essas permissões baseadas em funções é importante porque, se as permissões de uma pessoa forem expandidas por um motivo específico — digamos, as permissões de um funcionário júnior podem ser expandidas para que ele possa atuar temporariamente como gerente de departamento — mas suas permissões não forem alteradas de volta quando o novo gerente for contratado, a próxima pessoa a assumir esse nível júnior poderá herdar essas permissões quando não for apropriado para ela.

> Isso é chamado de *`privilege creep`* ou *`permissions creep`*. 

Ter múltiplas funções com diferentes combinações de permissões pode exigir um *monitoramento rigoroso para garantir que todos tenham o acesso necessário para realizar suas tarefas e **nada mais***. 

Neste mundo em que as funções estão em constante mudança, às vezes pode ser um desafio acompanhar isso, especialmente com funções e permissões extremamente granulares.

Ao contratar ou mudar de função, uma prática recomendada é não copiar perfis de usuário para novos usuários. Recomenda-se que funções padrão sejam estabelecidas e que novos usuários sejam criados com base nesses padrões, e não em um usuário real. Dessa forma, os novos funcionários começam com as funções e permissões apropriadas.

---
## RBAC — Rule-Based Access Control

Nesse modelo de controle de acesso, a equipe de segurança de rede especifica conjuntos de regras/condições associadas ao acesso a dados ou sistemas. Essas regras podem especificar endereços IP permitidos ou negados, ou determinados protocolos e outras condições.

---
## ABAC — Attribute-Based Access Control

O ABAC permite o acesso com base em atributos do objeto/recurso a ser acessado, o sujeito/usuário acessando o recurso e fatores ambientais sobre como o objeto deve ser acessado, como a hora do dia.

---
## TAC — Time-Based Access Control 

TAC Permite o acesso a recursos de rede com base na hora e no dia.

---
## LBAC - Lattice-Based Access Control

Neste tipo, temos vários níveis de acesso. Por exemplo, público, interno, secreto e ultrassecreto (tudo isso num formato de pirade, do mais acessível ao mais secreto). 

Quem tem acesso a um nível, tem acesso aos demais embaixo.