---
tags:
  - arquivo
---
## Desenvolvimento de Aplicativos

Para manter a segurança em todas as etapas de desenvolvimento de aplicativos, um processo robusto precisa ser seguido.


- Desenvolvimento e teste:

	O software é desenvolvido e atualizado em um ambiente de desenvolvimento, onde pode ser desenvolvido, testado e depurado antes de ser implantado. 

	**Um ambiente de desenvolvimento é menos restritivo do que o ambiente ativo e tem um nível de segurança mais baixo**. Porém, o software de controle de versão ajuda a rastrear e gerenciar alterações no código do software. 

	Além disso, os desenvolvedores também podem trabalhar em um **ambiente de sandbox** para que o código não seja substituído à medida que o desenvolve. 

	Durante o teste, os desenvolvedores analisam como o código interage com o ambiente normal. A **garantia de qualidade (QA)** pode encontrar falhas no software. É muito mais fácil corrigir qualquer defeito encontrado nessa fase do que depois de implementado.

- Preparo e produção:

	Os ambientes de preparação devem corresponder ao ambiente de produção da empresa.

	**Ao testar em um ambiente intermediário, os desenvolvedores podem verificar se o software é executado sob as configurações de segurança necessárias**. Depois que o desenvolvedor executa e testa a segurança, o programa pode ser implantado em produção.

- Provisionamento e desprovisionamento:

	**Provisionamento é a criação ou atualização de software. O desprovisionamento é sua remoção**. Uma empresa pode usar um portal de autoatendimento para automatizar o desprovisionamento e o provisionamento de software.

---
## Técnicas de codificação de segurança

Ao codificar aplicativos, os desenvolvedores usam várias técnicas para validar se todos os requisitos de segurança foram atendidos.


- Normalização:

	A normalização é usada para organizar dados em um banco de dados e ajudar a manter a integridade dos dados. 

	A normalização converte uma sequência de entrada em sua forma mais simples e conhecida para garantir que todas as sequências tenham representações binárias exclusivas e que qualquer entrada mal-intencionada seja identificada.

- Procedimento armazenado:

	Um procedimento armazenado é um grupo de instruções SQL pré-compiladas armazenadas em um banco de dados que executa uma tarefa. 

	Se você usar um procedimento armazenado para aceitar parâmetros de entrada de clientes que usam dados de entrada diferentes, reduzirá o tráfego de rede e obterá resultados mais rápidos.

- Ofuscação e camuflagem:

	Um desenvolvedor pode usar a ofuscação e a camuflagem para impedir que o software seja reprojetado. A ofuscação oculta dados originais com caracteres ou dados aleatórios. A camuflagem substitui os dados confidenciais por dados fictícios realistas.

- Reutilização de código:

	A reutilização de código significa usar o software atual para criar um novo software, economizando tempo e custos de desenvolvimento. É preciso ter cuidado, no entanto, para evitar a introdução de vulnerabilidades.

- SDKs:

	Kits de desenvolvimento de software e bibliotecas de terceiros (SDKs) fornecem um repositório de códigos úteis para tornar o desenvolvimento de aplicativos mais rápido e mais barato. 

	A desvantagem é que qualquer vulnerabilidade em SDKs ou bibliotecas de terceiros pode afetar muitos aplicativos.

---
## Outras práticas de segurança de aplicativos


- Assinatura de código:

	A assinatura de código ajuda a provar que um software é autêntico.

	Os executáveis projetados para instalar e executar em um dispositivo são assinados digitalmente para **validar a identidade do autor e fornecer garantia de que o código de software não foi alterado desde que foi assinado**.


- Cookies seguros:

	O uso de cookies seguros protege as informações armazenadas em cookies contra hackers.

	Quando o sistema do cliente interage com um servidor, o servidor envia uma resposta HTTP que instrui o navegador a criar pelo menos um cookie. O cookie armazena dados para solicitações futuras enquanto você estiver navegando no site.

	Os desenvolvedores da Web devem usar cookies com HTTPS para proteger os cookies e impedir que eles sejam transmitidos por HTTP não criptografado.
