---
tags:
  - arquivo
---
### Etapas básicas

O switch Cisco só precisa receber informações básicas de segurança antes de ser conectado à rede. Elementos que normalmente são configurados em um switch de LAN incluem: nome de host, informações de endereço IP de gerenciamento, senhas e informações descritivas.

- [Nome de host]

O nome de host do switch é o nome configurado para o dispositivo. Como cada computador ou impressora tem um nome atribuído, o equipamento de rede deve ser configurado com um nome descritivo. 

*Isso será útil se o nome do dispositivo incluir o [local onde o switch será instalado]. Um exemplo seria: SW_Bldg_R-Room_216.


- [IP de gerenciamento]

Um endereço IP de gerenciamento será *[necessário apenas se você configurar e gerenciar o switch através de uma conexão em banda na rede]*. Um endereço de gerenciamento permite acessar o dispositivo por clientes Telnet, SSH ou HTTP. 

As informações de endereço IP que devem ser configuradas em um switch são essencialmente as mesmas que você configura em um PC: [endereço IP, máscara de sub-rede e gateway padrão].


- [Senhas]

Para proteger um switch Cisco LAN, é necessário configurar [senhas em cada um dos métodos de acesso à linha de comando]. Os requisitos mínimos incluem a atribuição de senha a métodos de acesso remoto, como Telnet, SSH e a conexão do console. [Você também deve atribuir uma senha ao modo privilegiado] no qual as alterações de configuração podem ser feitas.

> [!NOTE]
> Telnet envia o nome de usuário e a senha em texto simples e não é considerado seguro. O SSH é um método mais seguro, pois criptografa o nome de usuário e a senha.


Configurar o nome do dispositivo.

- **[hostname]** _nome_

Proteger o modo EXEC usuário.

- **[line console 0]**
- **[senha]** _senha_
- **[login]**

Proteger o acesso remoto Telnet/SSH

- **[line vty 0 15]**
- **[senha]** _senha_
- **[login]**

Proteger o modo EXEC privilegiado.

- **[enable secret]** _password_

Proteger todas as senhas do arquivo de configuração.

- **[service password-encryption]**

Apresentar a notificação legal.

- **[banner motd]** _delimiter mensagem delimiter_

Configurar SVI de gerenciamento.

- **[interface vlan 1]**
- **[ip address]** _ip-address subnet-mask_
- **[no shutdown]**

Salvar a configuração.

- **[copy running-config startup-config]**

---
### Configuração da Interface Virtual de Switch

Para acessar o switch remotamente, um endereço IP e uma máscara de sub-rede devem ser configurados na SVI. Para configurar uma SVI em um switch, use o comando de configuração global **interface vlan 1** . 

Vlan 1 não é uma interface física real, mas virtual. Em seguida, atribua um endereço IPv4 usando o comando de configuração de interface **ip-address** _subnet-mask_. Por fim, ative a interface virtual com o comando de configuração de interface **no shutdown** .

Depois que o switch é configurado com esses comandos, o switch tem todos os elementos IPv4 prontos para comunicação pela rede local.

Semelhante aos hosts do Windows, os switches configurados com um endereço IPv4 normalmente também precisam ter um gateway padrão atribuído. Isso pode ser feito usando o comando de configuração global **ip default-gateway** _ip-address_ . 

O parâmetro _ip-address_ deve ser o endereço IPv4 do roteador local na rede, como mostrado no exemplo. No entanto, neste tópico, você configurará apenas uma rede com switches e hosts. Os roteadores serão configurados posteriormente.

``` shell
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# interface vlan 1
Sw-Floor-1(config-if)# ip address 192.168.1.20 255.255.255.0
Sw-Floor-1(config-if)# no shutdown
Sw-Floor-1(config-if)# exit
Sw-Floor-1(config)# ip default-gateway 192.168.1.1
```


