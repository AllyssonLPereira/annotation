---
tags:
  - arquivo
---
## Visão geral da segurança sem fio

Uma WLAN está aberta a qualquer pessoa dentro do alcance de um ponto de acesso sem fio (AP) e com as credenciais apropriadas para se associar a ele. Com uma placa de rede sem fio (NIC) e conhecimento de técnicas de quebra de segurança, um invasor pode não precisar entrar fisicamente no local de trabalho para obter acesso à sua rede por meio de uma WLAN.

Ataques podem ser gerados por pessoas externas, funcionários insatisfeitos e até mesmo acidentalmente. Redes sem fio são especialmente suscetíveis a uma série de ameaças, incluindo:

- *Interceptação de dados*

	Os dados sem fio devem ser criptografados para evitar que sejam lidos por pessoas que estejam bisbilhotando.

	Impedir um ataque como um ataque Man in the middle (MITM) depende da sofisticação da infraestrutura da WLAN e da vigilância no monitoramento da atividade na rede. O processo começa com a identificação de dispositivos legítimos na WLAN. Para fazer isso, os usuários devem ser autenticados. 

	Depois que todos os dispositivos legítimos são conhecidos, a rede pode ser monitorada quanto a dispositivos ou tráfego anormais. Para isso, os usuários devem ser autenticados.

- *Intrusos sem fio*

	Usuários não autorizados que tentam acessar recursos de rede podem ser impedidos por meio de técnicas eficazes de autenticação.

- *Ataques de Negação de Serviço (DoS)*

	O acesso aos serviços WLAN pode ser comprometido tanto acidentalmente quanto de forma maliciosa. Existem várias soluções, dependendo da origem do ataque DoS.

- *Rogue APs*

	Pontos de acesso não autorizados instalados por um usuário bem-intencionado ou com propósitos maliciosos podem ser detectados usando software de gerenciamento de rede sem fio. 

	Para evitar a instalação de pontos de acesso não autorizados, as organizações devem configurar **controladores de LAN sem fio (WLCs)** com políticas de pontos de acesso não autorizados, e utilizar software de monitoramento para monitorar ativamente o espectro de rádio em busca de pontos de acesso não autorizados.

---
## Ataques DoS

Os ataques de DoS sem fio podem ser o resultado de:

- *Dispositivos configurados incorretamente -* Erros de configuração podem desabilitar a WLAN. Por exemplo, um administrador pode alterar acidentalmente uma configuração e desativar a rede, ou um invasor com privilégios de administrador pode desativar intencionalmente uma WLAN.

- *Um usuário malicioso interfere intencionalmente na comunicação sem fio -* Seu objetivo é desabilitar completamente a rede sem fio ou a ponto de nenhum dispositivo legítimo poder acessar o meio.

- *Interferência acidental -* WLANs são suscetíveis a interferência de outros dispositivos sem fio, incluindo fornos de micro-ondas, telefones sem fio, babás eletrônicas e outros. **A banda de 2,4 GHz é mais propensa a interferências do que a banda de 5 GHz.

---
## Ocultação do SSID e filtragem de endereço MAC

Os sinais sem fio podem viajar através de materiais sólidos, como tetos, pisos, paredes, fora de casa ou escritórios. Sem medidas rigorosas de segurança, a instalação de uma WLAN pode ser equivalente a colocar portas Ethernet em qualquer lugar, mesmo fora do escritório ou casa.

Para lidar com as ameaças de impedir invasores sem fio e proteger dados, dois recursos de segurança anteriores foram usados e ainda estão disponíveis na maioria dos roteadores e pontos de acesso: camuflagem SSID e filtragem de endereço MAC.

- *Ocultação do SSID*

	Os pontos de acesso e alguns roteadores sem fio permitem que o quadro de sinalização SSID seja desativado. **Os clientes sem fio devem configurar manualmente o SSID para se conectar à rede.

- *Filtragem de endereços MAC*

	Um administrador pode permitir ou negar manualmente o acesso sem fio dos clientes com base em seu endereço físico de hardware MAC.

---
## Métodos de Autenticação 802.11

Embora esses dois recursos dissuadem a maioria dos usuários, a realidade é que nem a ocultação do SSID nem a filtragem de endereços MAC impediriam um intruso astuto. 

Os SSID's são facilmente descobertos mesmo se os APs não os transmitirem e os endereços MAC podem ser falsificados. A melhor maneira de proteger uma rede sem fio é usar sistemas de autenticação e criptografia.

Dois tipos de autenticação foram introduzidos com o padrão 802.11 original:

- *Autenticação de sistema aberto:*

	Qualquer cliente sem fio poderá se conectar facilmente. A autenticação de sistema aberto deve ser usada apenas em situações em que a segurança não é uma preocupação, como em locais que fornecem acesso gratuito à internet, como cafés, hotéis e áreas remotas. 

	O cliente sem fio é responsável por fornecer segurança, como por exemplo, usando uma rede virtual privada (VPN) para se conectar de forma segura. As VPNs fornecem serviços de autenticação e criptografia.

- *A autenticação de chave compartilhada:*

	Isso fornece mecanismos como WEP, WPA, WPA2 e WPA3 para autenticar e criptografar dados entre um cliente sem fio e um ponto de acesso (AP). No entanto, a senha deve ser pré-compartilhada entre as duas partes para se conectar.

---
## Métodos de Autenticação de Chave Compartilhada

Existem quatro técnicas de autenticação de chave compartilhada disponíveis, conforme descrito na tabela. Até que a disponibilidade dos dispositivos WPA3 se torne onipresente, as redes sem fio devem usar o padrão WPA2.

| Método de autenticação         | Descrição                                                                                                                                                                                                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| WEP (Wired Equivalent Privacy) | A especificação 802.11 original projetada para proteger os dados usando o método de criptografia Rivest Cipher 4 (RC4) com uma chave estática. No entanto, a chave nunca muda ao trocar pacotes. Isso facilita a invasão. O WEP não é mais recomendado e nunca deve ser usado. |
| WPA (Wi-Fi Protected Access)   | Um padrão da Wi-Fi Alliance que usa WEP, mas protege os dados com o algoritmo de criptografia TKIP (Temporal Key Integrity Protocol) muito mais forte. O TKIP muda a chave para cada pacote, dificultando o trabalho dos hackers.                                              |
| WPA2                           | O WPA2 é o padrão atual do setor para proteger redes sem fio. Usa a criptografia AES (Advanced Encryption Standard - Padrão de Criptografia Avançada). O AES é considerado atualmente o protocolo de criptografia mais forte.                                                  |
| WPA3                           | Esta é a próxima geração de segurança Wi-Fi. Todos os dispositivos habilitados para WPA3 usam os métodos de segurança mais recentes, desaprovam protocolos herdados desatualizados e exigem o uso de quadros de gerenciamento protegidos (PMF).                                |

---
## Autenticando um Usuário Doméstico

Os roteadores domésticos geralmente têm duas opções para autenticação: WPA e WPA2. WPA2 é o mais forte dos dois. A opção para selecionar um dos dois métodos de autenticação WPA2 são:

- *Personal:

	Destinado a redes domésticas ou de pequenos escritórios, os usuários autenticam-se usando uma chave pré-compartilhada (PSK). Os clientes sem fio se autenticam com o roteador sem fio usando uma senha pré-compartilhada. Nenhum servidor de autenticação especial é necessário

- *Enterprise:

	Destinado a redes empresariais, porém requer um servidor de autenticação Remote Authentication Dial-In User Service (RADIUS). Embora seja mais complicado de configurar, ele fornece segurança adicional. O dispositivo deve ser autenticado pelo servidor RADIUS e os usuários devem se autenticar usando o padrão 802.1X, que usa o EAP (Extensible Authentication Protocol) para autenticação.

---
## Métodos de Criptografia

Criptografia é usada para proteger os dados. Se um invasor capturar dados criptografados, não poderá decifrá-los em um período de tempo razoável.

Os padrões WPA e WPA2 usam os seguintes protocolos de criptografia:

- *Temporal Key Integrity Protocol (TKIP):

	O TKIP é o método de criptografia usado pelo WPA. Ele fornece suporte para equipamentos WLAN herdados, abordando as falhas originais associadas ao método de criptografia 802.11 WEP. 

	Ele usa o WEP, mas criptografa a carga útil da camada 2 usando o TKIP e executa um MIC (Message Integrity Check) no pacote criptografado para garantir que a mensagem não seja alterada.

- *Advanced Encryption Standard (AES):

	AES é o método de criptografia usado pelo WPA2. É o método preferido porque é um método muito mais forte de criptografia. Ele usa o Modo de Cifra de Contador com o Protocolo de Código de Autenticação de Mensagem em Cadeia de Blocos (CCMP - Chaining Message Authentication Code Protocol) que permite que os hosts de destino reconheçam se os bits criptografados e não criptografados foram alterados.

---
## Autenticação na Empresa

Em redes com requisitos de segurança mais rígidos, é necessária uma autenticação ou login adicional para conceder acesso a clientes sem fio. A opção do modo de segurança corporativa requer um servidor RADIUS de autenticação, autorização e contabilidade (AAA - Authentication, Authorization, and Accounting).

- *Endereço IP do servidor RADIUS -* Este é o endereço acessível do servidor RADIUS.

- *Números de porta UDP -* As portas UDP oficialmente designadas são 1812 para autenticação RADIUS e 1813 para contabilidade RADIUS, mas também podem operar usando as portas UDP 1645 e 1646, como mostrado na figura.

- *Chave compartilhada -* Usada para autenticar o ponto de acesso (AP) com o servidor RADIUS.


A chave compartilhada não é um parâmetro que deve ser configurado em um cliente sem fio. É necessário apenas no ponto de acesso para se autenticar com o servidor RADIUS. 

A autenticação e autorização do usuário são tratadas pelo padrão 802.1X, que fornece uma autenticação centralizada e baseada em servidor dos usuários finais.

O processo de login 802.1X usa o EAP para se comunicar com o servidor AP e RADIUS. O EAP é uma estrutura para autenticar o acesso à rede. 

Ele pode fornecer um mecanismo de autenticação segura e negociar uma chave privada segura que pode ser usada para uma sessão de criptografia sem fio usando a criptografia TKIP ou AES.

---
## WPA3

No momento da redação deste artigo, os dispositivos que suportam autenticação WPA3 não estavam disponíveis. No entanto, o WPA2 não é mais considerado seguro. WPA3, se disponível, é o método de autenticação 802.11 recomendado. O WPA3 inclui quatro aplicativos:

- WPA3-Personal
- WPA3-Enterprise
- Redes abertas
- Integração da Internet das Coisas (IoT)


- WPA3-Personal:

	No WPA2-Personal, os atores de ameaças podem ouvir o “aperto de mão” (handshake) entre um cliente sem fio e o AP e usar um ataque de força bruta para tentar adivinhar o PSK. O WPA3-Personal impede esse ataque usando a autenticação simultânea de iguais (SAE), um recurso especificado no IEEE 802.11-2016. **O PSK nunca é exposto, tornando impossível para o atacante adivinhar.


- WPA3-Enterprise:

	O WPA3-Enterprise ainda usa autenticação 802.1X / EAP. No entanto, requer o uso de um conjunto criptográfico de 192 bits e elimina a mistura de protocolos de segurança para os padrões 802.11 anteriores. 

	O WPA3-Enterprise adere ao conjunto comercial de algoritmos de segurança nacional (CNSA - Commercial National Security Algorithm), que é comumente usado em redes Wi-Fi de alta segurança.


- Redes abertas:

	As redes abertas no WPA2 enviam o tráfego do usuário em texto não autenticado e limpo. No WPA3, as redes Wi-Fi abertas ou públicas ainda não usam autenticação. No entanto, eles usam o OWE (Opportunistic Wireless Encryption) para criptografar todo o tráfego sem fio.


- Integração da IoT:

	Embora o WPA2 tenha incluído o Wi-Fi Protected Setup (WPS) para dispositivos embarcados rapidamente, sem configurá-los primeiro, o WPS é vulnerável a uma variedade de ataques e não é recomendado.

	Além disso, os dispositivos IoT geralmente são "headless", ou seja, não possuem interface gráfica integrada para configuração e precisam de uma maneira fácil de se conectar à rede sem fio.

	O Protocolo de provisionamento de dispositivo (DPP - Device Provisioning Protocol) foi projetado para atender a essa necessidade. Cada dispositivo projetado para operar sem tela, teclado e mouse possui uma chave pública codificada diretamente no seu firmware ou hardware. 

	A chave é tipicamente impressa na parte externa do dispositivo ou em sua embalagem como um código de resposta rápida (QR Code). O administrador da rede pode digitalizar o código QR e integrar rapidamente o dispositivo. Embora não faça parte estritamente do padrão WPA3, o DPP substituirá o WPS ao longo do tempo.

---
## Authentication Protocol

O *`Extensible Authentication Protocol — EAP —`* é uma estrutura de autenticação usada em redes sem fio. Vamos descobrir como isso funciona:

1. O usuário solicita a conexão à rede sem fio através de um access point.
2. O access point solicita dados de identificação (nome de usuário) do usuário, que é então enviado para um servidor de autenticação.
3. O servidor de autenticação solicita a prova de que a ID é válida.
4. O access point solicita prova de que a ID é válida do usuário, na forma de uma senha.
5. O usuário fornece a senha ao access point. O access point envia de volta para o servidor de autenticação.
6. O servidor confirma que o nome de usuário e a senha estão corretos e passa essas informações para o access point e o usuário.
7. Conecte-se à rede sem fio.

---
## Mutual Authentication

Sua rede sem fio e seus dados confidenciais estão sujeitos a acesso não autorizado por hackers que usam uma conexão sem fio. Mas o que você pode fazer para evitar um ataque?

A autenticação mútua é a autenticação de duas vias que pode impedir access points não autorizados. É um processo no qual as duas entidades em um link de comunicação se autenticam antes de se conectarem. Isso permite que os clientes detectem access points não autorizados e evitem esses ataques MitM. 

---
## Mobile Device Protections

Não importa se um dispositivo móvel é de propriedade da empresa ou é um dispositivo pessoal usado para o trabalho, medidas precisam ser implementadas para mantê-lo protegido contra ameaças digitais.

Quais são os riscos? As ameaças a dispositivos móveis incluem:

- Theft;
- Loss;
- Unauthorized access;
- Operating system risks;
- Application risks;
- Network risks.

#### Jailbreaking, root e sideloading

*`Jailbreaking`*, *`root`* e *`sideload`* são formas de contornar as limitações de um dispositivo para fazer coisas que o dispositivo está impedido de fazer. Os usuários podem tentar fazer o *`jailbreak`* — dispositivos da Apple, ou *`root`* — dispositivos Android — para executar um aplicativo que não está autorizado ou não está disponível na loja.

O *`jailbreak`* remove a restrição de que apenas aplicativos autorizados pela Apple podem ser executados no dispositivo. O *`root`* ignora a arquitetura de segurança do Android para permitir acesso administrativo completo ao dispositivo. Ambos representam um risco para a empresa. 

Há soluções disponíveis que podem detectar um dispositivo com "*`jailbroken`*" ou "*`rooteado`*". Um dispositivo é então marcado como não compatível e removido da rede ou tem o acesso negado a aplicativos organizacionais.

As lojas de aplicativos de terceiros também podem representar um risco para as empresas porque os aplicativos aos quais elas fornecem acesso não foram avaliados corretamente. O *`sideloading`* — *carregamento lateral* — ocorre quando o usuário percorre as configurações de aplicativo aprovado para instalar aplicativos não aprovados. Isso é menos invasivo do que fazer *`jailbreaking`* ou *`rooting`*, mas ainda é um risco.

Quais são as proteções? As proteções contra ameaças a dispositivos móveis incluem:

- Os bloqueios de tela exigem uma senha, um PIN ou um padrão para acessar o dispositivo.
- A autenticação biométrica usa uma característica física exclusiva (impressão digital, face, íris ou voz).
- A autenticação com reconhecimento de contexto usa aprendizado de máquina para determinar o acesso com base no comportamento normal do usuário.
- A limpeza remota exclui os dados do dispositivo, caso ele seja roubado ou perdido.
- A criptografia completa do dispositivo pode criptografar todos os dados em um dispositivo móvel.