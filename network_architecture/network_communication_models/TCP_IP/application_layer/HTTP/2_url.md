---
tags:
  - arquivo
---
***Recursos via HTTP são acessados ​​por meio de uma URL***, que oferece muito mais especificações do que simplesmente especificar um site que queremos visitar.

![[url_schema.png]]
*Fonte: HackTheBox*

Veja o significado de cada componente:

| Componente   | Exemplo           | Descrição                                                                                                                                                                                                             |
| ------------ | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scheme       | http:// https://  | Usado para ***identificar o protocolo que está sendo acessado*** pelo cliente e termina com dois pontos e uma barra dupla (://).<br>                                                                                  |
| User Info    | admin:password@   | Este é um ***componente opcional*** que contém as *credenciais* (separadas por dois pontos, ":") usadas para autenticação no host e é separado do host por um símbolo de arroba.                                      |
| Host         | inlanefreight.com | O host indica a ***localização do recurso***. Pode ser um nome de host ou um endereço IP.                                                                                                                             |
| Port         | :80               | A porta é separada do host por dois pontos. Se nenhuma porta for especificada, o Scheme HTTP usa como padrão a porta 80 e o HTTPS usa como padrão a porta 443.                                                        |
| Path         | /dashboard.php    | ***Aponta para o recurso que está sendo acessado***, que pode ser um arquivo ou uma pasta. Se nenhum caminho for especificado, o servidor retornará o índice padrão (por exemplo, index.html).                        |
| Query String | ?login=true       | A *Query String* começa com um ponto de interrogação - ?, e ***consiste em um parâmetro*** (por exemplo, login) ***e um valor*** (por exemplo, true). Vários parâmetros podem ser separados por um "e" comercial - &. |
| Fragments    | #status           | Os fragmentos são processados ​​pelos navegadores no lado do cliente para localizar seções dentro do recurso primário (por exemplo, um cabeçalho ou seção na página).                                                 |

Nem todos os componentes são necessários para acessar um recurso. Os principais campos obrigatórios são o *scheme* e o *host*, sem os quais a solicitação não teria nenhum recurso para solicitar.

---
### HTTP Flow

![[http_flow.png]]*Fonte: HackTheBox*


O diagrama acima apresenta a anatomia de uma solicitação HTTP em um nível muito alto.

Na primeira vez que um usuário insere a URL no navegador, ele envia uma requisição a um servidor DNS para resolver o domínio e obter seu IP. O servidor DNS procura o endereço IP de inlanefreight.com e o retorna.

***Todos os nomes de domínio precisam ser resolvidos dessa forma, pois um servidor não pode se comunicar sem um endereço IP.

> [!NOTE]
> Nossos navegadores geralmente procuram primeiro os registros no arquivo local '/etc/hosts' e, se o domínio solicitado não existir nele, eles entrarão em contato com outros servidores DNS. Podemos usar o '/etc/hosts' para adicionar manualmente os registros para resolução de DNS, adicionando o IP seguido do nome de domínio.

Assim que o navegador obtém o endereço IP vinculado ao domínio requisitado, ele envia uma requisição GET para a porta HTTP padrão (por exemplo, 80), requisitando a raiz/caminho. Em seguida, o servidor web recebe a solicitação e a processa. *Por padrão, os servidores são configurados para retornar um arquivo de índice quando uma solicitação para "/" é recebida.

Nesse caso, o conteúdo de index.html é lido e retornado pelo servidor web como uma resposta HTTP. A resposta também contém o código de status (por exemplo, *200 OK*), que indica que a solicitação foi processada com sucesso. O navegador web então renderiza o conteúdo de index.html e o apresenta ao usuário.

---
### cURL

***cURL (client URL)*** *é uma ferramenta e biblioteca de linha de comando que suporta principalmente HTTP, além de muitos outros protocolos*. 

Isso a torna uma boa candidata para scripts e automação, sendo essencial para o envio de vários tipos de solicitações web a partir da linha de comando, o que é necessário para muitos tipos de testes de penetração web.

Podemos enviar uma solicitação HTTP básica para qualquer URL usando-a como argumento do cURL, da seguinte forma:

``` shell
allysson7@htb[/htb]$ curl inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

Vemos que cURL não renderiza o código HTML/JavaScript/CSS, ao contrário de um navegador web, mas o imprime em seu formato bruto. No entanto, ***[como testadores de penetração, estamos principalmente interessados ​​no contexto de solicitação e resposta, que geralmente se torna muito mais rápido e conveniente do que um navegador web]***.

Também podemos usar cURL para baixar uma página ou um arquivo e gerar o conteúdo em um arquivo usando a flag -O. Se quisermos especificar o nome do arquivo de saída, podemos usar a flag -o e especificar o nome. Caso contrário, podemos usar -O e o cURL usará o nome do arquivo remoto, como a seguir:

``` shell
allysson7@htb[/htb]$ curl -O inlanefreight.com/index.html
allysson7@htb[/htb]$ ls
index.html
```

Percebemos que o cURL ainda exibiu algum status durante o processamento da solicitação. Podemos silenciar o status com a flag -s, como a seguir:

``` shell
allysson7@htb[/htb]$ curl -s -O inlanefreight.com/index.html
```

Desta vez, o cURL não imprimiu nada, pois a saída foi salva no arquivo index.html. Por fim, podemos usar a flag -h para ver quais outras opções podemos usar com o cURL:

``` shell
allysson7@htb[/htb]$ curl -h
Usage: curl [options...] <url>

 -d, --data <data>          HTTP POST data
 -h, --help <category>      Get help for commands
 -i, --include              Include protocol response headers in the output
 -o, --output <file>        Write to file instead of stdout
 -O, --remote-name          Write output to a file named as the remote file
 -s, --silent               Silent mode
 -u, --user <user:password> Server user and password
 -A, --user-agent <name>    Send User-Agent <name> to server
 -v, --verbose              Make the operation more talkative
```

Esta não é a ajuda completa; este menu está dividido em categorias.

- Use "--help category" para obter uma visão geral de todas as categorias.
- Use o manual do usuário `man curl` ou a flag "--help all" para todas as opções.

Se precisarmos ler documentação mais detalhada, podemos usar man curl para visualizar a página completa do manual do cURL.

| **Comando**                                                                                                      | **Descrição**                                                    |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `curl -h`                                                                                                        | menu de ajuda do CURL                                            |
| `curl inlanefreight.com`                                                                                         | Pedido básico GET                                                |
| `curl -s -O inlanefreight.com/index.html`                                                                        | Baixar arquivo                                                   |
| `curl -k https://inlanefreight.com`                                                                              | Ignorar validação de certificado HTTPS (SSL)                     |
| `curl inlanefreight.com -v`                                                                                      | Imprimir detalhes completos de solicitação/resposta HTTP         |
| `curl -I https://www.inlanefreight.com`                                                                          | Enviar solicitação HEAD (somente imprime cabeçalhos de resposta) |
| `curl -i https://www.inlanefreight.com`                                                                          | Imprimir cabeçalhos de resposta e corpo de resposta              |
| `curl https://www.inlanefreight.com -A 'Mozilla/5.0'`                                                            | Definir cabeçalho User-Agent                                     |
| `curl -u admin:admin http://<SERVER_IP>:<PORT>/`                                                                 | Definir credenciais de autorização básicas HTTP                  |
| `curl http://admin:admin@<SERVER_IP>:<PORT>/`                                                                    | Passe credenciais de autorização básicas HTTP no URL             |
| `curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/`                                     | Definir cabeçalho da solicitação                                 |
| `curl 'http://<SERVER_IP>:<PORT>/search.php?search=le'`                                                          | Passar parâmetros GET                                            |
| `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`                                     | Enviar solicitação POST com dados POST                           |
| `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`                                      | Definir cookies de solicitação                                   |
| `curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php` | Enviar solicitação POST com dados JSON                           |