---
tags:
  - arquivo
---
##### Estrutura de Comandos Básicos do IOS

Um administrador de rede deve conhecer a estrutura básica de comandos do IOS para poder usar a CLI para a configuração do dispositivo.

Um dispositivo Cisco IOS é compatível com muitos comandos. Cada comando do IOS possui um formato ou sintaxe específica e pode ser executado apenas no modo apropriado. A sintaxe geral de um comando, é o comando seguido por quaisquer palavras-chave e argumentos apropriados.

![[estrutura_de_comandos_cisco_ios.png]]

- **[Palavra-chave]** - Este é um parâmetro específico definido no sistema operacional (na figura, **protocolos ip**).

- **[Argumento]** - Não é predefinido; é um valor ou variável definida pelo usuário (na figura, **192.168.10.5**).

---
##### Sintaxe de Comandos do IOS

Um comando pode exigir um ou mais argumentos. Para determinar as palavras-chave e os argumentos necessários para um comando, consulte a sintaxe de comando. A sintaxe fornece o padrão, ou formato, que deve ser usado ao inserir um comando.

| Convenção                      | Descrição                                                                                                                                                                |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **negrito**                    | O texto em negrito indica comandos e palavras-chave que você insere literalmente.                                                                                        |
| _itálico_                      | O texto em itálico indica argumentos para os quais você fornece valores.                                                                                                 |
| **[**x**]**                    | Colchetes indicam um elemento opcional (palavra-chave ou argumento).                                                                                                     |
| **{**x**}**                    | Chaves indicam um elemento obrigatório (palavra-chave ou argumento).                                                                                                     |
| **[**x **{** y **\|** z **}]** | Chaves e linhas verticais entre colchetes indicam uma escolha obrigatória dentro de um elemento opcional. Espaços são usados para delinear claramente partes do comando. |

Por exemplo, a sintaxe para usar o comando **[description]** é **[description]** _string_. O argumento é um valor _string_ fornecido pelo usuário. O comando **[description]** é normalmente usado para identificar a finalidade de uma interface. 

Por exemplo, digitando o comando, **[description Connects]** no switch principal do escritório da matriz, descreve onde o outro dispositivo está no final da conexão.

Os exemplos a seguir demonstram as convenções usadas para documentar e utilizar comandos do IOS:

- **[ping]** _ip-address_ - O comando é **[ping]**, e o argumento definido pelo usuário _ip-address_ é o endereço IP do dispositivo de destino. Por exemplo, **[ping 10.10.10.5]**.

- **[traceroute]** _ip-address_ - O comando é **[traceroute]**, e o argumento definido pelo usuário _ip-address_ é o endereço IP do dispositivo de destino. Por exemplo, **[traceroute 192.168.254.254]**.

Se um comando é complexo com vários argumentos, você pode vê-lo representado assim:

``` shell
Switch(config-if)# switchport port-security aging { static | time time | type {absolute | inactivity}}
```

O comando normalmente vem seguido de uma descrição detalhada do comando e cada argumento no referência de comando no cisco IOS.

> [!NOTE]
> A Referência de Comandos do Cisco IOS é a fonte definitiva de informações para um determinado comando do IOS.


---
##### Teclas de Atalho e Atalhos

| Toque de tecla                         | Descrição                                                                                          |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Tabulação**                          | Completa um nome de comando parcialmente digitado.                                                 |
| **Ctrl+D**                             | Apaga o caractere no cursor.                                                                       |
| **Ctrl+K**                             | Apaga todos os caracteres do cursor até o final da linha de comando.                               |
| **Esc D**                              | Apaga todos os caracteres do cursor até o final da palavra.                                        |
| **Ctrl+U** ou **Ctrl+X**               | Apagam todos os caracteres do cursor até o início da linha de comando.                             |
| **Ctrl+W**                             | Apaga a palavra à esquerda do cursor.                                                              |
| **Ctrl+A**                             | Move o cursor para o início da linha.                                                              |
| **Ctrl+B**                             | Movem o cursor um caractere para a esquerda.                                                       |
| **Esc B**                              | Move o cursor uma palavra para a esquerda.                                                         |
| **Esc F**                              | Move o cursor uma palavra para a direita.                                                          |
| **Ctrl+F**                             | Movem o cursor um caractere para a direita.                                                        |
| **Ctrl+E**                             | Move o cursor para o final da linha de comando.                                                    |
| **Seta para cim**a ou **Ctrl+P**       | Relembram os comandos no buffer de histórico, a partir dos comandos mais recentes.                 |
| **Seta para baixo** ou **Ctrl+N**      | Vai para a próxima linha no buffer do histórico.                                                   |
| **Ctrl+R** ou **Ctrl+I** ou **Ctrl+L** | Reexibem o prompt do sistema e a linha de comando após o uma mensagem ter sido exibida no console. |

> [!NOTE]
> Embora a tecla **Delete** normalmente exclua o caractere à direita do prompt, a estrutura de comando do IOS não reconhece a tecla **Delete**.

Esta tabela lista os comandos usados para sair de uma operação.

|Toque de tecla|Descrição|
|---|---|
|**Ctrl-C**|Em qualquer modo de configuração, finaliza o modo de configuração e retorna ao modo EXEC privilegiado. No modo de instalação, volta para o prompt de comando.|
|**Ctrl-Z**|Em qualquer modo de configuração, finaliza o modo de configuração e retorna ao modo EXEC privilegiado.|
|**Ctrl-Shift-6**|Sequência de quebra para todos os fins usada para abortar pesquisas de DNS, traceroutes, pings e interromper um processo de IOS.|
