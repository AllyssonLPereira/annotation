## 1. Navegação, configuração e salvamento

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|enable|User EXEC|Entra no modo EXEC privilegiado, identificado pelo prompt `#`.|
|2|configure terminal|Privileged EXEC|Entra no modo de configuração global. Pode ser abreviado como `conf t`.|
|3|exit|Qualquer modo de configuração|Retorna um nível na hierarquia da CLI.|
|4|end|Qualquer modo de configuração|Retorna diretamente ao modo EXEC privilegiado.|
|5|do COMANDO|Modo de configuração|Executa um comando EXEC sem abandonar o modo de configuração.|
|6|show running-config|Privileged EXEC|Exibe a configuração atualmente ativa na memória RAM.|
|7|show startup-config|Privileged EXEC|Exibe a configuração salva na NVRAM e carregada durante a inicialização.|
|8|copy running-config startup-config|Privileged EXEC|Salva a configuração ativa na configuração de inicialização.|
|9|write memory|Privileged EXEC|Forma tradicional e abreviada de salvar a configuração ativa.|
|10|no COMANDO|Modo correspondente|Remove ou reverte o comando informado.|

---

## 2. Identificação e configuração básica do equipamento

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|hostname NOME|Global Configuration|Altera o nome do equipamento Cisco.|
|2|description TEXTO|Interface Configuration|Adiciona uma descrição administrativa à interface.|
|3|show version|Privileged EXEC|Exibe versão do IOS, modelo, uptime, memória e informações de inicialização.|
|4|show inventory|Privileged EXEC|Exibe informações sobre componentes físicos e números de série, quando suportado.|
|5|show cdp neighbors|Privileged EXEC|Mostra dispositivos Cisco diretamente conectados.|
|6|show cdp neighbors detail|Privileged EXEC|Apresenta detalhes dos vizinhos CDP, como IP, plataforma e porta remota.|

---

## 3. Configuração e verificação de interfaces

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|interface INTERFACE|Global Configuration|Seleciona uma interface específica para configuração.|
|2|interface range INTERVALO|Global Configuration|Seleciona várias interfaces para aplicar a mesma configuração.|
|3|description TEXTO|Interface Configuration|Descreve a finalidade da interface ou o dispositivo conectado.|
|4|shutdown|Interface Configuration|Desabilita administrativamente a interface.|
|5|no shutdown|Interface Configuration|Habilita administrativamente a interface.|
|6|speed 10|Interface Configuration|Configura a velocidade para 10 Mbps.|
|7|speed 100|Interface Configuration|Configura a velocidade para 100 Mbps.|
|8|speed 1000|Interface Configuration|Configura a velocidade para 1 Gbps, quando suportado.|
|9|speed auto|Interface Configuration|Habilita a autonegociação de velocidade.|
|10|no speed|Interface Configuration|Remove a configuração manual de velocidade.|
|11|duplex half|Interface Configuration|Configura a interface em half-duplex.|
|12|duplex full|Interface Configuration|Configura a interface em full-duplex.|
|13|duplex auto|Interface Configuration|Habilita a autonegociação de duplex.|
|14|no duplex|Interface Configuration|Remove a configuração manual de duplex.|
|15|show interfaces|Privileged EXEC|Exibe informações detalhadas de todas as interfaces.|
|16|show interfaces INTERFACE|Privileged EXEC|Exibe detalhes de uma interface específica.|
|17|show interfaces status|Privileged EXEC|Resume status, VLAN, duplex, velocidade e tipo das portas do switch.|
|18|show interfaces description|Privileged EXEC|Exibe interfaces, estados e descrições configuradas.|
|19|show interfaces counters errors|Privileged EXEC|Exibe contadores de erros das portas.|
|20|show ip interface brief|Privileged EXEC|Resume endereços IPv4, estado físico e protocolo das interfaces.|
|21|show ip interface|Privileged EXEC|Exibe detalhes dos recursos IPv4 habilitados nas interfaces.|

---

## 4. Endereçamento IPv4

| Ordem | Comando                                 | Modo de execução        | Finalidade                                              |
| ----- | --------------------------------------- | ----------------------- | ------------------------------------------------------- |
| 1     | interface INTERFACE                     | Global Configuration    | Seleciona a interface que receberá o endereço IPv4.     |
| 2     | ip address IP MÁSCARA                   | Interface Configuration | Configura endereço IPv4 e máscara na interface.         |
| 3     | no ip address                           | Interface Configuration | Remove o endereço IPv4 da interface.                    |
| 4     | show ip interface brief                 | Privileged EXEC         | Confirma o endereço e o estado da interface.            |
| 5     | show ip interface INTERFACE             | Privileged EXEC         | Exibe informações IPv4 detalhadas da interface.         |
| 6     | show running-config interface INTERFACE | Privileged EXEC         | Exibe a configuração ativa de uma interface específica. |
| 7     | ping IP                                 | User ou Privileged EXEC | Testa a comunicação IPv4 com o destino.                 |
| 8     | traceroute IP                           | Privileged EXEC         | Mostra os saltos de camada 3 até o destino.             |

---

## 5. Análise ARP e tabela MAC

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|show arp|Privileged EXEC|Exibe as associações conhecidas entre endereços IPv4 e MAC.|
|2|show ip arp|Privileged EXEC|Exibe a tabela ARP IPv4 do equipamento.|
|3|clear arp-cache|Privileged EXEC|Limpa entradas dinâmicas do cache ARP, conforme o IOS.|
|4|show mac address-table|Privileged EXEC|Exibe a tabela de endereços MAC do switch.|
|5|show mac address-table dynamic|Privileged EXEC|Exibe somente os endereços aprendidos dinamicamente.|
|6|show mac address-table address MAC|Privileged EXEC|Procura um endereço MAC específico.|
|7|show mac address-table interface INTERFACE|Privileged EXEC|Exibe os MACs aprendidos por uma interface.|
|8|show mac address-table vlan VLAN-ID|Privileged EXEC|Exibe os MACs aprendidos em uma VLAN específica.|
|9|clear mac address-table dynamic|Privileged EXEC|Remove todas as entradas MAC dinâmicas.|
|10|clear mac address-table dynamic address MAC|Privileged EXEC|Remove uma entrada MAC dinâmica específica.|
|11|clear mac address-table dynamic interface INTERFACE|Privileged EXEC|Remove os MACs aprendidos em uma interface.|

---

## 6. Criação de VLANs

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|vlan VLAN-ID|Global Configuration|Cria uma VLAN ou entra em sua configuração.|
|2|name NOME|VLAN Configuration|Atribui um nome à VLAN.|
|3|no vlan VLAN-ID|Global Configuration|Remove a VLAN do banco de VLANs.|
|4|show vlan brief|Privileged EXEC|Exibe VLANs, nomes, estados e portas associadas.|
|5|show vlan id VLAN-ID|Privileged EXEC|Exibe detalhes de uma VLAN específica.|

---

## 7. Portas de acesso

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|interface INTERFACE|Global Configuration|Seleciona a porta que será configurada.|
|2|switchport mode access|Interface Configuration|Define permanentemente a porta como access.|
|3|switchport access vlan VLAN-ID|Interface Configuration|Associa a porta à VLAN indicada.|
|4|show interfaces INTERFACE switchport|Privileged EXEC|Confirma o modo operacional e a VLAN de acesso.|
|5|show vlan brief|Privileged EXEC|Confirma em qual VLAN a porta aparece.|

---

## 8. Portas trunk 802.1Q

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|switchport trunk encapsulation dot1q|Interface Configuration|Seleciona IEEE 802.1Q em modelos que exigem a escolha do encapsulamento.|
|2|switchport mode trunk|Interface Configuration|Configura permanentemente a interface como trunk.|
|3|switchport trunk native vlan VLAN-ID|Interface Configuration|Define a VLAN nativa do trunk.|
|4|switchport trunk allowed vlan LISTA|Interface Configuration|Substitui a lista atual pelas VLANs especificadas.|
|5|switchport trunk allowed vlan add LISTA|Interface Configuration|Adiciona VLANs à lista atual.|
|6|switchport trunk allowed vlan remove LISTA|Interface Configuration|Remove VLANs específicas da lista.|
|7|switchport trunk allowed vlan all|Interface Configuration|Permite todas as VLANs.|
|8|switchport trunk allowed vlan none|Interface Configuration|Remove todas as VLANs da lista permitida.|
|9|switchport trunk allowed vlan except LISTA|Interface Configuration|Permite todas as VLANs, exceto as especificadas.|
|10|show interfaces trunk|Privileged EXEC|Exibe trunks ativos, VLAN nativa e VLANs permitidas.|
|11|show interfaces INTERFACE switchport|Privileged EXEC|Exibe os modos administrativo e operacional da interface.|

---

## 9. DTP, negociação dinâmica de trunk

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|switchport mode dynamic auto|Interface Configuration|Aguarda passivamente que o outro lado negocie o trunk.|
|2|switchport mode dynamic desirable|Interface Configuration|Tenta ativamente negociar um trunk.|
|3|switchport nonegotiate|Interface Configuration|Desabilita o envio de mensagens DTP.|
|4|show interfaces trunk|Privileged EXEC|Confirma se o trunk foi formado.|
|5|show interfaces INTERFACE switchport|Privileged EXEC|Compara modo administrativo e modo operacional.|

|Lado A|Lado B|Resultado|
|---|---|---|
|desirable|desirable|Forma trunk|
|desirable|auto|Forma trunk|
|auto|auto|Não forma trunk|
|trunk|trunk|Forma trunk manual|
|trunk com nonegotiate|trunk com nonegotiate|Forma trunk sem DTP|

---

## 10. Router-on-a-Stick

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|interface INTERFACE|Global Configuration|Seleciona e ativa a interface física do roteador.|
|2|no shutdown|Physical Interface Configuration|Ativa a interface física.|
|3|interface INTERFACE.SUBINTERFACE|Global Configuration|Cria ou seleciona uma subinterface.|
|4|encapsulation dot1Q VLAN-ID|Subinterface Configuration|Associa a subinterface à VLAN indicada.|
|5|encapsulation dot1Q VLAN-ID native|Subinterface Configuration|Associa a subinterface à VLAN nativa.|
|6|ip address IP MÁSCARA|Subinterface Configuration|Configura o gateway IPv4 da VLAN.|
|7|show ip interface brief|Privileged EXEC|Verifica o estado das subinterfaces.|
|8|show ip route connected|Privileged EXEC|Confirma as redes das VLANs como conectadas.|

---

## 11. Switch multicamada, SVI e portas roteadas

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|interface vlan VLAN-ID|Global Configuration|Cria ou seleciona a SVI da VLAN.|
|2|ip address IP MÁSCARA|SVI Configuration|Configura o endereço do gateway da VLAN.|
|3|no shutdown|SVI Configuration|Habilita administrativamente a SVI.|
|4|ip routing|Global Configuration|Habilita o roteamento IPv4 no switch multicamada.|
|5|no switchport|Interface Configuration|Converte uma porta Layer 2 em porta roteada Layer 3.|
|6|show ip interface brief|Privileged EXEC|Verifica SVIs e portas roteadas.|
|7|show ip route|Privileged EXEC|Exibe a tabela de roteamento do switch.|
|8|show ip route connected|Privileged EXEC|Exibe as redes diretamente conectadas.|

---

## 12. VTP

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|show vtp status|Privileged EXEC|Exibe versão, domínio, modo e revisão do VTP.|
|2|show vtp password|Privileged EXEC|Exibe informações relacionadas à senha, quando suportado.|
|3|vtp domain NOME|Global Configuration|Define o domínio VTP.|
|4|vtp mode server|Global Configuration|Configura o equipamento como servidor VTP.|
|5|vtp mode client|Global Configuration|Configura o equipamento como cliente VTP.|
|6|vtp mode transparent|Global Configuration|Configura o equipamento no modo transparente.|
|7|vtp version VERSÃO|Global Configuration|Define a versão do VTP.|
|8|vtp password SENHA|Global Configuration|Define a senha do domínio VTP.|
|9|vtp pruning|Global Configuration|Habilita VTP pruning.|

## 13. Tabela de roteamento

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|show ip route|Privileged EXEC|Exibe toda a tabela de roteamento IPv4.|
|2|show ip route connected|Privileged EXEC|Exibe somente as rotas diretamente conectadas.|
|3|show ip route local|Privileged EXEC|Exibe as rotas locais dos endereços das interfaces.|
|4|show ip route static|Privileged EXEC|Exibe somente as rotas estáticas instaladas.|
|5|show ip route IP|Privileged EXEC|Consulta a melhor rota para determinado endereço.|
|6|show running-config \| include ip route|Privileged EXEC|Exibe somente os comandos de rotas estáticas configurados.|

## 14. Rotas estáticas

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|ip route REDE MÁSCARA PRÓXIMO-SALTO|Global Configuration|Cria uma rota estática apontando para o próximo salto.|
|2|ip route REDE MÁSCARA INTERFACE|Global Configuration|Cria uma rota indicando a interface de saída.|
|3|ip route REDE MÁSCARA INTERFACE PRÓXIMO-SALTO|Global Configuration|Cria uma rota estática totalmente especificada.|
|4|ip route 0.0.0.0 0.0.0.0 PRÓXIMO-SALTO|Global Configuration|Configura uma rota padrão.|
|5|no ip route REDE MÁSCARA PRÓXIMO-SALTO|Global Configuration|Remove a rota estática correspondente.|
|6|show ip route static|Privileged EXEC|Confirma se as rotas estáticas foram instaladas.|
|7|ping IP|User ou Privileged EXEC|Testa a comunicação com o destino.|
|8|traceroute IP|Privileged EXEC|Identifica até qual salto o tráfego avança.|

---

## 15. Análise básica do Spanning Tree

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|show spanning-tree|Privileged EXEC|Exibe a situação geral do STP por VLAN.|
|2|show spanning-tree vlan VLAN-ID|Privileged EXEC|Exibe a árvore STP de uma VLAN específica.|
|3|show spanning-tree interface INTERFACE|Privileged EXEC|Exibe informações STP de uma interface.|
|4|show spanning-tree interface INTERFACE detail|Privileged EXEC|Mostra informações detalhadas da interface no STP.|
|5|show spanning-tree detail|Privileged EXEC|Exibe temporizadores, eventos e mudanças de topologia.|
|6|show spanning-tree root|Privileged EXEC|Resume a root bridge de cada VLAN.|
|7|show spanning-tree bridge|Privileged EXEC|Exibe as informações STP do switch local.|
|8|show spanning-tree summary|Privileged EXEC|Exibe o modo STP e um resumo das instâncias.|
|9|show spanning-tree inconsistentports|Privileged EXEC|Exibe portas bloqueadas por mecanismos de proteção.|

---

## 16. Ajustes de prioridade e caminho no STP

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|spanning-tree vlan VLAN-ID root primary|Global Configuration|Torna o switch preferencial para ser root da VLAN.|
|2|spanning-tree vlan VLAN-ID root secondary|Global Configuration|Torna o switch candidato secundário.|
|3|spanning-tree vlan VLAN-ID priority VALOR|Global Configuration|Define manualmente a prioridade STP.|
|4|spanning-tree vlan VLAN-ID cost VALOR|Interface Configuration|Altera o custo STP da interface.|
|5|spanning-tree vlan VLAN-ID port-priority VALOR|Interface Configuration|Altera a prioridade STP da porta.|
|6|show spanning-tree root|Privileged EXEC|Confirma a root bridge de cada VLAN.|
|7|show spanning-tree vlan VLAN-ID|Privileged EXEC|Confirma funções, estados, custos e prioridades.|

---

## 17. PortFast e BPDU Guard

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|spanning-tree portfast|Interface Configuration|Faz a porta de borda avançar rapidamente para forwarding.|
|2|spanning-tree portfast default|Global Configuration|Habilita PortFast por padrão nas portas de acesso.|
|3|spanning-tree bpduguard enable|Interface Configuration|Coloca a porta em err-disabled se ela receber uma BPDU.|
|4|spanning-tree portfast bpduguard default|Global Configuration|Habilita BPDU Guard nas portas PortFast.|
|5|show interfaces status err-disabled|Privileged EXEC|Exibe portas em estado err-disabled.|
|6|show errdisable recovery|Privileged EXEC|Exibe causas e temporizadores de recuperação.|
|7|errdisable recovery cause bpduguard|Global Configuration|Habilita recuperação automática para BPDU Guard.|
|8|errdisable recovery interval SEGUNDOS|Global Configuration|Define o tempo de recuperação automática.|
|9|shutdown seguido de no shutdown|Interface Configuration|Recupera manualmente a interface após corrigir a causa.|

---

## 18. BPDU Filter, Root Guard e Loop Guard

|Recurso|Comando|Modo|Finalidade|
|---|---|---|---|
|BPDU Filter|spanning-tree bpdufilter enable|Interface Configuration|Impede o envio e recebimento de BPDUs na interface.|
|BPDU Filter|spanning-tree portfast bpdufilter default|Global Configuration|Aplica BPDU Filter às portas PortFast.|
|Root Guard|spanning-tree guard root|Interface Configuration|Impede que a porta introduza uma root bridge não esperada.|
|Loop Guard|spanning-tree guard loop|Interface Configuration|Protege contra a perda de BPDUs que poderia liberar um caminho redundante.|
|Loop Guard|spanning-tree loopguard default|Global Configuration|Habilita Loop Guard globalmente nas interfaces apropriadas.|
|Verificação|show spanning-tree inconsistentports|Privileged EXEC|Exibe portas em root-inconsistent ou loop-inconsistent.|

---

## 19. Rapid PVST+

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|spanning-tree mode rapid-pvst|Global Configuration|Habilita Rapid PVST+.|
|2|spanning-tree mode pvst|Global Configuration|Retorna ao PVST+ tradicional.|
|3|spanning-tree link-type point-to-point|Interface Configuration|Define o enlace STP como ponto a ponto.|
|4|spanning-tree link-type shared|Interface Configuration|Define o enlace como compartilhado.|
|5|show spanning-tree summary|Privileged EXEC|Confirma o modo STP em operação.|
|6|show spanning-tree vlan VLAN-ID|Privileged EXEC|Exibe funções e estados da instância Rapid PVST+.|

---

## 20. EtherChannel

|Ordem|Comando|Modo de execução|Finalidade|
|---|---|---|---|
|1|interface range INTERVALO|Global Configuration|Seleciona as interfaces físicas que formarão o canal.|
|2|channel-group NÚMERO mode on|Interface Configuration|Cria EtherChannel estático.|
|3|channel-group NÚMERO mode desirable|Interface Configuration|Configura PAgP ativo.|
|4|channel-group NÚMERO mode auto|Interface Configuration|Configura PAgP passivo.|
|5|channel-group NÚMERO mode active|Interface Configuration|Configura LACP ativo.|
|6|channel-group NÚMERO mode passive|Interface Configuration|Configura LACP passivo.|
|7|interface port-channel NÚMERO|Global Configuration|Seleciona a interface lógica do EtherChannel.|
|8|show etherchannel summary|Privileged EXEC|Resume canais, protocolos, portas e estados.|
|9|show etherchannel port-channel|Privileged EXEC|Exibe detalhes dos Port-channels.|
|10|show interfaces port-channel NÚMERO|Privileged EXEC|Exibe informações detalhadas do canal lógico.|
|11|show pagp neighbor|Privileged EXEC|Exibe vizinhos PAgP.|
|12|show lacp neighbor|Privileged EXEC|Exibe vizinhos LACP.|
|13|port-channel load-balance MÉTODO|Global Configuration|Define o critério de distribuição dos fluxos.|
|14|show etherchannel load-balance|Privileged EXEC|Exibe o método de balanceamento utilizado.|
