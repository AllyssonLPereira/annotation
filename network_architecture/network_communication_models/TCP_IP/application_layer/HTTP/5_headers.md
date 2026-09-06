---
tags:
  - arquivo
---
Os cabeçalhos HTTP passam informações entre o cliente e o servidor. Alguns cabeçalhos são usados apenas com solicitações ou respostas, enquanto outros cabeçalhos gerais são comuns a ambos.

Podemos dividir cabeçalhos nas seguintes categorias:

1. `General Headers`;
2. `Entity Headers`;
3. `Request Headers`;
4. `Response Header`;
5. `Security Header`;

Vamos discutir cada uma dessas categorias.

---
### General Headers

[Cabeçalhos gerais](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html) são usados em solicitações e respostas HTTP. São contextuais e estão habituados a `describe the message rather (em vez) than its contents`.

| **Cabeçalho** | **Exemplo**                           | **Descrição**                                                                                                                                                                                                                                                                                                                                                 |
| ------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Date`        | `Date: Wed, 16 Feb 2022 10:38:44 GMT` | Mantém a data e hora em que a mensagem se originou. É preferível converter o tempo para o padrão [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).                                                                                                                                                                                             |
| `Connection`  | `Connection: close`                   | Dita se a conexão de rede atual deve permanecer viva após o término da solicitação. Dois valores comumente usados para este cabeçalho são `close` e `keep-alive`. O `close` do cliente ou servidor significa que eles gostariam de encerrar a conexão, enquanto o `keep-alive` indica que a conexão deve permanecer aberta para receber mais dados e entrada. |

---
### Entity Headers

Semelhante aos cabeçalhos gerais, [Cabeçalhos Entidade](https://www.rfc-editor.org/rfc/rfc9110.html) pode ser `common to both (ambos) the request and response`. Esses cabeçalhos são usados para `describe the content` (entidade) transferida por uma mensagem. Eles geralmente são encontrados em respostas e solicitações POST ou PUT.

| **Cabeçalho**      | **Exemplo**                   | **Descrição**                                                                                                                                                                                                                                                          |
| ------------------ | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Type`     | `Content-Type: text/html`     | Usado para descrever o tipo de recurso que está sendo transferido. O valor é adicionado automaticamente pelos navegadores no lado do cliente e retornado na resposta do servidor. O campo `charset` denota o padrão de codificação, tais como [UTF-8].                 |
| `Media-Type`       | `Media-Type: application/pdf` | O `media-type` é semelhante a `Content-Type`, e descreve os dados que estão sendo transferidos. Este cabeçalho pode desempenhar um papel crucial em fazer o servidor interpretar a nossa entrada. O `charset` também pode ser usado com este cabeçalho.                |
| `Boundary`         | `boundary="b4e4fbd93540"`     | Atua como um marcador para separar o conteúdo quando há mais de um na mesma mensagem. Por exemplo, dentro de um formulário de dados, esse limite é usado como `--b4e4fbd93540` para separar diferentes partes do formulário.                                           |
| `Content-Length`   | `Content-Length: 385`         | Detém o tamanho da entidade que está sendo passada. Esse cabeçalho é necessário, pois o servidor o usa para ler dados do corpo da mensagem e é gerado automaticamente pelo navegador e por ferramentas como o cURL.                                                    |
| `Content-Encoding` | `Content-Encoding: gzip`      | Os dados podem sofrer várias transformações antes de serem passados. Por exemplo, grandes quantidades de dados podem ser compactados para reduzir o tamanho da mensagem. O tipo de codificação que está sendo usado deve ser especificado usando o `Content-Encoding`. |

---
### Request Headers

Esses cabeçalhos são `used in an HTTP request and do not relate to the content` da mensagem. Os seguintes cabeçalhos são comumente vistos em solicitações HTTP.

| **Cabeçalho**   | **Exemplo**                              | **Descrição**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------- | ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Host`          | `Host: www.inlanefreight.com`            | Usado para especificar o host que está sendo consultado para o recurso. Pode ser um nome de domínio ou um endereço IP. Os servidores HTTP podem ser configurados para hospedar diferentes sites, que são revelados com base no nome do host. Isso torna o cabeçalho do host um destino de enumeração importante, pois pode indicar a existência de outros hosts no servidor de destino.                                                                                    |
| `User-Agent`    | `User-Agent: curl/7.77.0`                | O `User-Agent` é usado para descrever o cliente solicitando recursos. Esse cabeçalho pode revelar muito sobre o cliente, como o navegador, sua versão e o sistema operacional.                                                                                                                                                                                                                                                                                             |
| `Referer`       | `Referer: http://www.inlanefreight.com/` | Indica de onde vem a solicitação atual. Por exemplo, clicar em um link dos resultados de pesquisa do Google faria `https://google.com` o árbitro. Confiar neste cabeçalho pode ser perigoso, pois pode ser facilmente manipulado, levando a consequências não intencionais.                                                                                                                                                                                                |
| `Accept`        | `Accept: */*`                            | O `Accept` cabeçalho descreve quais tipos de mídia o cliente pode entender. Ele pode conter vários tipos de mídia separados por vírgulas. O `*/*` valor significa que todos os tipos de mídia são aceitos.                                                                                                                                                                                                                                                                 |
| `Cookie`        | `Cookie: PHPSESSID=b4e4fbd93540`         | Contém pares de valor de cookie no formato `name=value`. ***O cookie é um pedaço de dado armazenado no lado do cliente e no servidor, que atua como um identificador***. Estes são passados para o servidor por solicitação, mantendo assim o acesso do cliente. Os cookies também podem servir a outros propósitos, como salvar as preferências do usuário ou o rastreamento de sessão. Pode haver vários cookies em um único cabeçalho separados por um ponto e vírgula. |
| `Authorization` | `Authorization: BASIC cGFzc3dvcmQK`      | Outro método para o servidor identificar clientes. Após a autenticação bem-sucedida, o servidor retorna um token exclusivo para o cliente. ***Ao contrário dos cookies, os tokens são armazenados apenas no lado do cliente e recuperados pelo servidor por solicitação***. Existem vários tipos de tipos de autenticação com base no servidor web e no tipo de aplicativo usado.                                                                                          |

***Uma lista completa de cabeçalhos de solicitação e seu uso pode ser encontrada [aqui](https://tools.ietf.org/html/rfc7231#section-5).

---
### Response Header

[Cabeçalhos de Resposta](https://tools.ietf.org/html/rfc7231#section-7) pode ser `used in an HTTP response and do not relate to the content`. Alguns cabeçalhos de resposta, como `Age`, `Location` e `Server` são usados para fornecer mais contexto sobre a resposta. Os seguintes cabeçalhos são comumente vistos em respostas HTTP.

| **Cabeçalho**      | **Exemplo**                                 | **Descrição**                                                                                                                                                                                                   |
| ------------------ | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Server`           | `Server: Apache/2.2.14 (Win32)`             | Contém informações sobre o servidor HTTP, que processou a solicitação. Ele pode ser usado para obter informações sobre o servidor, como sua versão, e enumerá-lo ainda mais.                                    |
| `Set-Cookie`       | `Set-Cookie: PHPSESSID=b4e4fbd93540`        | Contém os cookies necessários para a identificação do cliente. Os navegadores analisam os cookies e os armazenam para solicitações futuras. Este cabeçalho segue o mesmo formato que o `Cookie` da solicitação. |
| `WWW-Authenticate` | `WWW-Authenticate: BASIC realm="localhost"` | Notifica o cliente sobre o tipo de autenticação necessária para acessar o recurso solicitado.                                                                                                                   |

---
### Security Header

Finalmente, temos [Cabeçalhos de Segurança](https://owasp.org/www-project-secure-headers/). Com o aumento da variedade de navegadores e ataques baseados na web, foi necessário definir certos cabeçalhos que aumentassem a segurança. Os cabeçalhos de segurança HTTP são `a class of response headers used to specify certain rules and policies` para ser seguido pelo navegador ao acessar o site.

| **Cabeçalho**               | **Exemplo**                                   | **Descrição**                                                                                                                                                                                                                                                                                                                                        |
| --------------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Security-Policy`   | `Content-Security-Policy: script-src 'self'`  | Dita a política do site em relação aos recursos injetados externamente. Isso pode ser código JavaScript, bem como recursos de script. Este cabeçalho instrui o navegador a aceitar recursos apenas de determinados domínios confiáveis, evitando assim ataques como [Scripts entre sites (XSS)](https://en.wikipedia.org/wiki/Cross-site_scripting). |
| `Strict-Transport-Security` | `Strict-Transport-Security: max-age=31536000` | Impede que o navegador acesse o site através do protocolo HTTP de texto simples e força toda a comunicação a ser transportada pelo protocolo HTTPS seguro. Isso impede que os invasores detectem o tráfego da Web e acessem informações protegidas, como senhas ou outros dados confidenciais.                                                       |
| `Referrer-Policy`           | `Referrer-Policy: origin`                     | Dita se o navegador deve incluir o valor especificado através do `Referer` ou não. Ele pode ajudar a evitar a divulgação de URLs e informações confidenciais durante a navegação no site.                                                                                                                                                            |

> [!NOTE] 
> Existem muitos outros cabeçalhos contextuais que podem ser usados em comunicações HTTP. Também é possível que os aplicativos definam cabeçalhos personalizados com base em seus requisitos. Uma lista completa de cabeçalhos HTTP padrão pode ser encontrada [aqui](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

---
### cURL

Na seção anterior, vimos como usar o `-v` com `cURL`, nos mostrando os detalhes completos da solicitação e resposta HTTP. 

Se estivéssemos interessados apenas em ver os cabeçalhos de resposta, poderíamos usar a flag `-I`para enviar um `HEAD` e exibir apenas os cabeçalhos de resposta. Além disso, podemos usar o `-i` para exibir os cabeçalhos e o corpo de resposta (por exemplo. código HTML). 

A diferença entre os dois é que `-I` envia um `HEAD` pedido, enquanto `-i` envia qualquer solicitação que especificar e imprime os cabeçalhos também.

O comando a seguir mostra uma saída de exemplo de uso do `-I` bandeira:

```shell
allysson7@htb[/htb]$ curl -I https://www.inlanefreight.com

Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/605.1.15 (KHTML, like Gecko)
Cookie: cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4
Accept: text/plain
Referer: https://www.inlanefreight.com/
Authorization: BASIC cGFzc3dvcmQK

Date: Sun, 06 Aug 2020 08:49:37 GMT
Connection: keep-alive
Content-Length: 26012
Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: gzip
Server: Apache/2.2.14 (Win32)
Set-Cookie: name1=value1,name2=value2; Expires=Wed, 09 Jun 2021 10:18:14 GMT
WWW-Authenticate: BASIC realm="localhost"
Content-Security-Policy: script-src 'self'
Strict-Transport-Security: max-age=31536000
Referrer-Policy: origin
```

Além de visualizar cabeçalhos, o cURL também nos permite definir cabeçalhos de solicitação com a flag `-H`. 

Alguns cabeçalhos, como o `User-Agent` ou `Cookie` têm suas próprias flags. Por exemplo, podemos usar o `-A` para definir o nosso `User-Agent`, como segue:

```shell
allysson7@htb[/htb]$ curl https://www.inlanefreight.com -A 'Mozilla/5.0'

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```
