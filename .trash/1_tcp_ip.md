---
tags:
  - arquivo
---
Há dois tipos básicos de modelos para descrever as funções que devem ocorrer para que as comunicações de rede sejam bem-sucedidas: [modelos de protocolo] e [modelos de referência].

- **[Modelo de protocolo]**
	
	Este modelo corresponde muito bem à estrutura de um conjunto específico de protocolos. Um conjunto de protocolos inclui o conjunto de protocolos relacionados que normalmente fornecem toda a funcionalidade necessária para as pessoas se comunicarem com a rede de dados. 

	O modelo TCP/IP é um modelo de protocolo porque descreve as funções que ocorrem em cada camada de protocolos dentro da suíte TCP/IP.


Resumidamente, o modelo é o que podemos chamar de uma “solução prática para problemas de transmissão de dados”.

Os modelos em camadas ajudam a visualizar o funcionamento conjunto dos diversos protocolos para possibilitar comunicações de rede. 

Um modelo de camadas representa a operação dos protocolos ocorrendo dentro de cada camada, bem como a interação com as camadas acima e abaixo dela. O modelo em camadas tem muitas vantagens:

- Auxilia no projeto de protocolos, porque os protocolos que operam em uma camada específica possuem informações definidas sobre as quais atuam e uma interface definida para as camadas acima e abaixo.

- Estimula a competição porque os produtos de diferentes fornecedores podem trabalhar em conjunto.

- Permite que ocorram mudanças tecnológicas em um nível sem que outros níveis sejam afetados.

- Fornece uma linguagem comum para descrever funções e habilidades de rede.

O primeiro modelo em camadas para comunicações internetwork foi criado no início dos anos 1970 e é conhecido como [modelo de Internet]. Ele define quatro categorias de funções que devem ocorrer para que a comunicação seja bem sucedida. 

A suite de protocolos TCP/IP que é usada para comunicações na Internet segue a estrutura deste modelo, conforme mostrado na tabela. Por causa disso, [o modelo de Internet é comumente chamado de modelo TCP/IP].

| Camada do modelo TCP/IP | Descrição                                                                      |
| ----------------------- | ------------------------------------------------------------------------------ |
| Aplicação               | Representa dados para o usuário, além da codificação e do controle de diálogo. |
| Transporte              | Permite a comunicação entre vários dispositivos diferentes em redes distintas. |
| Internet                | Determina o melhor caminho pela rede.                                          |
| Acesso à rede           | Controla os dispositivos de hardware e o meio físico que formam a rede.        |

---

![[tcp_ip_protocols.png]]

---
### Camada de aplicação

A camada de aplicação é responsável pelos [programas e protocolos que possibilitam o TCP/IP dar início a transmissão de dados].

Assim, essa camada serve para que o TCP/IP determine qual a finalidade específica da transmissão de dados. Após a definição do [tipo de transmissão], o processo é enviado para as próximas camadas.

Alguns exemplos de protocolos que podem ser utilizados são o HTTP e o HTTPS em navegadores web para a comunicação por meio das URLs; o protocolo FTP em clientes de transferência de arquivos; o protocolo SMTP em serviços de email; entre outros.

---
### Camada de Transporte

A camada de transporte [estabelece como os dados serão transmitidos na rede], levando em consideração o uso, prioridade e criticidade do conteúdo trafegado.

Essa camada é composta pelo protocolo TCP, que oferece uma comunicação confiável orientada à conexão. Porém, outros protocolos também podem ser usados, como o UDP (Protocolo de Datagrama de Usuário) que é mais simples e cuja comunicação fornecida não é confiável e adequada para aplicações que toleram perda de dados.

Nessa camada são estabelecidos [canais de comunicação de transferência de dados], que são independentes dos hosts e asseguram a transmissão de forma íntegra de todos os bytes desses dados.

Além disso, [na camada de transporte os dados são separados em pacotes e numerados]. Dessa forma, a garantia de que o processo será bem sucedido ocorre por meio da verificação da sequência lógica criada.

Essa camada também é responsável por definir para onde os dados devem ser enviados e qual a taxa de transferência para isso.

São utilizadas portas para a realização desse processo. As portas especificam de forma numérica quais são os pontos de uma transferência de dados.

---
### Camada de Rede

A camada de rede também é conhecida como [camada de Internet]. É responsável pelo [roteamento dos pacotes de dados entre os dispositivos em diferentes redes].

Mas o que isso significa? Na prática, essa camada cuida das interfaces dos hosts e faz a [transformação dos pacotes de dados em datagramas].

Cada datagrama é composto de dois elementos principais: um header (cabeçalho) que entre alguns dados, inclui os endereços IP da origem e destino, e a carga útil (payload) que traz os dados em si que estão sendo transmitidos.

Essa camada utiliza o protocolo IP para proporcionar endereçamento único, roteamento eficiente e outros serviços necessários para o encaminhamento bem sucedido dos pacotes de dados em uma rede.

---
### Camada de enlace

A camada de enlace também conhecida por [camada de interface], é responsável pela [transferência dos dados a nível físico], cuidando de aspectos como endereçamento físico, controle de acesso ao meio e detecção de erros a nível de enlace.

As camadas do TCP/IP trabalham juntas de forma colaborativa visando uma comunicação eficiente e confiável em redes de computadores.

![A imagem tem o título TCP/IP. Abaixo dele há o nome das camadas e uma seta associando-as a uma descrição. De cima pra baixo,  “Camada de Transporte: Define como os dados serão transmitidos”, “Camada de Redes: faz o roteamento de pacotes de dados” e “Camada de Enlace: Realiza a transmissão de dados a nível físico”.](https://www.alura.com.br/artigos/assets/rede-de-computadores/tcp-ip.png)

A comunicação entre as camadas do TCP/IP acontece por meio de interfaces bem definidas. Cada camada recebe serviços da camada imediatamente acima dela e fornece serviços à camada imediatamente abaixo.

Nesse modelo o **encapsulamento** é um conceito essencial, no qual os dados são empacotados na camada que os transmite e desempacotados na recepção.

![Na imagem temos duas colunas: a primeira coluna à direita que representa a origem dos dados (quem envia) e a segunda coluna que representa o receptor. Em ambas as colunas temos de cima para baixo as camadas de aplicação, transporte, rede e enlace. As colunas se conectam por meio de uma seta abaixo delas. Na primeira coluna temos setas de cima para baixo que conectam as camadas e um texto que diz “Dados sendo empacotados e passados para a camada inferior”. Na segunda coluna temos setas de baixo para cima que conectam as camadas e um texto que diz “Dados sendo desempacotados e passados para a camada superior”.](https://www.alura.com.br/artigos/assets/rede-de-computadores/origem-dos-dados.png)

___
### Referências

https://joaomarcuraa.medium.com/o-protocolo-tcp-ip-1dc2cdb88b07
https://www.alura.com.br/artigos/rede-de-computadores
https://www.hostinger.com.br/tutoriais/tcp-ip