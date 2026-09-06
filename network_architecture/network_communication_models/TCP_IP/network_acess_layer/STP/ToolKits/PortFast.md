
O PortFast permite que portas de switch conectadas a hosts finais entrem imediatamente no estado de Forwarding (Encaminhamento) do STP, ignorando os estados de listening e learning. 

Isso permite que os hosts comecem a se comunicar pela rede assim que se conectam – sem necessidade de esperar. 

## PortFast – o problema

Primeiramente, qual é exatamente o problema que o PortFast resolve? Vamos conectar este PC e o switch para descobrir. Quando um host final se conecta a uma porta de switch como esta, a porta fica no estado "up/up", mas ainda não consegue enviar ou receber dados.

Por "up/up", refiro-me ao status da porta no comando `SHOW IP INTERFACE BRIEF`, como você pode ver aqui. A interface G0/1 do switch está "up/up", mas quaisquer quadros que o PC tente enviar são descartados pelo switch.

E por que isso acontece? Bem, é uma porta designada pelo STP, mas levará um total de 30 segundos até entrar no estado de encaminhamento (*forwarding*). São 15 segundos no estado de escuta (*listening*) e 15 segundos no estado de aprendizado (*learning*). 

Isso resulta em uma experiência ruim para o usuário. O usuário espera conseguir acessar a rede imediatamente, mas, por algum motivo, não funciona. Provavelmente, o usuário nem sabe que o STP existe. Eles não têm motivo algum para saber disso.

Eles apenas sabem que "a internet não funciona" por 30 segundos quando conectam o computador. E isso é frustrante. E o pior de tudo: essa espera é totalmente desnecessária, pois não há risco de ocorrer um loop de Camada 2 entre um switch e um PC. 

Loops podem ocorrer entre switches devido à forma como eles propagam (*flood*) quadros, mas PCs não fazem isso.

Agora que vimos o problema, vamos ver como o PortFast o resolve. Mais uma vez, vou conectar este PC ao switch. Quando o PortFast está configurado em uma porta, ela entra imediatamente no estado de encaminhamento (Forwarding) ao ser conectada a outro dispositivo – ou seja, quando a porta é ativada.

Assim, ela ignora os estados de escuta (listening) e aprendizado (learning), podendo enviar e receber dados imediatamente, sem esperar 30 segundos. Isso, obviamente, proporciona uma experiência de usuário muito melhor: o dispositivo do usuário consegue acessar a rede imediatamente.

## Configuração do PortFast

Então, como podemos configurar o PortFast? É bem simples, mas existem duas maneiras de fazer isso.

A primeira é no modo de configuração de interface, com o comando `SPANNING-TREE PORTFAST`. Isso ativa o PortFast apenas na interface individual: aquela em que você configurou esse comando.

Mas você também pode ativá-lo no modo de configuração global com o comando `SPANNING-TREE PORTFAST DEFAULT`. Em vez de ativar o PortFast em uma porta específica, isso ativa o PortFast em todas as portas de acesso. 

Na maioria dos casos, usso ativará o PortFast em todas as conexões com hosts finais, mas não nas conexões com outros switches. Isso ocorre porque as conexões entre switches são quase sempre links de tronco (trunk links), já que a maioria das LANs modernas utiliza múltiplas VLANs. 

Mas as conexões com hosts finais são quase sempre links de acesso, já que a maioria dos hosts não precisa enviar e receber tráfego em múltiplas VLANs. 

Como veremos em um instante, é muito importante que você não habilite PortFast em portas que se conectam a outros switches.

### Configuração do PortFast: por porta

Vamos testar aquele primeiro método na CLI. Entrei no modo de configuração de interface para a G0/1 e usei o comando `SPANNING-TREE PORTFAST` para habilitar o PortFast. 

Ao habilitar o PortFast, você verá esta mensagem de aviso. Isso está relacionado ao ponto que mencionei no slide anterior, então vou lê-la: “O PortFast deve ser habilitado apenas em portas conectadas a um único host. Conectar hubs, concentradores, switches, bridges, etc., a esta interface com o PortFast habilitado pode causar loops de bridge temporários. Use com CUIDADO”. 

Basicamente, isso significa que o PortFast não deve ser configurado em portas conectadas a switches, caso contrário, podem ocorrer loops temporários de Camada 2.

O objetivo principal dos estados de *listening* (escuta) e *learning* (aprendizado) é garantir 100% que não haja loops na LAN antes que uma porta mude para o estado de *forwarding* (encaminhamento). 

Como o PortFast ignora esses estados e faz com que a porta inicie diretamente no estado de *forwarding*, ele pode causar um loop temporário se for habilitado em conexões com outros switches. Portanto, lembre-se de que o PortFast não deve ser habilitado em portas que se conectam a outros switches.

Certo, além desse aviso, outra mensagem é exibida aqui: "O PortFast foi configurado na GigabitEthernet0/1, mas só terá efeito quando a interface estiver em um modo que não seja *trunk*”.

Assim, mesmo que você configure o `SPANNING-TREE PORTFAST` em uma porta *trunk*, ele não ficará ativo. Por padrão, ele funciona apenas em portas de acesso.

Certo, após configurar o PortFast na porta, usei o comando `SHOW SPANNING-TREE INTERFACE G0/1 DETAIL` para confirmar. Aqui está a sintaxe do comando: `SHOW SPANNING-TREE INTERFACE`, seguido pelo nome da interface e, depois, `DETAIL`. 

E aqui está a saída do comando. Observe a linha que destaquei: "A porta está no modo PortFast edge". Isso requer uma breve explicação.

Existem dois tipos de PortFast: *edge* e *network*. 

O PortFast *edge* é o tipo que estamos abordando neste vídeo. O PortFast *network* é usado para um recurso chamado Bridge Assurance, que não é um tópico do CCNA. Portanto, não se preocupe com isso. 

Eu só queria esclarecer o significado de "*edge*" nesta saída.

### Configuração do PortFast: padrão

A seguir, vamos experimentar o segundo método de configuração: habilitar o PortFast como padrão no modo de configuração global.

Ampliei um pouco o exemplo de rede. Os switches SW1 e SW2 estão conectados pelas portas G0/0 e G0/1, que são portas *trunk*, enquanto as portas G0/2 e G0/3 estão conectadas a hosts, sendo, portanto, portas de acesso. 

Estou mostrando apenas a CLI do SW1 aqui, mas configurei `SPANNING-TREE PORTFAST DEFAULT` em ambos os switches. Assim como antes, uma mensagem de aviso aparece. Vamos lê-la: "%Warning: este comando habilita o PortFast como padrão em todas as interfaces. Você deve agora desabilitar o PortFast explicitamente em portas conectadas a hubs, switches e bridges, pois elas podem criar loops de bridge temporários".

Deixe-me esclarecer a parte que destaquei. O texto diz "todas as interfaces", mas, como mencionei anteriormente, ele ativa o PortFast apenas em todas as portas de acesso, não nas portas *trunk*.

Portanto, essa mensagem de aviso pode ser um pouco enganosa. Agora, se você quiser desabilitar o PortFast em uma porta de acesso específica após tê-lo habilitado por padrão, pode usar o comando `SPANNING-TREE PORTFAST DISABLE` no modo de configuração de interface.

Você deve fazer isso se conectar dois switches com um link de acesso, mas isso é raro: conexões entre switches geralmente são trunks. 

Certo, aqui está aquele mesmo comando que usei antes, analisando a saída para a interface G0/2 do SW1, uma porta de acesso. Ela indica que "a porta está no modo portfast edge por padrão". 

Portanto, o PortFast foi habilitado nessas quatro portas, as portas de acesso conectadas a hosts finais. E quanto aos trunks que conectam os switches? Usei o mesmo comando para a interface G0/1 do SW1, e ele não menciona o PortFast em lugar nenhum. 

Logo, o PortFast não está habilitado nas portas trunk. O ponto principal a lembrar aqui é que, quando você habilita o PortFast no modo de configuração global, ele é ativado apenas em portas de acesso, não em portas trunk.

## PortFast em portas trunk

Já vimos como configurar o PortFast em portas de acesso. Agora vamos abordar o tópico do PortFast em portas trunk, pois existem situações em que isso é válido.

Os comandos padrão de configuração do PortFast habilitam o recurso apenas em portas de acesso. Esses são os comandos que acabamos de ver: `SPANNING-TREE PORTFAST` no modo de configuração de interface e `SPANNING-TREE PORTFAST DEFAULT` no modo de configuração global. 

Mas, em alguns casos, você pode querer habilitar o PortFast em uma porta trunk.

O diagrama de rede acima mostra dois exemplos. O primeiro é uma porta conectada a um servidor de virtualização com máquinas virtuais (VMs) em VLANs diferentes. 

A virtualização é um tópico do CCNA, mas vamos abordá-la mais adiante no curso. Por enquanto, saiba apenas que servidores que utilizam virtualização frequentemente usam links de tronco para se conectar a switches, em vez de links de acesso como a maioria dos hosts finais. 

E o segundo exemplo é uma porta conectada a um roteador via *router-on-a-stick*. Como vimos na seção do curso sobre VLANs, o *router-on-a-stick* é basicamente um link *trunk* entre um switch e um roteador. 

Um roteador não faz *flooding* de quadros como um switch e não causará loops de Camada 2. Portanto, você pode configurar o PortFast em interfaces conectadas a um roteador dessa forma. 

Então, como configuramos o PortFast em um *trunk*?

Ele só pode ser configurado por porta, no modo de configuração de interface. O comando é `SPANNING-TREE PORTFAST TRUNK`. 

Vamos ver um exemplo na CLI. O comando exibe a mesma mensagem que vimos anteriormente, alertando que o PortFast não deve ser habilitado em portas conectadas a switches.

E aqui está o comando `SHOW SPANNING-TREE INTERFACE DETAIL`, mostrando apenas a linha relevante, já que não há espaço suficiente. Ele indica: "A porta está no modo *portfast edge trunk*".

Na maioria dos cenários do CCNA, você só precisará habilitar o PortFast em portas de acesso, mas lembre-se de que ele também pode ser habilitado em portas *trunk*.

## PortFast edge

Por fim, antes de encerrarmos, quero esclarecer brevemente o conceito de "PortFast edge", que mencionei anteriormente. 

Para recapitular, existem dois modos de PortFast: PortFast edge e PortFast network. O PortFast network não é um tópico do CCNA, então abordaremos apenas o PortFast edge.

Nos switches Cisco modernos, se você utilizar os comandos abordados nesta aula, o dispositivo adicionará automaticamente a palavra-chave `EDGE` à configuração. 

Então, por exemplo, se você configurar `SPANNING-TREE PORTFAST` em uma porta, na *running-config* (configuração em execução), isso se tornará `SPANNING-TREE PORTFAST EDGE`. 

Se você configurar `SPANNING-TREE PORTFAST TRUNK`, isso se tornará `SPANNING-TREE PORTFAST EDGE TRUNK`. 

E se você configurar `SPANNING-TREE PORTFAST DEFAULT`, isso se tornará `SPANNING-TREE PORTFAST EDGE DEFAULT` na *running-config*.

Você pode usar qualquer uma das versões dos comandos ao configurar o PortFast; não importa. O resultado final é o mesmo: EDGE sempre será adicionado à configuração.

Como você provavelmente imaginou, se quiser configurar o PortFast como *network* (rede) em vez de *edge* (borda), você precisa especificar a palavra-chave `NETWORK` nos comandos, como `SPANNING-TREE PORTFAST NETWORK`. 

Eu também mencionei o comando SPANNING-TREE PORTFAST DISABLE anteriormente, mas observe que ele não usa
12:25
a palavra-chave EDGE. É uma exceção. Certo, vamos verificar a palavra-chave EDGE na CLI. Eu configurei
12:32
SPANNING-TREE PORTFAST na interface G0/1 do SW1. Em seguida, usei SHOW RUNNING-CONFIG INTERFACE G0/1. Esse
12:41
é um comando útil. Você pode usá-lo para visualizar a *running-config* apenas da interface especificada,
12:46
em vez de toda a *running-config* do dispositivo. Mas, infelizmente, ele não funciona no Packet Tracer.
12:53
De qualquer forma, aqui está a configuração da interface. Observe que o switch adicionou automaticamente a palavra-chave EDGE ao
12:59
final do comando, embora eu tenha configurado apenas SPANNING-TREE PORTFAST. Certo,
13:04
para resumir, saiba que o tipo de PortFast abordado no CCNA,
13:09
aquele de que falamos neste vídeo, chama-se PortFast Edge. Para o exame CCNA, você
13:15
provavelmente deve conhecer as duas versões desses comandos: com e sem o termo EDGE. O efeito deles é
13:20
o mesmo. Mas lembre-se de que, se você estiver fazendo laboratórios no Packet Tracer, a versão atual não
13:26
suporta a palavra-chave EDGE. Portanto, não se confunda se tentar usar no Packet Tracer e não funcionar.
Resumo
13:33
Aqui está um resumo dos pontos principais abordados neste vídeo. Quando um host se conecta a uma porta de switch,
13:39
por padrão, leva-se 30 segundos até que a porta possa enviar ou receber dados. E isso pode
13:43
ser frustrante para os usuários, que não sabem por que não conseguem se conectar. O PortFast permite que uma porta
13:48
de switch entre imediatamente no estado de encaminhamento (forwarding) do STP, ignorando os estados de escuta (listening) e aprendizado (learning). Assim,
13:54
o host conectado pode acessar a rede imediatamente, proporcionando uma experiência muito melhor para o
13:59
usuário. O PortFast pode ser configurado de duas maneiras. A primeira é no modo de configuração de interface, com o
14:05
comando SPANNING-TREE PORTFAST, opcionalmente com a palavra-chave EDGE. Isso habilita o PortFast
14:11
apenas na interface específica, e ele só fica ativo quando a interface está no modo de acesso (access mode),
14:16
e não no modo tronco (trunk mode). A segunda opção é no modo de configuração global, com o comando SPANNING-TREE PORTFAST DEFAULT,
14:23
que habilita o PortFast em todas as portas de acesso. Se necessário, você pode desativá-lo em portas
14:29
específicas usando o comando SPANNING-TREE PORTFAST DISABLE. Lembre-se apenas de que o PortFast não deve ser configurado
14:35
em portas conectadas a um switch, pois isso pode causar loops temporários. Ele deve ser usado apenas em portas
14:41
conectadas a hosts finais ou, talvez, a um roteador. E tenha em mente que você também pode configurar o PortFast
14:47
em uma porta de tronco (trunk) usando o comando SPANNING-TREE PORTFAST TRUNK. Isso pode ser útil para topologias "router-on-a-stick"
14:53
ou ao conectar-se a um servidor de virtualização com VMs em diferentes VLANs diferentes. 