
# Introdução

Uma **VPN SSL (Secure Sockets Layer)**, que tecnicamente opera com **TLS (Transport Layer Security)** nas versões 1.2 ou 1.3, é uma implementação de Rede Privada Virtual que funciona na **camada 7 (Aplicação)** e **camada 4 (Transporte)** do modelo OSI.

Diferente de outras soluções que operam na camada de rede, a VPN SSL protege **dados da aplicação** e cria um túnel seguro permitindo acesso remoto a recursos corporativos usando um protocolo idêntico ao que protege sites HTTPS seguros. 

***
## O que é SSL VPN?

A VPN SSL foi projetada para permitir **acesso remoto seguro e universal** para colaboradores remotos. A solução oferece serviços de segurança completos aplicados na camada de aplicação:


- **Confidencialidade**: Dados trafegam criptografados com **AES-256-GCM** ou **ChaCha20-Poly1305**, tornando-os ilegíveis para interceptadores.

- **Integridade**: Cada mensagem possui **tag AEAD** (Authentication Tag) ou **HMAC** garantindo que nenhum bit foi alterado.

- **Autenticação do servidor**: O gateway SSL VPN apresenta **certificado X.509** assinado por CA confiável, provando sua identidade durante o handshake TLS.

- **Autenticação do usuário**: Após o túnel TLS ser estabelecido, o usuário deve se autenticar com **usuário/senha + MFA** (token TOTP, SMS, app autenticador) antes de acessar recursos.

- **Controle de acesso baseado em papéis (RBAC)**: Políticas definem quais recursos cada usuário pode acessar (ex: "departamento-financeiro" só vê share financeiro).

A característica distintiva da SSL VPN é operar **aplicação primeiro**: o túnel é estabelecido via navegador, e o acesso aos recursos é condicional baseado nas políticas do administrador. 

***
## Modos de operação: portal vs túnel
### **Modo portal (Clientless) — acesso seletivo via navegador**

No **modo portal**, o usuário **não precisa instalar nada**. Ele simplesmente abre o navegador, acessa `https://vpn.suaempresa.com`, faz login no portal web e vê uma lista de links para recursos internos (intranet, e-mail web, aplicativos SaaS). Quando o usuário clica em um link, o **gateway SSL VPN atua como proxy reverso**:

1. Gateway recebe requisição HTTPS do usuário (já criptografada no túnel TLS).
2. Gateway descriptografa a requisição e verifica autenticação + políticas RBAC.
3. Gateway faz nova requisição HTTP interna ao servidor de destino.
4. Servidor responde com o conteúdo.
5. Gateway **reescreve URLs** na resposta (ex: `/arquivos/file.pdf` → `/portal/resource?path=/arquivos/file.pdf`).
6. Gateway recriptografa a resposta e envia ao navegador.

**O que é protegido?**  

Apenas tráfego **HTTP/HTTPS** que passa pelo portal. Recursos não-web (SMB, RDP, SSH puro) **não são acessíveis** neste modo (a menos que usem plugins obsoletos Java/ActiveX, que não são recomendados).

**Vantagens:**

- **Zero instalação**: Funciona em qualquer navegador moderno (Chrome, Firefox, Edge, Safari).
- **Acesso granular**: Controle fino por recurso (cada link é acessível separadamente).
- **Segurança por design**: Usuário vê apenas o que o administrador permitiu, não a rede inteira.

**Desvantagens:**

- **Acesso limitado a apps web**: HTTP/HTTPS apenas.
- **URL rewriting**: Links em páginas podem quebrar se reescrita falhar.
- **Latência adicional**: Cada requisição HTTP passa pelo proxy, adicionando overhead.

Este modo é ideal para colaboradores que só precisam acessar **intranet, e-mail web ou aplicações web corporativas** sem instalar software. 


### **Modo Túnel — acesso completo à rede interna**

No **modo túnel**, o usuário inicia acessando o portal web, mas **após autenticação bem-sucedida**, o gateway envia um **plugin leve ou cliente nativo** (ex: FortiClient, Cisco AnyConnect) que instala um **adaptador virtual de rede** no computador. Esse adaptador recebe um **IP virtual** da rede corporativa (ex: 10.200.0.45) e a **tabela de roteamento é modificada**:

``` json
Tabela de roteamento após conexão SSL VPN túnel:
  Destino: 10.0.0.0/8    → Gateway: 10.200.0.1 (túnel SSL VPN)
  Destino: 0.0.0.0/0     → Gateway: 192.168.1.1 (roteador local, Internet)
```

Isso significa que **todo tráfego para a rede corporativa** (10.0.0.0/8) é direcionado para o túnel TLS, enquanto o resto da internet continua usando a conexão normal (**split tunnel**). Se configurado como **full tunnel**, até o tráfego para a internet passa pelo gateway.

**O que é protegido?**  

**Todo protocolo IP** que vai para a rede interna: HTTP, HTTPS, **SMB** (compartilhamento de arquivos Windows), **RDP** (área de trabalho remota), **SSH**, **MySQL**, **PostgreSQL**, **Exchange**, etc. O usuário tem acesso **completo** como se estivesse fisicamente no escritório.

**Diferença crítica do modo portal:**  

No modo portal, o gateway proxya requisições HTTP. No modo túnel, o **pacote IP inteiro** do usuário é encapsulado e criptografado dentro do túnel TLS, permitindo protocolos não-web.

***
## Estrutura detalhada dos pacotes SSL VPN

A estrutura de encapsulamento muda drasticamente entre os dois modos. Vamos analisar cada um.
### **Modo portal: Proxy HTTP

No modo portal, **não há encapsulamento de pacotes IP**. O que ocorre é um **proxy reverso HTTP** sobre TLS:

``` json
Fluxo no modo portal:

Navegador do usuário:

  Requisição: GET https://portal.suaempresa.com/resource?path=/arquivos/file.pdf
  ↓
[IP público cliente] [TCP porta 443] [TLS 1.3 criptografado] → Gateway SSL VPN
  ↓
Gateway descriptografa TLS, extrai requisição HTTP:
  GET /resource?path=/arquivos/file.pdf
  ↓
Gateway consulta RBAC: usuário tem permissão?
  ↓ SIM
Gateway faz requisição HTTP interna ao servidor:
  GET http://fileserver-interno/arquivos/file.pdf
  ↓
Fileserver responde com arquivo PDF.
  ↓
Gateway reescreve URLs no response PDF/HTML:
  Original: <a href="/arquivos/outro.pdf">
  Reescrito: <a href="/portal/resource?path=/arquivos/outro.pdf">
  ↓
Gateway recriptografa em TLS e envia ao navegador.
```

**Estrutura do pacote na internet (modo portal):**

``` json
[IP público cliente: 187.45.123.89] 
  [TCP externo: porta 54321 → porta 443]
    [Registro TLS 1.3]
      Content Type: 23 (Application Data)
      Version: 0x0304 (TLS 1.3)
      Length: 1484 bytes
      [Payload criptografado]
        Nonce: 12 bytes
        Ciphertext: 1444 bytes (requisição HTTP ou resposta HTML/PDF criptografada)
        Tag: 16 bytes (AEAD para integridade)
```

**O que é criptografado?**  

A requisição/resposta HTTP inteira está dentro do **ciphertext** criptografado com AES-256-GCM.

**O que NÃO é criptografado?**  

- IP público do cliente e do gateway
- Portas TCP externas
- Registro TLS (Content Type, Version, Length)

O **HTTP interno** (entre gateway e fileserver) **não precisa ser criptografado** se estiver na rede interna confiável, mas o tráfego entre cliente e gateway **é totalmente protegido pelo TLS**.


### Modo Túnel

No modo túnel, há **encapsulamento real de pacotes IP**, similar ao IPsec, mas usando **registro TLS** como wrapper em vez de cabeçalho ESP. Veja a transformação passo a paso:

**Pacote original (antes da SSL VPN túnel):**

``` json
[IP interno: 10.200.0.45 → 10.0.1.50] 
  [TCP interno: porta 54321 → porta 443]
    [HTTP: GET /arquivo.pdf HTTP/1.1]
      [Dados: conteúdo da requisição]
```

**Após encapsulamento SSL VPN (modo túnel):**

``` json
[IP externo: 187.45.123.89 → 203.0.113.5]  ← IP público do cliente → IP público do gateway
  [TCP externo: porta 54321 → porta 443]    ← Conexão TCP para HTTPS padrão
    [Registro TLS 1.3]
      Content Type: 23 (Application Data)
      Version: 0x0304 (TLS 1.3)
      Length: 1520 bytes
      [Payload criptografado]
        Nonce: 12 bytes (IV + sequence_number para replay protection)
        Ciphertext: 1484 bytes (IP interno + TCP interno + HTTP + dados + padding)
        Tag: 16 bytes (AEAD authentication tag para integridade)
```

**Detalhando o que está dentro do Ciphertext:**
``` json
Ciphertext (1484 bytes, criptografado com AES-256-GCM):
  [IP interno: 10.200.0.45 → 10.0.1.50]   ← 20 bytes criptografados
  [TCP interno: 54321 → 443]              ← 20 bytes criptografados
  [HTTP: GET /arquivo.pdf HTTP/1.1]       ← ~50 bytes criptografados
  [Dados da aplicação]                    ← Criptografados
  [Padding]                               ← Alinhamento para bloco AES (16 bytes)
```

**O que é criptografado?**  

Todo o **pacote IP interno completo** (cabeçalho IP + cabeçalho TCP + dados da aplicação) está dentro do ciphertext. Inclui endereços IP privados, portas, protocolos e conteúdo.

**O que NÃO é criptografado?** 

- **IP externo**: Endereços públicos visíveis para roteadores intermediários.
- **TCP externo**: Portas de origem/destino (cliente → gateway).
- **Registro TLS**: Content Type, Version, Length (necessários para o receptor entender o protocolo).

**Comparação direta de encapsulamento:**

| Campo | Modo Portal | Modo Túnel |
|-------|-------------|------------|
| **Encapsulamento de IP?** | Não (só proxy HTTP) | Sim (IP interno encapsulado) |
| **O que trafega no túnel?** | Requisição/resposta HTTP | Pacote IP inteiro (qualquer protocolo) |
| **Protocolos suportados** | HTTP/HTTPS apenas | HTTP, SMB, RDP, SSH, MySQL, qualquer IP |
| **IP virtual atribuído?** | Não | Sim (ex: 10.200.0.45) |
| **Tabela de roteamento alterada?** | Não | Sim (tráfego para 10.0.0.0/8 → túnel) |
| **Cliente necessário?** | Não (apenas navegador) | Sim (plugin/adapter virtual) |

***
## Estrutura do registro TLS no túnel SSL VPN

O **registro TLS** é o componente central que encapsula os dados no túnel SSL VPN. Vamos examinar sua estrutura detalhadamente:

**Estrutura do registro TLS 1.3 (Application Data):**
``` json
Registro TLS (5 bytes de cabeçalho + payload criptografado):

Byte 0: Content Type (1 byte)
  0x17 = 23 = Application Data (dados da aplicação encapsulados)

Bytes 1-2: Version (2 bytes)
  0x0303 = TLS 1.2
  0x0304 = TLS 1.3 (moderno, usado em 2026)

Bytes 3-4: Length (2 bytes, big-endian)
  Ex: 0x05E8 = 1512 bytes (tamanho do payload criptografado seguinte)

Payload criptografado (Length bytes):
  Nonce: 12 bytes
    = IV (12 bytes do HKDF) XOR sequence_number (64 bits)
    Garante unicidade por pacote para AEAD
  Ciphertext: Length - 12 - 16 bytes
    Contém: IP interno + TCP + HTTP + Dados + Padding
  Tag (Authentication Tag): 16 bytes
    = AEAD tag (AES-GCM: 16 bytes; ChaCha20-Poly1305: 16 bytes)
    Permite verificar integridade + autenticidade sem HMAC separado
```

**Função de cada componente:**

1. **Content Type = 23**: Indica que este registro contém dados da aplicação (não handshake, não alert, não change_cipher_spec).

2. **Version = 0x0304**: SSL VPN moderna usa TLS 1.3. Versões antigas (TLS 1.0/1.1) estão desabilitadas por segurança.

3. **Length**: Tamanho exato do payload criptografado seguinte (nonce + ciphertext + tag).

4. **Nonce**: Único para cada pacote. Evita replay attacks porque o receptor recusa pacotes com nonce repetido (janela de replay de 64 bits).

5. **Ciphertext**: Dados crutos criptografados com **AES-256-GCM** (chave derivada do handshake TLS). Sem a chave, são bytes aleatórios ilegíveis.

6. **Tag**: Autenticador AEAD. Se alguém alterar até 1 bit do ciphertext, a tag não baterá e o pacote será descartado.

**Exemplo real inspecionável no Wireshark:**

``` json
Frame 142: 1532 bytes on wire
Ethernet II: src=aa:bb:cc:dd:ee:ff, dst=11:22:33:44:55:66
IPv4: 187.45.123.89 → 203.0.113.5
TCP: 54321 → 443 [PSH, ACK]
TLSv1.3: Application Data
  Content Type: Application Data (23)
  Version: TLS 1.3 (0x0304)
  Length: 1512
  Encrypted Application Data: 1484 bytes
    [Decrypted: IP 10.200.0.45 → 10.0.1.50, TCP 54321 → 443, HTTP GET /arquivo.pdf]
```

***
## Estabelecimento da sessão: Handshake TLS + autenticação do usuário

O processo completo de conexão SSL VPN tem duas etapas distintas: 

**1) estabelecimento do túnel TLS** com o handshake TLS
**2) autenticação do usuário**.