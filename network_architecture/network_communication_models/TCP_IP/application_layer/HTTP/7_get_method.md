---
tags:
  - arquivo
---
Sempre que visitamos qualquer URL, nossos navegadores usam como padrão uma solicitação GET para obter os recursos remotos hospedados nessa URL. Uma vez que o navegador recebe a página inicial que está solicitando; ele pode enviar outras solicitações usando vários métodos HTTP.

---
### HTTP Basic Auth

Ao contrário dos formulários de login comuns, que utilizam parâmetros HTTP para validar as credenciais do usuário (por exemplo, solicitação POST), este tipo de autenticação utiliza uma autenticação HTTP básica, que é ***gerenciada diretamente pelo servidor web para proteger uma página/diretório específico***, sem interagir diretamente com a aplicação web.

Se tentássemos acessar uma página que utiliza `HTTP basic auth` com o `cURL`, aconteceria isso:

``` shell
allysson7@htb[/htb]$ curl -i http://<SERVER_IP>:<PORT>/
HTTP/1.1 401 Authorization Required
Date: Mon, 21 Feb 2022 13:11:46 GMT
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-cache, must-revalidate, max-age=0
WWW-Authenticate: Basic realm="Access denied"
Content-Length: 13
Content-Type: text/html; charset=UTF-8

Access denied
```

Como podemos ver, obtemos `Access denied` no corpo da resposta e também `Basic realm="Access denied"` no cabeçalho `WWW-Authenticate`, o que confirma que esta página realmente utiliza `HTTP basic auth`. 

Para fornecer as credenciais via `cURL`, podemos usar a flag `-u`, da seguinte forma:

``` shell
allysson7@htb[/htb]$ curl -u admin:admin http://<SERVER_IP>:<PORT>/

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
```

Desta vez, obtemos a página na resposta. Há outro método para fornecer as credenciais `HTTP basic auth`, que é diretamente pela URL - `username:password@URL`. Se tentarmos o mesmo com o `cURL` ou com o nosso navegador, também obteremos acesso à página:

``` shell
allysson7@htb[/htb]$ curl http://admin:admin@<SERVER_IP>:<PORT>/

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
```

---
### HTTP Authorization Header

Se adicionarmos o sinalizador `-v` a qualquer um dos nossos comandos `cURL` anteriores:

``` shell
allysson7@htb[/htb]$ curl -v http://admin:admin@<SERVER_IP>:<PORT>/

*   Trying <SERVER_IP>:<PORT>...
* Connected to <SERVER_IP> (<SERVER_IP>) port PORT (#0)
* Server auth using Basic with user 'admin'
> GET / HTTP/1.1
> Host: <SERVER_IP>
> Authorization: Basic YWRtaW46YWRtaW4=
> User-Agent: curl/7.77.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Mon, 21 Feb 2022 13:19:57 GMT
< Server: Apache/2.4.41 (Ubuntu)
< Cache-Control: no-store, no-cache, must-revalidate
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Pragma: no-cache
< Vary: Accept-Encoding
< Content-Length: 1453
< Content-Type: text/html; charset=UTF-8
< 

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
```

Como estamos usando autenticação HTTP básica, vemos que nossa requisição HTTP define o cabeçalho de Autorização como `Basic YWRtaW46YWRtaW4=`, que é o valor codificado em base64 de `admin:admin`.

Se estivéssemos usando um método de autenticação moderno - por exemplo, `JWT`, a Autorização seria do tipo Portador e conteria um token criptografado mais longo.

Vamos tentar definir manualmente a Autorização, sem fornecer as credenciais, para ver se ela nos permite acessar a página. Podemos definir o cabeçalho com a flag `-H` e usaremos o mesmo valor da requisição HTTP acima.

Podemos adicionar a flag `-H` várias vezes para especificar vários cabeçalhos:

``` shell
allysson7@htb[/htb]$ curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/

<!DOCTYPE html
<html lang="en">

<head>
...SNIP...
```

Como podemos ver, isso também nos deu acesso à página. 

Estes são alguns métodos que podemos usar para autenticar a página. A maioria dos aplicativos web modernos usa formulários de login criados com a linguagem de script back-end (por exemplo, PHP), que utiliza solicitações `HTTP POST` para autenticar os usuários e, em seguida, retorna um cookie para manter a autenticação.

---
## GET Parameters

Após a autenticação, temos acesso à função de Pesquisa de Cidades, na qual podemos inserir um termo de pesquisa e obter uma lista de cidades correspondentes