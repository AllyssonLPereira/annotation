---
tags:
  - arquivo
---
## URI, URN and URL

Recursos e serviços da *Web*, como APIs RESTful, são identificados usando uma *`Uniform Resource Identifier — URI`*. Um URI é uma sequência de caracteres que identifica um recurso de rede específico. Uma URI tem duas especializações:

- *`Uniform Resource Name — URN`* — identifica apenas o espaço para nome do recurso — página da web, documento, imagem etc., sem referência ao protocolo.

- *`Uniform Resource Locator — URL`* — define o local da rede de um recurso específico. URLs de HTTP ou HTTPS são normalmente usados por navegadores web. Outros protocolos como FTP, SFTP, SSH e outros podem ser usados por meio de uma URL. Uma URL usando SFTP pode estar no formato: `sftp://sftp.example.com`.

Estas são as partes de uma URI, como mostrado no exemplo a seguir:

	`https://www.example.com/author/book.html#page155`

- *Protocol/scheme* — HTTPS ou outros protocolos como FTP, SFTP e NNTP;
- *Host name* — `www.example.com`;
- *File path and name* — `/author/book.html`;
- *Fragment* — `#page155`.