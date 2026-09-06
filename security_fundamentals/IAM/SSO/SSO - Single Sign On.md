
## O que é?

O Single Sign On é uma facilitação de autenticação. Ele permite que um usuário se autentique em IDP (Identity Provider) e, uma vez autenticado nele, é possível se conectar em diversas outras aplicações/sites que cofiam nessa IDP.

Então, o conceito do single sign-on é bem simples: em vez de fornecer um nome de usuário e senha ou se identificar de outra forma em cada aplicação desejada, você fornece essas informações apenas uma vez para um servidor de autenticação. Feito isso, o servidor de autenticação envia certificados de identificação em seu nome quando você acessa qualquer aplicação que participe do sistema SSO.

## Tecnologias relacionadas

O SSO pode ser implementado usando qualquer um dos vários protocolos e serviços de autenticação.

### SAML/SAML 2.0

O Security Assertion Markup Language é uma especificação técnica que descreve a ***estrutura de um documento que servirá para autenticar usuários em aplicações***. 

O SAML usa o padrão ***XML*** amplamente aceito para especificar a estrutura do documento que os servidores de identidade, também conhecidos como provedores de identidade, criam e enviam para as aplicações. Essas aplicações são frequentemente chamadas de "provedores de serviço" na linguagem de SSO. 

Qualquer provedor de identidade que use SAML criará credenciais de autenticação que podem ser usadas por qualquer aplicação compatível com SAML, tornando-o uma boa opção para aplicações de internet.

O SAML não fornece um mecanismo para garantir que as informações de autenticação recebidas por uma aplicação permaneçam inalteradas. Isso é tratado por outras tecnologias.

### Kerberos

Criado no MIT no final da década de 1980 como parte do Projeto Athena, o Kerberos é uma arquitetura completa de autenticação e autorização.

O Projeto Athena buscava criar uma rede de recursos computacionais universalmente acessível aos estudantes do MIT em todo o campus. Originalmente, o Kerberos utilizava o Data Encryption Standard (DES) para criptografar as mensagens que trafegavam entre os servidores de autenticação e as aplicações. 

Ele usava chaves simétricas de 48 bits, o que significa que a mesma chave era usada para criptografar e descriptografar mensagens. Na época, o DES era a forma mais segura de criptografia disponível, sendo um padrão mantido pelo National Institute of Standards and Technology (NIST).

Atualmente, o Kerberos utiliza o Advanced Encryption Standard (AES), que substituiu o DES nos padrões de criptografia do NIST. O AES especifica chaves mais longas (até 256 bits) e permite múltiplos ciclos de criptografia, tornando o sistema muito difícil de ser violado.

Como o Kerberos usa criptografia de chave simétrica, ele exige uma terceira parte confiável para gerenciar as chaves, tornando-o mais adequado para aplicações corporativas onde um domínio de uso pode ser rigorosamente estabelecido, geralmente limitado às LANs e VPNs da empresa. 

O Kerberos pode ser usado na internet em locais onde os domínios não são estabelecidos, iniciando o processo por meio de outro padrão de autenticação (criptografia de chave pública), mas raramente é usado dessa forma. Ele pode usar seu próprio formato de credencial ou ser configurado para usar o SAML. 

Continua sendo popular, inclusive na Microsoft, que o utiliza por padrão em vez de seu sistema de autenticação NTLM, menos seguro, para redes corporativas.
### OAuth

Como uma estrutura de autorização aberta que não inclui uma estrutura de autenticação, OAuth é o sistema padrão quando uma aplicação da internet precisa acessar os recursos de um serviço protegido em nome de um usuário. A maioria dos provedores de nuvem, incluindo a Oracle, usa o OAuth para gerenciar o acesso aos seus recursos de nuvem.

A Oracle também oferece bibliotecas e serviços que facilitam aos desenvolvedores a criação de suas próprias aplicações que utilizam o OAuth.

Os principais componentes de um sistema OAuth são:

 - **O sistema cliente**, geralmente uma aplicação de usuário final que deseja acessar os recursos de vários serviços disponíveis na internet.

- **O servidor de autorização**, que recebe solicitações de tokens que permitirão que um cliente acesse serviços protegidos. O servidor de autorização receberá solicitações de tokens junto com o certificado de autenticação do cliente. Ele emitirá tokens de acesso que foram autorizados pelo proprietário do recurso.

- **O servidor de recursos**, que possui as informações ou fornece o serviço que o cliente deseja usar. Ele fornece dados ou serviços quando recebe tokens de acesso válidos do cliente.

Diversos tipos de concessão de acesso podem ser especificados pelo token de acesso. Os diferentes tipos são emitidos dependendo do nível de confiança exigido e da natureza do dispositivo do cliente. Por exemplo, uma smart TV pode receber uma concessão de acesso diferente de um laptop.

### OpenID Connect (OIDC)

O OpenID Connect é o sistema de gerenciamento de identidade desenvolvido para uso com OAuth. Juntos, OIDC e OAuth fornecem um ambiente SSO completo para aplicações baseadas na web e sistemas nativos da internet, como aplicativos móveis. Em vez de usar o SAML como base para retornar informações de credenciais, o OIDC usa um documento JSON conhecido como JSON Web Tokens, descrito abaixo, e protocolos RESTful. Ambos são nativos da internet e fáceis para os desenvolvedores usarem.

Em vez de usar criptografia de chave simétrica como o Kerberos, o OIDC usa criptografia de chave pública, que se adapta melhor a redes sem domínio, como a internet.

### Autenticação por cartão inteligente.

Sistemas como o OIDC usam criptografia de chave pública para garantir que apenas os destinatários autorizados possam ver os dados trocados com um provedor de gerenciamento de identidade durante e após a autenticação. A criptografia de chave pública é assimétrica e envolve uma chave pública, que pode ser usada para criptografar mensagens a serem enviadas a um cliente ou servidor, e uma chave privada, secreta, que deve ser usada para descriptografar as mensagens.

Geralmente, as chaves privadas são armazenadas no dispositivo de um usuário. A maioria dos laptops vem com um chip resistente a adulterações que usa a tecnologia Trusted Platform Module (TPM) para descriptografar mensagens destinadas ao sistema. Os telefones Apple e Android usam sistemas diferentes, mas semelhantes. O da Apple é chamado Secure Enclave, e o do Android é chamado Android Knox. Essas tecnologias permitem que o dispositivo forneça sua chave pública a qualquer sistema que a solicite corretamente e use sua chave privada, que nunca é divulgada, para descriptografar as mensagens recebidas.

A vantagem desses sistemas é que o usuário do dispositivo não precisa saber nada sobre como a criptografia é tratada em seus sistemas. A desvantagem é que cada dispositivo que o usuário possui terá um par de chaves pública/privada exclusivo, portanto, os dispositivos são conhecidos individualmente no processo de criptografia. Se um laptop ou celular for perdido ou roubado, o sistema de criptografia não impedirá o acesso se o criminoso souber a senha do proprietário.

O uso de um cartão inteligente com um chip semelhante aos chips incorporados em cartões de crédito permite que os usuários sejam autenticados com um único conjunto de chaves, independentemente dos dispositivos que estejam usando. O chip no cartão é o próprio microprocessador, portanto, precisa ser inserido em um leitor de cartão ou ativado e alimentado por meio de uma tecnologia RFID, como a comunicação de campo próximo. A segurança do cartão inteligente é semelhante à oferecida pelos chips TPM.

### LDAP

O Lightweight Directory Access Protocol foi introduzido na década de 1990 para permitir que os usuários encontrassem recursos que desejassem utilizar em uma rede local, como servidores ou impressoras. Ele pressupõe um servidor autorizado que conheça todos os recursos dentro de um domínio. Dessa forma, não é adequado para uso na internet.

Como o LDAP é usado para conceder acesso a recursos de rede, ele inclui um sistema de autenticação de usuário com as credenciais do usuário armazenadas no servidor LDAP. Seus mecanismos de autenticação de usuário não são robustos. Por exemplo, ele envia senhas pela rede em texto não criptografado. A criptografia pode ser fornecida por outro protocolo, como SSL/TLS.

O LDAP tem a vantagem de ser flexível e extensível, permitindo que as empresas o utilizem para armazenar informações adicionais sobre os funcionários, como funções organizacionais e associações a grupos, além de atributos como localização do escritório e número de telefone. No entanto, privilégios de acesso mais granulares são frequentemente necessários em empresas, como informações sobre quem tem acesso a determinados dados, e esses direitos de acesso não podem ser facilmente gerenciados pelo LDAP.

### JWT

Os JSON Web Tokens (JWTs) são documentos compactos usados ​​para transmitir informações de forma segura e estruturada entre as partes. Eles atendem à mesma necessidade dos documentos SAML, porém em um formato mais conciso, o que os torna adequados para inclusão em URLs. Os JWTs são assinados criptograficamente usando técnicas de criptografia de chave pública para garantir a autenticidade. Na Open Authentication (Oath), após a autenticação do usuário, o servidor de identidade retorna um token de ID JSON.

As solicitações de autorização para acessar recursos protegidos retornarão, subsequentemente, um token de acesso JSON, que deverá ser incluído em cada solicitação ao servidor de recursos. Essas transações transmitem o status do cliente – autenticado e autorizado, nesse caso – a cada solicitação e, portanto, são chamadas de trocas RESTful. REST, que significa "transferência de estado representacional", é vantajoso porque os servidores de recursos não precisam estabelecer e manter sessões com cada cliente que deseja usar os recursos do servidor.

Os JWTs são documentos de texto simples, portanto, devem ser usados ​​em conexões criptografadas por HTTPS. Os tokens geralmente são projetados para não conter dados sensíveis, como informações de identificação pessoal. Como cada token é assinado de acordo com o padrão X.509, o padrão internacional para formatação de certificados de chave pública, essa assinatura será validada pelos servidores de recursos para garantir que o token não tenha sido adulterado. Os JWTs são componentes de um sistema de autenticação e autorização OAuth/OpenID. Eles são projetados para uso em aplicações web, são escaláveis ​​e destinados a serem usados ​​em diversos domínios.