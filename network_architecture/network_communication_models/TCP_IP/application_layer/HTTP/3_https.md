---
tags:
  - arquivo
---
### HTTPS Overview

Se examinarmos uma solicitação HTTP, podemos ver o efeito de não impor comunicações seguras entre um navegador e uma aplicação web. Por exemplo, o seguinte é o conteúdo de uma solicitação de login HTTP:

![[http_wireshark.png]]

Podemos ver que as credenciais de login podem ser visualizadas em texto simples. Isso facilitaria para alguém na mesma rede (como uma rede sem fio pública) capturar a solicitação e reutilizá-la para fins maliciosos.

Por outro lado, quando alguém intercepta e analisa o tráfego de uma solicitação HTTPS, verá algo como o seguinte:

![[https_wireshark.png]]

Como podemos ver, os dados são transferidos como um único fluxo criptografado, o que dificulta bastante a captura de informações como credenciais ou quaisquer outros dados confidenciais.

Sites que utilizam HTTPS podem ser identificados por meio de https:// em sua URL, bem como pelo ícone de cadeado na barra de endereços do navegador, à esquerda da URL.

Portanto, se visitarmos um site que utiliza HTTPS, como o Google, todo o tráfego será criptografado.

> [!NOTE]
> Embora os dados transferidos pelo protocolo HTTPS possam ser criptografados, a solicitação ainda poderá revelar a URL visitada se tiver contatado um servidor DNS de texto simples. Por esse motivo, é recomendável utilizar servidores DNS criptografados (por exemplo, 8.8.8.8 ou 1.1.1.1) ou utilizar um serviço de VPN para garantir que todo o tráfego seja criptografado corretamente.

Em outras palavras, HTTPS (HyperText Transfer Protocol Secure) é o **HTTP com segurança**. Ele protege os dados entre o cliente (como um navegador) e o servidor por meio de criptografia. A segurança é feita com um protocolo chamado **TLS** (antigo SSL).

---
### Certificados HTTPS

Para usar HTTPS, o servidor precisa de um **[certificado digital]**, que serve para provar que ele é realmente quem diz ser. Esses certificados são emitidos por uma **[Autoridade Certificadora (CA)]** confiável, como o **Let's Encrypt**.

O certificado tem validade (geralmente 90 dias no caso do Let's Encrypt) e precisa ser **[renovado periodicamente]**.

***Agora, é importante compreender que a criptografia acontece ANTES do HTTP***. A conexão segura (TLS) acontece **abaixo do HTTP**, no nível do **TCP**.

Isso significa que, antes de qualquer dado HTTP ser enviado, o servidor e o cliente já combinaram como os dados serão criptografados. **O certificado é usado durante esse processo inicial (chamado de "handshake TLS").**

Vale lembrar que o TCP/IP não entende "nomes de domínio", só endereços IP. Como a conexão segura começa antes de saber qual domínio está sendo acessado, **parecia que só dava para ter um certificado por IP**.

Isso tem uma solução? SIM. 

**SNI (Server Name Indication)** — uma extensão do TLS que permite ao cliente informar qual domínio ele quer acessar **durante o handshake**. Assim, o servidor pode escolher o certificado certo **mesmo antes da requisição HTTP**. 

---
### Proxy de Terminação TLS

Como um só processo pode "escutar" em uma porta (como a porta 443, padrão do HTTPS), é comum usar um programa específico para cuidar só da parte HTTPS. Esse programa é chamado de **Proxy de Terminação TLS**.

- Ele faz o seguinte:

	1. Recebe a requisição HTTPS criptografada.
    
    2. **Descriptografa** os dados.
    
    3. Encaminha a requisição HTTP **sem criptografia** para sua aplicação (como uma API FastAPI).
    
    4. Pega a resposta da sua aplicação.
    
    5. **Criptografa** de novo e envia ao cliente.

Exemplos de proxies TLS:

- **Nginx**
- **Traefik**
- **Caddy**
- **HAProxy**

---
### HTTPS Flow

![[https_request.png]]


Se digitarmos `http://` em vez de `https://` para visitar um site que implementa HTTPS, o navegador tenta resolver o domínio e redireciona o usuário para o servidor web que hospeda o site de destino. 

Uma solicitação é enviada primeiro para a porta 80, que é o protocolo HTTP não criptografado. O servidor detecta isso e redireciona o cliente para a porta HTTPS segura 443. Isso é feito por meio do código de resposta `301 Moved Permanently`.

Em seguida, o cliente - navegador web - envia um pacote `client hello`, fornecendo informações sobre si mesmo. Após isso, o servidor responde com `server hello` com uma troca de chaves para a troca de certificados SSL.

O cliente verifica a chave/certificado e envia um certificado próprio. Em seguida, um handshake criptografado é iniciado para confirmar se a criptografia e a transferência estão funcionando corretamente.

Assim que o handshake for concluído com sucesso, a comunicação HTTP normal é continuada, sendo criptografada posteriormente. Esta é uma visão geral de alto nível da troca de chaves.

> [!NOTE]
> Dependendo das circunstâncias, um invasor pode realizar um ataque de downgrade de HTTP, que reduz a comunicação HTTPS para HTTP, tornando os dados transferidos em texto não criptografado. Isso é feito configurando um proxy Man-In-The-Middle (MITM) para transferir todo o tráfego através do host do invasor sem o conhecimento do usuário. No entanto, a maioria dos navegadores, servidores e aplicativos web modernos oferece proteção contra esse ataque.

---
### Passo a passo do processo

Vamos usar um exemplo na qual você acessa `https://meusite.com` no navegador.

##### 1. Cliente inicia a conexão (Client Hello)

O navegador (cliente) envia um **[Client Hello]** com informações como:

- A versão do protocolo TLS que ele suporta.
- Uma lista de **cifras de criptografia** suportadas.
- Um número aleatório (random number).
- **Extensões**, incluindo o **SNI (Server Name Indication)** com o **nome do domínio** (`meusite.com`), que ajuda o servidor a escolher o certificado correto.

##### 2. Servidor responde (Server Hello)

O servidor recebe o Client Hello e responde com o **[Server Hello]**, contendo:

- A versão do TLS escolhida.
- A cifra (algoritmo de criptografia) escolhida.
- Um segundo número aleatório.
- O **[certificado digital]**, que inclui a chave pública do servidor.
- Informações adicionais (se necessário).

##### 3. Verificação do certificado (lado do cliente)

O navegador:

- **Valida o certificado**:

    - Está assinado por uma **autoridade certificadora confiável (CA)**?
    - Está **dentro da validade**?
    - O **nome do domínio** do certificado bate com o site acessado?

- Se tudo estiver ok, o navegador confia no servidor.


##### 4. Troca da chave secreta (Key Exchange)

O cliente precisa combinar com o servidor **[uma chave secreta compartilhada]** que será usada para criptografar os dados.

Esse processo pode variar:

1.  No ***TLS 1.2*** (ainda comum):

	- O cliente gera uma **chave de sessão** (chave simétrica), a **criptografa com a chave pública do servidor** (vinda no certificado) e envia.
	
	- Só o servidor pode **descriptografar com sua chave privada**.

2. No ***TLS 1.3*** (mais moderno e seguro):

	- Usa um método chamado **[Diffie-Hellman Efêmero (ECDHE)]**.
	- O cliente e servidor trocam valores públicos, e **ambos geram a mesma chave secreta localmente**, sem nunca transmiti-la diretamente.

##### 5. Finalização do Handshake

Agora que ambos têm a chave secreta:

- O cliente envia uma mensagem chamada **"Finished"**, criptografada com a chave acordada.
- O servidor também responde com uma mensagem **"Finished"** criptografada.
- Se as mensagens forem válidas, a conexão segura está estabelecida.

---
### cURL para HTTPS

O cURL deve lidar automaticamente com todos os padrões de comunicação HTTPS, realizar um handshake seguro e, em seguida, criptografar e descriptografar os dados automaticamente. 

No entanto, se entrarmos em contato com um site com um certificado SSL inválido ou desatualizado, o cURL, por padrão, não prosseguirá com a comunicação para proteger contra os ataques MITM mencionados anteriormente:

``` shell
allysson7@htb[/htb]$ curl https://inlanefreight.com

curl: (60) Problema com certificado SSL: Cadeia de certificados inválida
Mais detalhes aqui: https://curl.haxx.se/docs/sslcerts.html
...SNIP...
```

Navegadores modernos fariam o mesmo, alertando o usuário para não visitar um site com um certificado SSL inválido.

Podemos enfrentar esse problema ao testar um aplicativo web local ou com um aplicativo web hospedado para fins práticos, pois esses aplicativos web podem ainda não ter implementado um certificado SSL válido. Para pular a verificação do certificado com cURL, podemos usar a flag -k:

``` shell
allysson7@htb[/htb]$ curl -k https://inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

Como podemos ver, a solicitação foi processada desta vez e recebemos os dados de resposta.