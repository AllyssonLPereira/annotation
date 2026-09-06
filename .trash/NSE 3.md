
- VDOMs (Virtual Domains): permite dividir um único FortiGate (NGFW) físico em múltiplos firewalls virtuais, cada uma com suas próprias políticas, interfaces, tabela de roteamentos e administradores.

	- Por padrão, não há tráfego de uma VDOM para outra, mas pode-se configurar rotas para que isso aconteça.

- O FortiGate recebe atualizações do FortiGuard Security Services, isto é, do FortiGuard Labs. O FortiGuard Labs é uma força tarefa de várias organizações que buscam uma maior proteção contra os riscos cibernéticos.

	- O FortiGuard Labs tem Threat Intelligence em tempo real e táticas preventivas inovadoras e ferramentas que podem ser categorizada em três frentes:
	
		- ML e AI para parar ameaças desconhecidas rapidamente;
		- Proteção em tempo real que provê uma postura de segurança proativa;
		- Threat Hunting e alertas que permite uma remediação rápida.

- VLANs e FortiGate:
	- in NAT mode: FortiGate opera na camada 3, podendo rotear tráfego entre VLANs e operar NAT
	- in Transparent mode: FortiGate opera como um layer 2 bridge
	- virtual VLAN switch

- Rotas estáticas:
	- Criar um rota estática não significa que o FortiGate vai usá-la (misconfigured, porta associada down ou disabled ou a uma rota melhor para o tráfego)

- Modos de inspeção no FortiGate:
	- ***Flow-based***: analisa o pacote em tempo real, sem retê-lo completamente na memória (para mais desempenho)
	- ***Proxy-based***: o FortiGate recebe o arquivo completo, reconstrói o conteúdo em seu buffer, inspeciona tudo e só então envia ao destino

- Autenticação:
	- Informações de usuários podem ser armazenadas no próprio FortiGate (**local***) ou **remotamente***

- SSL inspection:
	- ***Certification inspection***: o FortiGate só analise o handshake TLS, verificando a identidade do servidor; só é possível usar Web filtering aqui.
	
	- ***Deep inspection***: aqui, o FortiGate, descripgrafa o pacote, analisando o conteúdo com as tecnologias configuradas (como web filtering) e, uma vez aceito, recriptografa, enviando ao destinatário.
	
		- ***Usando FortiGate CA certificate***: o FortiGate cria um certificado de um determinado site que se parece com o real, mas é assinado pelo FortiGate CA, gerando um alerta toda vez que o usuário tenta acessar o determinado site. Para evitar esses aletar, é só instalar o certificado FORTIGATE_CA_SSL na estações xe trabalho como uma altoridade confiável

- Web filter:
	- Categories: www.fortiguard.com/webfilter/cayegories
	- Verificar se a URL pertence a uma categoria bloqueada ou permitida

- Tarefas comuns de manutenção no FortiGate
	- Backing up configuration (caso ocorra alguma falha na configuração ou a troca de hardware, é bom ter o backup das configurações);
	- Performing firmware upgrades (F - indica novos recursos; M - indica que não há novos recursos) (existe etapas a si seguir na instalação do firmware) - `https://docs.fortinet.com/upgrade-tool`;
	- Monitoring system performance (CPU, memória, disk, sessions e usuários conectados a VPN);
	- Examining licenses (System > FortiGuard)
	- Monitoring event logs

- HA
	- Ordem dos parâmetros de eleição do primário
		- 1. Interfaces monitoradas com menos falhas;
		- 2. FortiGate com maior uptime;
		- 3. FortiGate com maior prioridade;
		- 4. FortiGate com maior Serial Number.
		
	- O núcleo do FortiGate HA é o FortiGate Clustering Protocol (FGCP), ele faz a descoberta de membros, elege o primário, sincroniza dados entre os membros e monitora a saúde dos membros; tudo isso através da interface HA. É também ele quem atribui endereços MAC virtuais.

![[Screenshot_20260526-123929_Brave.jpg]]


- HA
	- Temos o modo ativo-passivo e o ativo-ativo.

- FortiLink
	- Isso é um protocolo propietário da Fortinet que permite aos admins gerenciar FortiSwitches diretamente através do FortiGate.
	- Então, ele é usado para descoberta de FortiSwitches, o gerenciamentos dos mesmos.
	- Temos, ainda, o uso dos protocolos LLDP
		- que também é utilizado durante a configuração de um stack de switches, pois permite que os links que conectam o switch sejam configurados automaticamente como trunk.; 
		- já o CAPWAP foi originalmente criado para centralizar o gerenciamento de Wi-Fi access point e, em adição a sua função original, a implementação do CAPWAP pela Fortinet realiza autenticação, autorização e verificações de integridade em switches, estabelecendo um túnel seguro entre um Fortigate e o switch gerenciado. Ele também é usado como uma alternativa, como um método legado, para o envio da imagem do firmware para o switch.
			- O switch também usa o CAPWAP para envio de logs