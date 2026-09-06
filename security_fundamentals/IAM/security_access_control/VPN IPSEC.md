
## Introdução

Uma **VPN IPsec (Internet Protocol Security)** é uma implementação de Rede Privada Virtual que opera na **camada 3 (camada de rede)** do modelo OSI, protegendo todo o tráfego de rede ao criptografar e autenticar **pacotes IP inteiros**. 

Diferente da SSL VPN, que protege principalmente comunicações web no nível da aplicação, o IPsec foi especificamente projetado para proteger a comunicação IP desde sua raiz, sendo definido por normas rigorosas da **IETF (Internet Engineering Task Force)**, principalmente nas **RFC 4301** (arquitetura de segurança), **RFC 4302** (Authentication Header) e **RFC 4303** (Encapsulating Security Payload). 

***
## IPsec, a arquitetura de segurança do IP

O IPsec não é um único protocolo, mas sim um **conjunto integrado de protocolos** que trabalham juntos para fornecer segurança no nível da rede. Segundo a **RFC 4301**, o objetivo do IPsec é oferecer quatro serviços de segurança fundamentais para qualquer comunicação IP que precise de proteção:

- O primeiro serviço é a **confidencialidade**, que garante que os dados não possam ser lidos por terceiros que interceptem o tráfego. Isso é alcançado por meio de criptografia forte, como **AES-256-GCM** ou **ChaCha20-Poly1305**, que tornam o conteúdo do pacote totalmente ilegível para quem não possui a chave de descriptografia.

- O segundo serviço é a **integridade dos dados**, que garante que o pacote não foi alterado durante o trânsito. O IPsec calcula um valor de verificação chamado **ICV (Integrity Check Value)** usando algoritmos como **HMAC-SHA256**. O receptor recalcula esse valor e o compara; se mesmo um único bit do pacote foi modificado, o cálculo não baterá e o pacote será descartado.

- O terceiro serviço é a **autenticação de origem**, que confirma que o pacote realmente veio do remetente declarado e não de um impostor. Isso é feito por meio de chaves pré-compartilhadas, certificados digitais X.509 ou algoritmos de assinatura digital, que provam a identidade do remetente antes de qualquer dado ser processado.

- O quarto serviço é a **proteção contra replay attacks**, que impede que um atacante capture um pacote válido e o reenvie mais tarde para executar uma ação não autorizada. O IPsec atribui um **número de sequência único** a cada pacote e mantém uma janela de verificação no receptor; se um número de sequência já foi visto, o pacote é imediatamente descartado.

***
## Componentes internos do IPsec

Para que tudo isso funcione de forma automática e segura, uma implementação IPsec mantém três componentes internos essenciais, que são descritos detalhadamente na **RFC 4301**:

O primeiro componente é o **SAD (Security Association Database)**, que armazena todas as informações de segurança de cada conexão ativa. Cada vez que uma VPN IPsec é estabelecida, é criada uma **SA (Security Association)**, que funciona como um "contrato" de segurança entre dois parceiros. O SAD guarda, para cada SA, a: 

- chave simétrica usada para criptografar;
- o algoritmo escolhido (AES, ChaCha20);
- o **SPI (Security Parameters Index)** que identifica essa SA exclusivamente; e 
- o número de sequência atual para controle anti-replay. 

Sem o SAD, o receptor não saberia como descriptografar ou autenticar os pacotes recebidos.

O segundo componente é o **SPD (Security Policy Database)**, que define **quais tráfegos devem ser protegidos** e como. O SPD contém regras que dizem, por exemplo, "todo tráfego que vai da rede 10.0.0.0/8 para a rede 172.16.0.0/12 DEVE usar IPsec com criptografia AES-256". Quando um pacote é gerado, o sistema consulta o SPD para decidir: deve ser **PROTEGIDO** (enviado com IPsec), **BYPASS** (enviado sem proteção, normalmente para tráfego confiável) ou **DISCARD** (bloqueado totalmente). O SPD é, portanto, o "cérebro" que decide quem pode comunicar e com qual nível de segurança.

O terceiro componente é o **IKE (Internet Key Exchange)**, que é o protocolo responsável pela **negociação automática de chaves** e criação das SAs. Sem o IKE, um administrador teria que configurar manualmente cada chave simétrica em cada dispositivo, o que seria impraticável em redes grandes. 

O IKE permite que dois dispositivos se autentiquem (usando pré-shared key, certificados ou senhas), negociem os algoritmos que vão usar, realizem uma **troca de chaves Diffie-Hellman** para gerar uma chave mestra secreta sem nunca transmiti-la pela rede, e criem automaticamente as SAs no SAD. 

O IKE existe em duas versões: **IKEv1** (mais antigo, ainda muito usado) e **IKEv2** (mais moderno, mais rápido e mais robusto). 

***
## ESP e AH

O IPsec se apoia principalmente em dois protocolos de cabeçalho, mas eles têm funções bem distintas e nem sempre são usados juntos.
### ESP (Encapsulating Security Payload)

O **ESP** é o protocolo **mais utilizado** no IPsec, presente em quase todas as implementações modernas, porque ele oferece **criptografia e autenticação em um único pacote**. Quando você configura uma VPN IPsec hoje em dia, na maioria das vezes está usando apenas ESP, sem precisar de AH.

O funcionamento do ESP no **modo túnel** (o mais comum) é o seguinte: 

- o pacote IP original, que contém o cabeçalho IP interno (com os endereços privados das redes interna, como 10.0.0.5 → 10.0.1.50), o cabeçalho TCP e os dados da aplicação, é **inteiramente criptografado**. 
- em seguida, um **cabeçalho ESP** é adicionado na frente, contendo o **SPI** (que identifica qual SA usar) e o **número de sequência** (para anti-replay). 
- por fim, um **ICV** (valor de verificação de integridade) é calculado sobre todo o conteúdo criptografado e adicionado no final do pacote.

A estrutura final do pacote, quando transmitido pela internet, fica assim: primeiro vem o **cabeçalho IP externo** (com os endereços públicos dos gateways, como 203.0.113.5 → 198.51.100.10), depois o cabeçalho ESP, depois o pacote IP interno inteiro criptografado, e por fim o ICV. Todo o tráfego entre os dois gateways, incluindo os endereços internos, permanece oculto para qualquer observador externo. 

Os algoritmos modernos usados pelo ESP são **AES-256-GCM** (que oferece criptografia e autenticação em uma única operação, chamada AEAD) e **ChaCha20-Poly1305** (ideal para dispositivos móveis ou sem aceleração hardware de AES). Algoritmos mais antigos como **AES-CBC** com **HMAC-SHA256** ainda são suportados, mas são menos eficientes porque exigem duas operações separadas (uma para criptografar e outra para autenticar).

![[images.jpeg]]

### AH (Authentication Header)

O **AH** é um protocolo **menos comum** hoje em dia, usado em menos de 1% das implementações, porque ele **não oferece criptografia**. Seu único objetivo é fornecer **autenticação de origem e integridade** para todo o pacote IP, **incluindo o cabeçalho IP externo**.

A estrutura do AH é mais simples: ele adiciona um cabeçalho entre o cabeçalho IP externo e o payload, contendo o SPI, o número de sequência e, no final, o **ICV calculado sobre quase tudo** (cabeçalho IP externo + payload). Isso significa que, se um atacante tentar alterar até mesmo um único bit do endereço IP de origem ou de destino, o ICV não vai bater e o pacote será rejeitado.

No entanto, o AH tem um **grande problema prático**: ele é **incompatível com NAT (Network Address Translation)**. Quando um pacote passa por um roteador NAT, o endereço IP de origem ou de destino é modificado. Como o ICV do AH inclui o cabeçalho IP original na sua verificação, qualquer alteração no IP quebra a integridade e o pacote é descartado. 

Por causa desse problema, o AH quase nunca é usado em redes modernas onde NAT é comum. A solução atual é usar **ESP com autenticação embutida (AEAD)**, que protege o payload sem incluir o cabeçalho IP externo na verificação, tornando-se compatível com NAT.

![[images (1).jpeg]]

***
## Modos de operação: Transporte vs Túnel

O IPsec pode operar de duas formas diferentes, dependendo de **onde** o encapsulamento ocorre e **qual parte** do pacote é protegida. A escolha entre esses modos depende do cenário de uso.
### Modo transporte: proteção P2P

No **modo transporte**, o IPsec protege apenas o **payload da camada 4** (ou seja, o segmento TCP ou UDP e os dados da aplicação), **sem criptografar o cabeçalho IP original**. Isso significa que os endereços IP de origem e destino permanecem visíveis e não criptografados.

Neste modo, a estrutura do pacote fica assim: o cabeçalho IP original (com os endereços reais, como 192.168.1.10 → 10.0.1.50) permanece no início, seguido pelo cabeçalho ESP, seguido pelo segmento TCP criptografado e os dados, e por fim o ICV. Os roteadores intermediários conseguem ver os IPs reais e encaminhar o pacote normalmente, mas não conseguem ler o conteúdo.

Esse modo é utilizado principalmente em cenários **host-to-host**, quando dois servidores específicos precisam se comunicar de forma segura diretamente, sem passar por um gateway intermediário. Por exemplo, dois servidores em DMZs diferentes que precisam trocar dados sensíveis, ou um computador e um servidor de banco de dados que estão na mesma rede física mas precisam de criptografia adicional.


### Modo túnel: proteção completa

No **modo túnel**, o IPsec protege o **pacote IP inteiro**, incluindo o cabeçalho IP original. Um **novo cabeçalho IP externo** é adicionado na frente, contendo os endereços públicos dos gateways. Todo o pacote original (IP interno + TCP + dados) é criptografado e encapsulado dentro do novo pacote.

A estrutura final fica assim: primeiro o **cabeçalho IP externo** (com os endereços públicos dos gateways, como 203.0.113.5 → 198.51.100.10), depois o cabeçalho ESP, depois o **pacote IP interno inteiro criptografado** (com os endereços privados 10.0.0.5 → 10.0.1.50), e por fim o ICV.

Este é o modo **mais comum** e é usado em dois cenários principais:

O primeiro cenário é **site-to-site**, quando duas redes inteiras precisam se comunicar de forma segura, como a matriz e uma filial. Os roteadores das duas empresas estabelecem um túnel IPsec entre si, e todo o tráfego entre as redes (10.0.0.0/8 → 172.16.0.0/12) passa criptografado pelo túnel. Os usuários em cada lado não percebem a VPN: eles apenas acessam recursos na outra rede como se estivessem na mesma rede local. 

O segundo cenário é **acesso remoto**, quando um usuário de fora da empresa (por exemplo, em casa ou em um café) precisa acessar recursos internos. O cliente IPsec (um software como Cisco AnyConnect, StrongSwan ou FortiClient) estabelece um túnel com o gateway da empresa, e todo o tráfego do usuário para a rede corporativa passa criptografado pelo túnel. Nesse caso, o usuário recebe um **IP virtual** da rede interna e sua tabela de roteamento é modificada para direcionar o tráfego para o túnel.

---
## Estabelecimento da sessão, o protocolo IKE

O IPsec **não cria túneis manualmente**. Em vez disso, ele usa o **IKE (Internet Key Exchange)** para negociar automaticamente todas as chaves, algoritmos e parâmetros de segurança antes que qualquer dado trafegue. O IKE é o "tratante" que faz a VPN se estabelecer sozinha, sem intervenção humana.
### IKEv1: antigo, mas ainda muito presente

O **IKEv1** opera em duas fases distintas:

Na **Fase 1**, o objetivo é criar um **canal seguro ISAKMP** (também chamado de **IKE SA**) entre os dois parceiros. Esse canal é usado para proteger as negociações da Fase 2. Existem dois modos na Fase 1:

- **Main Mode**: Usa 6 mensagens e é mais seguro contra ataques de negação de serviço (DoS), pois a identidade dos parceiros não é revelada até que o canal seguro já esteja estabelecido.

- **Aggressive Mode**: Usa apenas 3 mensagens e é mais rápido, mas expõe a identidade dos parceiros desde o início, o que pode ser um risco de segurança em redes públicas.

Depois que a Fase 1 termina, o canal ISAKMP está pronto e seguro para negociarmos a Fase 2.

Na **Fase 2**, chamada **Quick Mode**, o objetivo é criar as **SA de IPsec** (Child SA) que vão proteger o tráfego real. Nesse momento, os parceiros negociam:

- Qual protocolo usar (ESP ou AH)
- Quais algoritmos de criptografia e hash (AES-256, SHA-256, etc.)
- Se Perfect Forward Secrecy (PFS) será usado (gerando novas chaves Diffie-Hellman para cada SA)
- Quais sub-redes serão protegidas (por exemplo, 10.0.0.0/8 ↔ 172.16.0.0/12)

Com a Fase 2 concluída, o túnel IPsec está pronto e o tráfego começa a trafegar criptografado.


### **IKEv2: mais moderno e eficiente**

O **IKEv2** (definido na **RFC 7296**) foi projetado para ser mais simples, mais rápido e mais robusto que o IKEv1. Em vez de duas fases separadas, o IKEv2 consolida tudo em **apenas dois pares de mensagens**:

No primeiro par, chamado **IKE_SA_INIT**, os parceiros trocam:

- Propostas de algoritmos (cipher suites)
- Nonces (valores aleatórios para garantir frescor)
- Chaves públicas Diffie-Hellman

Ambos calculam então uma chave mestra chamada **SKEYSEED**, que será usada para derivar todas as chaves subsequentes.

No segundo par, chamado **IKE_AUTH**, os parceiros se **autenticam** (usando pré-shared key, certificados digitais ou EAP para senhas) e criam a **CHILD_SA** (SA de IPsec) que vai proteger o tráfego.

No total, o IKEv2 estabelece o túnel em **apenas 4 mensagens**, contra 6–9 do IKEv1. Além disso, o IKEv2 tem **suporte nativo para NAT Traversal**, **rehandshake automático** (sem precisar refazer toda a Fase 1 para renovar chaves) e **suporte a EAP**, que permite autenticação por senha, token ou smart card. Por tudo isso, o IKEv2 é o **padrão recomendado** para novas implementações em 2026. 

***
## Criptografia e algoritmos modernos em IPsec

Em 2026, as implementações modernas de IPsec usam algoritmos que são considerados seguros e eficientes, abandonando os mais antigos e vulneráveis.

Para **criptografia**, o padrão recomendado é **AES-256-GCM**, que é um algoritmo **AEAD (Authenticated Encryption with Associated Data)**. Isso significa que ele fornece **criproximação e autenticação em uma única operação**, sendo mais eficiente que usar AES-CBC separado do HMAC. Outra opção moderna é o **ChaCha20-Poly1305**, que é ideal para dispositivos como smartphones ou roteadores sem aceleração hardware para AES.

Para **autenticação de mensagens** (quando não se usa AEAD), o algoritmo padrão é **HMAC-SHA256**, que oferece integridade forte e é resistente a ataques de colisão. Algoritmos mais antigos como **HMAC-SHA1** ou **MD5** estão obsoletos e não devem ser usados.

Para a **troca de chaves Diffie-Hellman**, que garante **Perfect Forward Secrecy**, o mínimo recomendado é o **Group 14 (2048 bits)**, mas o ideal é usar o **Group 19 (256 bits ECDH)**. O ECDH é muito mais rápido que o DH tradicional e oferece o mesmo nível de segurança com chaves menores.

Para **assinaturas digitais** na autenticação por certificado, o padrão é **RSA-SHA256** com chaves de no mínimo **2048 bits** (4096 bits é recomendado para alta segurança). Algoritmos como **RSA-SHA1** ou chaves de 1024 bits estão obsoletos.

