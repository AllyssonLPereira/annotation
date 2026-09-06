---
tags:
  - arquivo
---
## Basic security zone topology

Há dois modelos de configuração para o Cisco IOS Firewall:

- *`Classic Firewall`* — o modelo de configuração tradicional em que a política de firewall é aplicada em interfaces.
- *`Zone-based policy firewall`* — `ZPF` — O modelo de configuração na qual as interfaces são atribuídas a zonas de segurança, e a política de firewall é aplicada ao tráfego em movimento entre as zonas.

Se uma interface adicional for adicionada à zona privada, os hosts conectados à nova interface na zona privada podem passar tráfego para todos os hosts na interface existente na mesma zona. Uma rede simples de três zonas é mostrada na figura.

![[demilitarized_zone.png]]

As principais motivações para profissionais de segurança de rede migram para o modelo ZPF são estrutura e facilidade de uso. A abordagem estruturada é útil para documentação e comunicação. A facilidade de uso torna as implementações de segurança de rede mais acessíveis a uma comunidade maior de profissionais de segurança.

Existem vários benefícios de um ZPF:

- Não é dependente de ACL.
- A postura de segurança do roteador é bloquear a menos que explicitamente permitido.
- As políticas são fáceis de ler e pesquisar defeitos com o Cisco Common Classification Policy Language (C3PL). C3PL é um método estruturado para criar políticas de tráfego com base em eventos, condições e ações. Isto fornece a escalabilidade porque uma política afeta todo o tráfego dado, em vez de precisar de ACLs múltiplos e ações da inspeção para tipos diferentes de tráfego.
- Interfaces virtuais e físicas podem ser agrupadas em zonas.
- As políticas são aplicadas ao tráfego unidirecional entre zonas.

Ao decidir se deseja implementar o iOS Classic Firewall ou um ZPF, é importante observar que ambos os modelos de configuração podem ser ativados simultaneamente em um roteador. 

No entanto, os modelos não podem ser combinados em uma única interface. Por exemplo, uma interface não pode ser configurada simultaneamente como membro da zona de segurança e para inspeção de IP.

---
## ZPF Project

#### Etapa 1. Determine as zonas

O administrador se concentra na separação da rede em zonas. Zonas estabelecem as fronteiras de segurança de uma rede. Uma zona define um limite onde o tráfego é submetido a restrições políticas à medida que cruza para outra região da rede. Por exemplo, a rede pública seria uma zona e a rede interna seria outra zona.

#### Etapa 2. Estabelecer políticas entre zonas

Para cada par de zonas "fonte de destino" (por exemplo, da rede interna para a Internet externa), defina as sessões que os clientes nas zonas de origem podem solicitar os servidores nas zonas de destino. 

Essas sessões são mais frequentemente as sessões TCP e UDP, mas também podem ser sessões ICMP, como o ICMP ECHO. Para o tráfego que não é baseado no conceito de sessões, o administrador deve definir fluxos de tráfego unidirecionais da fonte para o destino e vice-versa. 

As políticas são unidirecionais e são definidas com base nas zonas de origem e destino, que são conhecidas como pares de zona.

#### Etapa 3. Projete a infraestrutura física

Após as zonas terem sido identificadas e os requisitos de tráfego entre eles documentados, o administrador deve projetar a infraestrutura física. 

O administrador deve levar em conta os requisitos de segurança e disponibilidade ao projetar a infraestrutura física. Isso inclui ditar o número de dispositivos entre zonas mais seguras e menos seguras e determinar dispositivos redundantes.

#### Etapa 4. identificar subconjuntos dentro de zonas e mesclar requisitos de tráfego

Para cada dispositivo de firewall no projeto, o administrador deve identificar subconjuntos de zonas que estão conectados às suas interfaces e mesclar os requisitos de tráfego para essas zonas. 

Por exemplo, várias zonas podem ser ligadas indiretamente a uma única interface de um firewall. Isso resultaria em uma política interzone específica do dispositivo. Embora uma consideração importante, os subconjuntos de zona de implementação estão além do escopo deste currículo.

---
## Exemplos de projetos:

#### Lan-to-internet

![[Lan-to-internet.png]]

#### Firewall-with-public-servers-1

![[Firewall-with-public-servers-1.png]]

#### Firewall-with-public-servers-2

![[Firewall-with-public-servers-2.png]]

#### Firewalls redundantes

![[Firewalls_redundantes.png]]

#### Firewall complexo

![[Firewall_complexo.png]]