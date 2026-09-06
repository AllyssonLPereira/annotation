

## What is "Intelligence"?

`Intelligence` é o auxílio que você dá a alguém para que ela tome as *melhores decisões possíveis perante um problema/evento*.

---
## Intelligence cycle

Todo esse processo de `Intelligence` não é simples, ele envolve desafios.

Alguns desses desafios são: 

- "Como vou identificar as fontes de informação e avaliar se elas são boas?";
- "Como devo extrair e analisar esse conteúdo?";
- "Como vou reportar a informação de acordo com o público alvo?".

![[intelligence_cycle.png]]

---
## Hard Skills

![[hard_skills_CTI.png]]

---
## CTI services

Os serviços de inteligência contra ameaças permitem a troca de informações sobre ameaças, como *vulnerabilidades*, *`indicators of commitment`* — *`IOC`* — e *técnicas de mitigação*. Essas informações não são compartilhadas apenas com o pessoal, mas também com sistemas de segurança. 

À medida que as ameaças surgem, os serviços de inteligência de ameaças criam e distribuem regras de firewall e IOCs para os dispositivos que assinaram o serviço.

- *Cisco Talos Threat Intelligence Group*

	Um desses serviços é o Cisco Talos Threat Intelligence Group. Talos é uma das maiores equipes de inteligência de ameaças comerciais do mundo e é composta por pesquisadores, analistas e engenheiros de classe mundial. 

	O objetivo do Talos é ajudar a proteger os usuários, dados e infraestrutura da empresa de adversários ativos. A equipe do Talos coleta informações sobre ameaças ativas, existentes e emergentes. O Talos então fornece proteção abrangente contra esses ataques e malware aos seus assinantes.

	﻿Os produtos da Cisco Security podem usar a inteligência de ameaças Talos em tempo real para fornecer soluções de segurança rápidas e eficazes. O Cisco Talos também fornece software, serviços, recursos e dados gratuitos. Talos mantém os conjuntos de regras de detecção de incidentes de segurança para as ferramentas de segurança de rede Snort.org, ClamAV e SpamCop.


- *FireEye*

	FireEye é outra empresa de segurança que oferece serviços para ajudar as empresas a proteger suas redes. A FireEye usa uma abordagem de três frentes combinando inteligência de segurança, experiência em segurança e tecnologia.

	A FireEye oferece SIEM e SOAR com a *`Helix Security Platform`*, que usa análise comportamental e detecção avançada de ameaças e é suportada pela rede mundial de inteligência contra ameaças da *`FireEye Mandiant`*. *Helix* é uma plataforma de operações de segurança hospedada em nuvem que combina diversas ferramentas de segurança e inteligência de ameaças em uma única plataforma.

	O FireEye Security System bloqueia ataques em vetores de ameaças da Web e de e-mail e malware latente que reside em compartilhamentos de arquivos. 

	Ele pode bloquear malware avançado que facilmente ignora as defesas tradicionais baseadas em assinaturas e compromete a maioria das redes empresariais. Ele aborda todos os estágios de um ciclo de vida de ataque com um mecanismo sem assinatura que utiliza análise de ataque stateful para detectar ameaças de dia zero.


- *Department of Homeland Security*

	O Departamento de Segurança Interna dos EUA — DHS — oferece um serviço gratuito chamado Compartilhamento Automatizado de Indicador — AIS. 

	O AIS permite a troca em tempo real de indicadores de ameaças cibernéticas (por exemplo, endereços IP maliciosos, o endereço do remetente de um e-mail de phishing, etc.) entre o Governo Federal dos EUA e o setor privado.

	O AIS cria um ecossistema onde, assim que uma ameaça é reconhecida, ela é imediatamente compartilhada com a comunidade para ajudá-la a proteger suas redes dessa ameaça específica.

---
## Threat Intelligence Communication Standards

Organizações e profissionais de rede devem compartilhar informações para aumentar o conhecimento sobre os atores da ameaça e os ativos que desejam acessar. 

Vários padrões abertos de compartilhamento de inteligência evoluíram para permitir a comunicação em várias plataformas de rede. Esses padrões permitem a troca de inteligência contra ameaças cibernéticas em um formato automatizado, consistente e legível por máquina.

Três padrões comuns de compartilhamento de informações sobre ameaças incluem o seguinte:

- *`Expression of Structured Threat Information`* — *`STIX`* — Este é um conjunto de especificações para a troca de informações sobre ameaças cibernéticas entre organizações. O padrão *`Cyber Observable Expression`* — *`CybOX`* — foi incorporado ao STIX.

- *`Reliable and Automated Exchange of Indicator Information`* — *`TAXII`* — Esta é a especificação de um protocolo da camada de aplicativo que permite a comunicação de CTI sobre HTTPS. *TAXII* foi projetado para suportar STIX.

- *`CybOX`* — Este é um conjunto de esquemas padronizados para especificar, capturar, caracterizar e comunicar eventos e propriedades de operações de rede que oferecem suporte a muitas funções de segurança cibernética.

Esses padrões abertos fornecem as especificações que auxiliam na troca automatizada de informações de inteligência de ameaças cibernéticas em um formato padronizado. Pesquise na Internet para saber mais sobre *STIX*, *TAXII* e *CybOX*.

A *`Malware Information Sharing Platform`* — *`MISP`* — é uma plataforma de código aberto para compartilhar indicadores de comprometimento para ameaças recém-descobertas. O *MISP* é apoiado pela União Europeia e usado por mais de 6.000 organizações em todo o mundo. 

O *MISP* permite o compartilhamento automatizado de IOCs entre pessoas e máquinas usando STIX e outros formatos de exportação.

---
## Threat Intelligence Platforms

Como vimos, existem muitas fontes de informações de inteligência de ameaças, cada uma das quais pode ter seu próprio formato de dados. Acessar e usar várias fontes de inteligência de ameaças pode consumir muito tempo. Para ajudar o pessoal de segurança cibernética a fazer o melhor uso da inteligência de ameaças, as plataformas de inteligência de ameaças (TIP) foram desenvolvidas.

Uma plataforma de inteligência de ameaças centraliza a coleta de dados de ameaças de várias fontes e formatos de dados. Existem três tipos principais de dados de inteligência de ameaças. 

- O primeiro são *`indicators of commitment`* — *`IOC`*. 
- O segundo são *`tools, techniques and procedures`* — *`TTP`*. 
- A terceira são as informações de *reputação sobre destinos ou domínios da Internet*. 

O volume de dados de inteligência de ameaças pode ser esmagador, portanto, a plataforma de inteligência de ameaças foi projetada para agregar os dados em um só lugar e — o mais importante — apresentar os dados em um formato compreensível e utilizável.

As organizações podem contribuir com informações sobre ameaças compartilhando seus dados de intrusão pela Internet, geralmente por meio de automação. Muitos serviços de inteligência de ameaças usam dados de assinantes para aprimorar seus produtos e se manter atualizados com o cenário de ameaças em constante mudança.

> [!NOTE] Honeypots
> Honeypots são redes simuladas ou servidores projetados para atrair atacantes. As informações relacionadas ao ataque coletadas de honeypots podem então ser compartilhadas com os assinantes da plataforma de inteligência de ameaças. No entanto, hospedar honeypots pode ser um risco. Basear um honeypot na nuvem isola o honeypot das redes de produção. Essa abordagem é uma alternativa atraente para coletar informações sobre ameaças.

