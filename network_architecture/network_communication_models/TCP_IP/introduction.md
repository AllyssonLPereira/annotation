
TCP/IP é o conjunto de protocolos fundamental que permite a comunicação entre dispositivos em redes, especialmente na Internet. Ele combina o Protocolo de Internet (IP), que cuida do roteamento e endereçamento dos dados, com o Protocolo de Controle de Transmissão (TCP), que garante a entrega confiável dos pacotes [1][2].

## Camadas Principais

O modelo TCP/IP é dividido em quatro camadas principais, cada uma com funções específicas para processar e transmitir dados.

- **Camada de Aplicação**: Gerencia protocolos como HTTP, FTP e SMTP para apps como navegadores e e-mails.

- **Camada de Transporte**: Usa TCP para conexões confiáveis (com verificação de erros e reenvio) ou UDP para mais velocidade, sem garantias [3].

- **Camada de Internet**: O IP roteia pacotes entre redes usando endereços IP, sem se preocupar com a ordem ou integridade [6].

- **Camada de Acesso à Rede**: Lida com hardware físico, como Ethernet e Wi-Fi, para enviar bits pela mídia [4].

Essa estrutura simplifica o modelo OSI (com sete camadas) e foi desenvolvida nos anos 1970 pelo Departamento de Defesa dos EUA para redes robustas [3].

## Como Funciona

O TCP/IP divide mensagens em pacotes pequenos, que podem viajar por rotas diferentes e são remontados no destino. O TCP usa um "handshake de três vias" (SYN, SYN-ACK, ACK) para estabelecer conexões seguras, enquanto o IP define o "envelope" com endereços de origem e destino [3][6].

Por exemplo, ao carregar uma página web, o TCP garante que todos os dados cheguem na ordem certa, mesmo se alguns pacotes se perderem [2].

---

## Desenvolvimento Inicial

A história do TCP/IP remonta aos anos 1960 e 1970, quando o Departamento de Defesa dos EUA (DoD), por meio da ARPA (atual DARPA), buscava criar redes robustas de comunicação para conectar computadores militares e acadêmicos em caso de ataques nucleares. Isso culminou na ARPANET, lançada em 1969, que usava inicialmente o protocolo NCP, mas precisava de algo mais escalável para interconectar redes heterogêneas [3][1].

Tudo começou com Vinton Cerf e Bob Kahn, considerados os "pais da Internet", que em 1974 publicaram o artigo "A Protocol for Packet Network Intercommunication". Nele, propuseram o TCP (Transmission Control Program) para gerenciar a transmissão confiável de pacotes em redes de comutação [5][7]. Em dezembro de 1974, a RFC 675 formalizou o conceito, separando o que viria a ser TCP e IP [1].

- De 1973 a 1978, o grupo INWG refinou o protocolo, influenciado pelo PUP da Xerox PARC.
- Em 1977, testes bem-sucedidos conectaram redes nos EUA, Reino Unido e Noruega.
- Até 1983, protótipos foram implementados em vários centros de pesquisa [3].

## Adoção e Padronização

O marco decisivo foi 1º de janeiro de 1983: a ARPANET migrou oficialmente do NCP para o TCP/IP, chamado de "flag day". Isso integrou rádio e satélites, resolvendo limitações anteriores [1][3]. Nos anos 1980, o NSFNET adotou o TCP/IP como backbone, espalhando-o globalmente; em 1990, tornou-se o padrão da Internet moderna [3][5].

---

## Camada

O modelo TCP/IP organiza a comunicação em rede em quatro camadas principais, cada uma com responsabilidades específicas para garantir que os dados fluam de forma eficiente entre dispositivos. Essa estrutura é mais prática que o modelo OSI (com sete camadas), agrupando funções para simplificar implementações reais, como na Internet [1][7].

### Camada de Acesso à Rede

Essa camada (equivalente às camadas Física e Enlace do OSI) lida com a transmissão física dos dados pela mídia, como cabos Ethernet, Wi-Fi ou fibra óptica. Ela gerencia endereços MAC, detecção de colisões (via CSMA/CD no Ethernet) e formata bits em quadros para envio local [3][1].

- Protocolos comuns: Ethernet, PPP, Wi-Fi (IEEE 802.11).
- Função chave: Converter pacotes em sinais elétricos/ópticos e vice-versa.

### Camada de Internet

Responsável pelo roteamento global de pacotes (datagramas), usa o IP (IPv4 ou IPv6) para endereçar e encaminhar dados entre redes diferentes, sem garantia de entrega ou ordem. Protocolos como ICMP (para ping) e IGMP auxiliam em diagnósticos e multicast [7][5].

- Não orientada a conexão: Pacotes podem se perder ou chegar fora de ordem.
- Exemplo: Um roteador usa IP para decidir o melhor caminho até o destino.

### Camada de Transporte

Garante comunicação fim-a-fim entre hosts, segmentando dados em pacotes e controlando fluxo, erros e retransmissões. TCP oferece confiabilidade (com handshake e ACKs), enquanto UDP prioriza velocidade para apps como streaming [1][2].

| Protocolo | Confiável? | Uso Típico |
|-----------|------------|------------|
| TCP      | Sim (ordenado, sem erros) | Web, e-mail |
| UDP      | Não       | Vídeo, jogos |
### Camada de Aplicação

Agrupa interfaces para apps finais (equivalente às camadas Aplicação, Apresentação e Sessão do OSI), lidando com protocolos específicos do usuário. Ela encapsula dados de serviços como navegação ou e-mail [7][4].

- Exemplos: HTTP/HTTPS (web), SMTP (e-mail), DNS (resolução de nomes), FTP (arquivos).
- No envio, dados descem pelas camadas; no recebimento, sobem na ordem inversa.



