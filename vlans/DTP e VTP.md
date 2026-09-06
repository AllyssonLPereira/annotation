
## DTP - Dynamic Trunking Protocol

O **Dynamic Trunking Protocol**, ou simplesmente DTP, foi criado com o objetivo principal de automatizar a configuração das portas dos switches. Em uma rede tradicional, o administrador precisa decidir e configurar manualmente se cada interface vai se conectar a um computador ou a outro switch. 

O DTP elimina essa necessidade inicial operando como um protocolo de plug-and-play na Camada 2. Assim que você conecta um cabo ligando dois switches, eles começam a trocar mensagens em segundo plano para negociar se aquele link deve se tornar um tronco ou uma porta de acesso, sem que nenhum comando precise ser digitado para isso acontecer.

Apesar de parecer uma facilidade excelente para o dia a dia, esse comportamento automatizado traz um problema grave de segurança para o ambiente corporativo. 

Se uma porta de switch está aberta para negociar seu estado de forma dinâmica, qualquer pessoa com más intenções pode se aproveitar disso. Um atacante pode desconectar o computador de uma mesa, plugar o seu próprio notebook e usar um software específico para fingir que é um switch.

O switch legítimo da empresa cai na armadilha do DTP, transforma aquela porta comum em um link de tronco e passa a enviar o tráfego de todas as VLANs da empresa para o computador do invasor. Esse ataque é conhecido como **VLAN Hopping** ou falsificação de tronco, e é o motivo pelo qual a recomendação absoluta no mercado atual é desativar completamente o DTP em redes reais.

## Estados Administrativos VS Estados Operacionais

Para compreender a lógica de funcionamento do DTP, é fundamental separar a intenção do administrador do resultado real na porta. O que você configura na interface é chamado de **estado administrativo**, enquanto o modo como a porta realmente passa a trabalhar depois da negociação é o **estado operacional**. O protocolo se baseia essencialmente em dois perfis de comportamento para tentar adivinhar o que está conectado na outra ponta do cabo, chamados de _Dynamic Desirable_ e _Dynamic Auto_.

O modo **Dynamic Desirable** representa o comportamento proativo dentro da rede. Uma porta configurada assim toma a iniciativa de enviar quadros DTP de forma contínua, basicamente dizendo para o vizinho que quer muito formar um tronco e perguntando se o outro lado aceita o convite. 

Já o modo **Dynamic Auto** adota uma postura totalmente passiva. Uma interface em modo Auto não gasta recursos enviando propostas e apenas fica escutando o cabo. Se ninguém falar com ela, ela opera como uma porta de acesso comum, mas se o vizinho enviar um convite de tronco, ela aceita imediatamente.

Quando juntamos esses comportamentos nas duas pontas de um cabo, o resultado operacional segue uma lógica previsível.

- Se conectarmos uma porta em modo Desirable com outra também em Desirable, ambas querem o tronco ativamente, então o link se torna um **Tronco**. 

- Se juntarmos Desirable com Auto, o lado proativo faz o pedido e o lado passivo aceita, gerando também um link de **Tronco**.

- O grande problema acontece quando conectamos Auto com Auto. Como as duas pontas são passivas e ficam apenas esperando uma iniciativa mútua, nenhuma delas envia o primeiro quadro DTP, a negociação falha por inércia e o link vira uma porta de **Acesso** simples, o que geralmente quebra a comunicação esperada entre os switches.

### Conexões Fixas, Roteadores e o Erro de Mismatch

A negociação dinâmica também interage com portas configuradas manualmente pelo administrador. Se você travar uma ponta como tronco fixo, ela ainda enviará mensagens DTP por padrão, o que significa que o outro lado mudará para tronco se estiver em modo Auto ou Desirable.

Contudo, dispositivos como computadores e roteadores não entendem o protocolo DTP. Na arquitetura _Router-on-a-Stick_, por exemplo, o switch jamais conseguirá negociar um tronco sozinho com o roteador, tornando obrigatória a configuração manual e fixa daquela porta.

> **Nota sobre Falhas Críticas:** Se houver um erro humano e um administrador travar uma ponta do cabo como tronco fixo e a outra ponta como acesso fixo, a negociação do DTP é totalmente ignorada porque as configurações manuais têm prioridade. Isso gera um erro crítico de incompatibilidade conhecido como **mismatch**, onde os dados de uma VLAN acabam sendo descartados ou entregues na rede errada, paralisando o tráfego daquele link.

## O Propósito do VTP e a Sincronização Lógica

O **VLAN Trunking Protocol**, conhecido como VTP, é outro protocolo proprietário criado para resolver um problema de escala na gerência de redes. Quando uma empresa cresce e passa a ter dezenas de switches espalhados pelos blocos e andares, criar manualmente as mesmas VLANs em cada um desses equipamentos se torna uma tarefa demorada e muito sujeita a erros humanos. 

O VTP resolve isso permitindo que você configure as VLANs em um único switch central, que atuará como uma matriz, e essa tabela de redes virtuais seja replicada automaticamente para todos os outros switches interconectados por links de tronco.

É importante destacar que o VTP sincroniza apenas a existência e os nomes das VLANs, mas ele nunca distribui a atribuição das portas locais, o que significa que definir qual tomada pertence a qual VLAN ainda continua sendo uma tarefa individual de cada switch.

O coração do mecanismo de sincronização do VTP é um contador interno chamado **número de revisão de configuração**. Esse número começa em zero e funciona essencialmente como o indicador de versão do banco de dados de VLANs da rede.

Toda vez que um administrador cria uma nova VLAN, altera o nome de uma rede existente ou deleta um setor dentro do switch principal, esse contador avança uma unidade. 

Os switches da rede usam esse número para determinar qual informação é a mais recente; se um switch recebe um aviso do VTP contendo um número de revisão maior do que o número que ele possui guardado em sua própria memória, ele entende que sua tabela local está desatualizada e substitui imediatamente todos os seus dados lógicos pelas novas informações recebidas.

## Os Três Modos de Operação do VTP

Para que a propagação de dados ocorra de forma organizada, cada switch na topologia precisa assumir um papel específico, definido por três modos lógicos de operação conhecidos como Servidor, Cliente e Transparente.

### O Modo Servidor

O modo **VTP Server** é o comportamento padrão de fábrica de qualquer switch. Os switches configurados nesse modo possuem autoridade total sobre o domínio de rede, permitindo que o administrador crie, modifique e apague VLANs livremente por meio do sistema operacional. 

Toda alteração feita em um servidor altera o número de revisão e dispara anúncios atualizados através das portas de tronco. Além disso, as informações lógicas de um servidor são salvas em sua memória não-volátil, garantindo que a tabela de VLANs não se apague caso o equipamento sofra uma queda de energia ou seja reiniciado.

### O Modo Cliente

O modo **VTP Client** impõe uma postura de subordinação ao equipamento. Um switch operando como cliente fica proibido de fazer qualquer alteração local em seu banco de dados de VLANs; se um técnico tentar criar uma rede diretamente na linha de comando de um cliente, o sistema operacional rejeitará a ordem imediatamente. 

A única função do cliente é escutar as atualizações vindas dos servidores, ajustar sua própria tabela para ficar idêntica à do switch mestre e repassar esses mesmos anúncios para os próximos switches da fila. Em versões legadas do protocolo, os clientes não salvam essa tabela na memória permanente, dependendo de uma nova carga de dados vinda do servidor toda vez que são ligados.

### O Modo Transparente

O modo **VTP Transparent** funciona como um isolador de gerência dentro da infraestrutura. Um switch em modo transparente não participa ativamente do processo de sincronização do domínio corporativo, mantendo um banco de dados de VLANs totalmente independente e isolado em sua própria memória permanente. 

O administrador pode criar e apagar VLANs localmente nesse switch sem que isso afete ninguém, e o switch ignorará completamente os pedidos de atualização vindos dos servidores externos.

Apesar de não aplicar as regras do domínio para si mesmo, o switch transparente possui a capacidade de receber os anúncios do VTP em uma porta de tronco e encaminhá-los intactos pelas suas outras portas de tronco, permitindo que os switches clientes localizados adiante na topologia continuem recebendo as atualizações do servidor central.

## O Perigo do VTP e a destruição da Rede

Embora o VTP ofereça uma grande comodidade na automação das tabelas de redes, ele esconde uma falha arquitetural severa que o tornou um protocolo perigoso e amplamente evitado em redes profissionais modernas. O problema reside no fato de que o protocolo confia cegamente no maior número de revisão, e um switch configurado como servidor também se comporta como um cliente se encontrar uma revisão mais alta do que a sua.

Se um técnico pegar um switch antigo que estava guardado no estoque e decidir reaproveitá-lo na rede principal sem os devidos cuidados, um desastre pode acontecer. 

Caso esse switch antigo possua o mesmo nome de domínio configurado no passado e, por coincidência, um número de revisão de configuração muito alto (por exemplo, revisão cinquenta, fruto de muitos testes antigos), o estrago estará feito assim que o cabo de tronco for conectado. 

O switch antigo enviará seus anúncios e todos os switches da rede de produção — incluindo o servidor principal que estava na revisão dez — vão olhar para aquele número cinquenta e concluir que aquela é a versão mais atual do banco de dados. Em fração de segundos, toda a rede corporativa apagará suas VLANs legítimas e adotará a tabela do switch antigo, o que resulta na desconexão imediata e catastrófica de todos os computadores, servidores e telefones da empresa.

Para evitar que esse colapso aconteça ao introduzir um switch seminovo na infraestrutura, o administrador precisa obrigatoriamente forçar o zeramento do número de revisão de configuração antes de conectar o equipamento aos links de tronco principais.

Existem duas formas conceituais de redefinir esse contador interno para zero no sistema operacional. A primeira é alterar temporariamente o nome do domínio VTP para um termo qualquer que não exista na rede e depois retornar para o nome correto. 

A segunda alternativa é mudar o modo de operação do switch para Transparente, uma ação que zera o contador instantaneamente devido ao isolamento do modo, e depois devolvê-lo para o modo Cliente ou Servidor conforme o planejamento da topologia. Devido à gravidade desse risco de parada total, a maioria das empresas atuais opta por desligar o recurso e gerenciar suas VLANs de forma estática ou por meio de softwares de orquestração modernos.