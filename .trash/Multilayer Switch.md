
## Switches de Camada 3

Até agora, tratamos os switches estritamente como dispositivos de Camada 2, ou seja, equipamentos que tomam decisões de encaminhamento baseadas apenas em endereços MAC e ignoram completamente os pacotes IP. No entanto, o avanço das arquiteturas de rede trouxe os **switches de Camada 3**, também conhecidos como **switches multi-layer**. 

Esses ativos unem o melhor dos dois mundos: eles mantêm a capacidade de comutar quadros em altíssima velocidade nas portas locais e ganham a inteligência de analisar cabeçalhos de rede e processar tabelas de roteamento, funcionando como se houvesse um roteador embutido diretamente em seu chassi de hardware.

A grande vantagem dessa arquitetura consolidada fica clara quando comparamos seu desempenho com o modelo Router-on-a-Stick. No cenário com roteador dedicado, todo o tráfego inter-VLAN precisa obrigatoriamente sair do switch, subir pelo link físico de tronco, ser processado no roteador e retornar pelo mesmo caminho para o switch antes de chegar ao destino. 

Esse vaivém de pacotes cria um gargalo natural na infraestrutura e abre espaço para congestionamentos severos. Com um switch de camada 3 posicionado no núcleo da rede, o roteamento entre as sub-redes acontece internamente no próprio equipamento através de circuitos integrados de aplicação específica (ASICs), o que elimina a dependência de links externos e garante uma comunicação extremamente veloz entre os setores da empresa.

## SVI - Switch Virtual Interface

Para viabilizar esse roteamento interno sem depender de cabos conectados a interfaces físicas distintas, o switch multi-layer utiliza as chamadas **Interfaces Virtuais de Switch (SVIs)**. 

Trata-se de interfaces puramente lógicas, criadas no próprio software do equipamento e associadas diretamente a uma determinada VLAN. Quando uma SVI recebe a configuração de um endereço IP, ela passa a atuar formalmente como o **gateway padrão** de todos os computadores pertencentes àquela rede virtual, recebendo o tráfego local e decidindo o destino do pacote de forma transparente para o usuário final.

> **Nota:** Diferente de uma interface física que se ativa mecanicamente assim que um cabo funcional é plugado, uma interface virtual depende de uma série de validações lógicas do sistema operacional para alcançar o status operacional ativo, conhecido tecnicamente como estado _up/up_.

Para que uma SVI mude para o estado ativo e comece a rotear os pacotes, o sistema operacional do switch exige o cumprimento simultâneo de regras bem específicas. 

- A primeira exigência é que a VLAN correspondente à SVI tenha sido previamente criada no banco de dados do switch, pois a criação de uma interface virtual não gera automaticamente a VLAN de suporte. 

- A segunda condição obriga a existência de pelo menos uma porta física ativa no switch associada a essa VLAN; essa porta pode ser uma interface de acesso com um computador ligado ou uma porta de tronco operacional que permita explicitamente a passagem daquela VLAN.

- As duas últimas validações estão ligadas ao estado administrativo dos recursos dentro do equipamento. O administrador precisa garantir que a VLAN em si não tenha sido desativada administrativamente no sistema, uma condição que congelaria qualquer comunicação lógica associada a ela.

- Por fim, como as SVIs são criadas de fábrica configuradas em modo de desativação padrão para proteção do equipamento, é obrigatório ordenar explicitamente a ativação administrativa da própria interface virtual através dos comandos do sistema operacional. 

Se qualquer um desses requisitos lógicos falhar, a SVI permanecerá listada em estado inativo, interrompendo o roteamento daquela sub-rede.