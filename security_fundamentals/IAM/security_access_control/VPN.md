## O que é VPN?

Uma **VPN (Rede Privada Virtual)** é uma tecnologia que cria uma conexão segura e criptografada sobre uma rede pública não confiável (como a internet), estabelecendo um **túnel virtual ponto a ponto** entre o dispositivo do usuário (cliente VPN) e um servidor VPN remoto, permitindo transmissão de dados privada e autenticada como se fosse uma rede física dedicada. 

| Termo | O Que É | Responsabilidade |
|-------|---------|------------------|
| **VPN (conceito geral)** | **A tecnologia de Rede Privada Virtual** como um todo | Criar o **túnel seguro** entre cliente e servidor |
| **Protocolo de VPN** (IPsec, SSL/TLS, WireGuard, OpenVPN) | A **implementação específica** que faz o tunelamento + segurança | Aplicar a **criptografia, autenticação e encapsulamento** |
| **Tunelamento** | O **processo** de encapsular pacotes dentro de outros pacotes | Feito **pelo protocolo** (IPsec encapsula IP, SSL encapsula TCP/HTTP) |
| **Segurança (criptografia)** | Proteção dos dados no túnel | Feita **pelo protocolo** (IPsec usa ESP+AES, SSL usa TLS+AES) |

- **VPN** = o **conceito/tecnologia** (Rede Privada Virtual)
- **IPsec/SSL/WireGuard** = os **protocolos** que **implementam** a VPN (fazem o tunelamento e a segurança)
- **Tunelamento + Segurança** = as **duas funções** que qualquer protocolo VPN deve fazer

VPN não é um protocolo. É o que você quer alcançar (rede privada sobre pública), não como alcançar.

## Funcionamento técnico detalhado

O processo inicia com o **cliente VPN** (software como OpenVPN Connect, Cisco AnyConnect ou WireGuard) no dispositivo local, que inicia uma conexão com o servidor VPN via protocolo específico (ex: TLS para SSL VPN, UDP para WireGuard). Ocorre então um **handshake de autenticação** (usando certificados digitais, pré-shared keys ou credenciais RADIUS/LDAP), seguido de **negociação de chaves criptográficas** (ex: Diffie-Hellman para troca de chaves, gerando chaves simétricas AES-256 ou ChaCha20).

Os dados são **encapsulados** (um pacote original é envolvido em outro cabeçalho VPN) e **criptografados** antes de trafegar pela internet, criando o túnel virtual. No servidor VPN, ocorre o **desencapsulamento** e **descriptografia**, restando o pacote original roteado ao destino final na internet. O servidor atribui um **endereço IP temporário** ao cliente, mascarando seu IP real e localização geográfica, enquanto todo o tráfego é roteado via esse servidor intermediário. 

## Componentes técnicos chave

| Componente | Função Técnica |
|------------|----------------|
| **Protocolo VPN** | Define encapsulamento + criptografia (IPsec, SSL/TLS, WireGuard, L2TP) |
| **Cliente VPN** | Software que gerencia autenticação, criptografia e tunelamento no dispositivo |
| **Servidor VPN** | Endpoint que termina o túnel, desencapsula dados e roteia tráfego à rede destino |
| **Criptografia** | Algoritmos simétricos (AES-128/256, ChaCha20) para confidencialidade + HMAC para integridade |
| **Túnel Virtual** | Canal lógico ponto a ponto que isola tráfego da rede pública subjacente |

A VPN garante **confidencialidade** (dados ilegíveis para interceptadores), **integridade** (HMAC detecta alterações), **autenticação** (certificados/keys validam identidades) e **não-repúdio** (logs de auditoria). 

É amplamente usada para **acesso remoto seguro** (colaboradores fora do escritório), **site-to-site** (conectar filiais à matriz) e **privacidade online** (mascarar IP contra ISPs/rastreadores). 

## Tipos de VPN

#### 1. **IPsec VPN** (Internet Protocol Security)

- **Uso principal**: Acesso remoto e conexões **site-to-site** (ligar duas redes inteiras, como filial à matriz).
- **Como funciona**: Cria túneis na camada de rede (camada 3), encriptando todo o tráfego IP. Exige **cliente VPN instalado** (ex.: Cisco AnyConnect, strongSwan).
- **Vantagens**: Mais robusta para tráfego de alto volume, ideal para site-to-site permanente.
- **Desvantagens**: Configuração complexa, problemas com NAT/firewalls, menos amigável para usuários leigos. 

#### 2. L2TP (Layer 2 Tunneling Protocol)

- **Uso**: Acesso remoto com suporte nativo em Windows, macOS, iOS e Android.
- **Funcionamento**: Combina L2TP (tunelamento na camada 2) com IPsec (encriptação).
- **Vantagens**: Compatibilidade universal, bom para dispositivos móveis.
- **Desvantagens**: Mais lento (duplo encapsulamento), bloqueado em alguns redes restritas.

#### 3. **OpenVPN**

- **Uso**: Acesso remoto e site-to-site, muito popular em soluções open-source.
- **Funcionamento**: Usa TLS/SSL como o SSL VPN, mas **exige cliente dedicado** (OpenVPN Connect).
- **Vantagens**: Altamente configurável, atravessa firewalls/NAT facilmente, encriptação forte (AES-256).
- **Desvantagens**: Instalação de cliente necessária, configuração manual pode ser difícil. 

#### 4. **WireGuard**

- **Uso**: Acesso remoto moderno, focado em performance e simplicidade.
- **Funcionamento**: Protocolo leve na camada de rede, com código mínimo (cerca de 4.000 linhas vs. 600 mil do OpenVPN).
- **Vantagens**: Muito rápido, baixa latência, fácil configuração, criptografia moderna (ChaCha20).
- **Desvantagens**: Mais novo (menos maduro que IPsec/OpenVPN), requires cliente. 

#### 5. **PPTP** (Point-to-Point Tunneling Protocol) – **Obsoleto**

- **Uso**: Antes comum, hoje **não recomendado** por segurança fraca (criptografia MS-CHAP v2 quebrada).
- **Status**: Abandonado; evite usar.

#### 6. **SSTP** (Secure Socket Tunneling Protocol)

- **Uso**: Acesso remoto nativo no Windows.
- **Funcionamento**: Usa TLS (semelhante ao SSL VPN), empacota tráfego PPP em HTTPS.
- **Vantagens**: Atravessa firewalls facilmente (porta 443), bom para Windows.
- **Desvantagens**: Proprietário da Microsoft, menos suporte em outros SOs.

### Comparação Rápida: SSL VPN × IPsec × OpenVPN × WireGuard

| Característica          | SSL VPN                | IPsec VPN             | OpenVPN            | WireGuard         |
|-------------------------|------------------------|------------------------|--------------------|-------------------|
| **Cliente necessário**  | Não (portal web) ou leve | Sim (obrigatório)      | Sim                | Sim               |
| **Camada**              | Aplicação/Transporte   | Rede (camada 3)        | Rede/Transporte    | Rede              |
| **Protocolo**           | SSL/TLS (HTTPS, porta 443) | UDP/TCP (portas 500/4500) | TLS (porta 443)    | UDP (porta 51820) |
| **Facilidade de uso**   | ⭐⭐⭐⭐⭐ (zero-touch)     | ⭐⭐ (configuração complexa) | ⭐⭐⭐              | ⭐⭐⭐⭐             |
| **Performance**         | ⭐⭐⭐                    | ⭐⭐⭐⭐                   | ⭐⭐⭐                | ⭐⭐⭐⭐⭐            |
| **Site-to-site**        | Raro                   | **Excelente**          | Bom                | Bom               |
| **Acesso remoto fácil** | **Ideal**              | Médio                  | Bom                | Muito bom         |

