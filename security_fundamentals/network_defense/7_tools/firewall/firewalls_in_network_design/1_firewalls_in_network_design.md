---
tags:
  - arquivo
---
## Common security architectures

O design do firewall se dá principalmente sobre interfaces de dispositivo que permitem ou negam tráfego com base na origem, no destino e no tipo de tráfego. Alguns designs são tão simples quanto projetar uma rede externa e uma rede interna, que são determinados por duas interfaces em um firewall.

Aqui estão três designs comuns de firewall:

#### Private and Public

Como mostrado na figura, a rede pública não é confiável e a rede privada é confiável.

![[private_and_public_firewall.png]]

Normalmente, um firewall com duas interfaces é configurado da seguinte forma:

- O tráfego proveniente da rede privada é permitido e inspecionado à medida que viaja em direção à rede pública. É permitido o tráfego inspecionado que retorna da rede pública e associado ao tráfego originado da rede privada.

- O tráfego originado da rede pública e que viaja para a rede privada geralmente é bloqueado.

#### Demilitarized Zone

Uma `Demilitarized Zone` — `DMZ` — é um projeto de firewall onde normalmente há uma interface interna conectada à rede privada, uma interface externa conectada à rede pública e uma interface DMZ, conforme mostrado na figura.

![[Demilitarized Zone.png]]

- O tráfego proveniente da rede privada é inspecionado à medida que ele viaja para a rede pública ou DMZ. Este tráfego é permitido com pouca ou nenhuma restrição. Tráfego inspecionado que retorna da DMZ ou da rede pública para a rede privada é permitido.

- O tráfego originado da rede DMZ e que viaja para a rede privada geralmente é bloqueado.

- O tráfego originado da rede DMZ e viajando para a rede pública é permitido seletivamente com base nos requisitos de serviço.

- O tráfego proveniente da rede pública e que viaja em direção à DMZ é seletivamente permitido e inspecionado. Esse tipo de tráfego normalmente é tráfego de email, DNS, HTTP ou HTTPS. O tráfego de retorno da DMZ para a rede pública é permitido dinamicamente.

- O tráfego originado da rede pública e que viaja para a rede privada está bloqueado.

#### Zone-based policy firewalls

Os `Zone-based policy firewalls` — `ZPFs` — usam o conceito de zonas para fornecer flexibilidade adicional. Uma zona é um grupo de uma ou mais interfaces que têm funções ou recursos semelhantes. 

As zonas ajudam a especificar onde uma regra ou política de firewall deve ser aplicada. 

Na figura, as políticas de segurança para LAN 1 e LAN 2 são semelhantes e podem ser agrupadas em uma zona para configurações de firewall. Por padrão, o tráfego entre interfaces na mesma zona não está sujeito a nenhuma política e passa livremente. No entanto, todo o tráfego de zona para zona está bloqueado. 

Para permitir o tráfego entre as zonas, uma política que permite ou inspeciona o tráfego deve ser configurada.

A única exceção a esta política padrão *deny any* é a zona própria do roteador. A zona auto é o próprio roteador e inclui todos os endereços IP da interface do roteador. As configurações de política que incluem a zona automática aplicar-se-iam ao tráfego destinado e proveniente do roteador. 

Por padrão, não há nenhuma política para esse tipo de tráfego. O tráfego que deve ser considerado ao projetar uma política para a auto zona inclui o tráfego de plano de gerenciamento e plano de controle, como SSH, SNMP e protocolos de roteamento.

![[Zone-based policy firewalls.png]]

---
## Layered Defense

1. *`Network Core Security`* — Protege contra software malicioso e anomalias de tráfego, impõe políticas de rede e garante capacidade de sobrevivência.
2. *`Perimeter security`* — Protege limites entre zonas.
3. *`Communications security`* — Fornece garantia de informação.
4. *`Endpoint Security`* — Fornece identidade e conformidade com a política de segurança do dispositivo.

#### Considerations for Layered Network Defense

Uma defesa em camadas usa diferentes tipos de firewalls que são combinados em camadas para adicionar profundidade à segurança de uma organização. As políticas podem ser aplicadas entre as camadas e dentro das camadas. Estes pontos de aplicação da política determinam se o tráfego é encaminhado ou descartado. 

Por exemplo, o tráfego que vem dentro da rede não confiável encontra primeiramente um filtro de pacote no roteador de borda. Se permitido pela política, o tráfego vai ao Firewall selecionado ou ao sistema *host bastion* que aplica mais regras ao tráfego e descarta pacotes suspeitos. 

> *Um host bastion é um computador endurecido que normalmente está localizado na DMZ.*

Então o tráfego vai para um roteador de triagem interior. 

O tráfego move-se para o host de destino interno somente após passar com sucesso todos os pontos de imposição da política entre o roteador externo e a rede interna. Esse tipo de configuração DMZ é chamado de *`tracked subnet configuration`*.

Uma abordagem de defesa em camadas não é tudo o que é necessário para garantir uma rede interna segura. Um administrador de rede deve considerar muitos fatores ao construir uma defesa completa em profundidade:

- Os firewalls normalmente não interrompem as intrusões provenientes de hosts dentro de uma rede ou zona.

- Firewalls não protegem contra instalações de ponto de acesso desonestos.

- Os firewalls não substituem os mecanismos de backup e recuperação de desastres resultantes de ataques ou falhas de hardware.

- Os firewalls não substituem administradores e usuários informados.

> *Essa lista parcial de práticas recomendadas pode servir como ponto de partida para uma política de segurança de firewall.*
> 
> - *Posicione firewalls nos limites de segurança. Os firewalls são uma parte crítica da segurança de rede, mas não é sensato confiar exclusivamente em um firewall para segurança.*
> - *Negue todo o tráfego por padrão.*
> - *Permitir apenas serviços que são necessários.*
> - *Assegure-se de que o acesso físico ao firewall esteja controlado.*
> - *Monitore regularmente logs de firewall.*
> - *Pratique o gerenciamento de alterações para alterações de configuração de firewall.*
> - *Lembre-se de que os firewalls protegem principalmente contra ataques técnicos originários do exterior.*

