---
tags:
  - arquivo
---
HTTP suporta vários métodos para acessar um recurso. No protocolo HTTP, vários métodos de solicitação permitem que o navegador envie informações, formulários ou arquivos para o servidor. 

***Esses métodos são usados, entre outras coisas, para informar ao servidor como processar a solicitação que enviamos ([COMO DEVE PROCEDER À SOLICITAÇÃO]) e como responder.

Com cURL, se nós usarmos `-v` para visualizar a solicitação completa, a primeira linha contém o método HTTP (por exemplo. `GET / HTTP/1.1`), enquanto com devtools do navegador, o método HTTP é mostrado na coluna `Method`. 

***Além disso, os cabeçalhos de resposta também contêm o código de resposta HTTP, que indica o status do processamento de nossa solicitação HTTP.

---
### Request Methods

A seguir estão alguns dos métodos comumente usados:

|**Método**|**Descrição**|
|---|---|
|`GET`|Solicita um recurso específico. Dados adicionais podem ser passados para o servidor através de strings de consulta no URL (por exemplo. `?param=value`).|
|`POST`|Envia dados para o servidor. Ele pode lidar com vários tipos de entrada, como texto, PDFs e outras formas de dados binários. Esses dados são anexados no corpo da solicitação presente após os cabeçalhos. O método POST é comumente usado ao enviar informações (por exemplo, formulários/logins) ou carregar dados para um site, como imagens ou documentos.|
|`HEAD`|Solicita os cabeçalhos que seriam retornados se uma solicitação GET fosse feita ao servidor. Ele não retorna o corpo da solicitação e geralmente é feito para verificar o comprimento da resposta antes de baixar os recursos.|
|`PUT`|Cria novos recursos no servidor. Permitir esse método sem controles adequados pode levar ao upload de recursos maliciosos.|
|`DELETE`|Exclui um recurso existente no servidor web. Se não estiver devidamente protegido, pode levar a Negação de Serviço (DoS), excluindo arquivos críticos no servidor web.|
|`OPTIONS`|Retorna informações sobre o servidor, como os métodos aceitos por ele.|
|`PATCH`|Aplica modificações parciais ao recurso no local especificado.|

> [!NOTE]
> A lista destaca apenas alguns dos métodos HTTP mais usados. A disponibilidade de um método específico depende do servidor, bem como da configuração do aplicativo. Para obter uma lista completa de métodos HTTP, você pode visitar este [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

> [!NOTE]
> A maioria dos aplicativos web modernos depende principalmente do `GET` e `POST` métodos. No entanto, qualquer aplicativo da Web que utiliza APIs REST também depende de `PUT` e `DELETE`, que são usados para atualizar e excluir dados no endpoint da API, respectivamente.

---
### Response Codes

Os códigos de status HTTP são usados para informar ao cliente o status de sua solicitação. Um servidor HTTP pode retornar cinco tipos de códigos de resposta:

|**Tipo**|**Descrição**|
|---|---|
|`1xx`|Fornece informações e não afeta o processamento da solicitação.|
|`2xx`|Retornado quando uma solicitação é bem-sucedida.|
|`3xx`|Retornado quando o servidor redireciona o cliente.|
|`4xx`|Significa solicitações impróprias `from the client`. Por exemplo, solicitar um recurso que não existe ou solicitar um formato incorreto.|
|`5xx`|Retornado quando há algum problema `with the HTTP server` em si.|

A seguir estão alguns dos exemplos comumente vistos de cada um dos tipos de método HTTP acima:

|**Código**|**Descrição**|
|---|---|
|`200 OK`|Retornado em uma solicitação bem-sucedida e o corpo de resposta geralmente contém o recurso solicitado.|
|`302 Found`|Redireciona o cliente para outro URL. Por exemplo, redirecionando o usuário para o painel após um login bem-sucedido.|
|`400 Bad Request`|Retornado ao encontrar solicitações malformadas, como solicitações com terminadores de linha ausentes.|
|`403 Forbidden`|Significa que o cliente não tem acesso apropriado ao recurso. Ele também pode ser retornado quando o servidor detecta entrada maliciosa do usuário.|
|`404 Not Found`|Retornado quando o cliente solicita um recurso que não existe no servidor.|
|`500 Internal Server Error`|Retornado quando o servidor não pode processar a solicitação.|

> [!NOTE]
> Para obter uma lista completa de códigos de resposta HTTP padrão, você pode visitar este [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). Além dos códigos HTTP padrão, vários servidores e provedores, como [Cloudflare](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes) ou [AWS](https://docs.aws.amazon.com/AmazonSimpleDB/latest/DeveloperGuide/APIError.html) implementar seus próprios códigos.

