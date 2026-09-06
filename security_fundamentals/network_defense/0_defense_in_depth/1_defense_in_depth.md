---
tags:
  - arquivo
---
## Defense in Depth

Permissões de acesso total incluem acesso a edifícios, salas de servidores, redes, aplicativos e serviços públicos. Todas essas são implementações de controle de acesso e fazem parte de uma estratégia de defesa em camadas, também conhecida como *`Defense in Depth`*, desenvolvida por uma organização.

A defesa em profundidade descreve uma estratégia de segurança da informação que integra pessoas, tecnologia e recursos operacionais para estabelecer barreiras variáveis em múltiplas camadas e missões da organização.

Ela aplica *múltiplas contramedidas em camadas para atingir os objetivos de segurança*. A defesa em profundidade deve ser implementada para prevenir ou dissuadir um ataque cibernético, mas não pode garantir que um ataque não ocorrerá.

Um exemplo técnico de defesa em profundidade, em que múltiplas camadas de controles técnicos são implementadas, é quando um nome de usuário e uma senha são exigidos para fazer login em uma conta, seguidos por um código enviado ao telefone do usuário para verificar sua identidade.

Esta é uma forma de autenticação multifator que utiliza métodos em duas camadas: algo que você tem e algo que você sabe. A combinação das duas camadas é muito mais difícil para um adversário obter do que qualquer um dos códigos de autenticação individualmente.

Outro exemplo de múltiplas camadas técnicas é quando firewalls adicionais são usados para separar redes não confiáveis com diferentes requisitos de segurança, como a internet, de redes confiáveis que hospedam servidores com dados confidenciais na organização.

Quando uma empresa possui informações com múltiplos níveis de sensibilidade, pode ser necessário que o tráfego de rede seja validado por regras em mais de um firewall, com as informações mais sensíveis sendo armazenadas atrás de múltiplos firewalls.

![[defense_in_depth.png]]

Para um exemplo não técnico, considere as múltiplas camadas de acesso necessárias para acessar os dados em um data center. Primeiro, uma fechadura na porta fornece uma barreira física para acessar os dispositivos de armazenamento de dados.

Segundo, uma regra de acesso técnico impede o acesso aos dados pela rede. Por fim, uma política ou controle administrativo define as regras que atribuem acesso a indivíduos autorizados.

Aqui estão alguns exemplos que explicam melhor o conceito de defesa em profundidade: 

- *Dados*

	Controles que protegem os dados reais com tecnologias como criptografia, prevenção de vazamento de dados, gerenciamento de identidade e acesso e controles de dados. 

- *Aplicativo*

	Controles que protegem o aplicativo com tecnologias como prevenção de vazamento de dados, firewalls de aplicativos e monitores de banco de dados. 

- *Host*

	Todo controle que é colocado no nível do endpoint, como antivírus, firewall de endpoint, configuração e gerenciamento de patches. 

- *Rede interna*

	Controles que estão em vigor para proteger o fluxo de dados não controlado e o acesso de usuários em toda a rede organizacional. Tecnologias relevantes incluem sistemas de detecção de intrusão, sistemas de prevenção de intrusão, barreiras de segurança internas e controles de acesso à rede. 

- *Perímetro*

	Controles que protegem contra acesso não autorizado à rede. Este nível inclui o uso de tecnologias como barreiras de segurança de gateway, honeypots, análise de malware e zonas desmilitarizadas seguras (DMZs). 

- *Físico*

	Controles que fornecem uma barreira física, como fechaduras, barreiras ou controle de acesso. 

- *Políticas, procedimentos e conscientização*

	Controles administrativos que reduzem ameaças internas (intencionais e não intencionais) e identificam os riscos assim que eles surgem