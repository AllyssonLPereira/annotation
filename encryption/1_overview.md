---
tags:
  - arquivo
---
## A tríade CIA e a criptografia

A segurança da informação é estruturada sob três pilares fundamentais denominados Tríade CIA: **Confidencialidade**, **Integridade** e **Disponibilidade**. A criptografia atua diretamente como o mecanismo para garantir os dois primeiros componentes e apoiar o terceiro. 

- A confidencialidade é alcançada ao transformar dados legíveis em texto cifrado inteligível apenas por quem possui a chave correta. 

- A integridade utiliza funções matemáticas para assegurar que a informação não foi alterada de forma maliciosa ou acidental durante o trânsito ou armazenamento. 

- Por fim, a disponibilidade é protegida indiretamente, pois sistemas criptográficos robustos evitam ataques baseados na falsificação de credenciais ou na manipulação de comandos de controle que poderiam derrubar um serviço. 

Temos, ainda, a classificação da criptografia em duas partes, a simétrica e a assimétrica. Vejamos elas:

### Criptografia simétrica

A criptografia simétrica fundamenta-se na utilização de um único segredo compartilhado, conhecido como chave simétrica, para realizar tanto a encriptação quanto a desencriptação. 

Neste modelo, a entidade que envia a mensagem e a que a recebe precisam ter acesso à mesma chave. O processo de cifragem transforma o dado original em um texto codificado por meio de operações matemáticas governadas por essa chave. Para reverter o processo, o receptor aplica a operação inversa utilizando a mesmo chave. 

A principal vantagem técnica é a velocidade de processamento e o baixo consumo de recursos computacionais, o que torna a criptografia simétrica a escolha ideal para proteger grandes volumes de dados armazenados ou transmissões de rede de alta velocidade. 

Já o principal desafio reside na distribuição segura dessa chave, já que qualquer interceptação do segredo compromete toda a comunicação.

#### Cifra em bloco

A cifra em bloco é uma abordagem dentro da criptografia simétrica que divide o texto original em segmentos de tamanho fixo e predeterminado, denominados blocos. O algoritmo processa um bloco de cada vez, aplicando sequências repetitivas de substituições e permutações matemáticas baseadas na chave secreta. 

Caso o volume total de dados a ser criptografado não seja um múltiplo exato do tamanho do bloco, o sistema aplica obrigatoriamente técnicas de preenchimento, conhecidas como _padding_, para completar o último bloco antes de iniciar o cálculo.

Como os blocos são estáticos, a cifragem pura de blocos idênticos com a mesma chave resultaria em blocos de texto cifrado também idênticos, o que permitiria a detecção de padrões por um analista malicioso. Para evitar essa vulnerabilidade, as cifras em bloco utilizam modos de operação. 

Esses modos introduzem dependências matemáticas entre os blocos, como fazer com que o resultado do bloco anterior influencie a cifragem do bloco atual, ou a utilização de contadores e vetores de inicialização aleatórios. Essa categoria de cifra é altamente indicada para a proteção de dados em repouso, como arquivos locais, partições de sistemas operacionais e bancos de dados, onde a integridade do arquivo completo é gerenciada em unidades estruturadas.

#### Cifra em fluxo

A cifra em fluxo adota uma filosofia distinta, operando de maneira contínua e individualizada sobre os dados. Em vez de agrupar a informação em blocos, este método processa o texto original bit a bit ou byte a byte. 

O mecanismo central de uma cifra em fluxo consiste em um gerador de números pseudoaleatórios que utiliza a chave simétrica secreta como semente. Esse gerador produz uma sequência ininterrupta e matematicamente complexa de bits binários chamada de fluxo de chave, ou _keystream_.

Uma vez gerado o fluxo de chave, ele é combinado diretamente com o texto original por meio de uma operação lógica binária, geralmente o OU Exclusivo (XOR). 

O processo de decifragem é idêntico: o receptor gera o mesmo fluxo de chave a partir da chave compartilhada e aplica novamente a operação lógica sobre o texto cifrado para recuperar o dado original. A principal característica técnica da cifra em fluxo é a ausência de necessidade de preenchimento de dados e o baixíssimo índice de latência, uma vez que os dados são transmitidos e cifrados simultaneamente.

#### Diferenças e aplicações

A escolha entre cifras em bloco e cifras em fluxo depende diretamente dos requisitos do sistema de computação e da natureza dos dados.

Cifras em bloco exigem maior capacidade de memória temporária, pois o sistema precisa reter os dados em buffers até que o tamanho mínimo do bloco seja alcançado para iniciar o processamento. Em contrapartida, as cifras em fluxo demandam menos memória e poder computacional imediato, processando os dados na velocidade em que chegam ao circuito ou à interface de rede.

8Devido a essa flexibilidade de fluxo contínuo, esse segundo modelo é amplamente empregado em canais de comunicação em tempo real, como transmissões de streaming de áudio e vídeo, conexões de redes móveis e comunicações de rádio, onde o tamanho total do arquivo é desconhecido no início da transmissão e os atrasos de processamento devem ser evitados.

### Criptografia assimétrica

A criptografia assimétrica, também conhecida como criptografia de chave pública, baseia-se em um modelo operacional que utiliza um par de chaves distintas, mas correlacionadas matematicamente: a chave pública e a chave privada.

A chave pública é projetada para ser compartilhada abertamente com qualquer entidade, funcionando como o endereço de recebimento ou o mecanismo de cifragem. A chave privada, por outro lado, deve ser mantida sob o controle exclusivo de seu proprietário e nunca transmitida pela rede.

A fundação técnica desse modelo reside em funções matemáticas unidirecionais com "alçapão" (_trapdoor functions_). Essas funções permitem que uma operação seja realizada facilmente em um sentido (cifrar o dado com a chave pública), mas tornam a inversão do processo (decifrar) computacionalmente inviável, a menos que se possua uma informação adicional específica, que é a chave privada. 

Dessa forma, qualquer pessoa pode codificar uma mensagem direcionada a um destinatário, mas apenas o portador da chave privada correspondente conseguirá reverter o texto cifrado para o formato original. Esse mecanismo resolve o problema histórico da distribuição de chaves que afeta os modelos simétricos.
#### Aplicação prática e o modelo híbrido

Dado o limite de tamanho e o alto consumo de processamento da criptografia assimétrica, a engenharia de segurança de sistemas não a utiliza para cifrar arquivos grandes ou tráfego de dados volumosos. Em vez disso, o modelo assimétrico é empregado primordialmente para duas funções específicas: a autenticação de identidade (através de assinaturas digitais) e o estabelecimento seguro de canais de comunicação através da troca de chaves.

Na prática, os sistemas modernos utilizam uma arquitetura híbrida. Quando um cliente se conecta a um servidor seguro, a criptografia assimétrica é ativada apenas na fase inicial da conexão para verificar a identidade das partes e permitir que elas combinem, de forma segura e através de um canal público, uma chave simétrica temporária. Uma vez que essa chave simétrica única é estabelecida por meio do processo assimétrico, o sistema altera o modo de operação para a criptografia simétrica (utilizando cifras em bloco ou fluxo), garantindo assim a velocidade necessária para a transmissão contínua dos dados cotidianos.

### O hash criptográfico

O hash criptográfico é uma função matemática unidirecional que recebe um volume de dados de qualquer tamanho como entrada e o transforma em uma sequência de caracteres de comprimento fixo, denominada resumo ou _digest_. Diferente dos algoritmos de cifragem, o hash não foi projetado para ser revertido; é computacionalmente inviável recuperar o dado original a partir do seu resumo.

Para ser considerado seguro, um hash precisa atender a critérios matemáticos rígidos.

- O primeiro deles é o determinismo, o que significa que o mesmo dado de entrada sempre gerará exatamente o mesmo hash. 

- O segundo é o efeito avalanche, onde a alteração de um único bit no arquivo original resulta em um hash completamente diferente e imprevisível. 

- Por fim, a função deve possuir alta resistência a colisões, garantindo que seja praticamente impossível encontrar dois arquivos distintos que produzam o mesmo resumo. 

Devido a essas características, o hash é amplamente utilizado para verificar a integridade de arquivos e sistemas, permitindo detectar imediatamente se um dado foi modificado durante o armazenamento ou o tráfego.

### Assinatura digital

A assinatura digital é um mecanismo criptográfico que associa a identidade de um remetente a um documento eletrônico, garantindo autenticidade, integridade e o não-repúdio. O processo baseia-se na combinação do hash criptográfico com a criptografia assimétrica.

Para assinar um documento, o sistema do remetente calcula primeiramente o hash do arquivo. Em seguida, esse hash é cifrado utilizando a chave privada do remetente. O resultado dessa cifragem é a assinatura digital, que é anexada ao documento enviado. Ao receber o arquivo, o destinatário realiza o processo de verificação: calcula de forma independente o hash do documento recebido e, simultaneamente, utiliza a chave pública do remetente para decifrar a assinatura digital, recuperando o hash original.

Se os dois hashes forem idênticos, o destinatário tem a confirmação matemática de que o documento não foi alterado (integridade) e de que ele foi emitido pelo dono daquela chave privada (autenticidade). O não-repúdio decorre do fato de que, como a chave privada é exclusiva do proprietário, ele não pode negar a autoria da assinatura.

### Certificado digital

Embora a assinatura digital comprove que uma mensagem foi assinada por uma determinada chave privada, ela não resolve o problema de identidade no ambiente digital. Resta a dúvida sobre a quem pertence, de fato, a chave pública correspondente. O certificado digital soluciona essa vulnerabilidade, funcionando como uma identidade ou passaporte eletrônico emitido por uma entidade confiável.

O certificado digital é um documento eletrônico assinado por uma Autoridade Certificadora (CA). Ele vincula formalmente uma entidade (uma pessoa, uma empresa ou um servidor web) a um par de chaves criptográficas. A estrutura de um certificado segue padrões internacionais rígidos, contendo informações como o nome do titular, o período de validade, o nome da Autoridade Certificadora que o emitiu, o número de série e, principalmente, a chave pública do titular. 

Quando um navegador se conecta a um site seguro, o servidor apresenta seu certificado digital. O navegador valida a assinatura da Autoridade Certificadora contida no certificado utilizando as chaves das CAs confiáveis pré-instaladas no sistema operacional. Uma vez validado o certificado, estabelece-se a confiança de que a chave pública apresentada pertence legitimamente àquela entidade, permitindo o início de uma comunicação segura e autenticada.