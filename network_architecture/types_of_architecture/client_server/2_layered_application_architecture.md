---
tags:
  - arquivo
---
## What is layered architecture?

Arquitetura em camadas é um maneira de organizar um sistema em camadas distintas, na qual cada camada possui uma função singular. Com isso, temos uma:

- Hierarquia de comunicação entre as camadas;
- Abstração das camadas superiores em relação às inferiores.

Uma arquitetura comum em camadas para aplicações web teria a:

- *Presentation layer*: responsável pelo que o usuário vê e pela interação dele com o sistema.

	- Exibe a interface para o usuário e captura sua interação;
	- Envia requisições para a camada de aplicação;
	- Recebe os resultados para exibição;

- *Application layer*: contém a lógica principal do sistema, coordenando a funcionalidade geral e o fluxo de dados.

- *Data layer*: armazena os dados.

---
## Two layer applications

Nas aplicações de 2 camadas, nos temos a *presentation* — código que gera a interface visual do programa — e a *business logic* — maneira como os dados serão acessados e processados, além de questões relacionadas à legislação fiscal e escrita contábil — pertencentes à aplicação client.

Com isso, temos problemas sérios, pois, uma simples mudança na interface do usuário ou, ainda, uma mudança de lei torna necessário a atualização da aplicações em cada dispositivo client.

Já a outra camada é o banco de dados.

Resumindo:

- Camada client trabalha com a lógica de negócios e a UI.
- Camada server trata do dados.

---
## Three layer applications

O modelo em 3 camadas é uma evolução da de 2 camadas, retirando a parte da *business logic* do lado client e centralizando-o em um server, chamado *application server*. 

Inicialmente, o desenvolvimento é mais demorado por dar suporte a uma quantidade maior de plataformas e ambientes. Mas o retorno é positivo, tendo respostas mais rápidas nas requisições.

Toda a regra para acessar o *data base* está contida no *application server*, sendo assim, os clients não acessam o banco sem antes passar pelo *application server*.

---
## Four layer applications

O modelo em 4 camadas é uma evolução da de 3 camadas, retirando a parte da *presentation* do lado client e centralizando-o em um server, sendo, geralmente, um *web server*. O acesso a aplicação é feito por meio de um navegador.


