
## Tabela de roteamento

O roteamento é o processo essencial que os roteadores utilizam para determinar o caminho que os pacotes IP devem tomar sobre uma rede para alcançar seu destino. 

Para realizar essa tarefa, o roteador armazena as rotas para todos os destinos conhecidos em uma estrutura interna denominada tabela de roteamento. Enquanto os switches mantêm uma tabela de endereços MAC com seus endereços de destino conhecidos, os roteadores mantêm uma tabela de roteamento com suas redes de destino conhecidas. 

Sempre que um roteador recebe um pacote, ele consulta essa tabela interna para localizar a melhor rota disponível para encaminhar o pacote adequadamente.

Existem dois métodos principais que os roteadores utilizam para aprender essas rotas. 

- O primeiro é o roteamento dinâmico, no qual os roteadores utilizam protocolos de roteamento dinâmico, como o OSPF, para compartilhar informações de rede entre si de forma automática e construir suas tabelas. 

- O segundo método é o roteamento estático, onde um engenheiro de rede configura manualmente as rotas no dispositivo. 

No entanto, existe uma categoria de rotas que não se enquadra em nenhuma dessas duas divisões. Quando um endereço IP é configurado em uma interface e essa interface é habilitada, duas rotas por interface são adicionadas automaticamente à tabela de roteamento. Essas rotas automáticas são divididas em rotas conectadas e rotas locais, constituindo a base inicial de uma tabela de roteamento ativa.

## Rota conectada

Uma rota conectada é indicada pelo código "C" na legenda e no corpo da tabela de roteamento, representando uma rota direta para a rede à qual a interface do roteador está conectada. 

Para entender como o roteador calcula essa entrada, deve-se observar a estrutura do endereço IP e da máscara de sub-rede configurados na interface. Em uma configuração com máscara de vinte e quatro bits, por exemplo, os primeiros três octetos representam a porção de rede e o último octeto representa a porção de host. Quando o roteador altera todos os bits dessa porção de host para zeros, o resultado obtido é o endereço exato da rede identificada pela interface.

Essa entrada na tabela fornece uma instrução de encaminhamento válida para todos os hosts pertencentes àquela faixa de rede específica.

A saída do comando de verificação da tabela de roteamento indicará explicitamente que a rede está diretamente conectada à respectiva interface física ou lógica do roteador. Dessa forma, o roteador armazena a instrução de que, se precisar enviar um pacote para qualquer host situado dentro desse intervalo de rede, ele deve encaminhar o pacote para fora daquela interface específica. 

## Rota local

A rota local é identificada pelo código "L" na tabela de roteamento. Essa entrada possui uma característica técnica muito específica: ela utiliza sempre uma máscara de host, representada por um prefixo de trinta e dois bits (`/32`) no IPv4. 

Diferente da rota conectada, que engloba toda a rede adjacente, a rota local aponta única e exclusivamente para o endereço IP exato que foi configurado na própria interface do roteador. Isso significa que nenhum outro endereço dentro daquela sub-rede fará correspondência com essa rota específica.

O propósito operacional da rota local é otimizar o processamento interno do roteador e definir estritamente como ele deve manipular o tráfego destinado a si próprio. Quando o dispositivo consulta a tabela de roteamento e encontra uma correspondência com uma rota local, ele recebe a instrução de que a mensagem não deve ser encaminhada para fora por nenhuma interface. 

Em vez de enviar o pacote adiante, o roteador retém o pacote, realiza o desencapsulamento das camadas e processa as informações internamente, identificando que ele próprio é o destinatário final do tráfego (como em conexões SSH de gerência ou mensagens de ping direcionadas a ele).

Assim como as rotas conectadas, as rotas locais são inseridas de forma automática pelo sistema operacional assim que a interface se torna ativa.

## Mecanismo de seleção de rotas: a regra do prefixo mais longo

A coexistência de rotas conectadas e locais cria um cenário onde um único pacote IP pode encontrar múltiplas correspondências válidas dentro da tabela de roteamento. Se uma interface está configurada com um determinado IP sob uma máscara de vinte e quatro bits, o roteador gerará automaticamente uma rota conectada para a rede completa (`/24`) e uma rota local para o IP exato da interface (`/32`). 

Caso chegue um pacote cujo destino seja precisamente o IP da interface do roteador, esse pacote passará nos critérios de checagem de ambas as rotas. Para resolver essa redundância e determinar com precisão qual instrução seguir, o roteador aplica o princípio da seleção da rota mais específica.

A determinação da rota mais específica é baseada na regra do prefixo mais longo (_Longest Prefix Match_), o que significa que o roteador selecionará a rota correspondente que possuir o maior número de bits estritos na sua máscara de sub-rede.

Comparando uma rota conectada de rede com prefixo de vinte e quatro bits e uma rota local de host com prefixo de trinta e dois bits, a rota de trinta e dois bits é mais específica porque aponta para um único endereço isolado, enquanto a outra abrange uma faixa de duzentos e vinte e seis endereços potenciais. 

Portanto, para o pacote destinado ao IP do próprio roteador, a rota local `/32` é a escolhida, garantindo que o pacote seja consumido internamente. Para qualquer outro pacote destinado àquela rede, mas direcionado a um host vizinho, a rota local `/32` não será uma correspondência, restando apenas a rota conectada `/24` para guiar o tráfego para fora da interface.

## Comportamento do Roteador vs. Switch diante de Destinos Desconhecidos

Há uma diferença filosófica e estrutural profunda no modo como os switches operam na Camada 2 em comparação com a forma como os roteadores gerenciam pacotes na Camada 3 quando encontram um destino desconhecido. 

Quando um switch recebe um quadro Ethernet e realiza a busca pelo endereço MAC de destino em sua tabela de endereços MAC, caso não encontre nenhuma correspondência, ele executa o processo de inundação (_flooding_).

Esse mecanismo força o switch a encaminhar uma cópia desse quadro unicast desconhecido por todas as suas portas ativas pertencentes àquela mesma VLAN, exceto pela porta de origem por onde o quadro entrou, com o objetivo de localizar o destino.

Se um roteador recebe um pacote IP, extrai o endereço de destino e, ao consultar sua tabela de roteamento, não localiza nenhuma rota correspondente — seja ela conectada, local, estática ou aprendida por protocolos dinâmicos —, o dispositivo descarta o pacote imediatamente.

Roteadores não propagam tráfego para redes desconhecidas; a tabela de roteamento deve conter uma instrução explícita para o destino ou o pacote será eliminado, o que previne a saturação dos links de longa distância com tráfego desnecessário.