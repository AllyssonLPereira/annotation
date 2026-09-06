---
tags:
  - arquivo
---
 As comunicações HTTP consistem principalmente em uma solicitação HTTP e uma resposta HTTP. Uma solicitação HTTP é feita pelo cliente (por exemplo, cURL/browser) e é processada pelo servidor (por exemplo, servidor web). 

As solicitações contêm todos os detalhes que exigimos do servidor, incluindo o recurso (por exemplo. URL, caminho, parâmetros), quaisquer dados de solicitação, cabeçalhos ou opções que especificarmos e muitas outras opções.

Uma vez que o servidor recebe a solicitação HTTP, ele a processa e responde enviando a resposta HTTP, que contém o código de resposta e pode conter os dados do recurso se o solicitante tiver acesso a ele.

---
### HTTP request

Vamos começar examinando o seguinte exemplo de solicitação HTTP:

![[http_request.png]]

A imagem acima mostra uma solicitação HTTP GET para o URL:

- `http://inlanefreight.com/users/login.html`

A primeira linha de qualquer solicitação HTTP contém três campos principais 'separados por espaços':

|**Campo**|**Exemplo**|**Descrição**|
|---|---|---|
|`Method`|`GET`|O método ou verbo HTTP, que especifica o tipo de ação a ser executada.|
|`Path`|`/users/login.html`|O caminho para o recurso que está sendo acessado. Este campo também pode ser sufixo com uma string de consulta (por exemplo. `?username=user`).|
|`Version`|`HTTP/1.1`|O terceiro e último campo é usado para denotar a versão HTTP.|

O próximo conjunto de linhas contém pares de valores de cabeçalho HTTP, como: `Host`, `User-Agent`, `Cookie`, e muitos outros cabeçalhos possíveis. Esses cabeçalhos são usados para especificar vários atributos de uma solicitação. 

Os cabeçalhos são terminados com uma nova linha, que é necessária para o servidor validar a solicitação. Finalmente, uma solicitação pode terminar com o corpo e os dados da solicitação.

> [!NOTE]
> HTTP versão 1.X envia solicitações como texto claro e usa um caractere de nova linha para separar campos diferentes e solicitações diferentes. HTTP versão 2.X, por outro lado, envia solicitações como dados binários em um formulário de dicionário.

---
### HTTP response

Uma vez que o servidor processa nossa solicitação, ele envia sua resposta. A seguir, um exemplo de resposta HTTP:

![[http_response.png]]

A primeira linha de uma resposta HTTP contém dois campos separados por espaços. O primeiro é o `HTTP version` (por exemplo. `HTTP/1.1`), e o segundo denota o `HTTP response code` (por exemplo, `200 OK`).

Os códigos de resposta são usados para determinar o status da solicitação. Após a primeira linha, a resposta lista seus cabeçalhos, semelhante a uma solicitação HTTP.

Finalmente, a resposta pode terminar com um corpo de resposta, que é separado por uma nova linha após os cabeçalhos. O corpo de resposta é geralmente definido como código `HTML`. 

No entanto, ele também pode responder com outros tipos de código, como `JSON`, recursos do site, como imagens, folhas de estilo ou scripts, ou até mesmo um documento, como um documento PDF hospedado no servidor da web.

---
## cURL

Em nossos exemplos anteriores com cURL, especificamos apenas a URL e obtivemos o corpo de resposta em troca. 

No entanto, o cURL também nos permite visualizar a solicitação HTTP completa e a resposta HTTP completa, o que pode se tornar muito útil ao realizar testes de penetração na web ou escrever exploits. 

Para visualizar a solicitação e a resposta HTTP completas, podemos simplesmente adicionar o `-v` para nossos comandos anteriores, e deve imprimir tanto a solicitação e resposta:

``` shell
allysson7@htb[/htb]$ curl inlanefreight.com -v

*   Trying SERVER_IP:80...
* TCP_NODELAY set
* Connected to inlanefreight.com (SERVER_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: inlanefreight.com
> User-Agent: curl/7.65.3
> Accept: */*
> Connection: close
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< WWW-Authenticate: Basic realm="Restricted Content"
< Content-Length: 464
< Content-Type: text/html; charset=iso-8859-1
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>

...SNIP...
```

Como podemos ver, desta vez, obtemos a solicitação e a resposta HTTP completas. O pedido foi simplesmente enviado `GET / HTTP/1.1` junto com o `Host`, `User-Agent` e `Accept` cabeçalhos. 

Em troca, a resposta HTTP continha o `HTTP/1.1 401 Unauthorized`, o que indica que não temos acesso sobre o recurso solicitado. Semelhante ao pedido, a resposta também continha vários cabeçalhos enviados pelo servidor, incluindo `Date`, `Content-Length` e `Content-Type`. 

Finalmente, a resposta continha o corpo de resposta em HTML, que é o mesmo que recebemos anteriormente ao usar cURL sem o `-v`.

---
## DevTools

A maioria dos navegadores modernos vem com ferramentas de desenvolvedor integradas (`DevTools`), que são destinados principalmente para desenvolvedores para testar suas aplicações web. 

No entanto, como testadores de penetração na web, essas ferramentas podem ser um ativo vital em qualquer avaliação da web que realizamos, pois um navegador (e seu DevTools) estão entre os ativos que provavelmente teremos em todos os exercícios de avaliação da web. 

Sempre que visitamos qualquer site ou acessamos qualquer aplicativo da web, nosso navegador envia várias solicitações da web e lida com várias respostas HTTP para renderizar a visualização final que vemos na janela do navegador. .

Se clicarmos no separador Rede e atualizarmos a página, poderemos ver a lista de pedidos enviados pela página: