---
tags:
  - arquivo
---
## Overview

O gerenciamento de configuração é um processo e uma disciplina usados para *garantir que as únicas alterações feitas em um sistema sejam aquelas que foram autorizadas e validadas*.

É tanto um processo de tomada de decisão quanto um conjunto de processos de controle. Se analisarmos mais detalhadamente essa definição, o processo básico de gerenciamento de configuração inclui componentes como identificação, linhas de base, atualizações e patches.

#### Identificação

Identificação da linha de base de um sistema e de todos os seus componentes, interfaces e documentação.

#### Linha de base

Uma linha de base de segurança é um nível mínimo de proteção que pode ser usado como ponto de referência. As linhas de base fornecem uma maneira de garantir que as atualizações de tecnologia e arquiteturas sejam submetidas ao nível mínimo compreendido e aceitável de requisitos de segurança.

#### Controle de Mudanças

Um processo de atualização para solicitar alterações em uma linha de base, por meio de alterações em um ou mais componentes dessa linha de base. Um processo de revisão e aprovação para todas as alterações. Isso inclui atualizações e patches.

#### Verificação e Auditoria

Um processo de regressão e validação, que pode envolver testes e análises, para verificar se nada no sistema foi danificado por um novo conjunto de alterações aplicadas. Um processo de auditoria pode validar se a linha de base atualmente em uso corresponde à soma total de sua linha de base inicial mais todas as alterações aprovadas aplicadas em sequência.

#### Inventário

Fazer um inventário, catálogo ou registro de todos os ativos de informação dos quais a organização tem conhecimento, sejam eles já existentes, ou se há uma lista de desejos ou a necessidade de criá-los ou adquiri-los, é o primeiro passo em qualquer processo de gestão de ativos. Exige que localizemos e identifiquemos todos os ativos de interesse, incluindo, e especialmente, os ativos de informação.

> *Você não pode proteger o que não sabe que possui.*

Torna-se ainda mais desafiador manter esse inventário, sua integridade e status em relação a atualizações e patches, consistentes e atualizados, dia após dia. Na verdade, é bastante desafiador identificar cada host físico e endpoint, quanto mais coletar os dados de todos eles.

#### Linhas de base

Um produto de software comercial, por exemplo, pode ter milhares de módulos, processos, parâmetros e arquivos de inicialização individuais ou outros elementos. Se algum deles estiver ausente, o sistema não poderá funcionar corretamente. 

A linha de base é um inventário total de todos os componentes do sistema, hardware, software, dados, controles administrativos, documentação e instruções do usuário.

Uma vez que os controles estejam implementados para mitigar os riscos, as linhas de base podem ser referenciadas. Todas as comparações e desenvolvimentos posteriores são medidos em relação às linhas de base.

Ao proteger ativos, as linhas de base podem ser particularmente úteis para atingir um nível mínimo de proteção desses ativos com base no valor. 

> *Lembre-se: se os ativos foram classificados com base no valor e linhas de base significativas foram estabelecidas para cada um dos níveis de classificação, podemos nos conformar com os níveis mínimos exigidos. Em outras palavras, se classificações como alta, média e baixa estiverem sendo usadas, linhas de base podem ser desenvolvidas para cada uma de nossas classificações e fornecer o nível mínimo de segurança necessário para cada uma.*

#### Atualizações

Reparos, ações de manutenção e atualizações são frequentemente necessários em quase todos os níveis dos elementos do sistema, desde a infraestrutura básica da arquitetura de TI até sistemas operacionais, plataformas de aplicativos, redes e interfaces de usuário. 

Tais modificações devem ser submetidas a testes de aceitação para verificar se a funcionalidade recém-instalada ou reparada funciona conforme o necessário.

Elas também devem ser submetidas a testes de regressão para verificar se as modificações não introduziram outros comportamentos errôneos ou inesperados no sistema. A avaliação contínua de segurança e os testes de avaliação avaliam se o mesmo sistema que passou no teste de aceitação ainda é seguro.

#### Patches

O gerenciamento de patches se aplica principalmente a dispositivos de software e hardware que estão sujeitos a modificações regulares. Um patch é uma atualização, upgrade ou modificação de um sistema ou componente. Esses patches podem ser necessários para corrigir uma vulnerabilidade ou melhorar a funcionalidade.

O desafio para o profissional de segurança é manter todos os patches, pois eles podem vir em intervalos irregulares de diversos fornecedores. 

Alguns patches são críticos e devem ser implantados rapidamente, enquanto outros podem não ser tão críticos, mas ainda assim devem ser implantados, pois patches subsequentes podem depender deles. Padrões como o PCI DSS exigem que as organizações implantem patches de segurança dentro de um determinado prazo.

Existem alguns problemas com o uso de patches. Muitas organizações foram afetadas por um patch legal de um fornecedor confiável que afetou a funcionalidade do sistema. 

Portanto, uma organização deve testar o patch antes de implementá-lo em toda a organização. Isso geralmente é complicado pela falta de um ambiente de teste que corresponda ao ambiente de produção. Poucas organizações têm orçamento para manter um ambiente de teste que seja uma cópia exata do ambiente de produção.

Sempre existe o risco de que nem tudo seja testado e que problemas possam surgir na produção que não eram aparentes no ambiente de teste. Na medida do possível, os patches devem ser testados para garantir que funcionem corretamente na produção.

Se o patch não funcionar ou apresentar efeitos inaceitáveis, pode ser necessário reverter para um estado anterior — pré-patch. Normalmente, os critérios para reversão são documentados previamente e seriam executados automaticamente quando os critérios de reversão fossem atendidos.

Muitos fornecedores oferecem uma solução de gerenciamento de patches para seus produtos. Esses sistemas geralmente possuem certos processos automatizados, ou atualizações autônomas, que permitem a aplicação de patches em sistemas sem a interação do administrador.

O risco de usar patches autônomos deve ser ponderado em relação ao risco de ter sistemas sem patches na rede da organização.

A aplicação de patches autônomos pode resultar em interrupções não programadas, à medida que os sistemas de produção são colocados fora de operação ou reinicializados como parte do processo de patch.