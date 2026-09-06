---
tags:
  - arquivo
---
## Introduction

O modelo *`client/server`* é uma *estrutura de aplicação distribuída* que distribui as tarefas e cargas de trabalho entre os fornecedores de um recurso ou serviço, designados como *`servers`*, e os requerentes dos serviços, designados como *`clients`*.

> Geralmente os *clients e servers* comunicam através de uma rede de computadores em computadores distintos.

Um *server* é um _host_ que está executando um ou mais serviços ou programas que compartilham recursos com os *client*s. Um *client* não compartilha qualquer de seus recursos, mas solicita um conteúdo ou função do *server*. Os *client*s iniciam sessões de comunicação com os *servers* que aguardam requisições de entrada.

---
## Types of client/server:

Após vários modelos estudados de *client/server*, caracterizou-se chamar tecnicamente de *multilayer architecture*, inspirado nas camadas no modelo OSI.

O processo de dividir a arquitetura de *client/server* em várias camadas lógicas facilita o processo de *distributed programming*, existindo desde o modelo mais simples de *two layers*, e o mais utilizado atualmente que é o modelo de *three layers*, que é paralelo ao modelo de arquitetura de software denominado *`Model View Controller — MVC`*.

---
## Advantages:

Todos os dados são armazenados nos *servers*, que geralmente possuem controles de segurança muito maiores do que a maioria dos *client*s. Os *servers* podem controlar melhor o acesso a recursos, para garantir que apenas os *client*s com credenciais válidas possam aceder e alterar os dados.

Como o armazenamento de dados é centralizado, as atualizações dos dados são muito mais fáceis de administrar em comparação com o paradigma P2P.

## Disadvantages:

*Client*s podem solicitar serviços, mas não podem oferecê-los para outros *client*s, sobrecarregando o *server*, pois quanto mais *client*s, mais informações, o que irá demandar mais banda.

Um *server* poderá ficar sobrecarregado caso receba mais solicitações simultâneas dos *client*s do que pode suportar.

Este modelo não possui a robustez de uma rede baseada em P2P. Na arquitetura *client/server*, se um *server* crítico falha, os pedidos dos *client*s não poderão ser cumpridos.



