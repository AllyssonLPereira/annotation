---
tags:
  - arquivo
---
## What is "thin client"?

Um "cliente magro" é um computador cliente numa rede modelo client/server de duas camadas na qual tem poucos ou nenhum aplicativo instalado, dependendo primariamente/totalmente de um servidor para o processamento de atividades.

A palavra "thin" se refere a uma pequena imagem de boot que tais clientes tipicamente requerem - talvez não mais do que o necessário para fazer a conexão com a rede e iniciar um navegador web dedicado ou uma conexão de "Área de Trabalho Remota".

Um "_thin client_" é um computador de rede diskless, projetado para ser pequeno e de custo reduzido. Ele executa aplicativos cliente/servidor, onde o processamento em massa dos dados ocorre no servidor.

> [!NOTE] Diskless
> Ele é apresentado como diskless, pois a operação da máquina é totalmente sem _disco rígido_, com um boot "remoto". O boot pode ser realizado por meio de _disquete_, _boot rom_ ou pelo _PXE_.

---
## Details

Ao se projetar um aplicativo cliente-servidor, há uma decisão a ser tomada sobre quais partes da tarefa devem ser executadas no cliente e quais o seriam no servidor. 

Esta decisão pode afetar de modo crucial o custo de clientes e servidores, a robustez e a segurança do aplicativo como um todo e a flexibilidade do projeto para uma modificação ou porte posterior para outra plataforma.

Uma questão de projeto é o quão específico o programa aplicativo do cliente deverá ser. Usar programas de clientes padronizados tais como um navegador Web ou um gerenciador de janelas X11 pode economizar custos de desenvolvimento, visto que não se precisa desenvolver um programa cliente customizado - porém, deve-se aceitar as limitações do cliente padrão.

A maioria do thin client existe só em nível de software.

---
## Application program

Um "thin client", como um programa aplicativo, conta com um servidor de aplicativos para as tarefas mais relevantes de sua lógica interna, tendo um mínimo de hardware e software presentes na máquina cliente. Este servidor de aplicativos é um sistema executado num servidor localizado na LAN, MAN ou WAN.

Outro critério está relacionado com o gerenciamento da máquina ou do programa cliente. Se for feito de modo centralizado, ele é, muito provavelmente, _thin_.

---
## User interface device

Um "thin client", como dispositivo, contém apenas o necessário para os programas de interface de usuário. Geralmente, eles não possuem HD's, usando armazenamento em memória somente leitura, tais como CD-ROM, Network virtual drive ou memória flash.

Idealmente, seria necessário apenas uma tela, um teclado, um dispositivo apontador e processamento o suficiente para a exibição de imagens e as comunicações.

---
## Ultra thin client

O ultra thin client vai além do thin client, pois este executa o programa de execução cliente diretamente do hardware do aplicativo. Um thin client legado executa o S.O. — geralmente Windows CE ou linux — entre o hardware e o programa de conexão cliente, já o ultra não possui S.O.

---
## What is "thick client"?

Um "thick cliente" é um computador que possui capacidade/recursos suficientes para realizar boa parte das operações por si próprio, dependendo o mínimo possível do servidor.
