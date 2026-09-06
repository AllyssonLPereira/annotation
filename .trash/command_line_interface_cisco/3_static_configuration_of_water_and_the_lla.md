---
tags:
  - arquivo
---
### Configuração de GUA Estático em um Roteador

As GUAs IPv6 são iguais aos endereços IPv4 públicos. O endereço IPv6 unicast global (GUA) é globalmente exclusivo e roteável na Internet IPv6. 

Um LLA IPv6 permite que dois dispositivos habilitados para IPv6 se comuniquem uns com os outros no mesmo link (sub-rede). É fácil configurar estaticamente GUAs e LLAs IPv6 em roteadores para ajudá-lo a criar uma rede IPv6.

A maioria dos comandos de configuração e verificação do IPv6 no Cisco IOS são semelhantes aos seus equivalentes no IPv4. *Em muitos casos a única diferença é o uso do ipv6 em vez do ip dentro dos comandos.

Por exemplo, o comando Cisco IOS para configurar um endereço IPv4 em uma interface é [ip address endereço-IP máscara-de-subrede]. Em contraste, o comando para configurar um GUA IPv6 em uma interface é [ipv6 address endereço-ipv6/comprimento do prefixo].

> Observe que não um espaço entre ipv6-address e prefix-length .

O exemplo de configuração usa as seguintes sub-redes IPv6:

- 2001:db8:acad:1::/64
- 2001:db8:acad:2::/64
- 2001:db8:acad:3::/64


![[configuracao_estatica_gua.png]]


O exemplo mostra os comandos necessários para configurar o IPv6 GUA no GigabitEthernet 0/0/0, GigabitEthernet 0/0/1 e na interface Serial 0/1/0 do R1.

``` shell
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface serial 0/1/0
R1(config-if)# ipv6 address 2001:db8:acad:3::1/64
R1(config-if)# no shutdown
```

---
### Configuração de GUA Estático em um Host Windows

Configurar manualmente o endereço IPv6 em um host é semelhante a configurar um endereço IPv4.

O endereço de gateway padrão configurado para PC1 é 2001:db8:acad:1::1/64. Essa é a GUA da interface R1 GigabitEthernet 0/0/0 na mesma rede. Como alternativa, o endereço de gateway padrão pode ser configurado para corresponder ao endereço LLA da interface Gigabit Ethernet. 

*O uso do LLA do roteador como endereço de gateway padrão é considerado prática recomendada. Porém, qualquer uma das configurações funcionará.

Assim como ocorre no IPv4, a configuração de endereços estáticos em clientes não escala para ambientes maiores. Por esse motivo, a maioria dos administradores de redes IPv6 permite a atribuição dinâmica de endereços IPv6.

Há duas maneiras de um dispositivo obter um endereço IPv6 unicast global automaticamente:

- Configuração automática do endereço sem estado (SLAAC)
- DHCPv6 com estado

> [!NOTE]
> Quando DHCPv6 ou SLAAC é usado, o LLA do roteador será especificado automaticamente como o endereço de gateway padrão.

---
### Configuração estática de um endereço unicast de link-local

A configuração manual do LLA permite criar um endereço reconhecível e fácil de lembrar. *Geralmente, só é necessário criar endereços de link local reconhecíveis nos roteadores. 

Isso é benéfico porque os LLAs do roteador são usados como endereços de gateway padrão e no roteamento de mensagens de anúncio.

Os LLAS podem ser configurados manualmente usando o comando `ipv6 address endereço-de-link-local-ipv6 link-local` . Quando um endereço começa com esse hexteto dentro do intervalo de `fe80` a `febf`, o parâmetro link-local deve seguir o endereço, literalmente.

![[configuracao_estatica_lla.png]]

``` shell
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address fe80::1:1 link-local
R1(config-if)# exit
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address fe80::2:1 link-local
R1(config-if)# exit
R1(config)# interface serial 0/1/0
R1(config-if)# ipv6 address fe80::3:1 link-local
R1(config-if)# exit
```


> [!NOTE] 
> O mesmo LLA pode ser configurado em cada link, desde que seja exclusivo nesse link. Isso é possível porque as interfaces de link local só precisam ser exclusivas nesse link. No entanto, a prática comum é criar um LLA diferente em cada interface do roteador para facilitar a identificação do roteador e da interface específica.

