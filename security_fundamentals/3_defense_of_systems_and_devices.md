---
tags:
  - arquivo
---
## Gerenciamento de patches

Os criminosos digitais trabalham incansavelmente para explorar a fraqueza dos sistemas de computador. Para ficar um passo à frente, mantenha os sistemas seguros e atualizados com a instalação regular de patches.


- *O que são correções?:*

	Os **patches são atualizações de código que os fabricantes fornecem para evitar que um vírus ou um worm recém-descoberto façam um ataque bem-sucedido**. 

	Patches e atualizações são frequentemente combinados em um service pack. Muitos ataques de malware poderiam ter sido evitados se os usuários instalassem o service pack mais recente.

	Sistemas operacionais como o Windows verificam rotineiramente atualizações que podem proteger um computador contra as ameaças à segurança mais recentes. Isso inclui atualizações de segurança, atualizações críticas e service packs.
	

- *O que você precisa fazer?:*

	**Como um profissional de segurança digital, é uma boa prática testar um patch antes de implantá-lo em toda a empresa**. Uma ferramenta de gerenciamento de patches pode ser usada para gerenciar patches localmente, em vez de usar o serviço de atualização on-line do fornecedor.

	Um serviço de patch automatizado fornece aos administradores um controle maior em vez de esperar pelos patches para download. Vejamos alguns dos benefícios

	- Os administradores podem aprovar ou recusar atualizações.
	- Os administradores podem forçar a atualização de sistemas para uma data específica.
	- Os administradores podem obter relatórios sobre a atualização necessária para cada sistema.
	- Cada computador não tem que se conectar ao serviço do fornecedor para baixar os patches. Um sistema obtém a atualização de um servidor local.
	- Os usuários não podem desativar ou contornar as atualizações.


- *Uma abordagem proativa:*

	Além de proteger o sistema operacional, é importante atualizar aplicativos de terceiros, como Adobe Acrobat, Java e Google Chrome, para solucionar vulnerabilidades que podem ser exploradas. 

	**Uma abordagem proativa ao gerenciamento de patches oferece segurança de rede e ajuda a evitar ransomware e outras ameaças.

---
## Integridade da inicialização

Os invasores podem atacar a qualquer momento, mesmo no curto espaço de tempo que um sistema leva para iniciar. É fundamental garantir que os sistemas e dispositivos permaneçam seguros durante a inicialização.


- ##### O que é integridade de inicialização?

	A integridade de inicialização garante que o sistema seja confiável e não tenha sido alterado enquanto o sistema operacional é carregado.

	O firmware - instruções de software sobre as funções básicas do computador - é armazenado em um pequeno chip de memória na placa-mãe. O sistema básico de entrada / saída (BIOS) é o primeiro programa executado quando você liga o computador.

	A Unified Extensible Firmware Interface (UEFI), uma versão mais recente do BIOS, define uma interface padrão entre o sistema operacional, o firmware e os dispositivos externos. Um sistema que usa UEFI é preferível a um que usa BIOS porque um sistema UEFI pode ser executado no modo de 64 bits.


- ##### Como funciona a inicialização segura?

	A inicialização segura é um padrão de segurança para garantir que um dispositivo inicialize usando software confiável. 

	Quando um sistema de computador é inicializado, o firmware verifica a assinatura de cada parte do software de inicialização, incluindo os drivers de firmware UEFI, aplicativos UEFI e o sistema operacional. 

	Se as assinaturas forem válidas, o sistema inicializará e o firmware dará controle ao sistema operacional.


- ##### O que é a inicialização medida?

	A inicialização medida fornece uma validação mais forte do que a inicialização segura. A inicialização medida mede cada componente, começando pelo firmware até os drivers de inicialização, e armazena as medidas no chip TMP para criar um log. 

	O log pode ser testado remotamente para verificar o estado de inicialização do cliente. A inicialização medida pode identificar aplicativos não confiáveis que tentam carregar e também permite que o antimalware seja carregado mais cedo.



