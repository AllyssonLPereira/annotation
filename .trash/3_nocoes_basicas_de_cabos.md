---
tags:
  - arquivo
---
### Noções básicas de cabos de dados

A categoria de um cabo pode ser comparada a uma estrada com várias pistas; quanto mais pistas uma estrada tem, mais veículos podem viajar nesta estrada simultaneamente. 

Geralmente, os padrões baseiam-se em um comprimento máximo de cabo de 100 metros. Este comprimento do cabo consiste em 90 metros de cabo de instalação e 10 metros de cabo de remendo. 

Após os 100 metros iniciais, repetidor/extensor é adicionado ao sistema de cabos, que fortalece o sinal e prepara-o para a transmissão de sinal adicional de 100 metros conforme necessário para conectar a máquina ou seus aparelhos à unidade de controle. 

Além disso, as categorias de cabos de dados precisam cumprir os valores de desacoplamento dos pares, por exemplo, NEXT (cross end talk).


| Categoria | Padrão          | Taxa de dados | Frequência        | Nº de condutores |
| --------- | --------------- | ------------- | ----------------- | ---------------- |
| Cat 5     | 100BASE-TX      | 100 Mbit      | 100 MHz           | 4 ou 8           |
| Cat 5e    | 1000BASE-TX     | 1 Gbit        | Duplex de 100 MHz | 8                |
| Cat 6     | EIA/TIA 568B2.1 | 1-10 Gbit*    | 250 MHz           | 8                |
| Cat 6A    | 10GBASE-T       | 10 Gbit       | 500 MHz           | 8                |
| Cat 7     | 10GBASE-T       | 10 Gbit       | 600 MHz           | 8                |
| Cat 7A    | 10GBASE-T       | 10 Gbit       | 1000 MHz          | 8                |
| Cat 8     | 40GBASE-T       | 40 Gbit       | 1600-2000 MHz     | 8                |
* Depende do comprimento e do tipo de cabo

Esta tabela mostra a diferença entre a categoria 5 e a categoria 8, mas também é necessário considerar os materiais de revestimento, a qualidade do cabo e outros detalhes para encontrar o cabo certo, que corresponda a uma determinada aplicação.

Para os cabos de categoria 5, o desacoplamento dos pares é realizado na construção do cabo com diferentes comprimentos de torção de cada par. Isso significa que para quatro pares, há quatro comprimentos individuais de torção durante a produção.

*A eficácia da torção não é capaz de alcançar os valores-alvo e você tem que considerar etapas adicionais durante a construção de cabos para categorias superiores.

Os cabos de categoria 6 permitem que você escolha entre dois desenhos técnicos. Os valores de dissociação relevantes da categoria 6 podem ser alcançados com uma cruz de plástico que cria distância entre os pares. 

Outra forma é usar um par em folha metálica (PIMF). [A espessura da folha de alumínio influencia a eficácia da blindagem]. 

*Muitas pessoas pensam que a blindagem protege o cabo de influências ambientais. No entanto, ele também tem o efeito inverso – a blindagem mantém o sinal elétrico no cabo e evita influenciar negativamente outros equipamentos nas proximidades.

Para categorias ainda maiores, como categoria 7, 7e e 7A, uma trança de cobre é obrigatória para cumprir os valores elétricos padronizados, porque uma folha de alumínio por si só não é suficiente. Além disso, cada material de blindagem tem vantagens e desvantagens.

A folha de alumínio é barata, mas por si só este material não tem um bom desempenho em aplicações que requerem cabos flexíveis, de pista ou de torção. Se você mover uma folha de metal repetidamente, começará a ver rachaduras, o que diminui a eficácia da blindagem no cabo. 

Esta é a razão pela qual alguns fabricantes constroem cabos, que se movem frequentemente ou estão localizados em áreas de vulnerabilidade eletromagnética (EMV), usando tanto a folha de alumínio quanto a trança de cobre. Isso se aplica até a cabos que são “apenas” categoria 5.

---
### Marcações de cabos

As marcas de identificação antes do símbolo de barra (/) referem-se à blindagem geral do cabo; as marcas de identificação após a barra referem-se à blindagem dos pares. Aqui estão algumas marcações comuns de cabos de dados:


| –      | Blindagem total / Blindagem em pares                    | Categorias                                      |
| ------ | ------------------------------------------------------- | ----------------------------------------------- |
| U/UTP  | Par trançado não blindado / não blindado                | categoria 5 / categoria 6 com cruz de distância |
| F/UTP  | Par trançado blindado / não blindado                    | categoria 5 / categoria 6 com cruz de distância |
| S/UTP  | Par trançado blindado / não blindado da trança          | categoria 5 / categoria 6 com cruz de distância |
| SF/UTP | Trançado e folha blindada / par trançado não blindado   | categoria 5 / categoria 6 com cruz de distância |
| U/FTP  | Par trançado blindado / não blindado                    | categoria 6                                     |
| F/FTP  | Folha trançada / Folha trançada par trançado            | <br>categoria 6 / 6A                            |
| S/FTP  | Trançado blindado / Folha trançada par trançado         | categoria 7 / 7e / 7A / 8                       |
| SF/FTP | Trançado e folha blindada / folha trançada par trançado | categoria 7 / 7e / 7A / 8                       |

---
### Tipos de Revestimento

Em relação aos Cabos UTP de [Baixa Emissão de Fumaça e Sem Halogênios] (LSZH — [Low Smoke Zero Halogen]), estes possuem cobertura especial no isolamento e na capa. Em casos de incêndios, a fumaça liberada não é tóxica e é totalmente livre de halogênios (elementos químicos que, quando em combustão, emitem gases extremamente danosos à saúde). 

Vale ressaltar, que os prejuízos podem ser até reversíveis nas construções, porém os danos à saúde das pessoas muitas vezes não, podendo até mesmo levar ao óbito.

*Os cabos LSZH (metálicos, ópticos ou coaxiais) são recomendados aos espaços ou caminhos verticais ou horizontais com ou sem fluxo de ar forçado onde haja a circulação ou concentração de pessoas. Isso inclui hospitais, aeroportos e shoppings, por exemplo.

---
### Especificação do Cabeamento UTP

A instalação de cabos UTPs precisa seguir a Norma Brasileira e Internacional. Para cada tipo de aplicação cabos com capa CMR e LSZH, serão recomendados tipos específicos:


- [CMX]: Cabos destinado a instalações residenciais, com menor concentração de cabos e sem fluxo de ar forçado. A exposição do cabo não deve ultrapassar 3 m;

- [CM]: Instalações horizontais com grande ocupação e sem fluxo de ar forçado;

- [CMR (riser)]: Instalações verticais em “shafts” prediais. Também para instalações em prédio que possuem mais de um andar, sem fluxo de ar forçado;

- [CMP (plenum)]: Em locais fechados, aplicação horizontal, com ou sem fluxo de ar forçado, locais confinados ou dutos de ar condicionado, por exemplo;

- [LSZH]: Aplicações tanto horizontais quanto verticais, com ambientes que possuem grande circulação e concentração de pessoas;

- [MAX Green LSZH]:  Cabos de locais com grande circulação e contração de pessoas, como teatros, cinemas, restaurantes e rodoviárias. O foco é a sustentabilidade.

---
### Referências

https://www.helukabeldobrasil.com.br/como-diferenciar-as-categorias-dos-cabos-de-dados/
https://via.eng.br/cabeamento-utp/