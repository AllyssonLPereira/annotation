---
tags:
  - arquivo
---
### Script entre sites (Cross-Site Scripting - XSS)


Os ataques realizados por meio de aplicativos da Web estão se tornando cada vez mais comuns. Atores de ameaças exploram vulnerabilidades na codificação de um aplicativo baseado na Web para obter acesso a um banco de dados ou servidor. 

Cross-site scripting (XSS) é uma ameaça comum encontrada em muitos aplicativos da web. Funciona assim:

1. Os criminosos digitais exploram a vulnerabilidade XSS ao injetar scripts que contêm código mal-intencionado em uma página da Web.

2. A página da Web é acessada pela vítima, e ***[os scripts mal-intencionados passam inadvertidamente para o navegador]. 

3. O script malicioso pode acessar cookies, tokens de sessão ou outras informações sensíveis sobre o usuário, que são enviadas de volta para o cibercriminoso.

4. Munido dessas informações, o criminoso digital pode se passar por um usuário.

---
### Injeção de Código


A maioria dos sites modernos usa um banco de dados, como um banco de dados de linguagem de consulta estruturada (SQL) ou um XML (Extensible Markup Language), para armazenar e gerenciar dados. ***[Os ataques de injeção buscam explorar os pontos fracos desses bancos de dados].


- ##### Ataque de injeção de XML

	Um ataque de injeção de XML pode corromper os dados no banco de dados XML e ameaçar a segurança do site.

	***[Ele funciona ao interferir no processamento de dados XML ou na consulta de uma aplicação inserida por um usuário]. 

	Os criminosos digitais podem manipular essa consulta ao programá-la para atender às suas necessidades. Isso concederá a eles acesso a todas as informações confidenciais armazenadas no banco de dados e permitirá que eles façam qualquer alteração no site.


- ##### Ataque de injeção de SQL

	Os criminosos digitais podem realizar um ataque de injeção de SQL em sites ou em qualquer banco de dados SQL inserindo uma instrução SQL mal-intencionada em um campo de entrada.

	***[Esse ataque aproveita uma vulnerabilidade na qual o aplicativo não filtra corretamente os dados inseridos por um usuário por caracteres em uma instrução SQL]. 

	Como resultado, o criminoso digital pode obter acesso não autorizado a informações armazenadas no banco de dados, das quais pode falsificar uma identidade, modificar dados atuais, destruir dados ou até mesmo se tornar um administrador do próprio servidor de banco de dados.


- ##### Ataque de injeção de DLL

	Um arquivo Dynamic Link Library (DLL) é uma biblioteca que contém um conjunto de códigos e dados para realizar uma determinada atividade no Windows. Os aplicativos usam esse tipo de arquivo para adicionar funcionalidades não incorporadas, quando precisam realizar essa atividade.

	A injeção de DLL permite que um criminoso digital engane um aplicativo para chamar um arquivo DLL mal-intencionado, que é executado como parte do processo de destino.


- ##### Ataque de injeção de LDAP

	O Lightweight Directory Access Protocol (LDAP) é um protocolo aberto para autenticar o acesso do usuário a serviços de diretório.

	Um ataque de injeção de LDAP explora vulnerabilidades de validação de entrada ao injetar e executar consultas a servidores LDAP, dando aos criminosos digitais a oportunidade de extrair informações confidenciais do diretório LDAP de uma empresa.

--- 
### Estouro de buffer (Buffer Overflow)


Os buffers são áreas de memórias alocadas a um aplicativo. Um estouro de buffer ocorre quando os dados são gravados além dos limites de um buffer. 

Ao alterar os dados além dos limites de um buffer, o aplicativo pode acessar a memória alocada para outros processos. Isso pode levar a uma falha do sistema ou comprometimento de dados, ou fornecer escalação de privilégios.

Essas falhas de memória também podem oferecer aos invasores controle total sobre o dispositivo de um alvo. 

Por exemplo, um invasor pode alterar as instruções de uma aplicação vulnerável enquanto o programa está carregando na memória e, como resultado, pode instalar malware e acessar a rede interna do dispositivo infectado.

--- 
### Execuções Remotas de Código


A execução remota de código permite que um cibercriminoso aproveite as vulnerabilidades do aplicativo para executar qualquer comando com os privilégios do usuário que executa o aplicativo no dispositivo de destino.

O escalonamento de privilégios explora um bug, falha de projeto ou configuração incorreta em um sistema operacional, ou aplicativo de software para obter acesso a recursos que normalmente são restritos.

---
### Defesa contra ataques à Aplicação


Existem várias ações que você pode tomar para se defender contra um ataque a aplicativo.

- A primeira linha de defesa contra um ataque a aplicativo é escrever um código sólido. 

- Prática prudente de programação envolve tratar e validar todas as entradas de fora de uma função como se fosse hostil. 

- Use ferramentas de teste de segurança para avaliar o código-fonte e o software binário continuamente durante o ciclo de vida do desenvolvimento do software.

- Mantenha todos os softwares atualizados, incluindo os sistemas operacionais e aplicativos, e não ignore os prompts de atualização. Nem todos os programas são atualizados automaticamente.