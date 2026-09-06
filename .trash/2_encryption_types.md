---
tags:
  - arquivo
---
## Types:

#### Private/Symmetric Key Cryptography

Esse utiliza uma única chave.

O emissor utiliza essa chave para encriptar a mensagem, e o receptor usa a mesma chave para desencriptar a mensagem — shared key.

Esse tipo de algoritmo protege os dados, pois uma pessoa que não possua a chave correta não conseguiria ler a mensagem criptografada. No entanto, como a chave é compartilhada, isso pode levar a vários outros desafios:

- Se duas partes suspeitarem que um caminho de comunicação específico entre elas está comprometido, elas obviamente não poderão compartilhar o material da chave por esse caminho. Alguém que tenha comprometido as comunicações entre as partes também interceptaria a chave.

- *A distribuição da chave é difícil, pois a chave não pode ser enviada no mesmo canal que a mensagem criptografada, ou o intermediário — `MITM` — teria acesso à chave. O envio da chave por um canal — `banda` — diferente do canal da mensagem criptografada é chamado de distribuição de chaves fora de banda. Exemplos de distribuição de chaves fora de banda incluem o envio da chave por correio, fax ou telefone.*

- Qualquer pessoa com conhecimento da chave pode acessar — e, portanto, alterar — a mensagem.

- Cada indivíduo ou grupo de pessoas que deseja se comunicar precisaria usar uma chave diferente para cada indivíduo ou grupo com o qual deseja se conectar. Isso levanta o desafio da escalabilidade. Nesse tipo de arranjo simétrico, uma organização com 1.000 funcionários precisaria gerenciar 499.500 chaves se cada funcionário quisesse se comunicar confidencialmente com todos os outros funcionários.

Principais usos de algoritmos simétricos

- Criptografia de dados em massa — por exemplo, backups, discos rígidos, mídia portátil.
- Criptografia de mensagens que atravessam canais de comunicação — por exemplo, IPsec, TLS.
- Transmissão de dados em larga escala e sensíveis ao tempo — por exemplo, materiais de áudio/vídeo, jogos.

*Usada no modo stream e pode usar a CRIFRAGEM DE FLUXO ou de BLOCO.

- *`Block cipher`*: quebra a mensagem em blocos fixos — ex: 128 bits — e cifra bloco por bloco. Ex.: AES, DES.

- *`Stream cipher`*: cifra os dados bit a bit ou byte a byte, ideal para transmissões em tempo real. Ex.: RC4, OTP.

> *Outros exemplos: 3DES, Blowfish...*

#### Public-key or asymmetric cryptography

A criptografia assimétrica utiliza uma chave para criptografar e uma chave diferente para descriptografar o texto simples de entrada. Isso contrasta fortemente com a criptografia simétrica, que utiliza a mesma chave para criptografar e descriptografar.

Para a maioria dos profissionais de segurança, a matemática da criptografia assimétrica pode ser deixada para os criptoanalistas e criptógrafos.

Um usuário que deseja se comunicar usando um algoritmo assimétrico primeiro gera um par de chaves. Para garantir a solidez do processo de geração de chaves, isso geralmente é feito pelo aplicativo criptográfico ou pela implementação da infraestrutura de chave pública — PKI — sem o envolvimento do usuário.

Metade do par de chaves é mantida em segredo; apenas o detentor da chave a conhece. É por isso que ela é chamada de *`private key`*. 

A outra metade do par de chaves pode ser fornecida gratuitamente a qualquer pessoa que queira uma cópia. Em muitas empresas, ela pode estar disponível no site corporativo ou no acesso a um servidor de chaves.

Portanto, essa segunda metade do par de chaves é chamada de chave pública. Observe que qualquer pessoa pode criptografar algo usando a chave pública do destinatário, mas somente o destinatário — com sua chave privada — pode descriptografá-lo.

A criptografia de chave assimétrica resolve o problema da distribuição de chaves, permitindo que uma mensagem seja enviada por um meio não confiável de forma segura, sem a sobrecarga da troca prévia de chaves ou da distribuição do material da chave.

Ela também permite vários outros recursos não prontamente disponíveis na criptografia simétrica, como a irretratabilidade da origem e da entrega, o controle de acesso e a integridade dos dados.

A criptografia de chave assimétrica também resolve o problema da escalabilidade. Ela escala bem à medida que os números aumentam, pois cada parte requer apenas um par de chaves: as chaves privada e pública. 

> *Uma organização com 100.000 funcionários precisaria de um total de apenas 200.000 chaves (uma privada e uma pública para cada funcionário). Isso é menos da metade do número de chaves necessárias para a criptografia simétrica.*

O problema, no entanto, é que a criptografia assimétrica é extremamente lenta em comparação com sua contraparte simétrica. A criptografia assimétrica é impraticável para o uso diário na criptografia de grandes quantidades de dados ou para transações frequentes que exigem velocidade.

*O emissor encripta a mensagem com a chave pública do receptor, desse modo, a mensagem só pode ser desencriptada com a chave privada deste.

*Usada em *`Block Mode`*.

> *Ex.: DSA, RSA, GPG.*

#### Hash functions

Essa não utiliza uma chave, mas sim um valor de hash de tamanho fixo, o qual é computado sobre o texto plano.

*Elas são usadas para verificar a integridade dos dados para garantir que não tenham sido inadvertidamente alterados.

> *Ex.: MD5, SHA1, SHA2*

---
## What is a cipher?


Um par de algoritmos de encriptação — E — e desencriptação — D.

$$
c = E(k,m)
$$
$$ m = D(k,c) $$

m = texto plano;
c = texto cifrado;
k = key
E = algoritmo de encriptação
D = algoritmo de desencriptação

Podemos relacionar os dois algoritmos da seguinte forma:

$$
m = D(k, E(k, m)) \equacao \de \consistencia
$$

O algoritmo E é frequentemente randomizado, não tendo como prever o resultado dessa criptografia. Já o algoritmo D é sempre determinístico.
