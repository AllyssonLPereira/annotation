---
tags:
  - arquivo
---
### Man-in-the-Middle e Ataques Man-in-the-Mobile

Os invasores podem interceptar ou modificar as comunicações entre dois dispositivos para roubar informações ou se passar por um dos dispositivos.


- ##### Man-in-the-Middle

	Um ataque MitM, também conhecido como ***[ataque no caminho]***, ocorre quando um cibercriminoso assume o ***[controle de um dispositivo intermediário]*** sem o conhecimento do usuário. Com esse nível de acesso, um invasor pode interceptar, manipular e retransmitir informações falsas entre o remetente e o destino pretendido.


- ##### Man-in-the-Mobile (MitMo)

	Uma variação do man-in-the-middle, o MitMo é um tipo de ataque usado para ***[assumir o controle do dispositivo móvel de um usuário]***. Quando infectado, o dispositivo móvel é instruído a capturar informações confidenciais do usuário e enviá-las aos invasores.

	O ZeuS é um exemplo de pacote de malware com recursos MitMo. Ele permite que os invasores capturem silenciosamente as mensagens SMS de verificação em duas etapas enviadas aos usuários.

---
### Pontos de acesso não autorizados

Um access point não autorizado é um access point sem fio instalado em uma rede segura sem autorização explícita. 

Embora possa ser configurado por um funcionário bem-intencionado que procura uma conexão sem fio melhor, ele também apresenta uma oportunidade para os invasores que desejam obter acesso à rede de uma empresa.

Um invasor geralmente usa táticas de engenharia social para obter acesso físico à infraestrutura de rede de uma empresa e instalar o **access point não autorizado**.

Também conhecido como access point de criminosos, ***[o access point pode ser configurado como um dispositivo MitM para capturar suas informações de login].

Isso funciona desconectando o access point não autorizado, que aciona a rede para enviar um quadro de autenticação e desassociar o access point. Esse processo é então explorado falsificando seu endereço MAC e enviando uma transmissão de dados de autenticação para o access point sem fio.


![[acess_point_mint.png]]


Um **[ataque evil twin (gêmeos do mal)]** descreve uma situação em que o access point do invasor é configurado para parecer uma opção de conexão melhor. Depois de se conectar ao ponto de acesso maligno, o invasor pode analisar o tráfego da rede e executar ataques MitM.


![[evil_twinl.png]]



