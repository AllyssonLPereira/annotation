---
tags:
  - arquivo
---
##### Interface de linha de comando do Cisco IOS

A interface da linha de comando (CLI) do Cisco IOS é um programa baseado em texto que permite inserir e executar o comandos do Cisco IOS para configurar, monitorar e administrar dispositivos da Cisco. É possível usar a CLI da Cisco com tarefas de gerenciamento em banda ou fora da banda.

Os comandos da CLI são usados para modificar a configuração de dispositivos e exibir o status atual dos processos no roteador. Para usuários experientes, a CLI oferece muitos recursos de economia de tempo para criar configurações simples e complexas. 

Quase todos os dispositivos de rede da Cisco usam uma CLI semelhante. Quando o roteador conclui a sequência de inicialização e o prompt **Router>** aparece, a CLI pode ser usada para inserir comandos do Cisco IOS.

Os técnicos familiarizados com os comandos IOS e a operação de CLI facilmente monitoram e configuram diferentes dispositivos de rede porque os mesmos comandos básicos são usados configurar um switch e um roteador. A CLI tem um sistema amplo de ajuda que auxilia os usuários na configuração e no monitoramento de dispositivos.

---
##### Modos de Comando Primários

Todos os dispositivos de rede requerem um SO e podem ser configurados usando a CLI ou uma GUI. O uso da CLI pode fornecer ao administrador de rede controle e flexibilidade mais precisos do que usar a GUI.

Como recurso de segurança, o software Cisco IOS separa o acesso de gerenciamento nestes dois modos de comando:

- **[Modo EXEC do usuário]** - Este modo tem recursos limitados, mas é útil para operações básicas. Ele permite apenas um número limitado de comandos de monitoramento básicos, mas não permite a execução de nenhum comando que possa alterar a configuração do dispositivo. [O modo EXEC usuário é identificado pelo prompt da CLI que termina com o símbolo >].

- **[Modo EXEC privilegiado]** - Para executar comandos de configuração, um administrador de rede deve acessar o modo EXEC privilegiado. Modos de configuração mais altos, como o modo de configuração global, só podem ser acessados do modo EXEC privilegiado. [O modo EXEC privilegiado pode ser identificado pelo prompt que termina com o símbolo #].

A tabela resume os dois modos e exibe os prompts da CLI padrão de um switch e roteador Cisco.

| Modo de comando        | Descrição                                                                                                                                                                   | Prompt padrão do dispositivo |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| Modo EXEC do Usuário   | - O modo permite somente uma quantidade limitada de comandos básicos de monitoramento.<br>- Ele é frequentemente denominado modo “Somente visualização”.                    | Switch>   <br>Router>        |
| Modo EXEC privilegiado | - O modo permite acesso a todos os comandos e recursos.<br>- O usuário pode utilizar qualquer comando de monitoramento e executar comandos de configuração e gerenciamento. | Switch#  <br>Router#         |

