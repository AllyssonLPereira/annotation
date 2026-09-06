---
tags:
  - arquivo
---
Já vimos como as solicitações `GET` podem ser usadas por aplicativos da Web para funcionalidades como pesquisa e acesso a páginas. No entanto, sempre que os aplicativos da Web precisam transferir *arquivos ou mover os parâmetros do usuário do URL*, eles utilizam o método `POST`.

Diferente do `HTTP GET`, que coloca os parâmetros do usuário dentro da URL, `HTTP POST` *coloca os parâmetros do usuário dentro do corpo de solicitação* `HTTP`. Isso tem três benefícios principais:

- ***[Falta de registro]***: 

	Como as *solicitações POST podem transferir arquivos grandes* (por exemplo, upload de arquivos), não seria eficiente para o servidor registrar todos os arquivos carregados como parte da URL solicitada, como seria o caso de um arquivo carregado por meio de uma solicitação GET.

- ***[Menos requisitos de codificação]***: 

	As URLs são projetadas para serem compartilhadas, o que significa que elas precisam estar em conformidade com caracteres que podem ser convertidos em letras. A solicitação POST coloca dados no corpo, que podem aceitar dados binários.

	Os únicos caracteres que precisam ser codificados são aqueles que são usados para separar parâmetros.

- ***[Mais dados podem ser enviados]***: 

	O comprimento máximo de URL varia entre navegadores (Chrome/Firefox/IE), servidores web (IIS, Apache, nginx), Redes de Entrega de Conteúdo (Fastly, Cloudfront, Cloudflare) e até mesmo Encurtadores de URL (bit.ly, amzn.to). 

	De um modo geral, os comprimentos de um URL devem ser mantidos abaixo de 2.000 caracteres e, portanto, eles não podem lidar com muitos dados.

---
Com os dados da solicitação em mãos, podemos tentar enviar uma solicitação semelhante com cURL para verificar se isso nos permite efetuar login também.

No entanto, é importante poder criar solicitações POST manualmente, então vamos tentar fazer isso.

Usaremos a flag `-X POST` para enviar uma solicitação `POST`. Em seguida, para adicionar nossos dados `POST`, podemos usar a flag `-d` e adicionar os dados acima depois dela, da seguinte maneira:

``` shell
allysson7@htb[/htb]$ curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```

