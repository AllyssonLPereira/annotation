---
tags:
  - arquivo
---
##### What is IPv4?

IPv4 é um endereço lógico e exclusivo atribuído a um host, indentificando-o numa rede. Isso possibilita a sua comunicação na LAN e no mundo.

---

##### Octetos e notação decimal com ponto:

O endereço IPv4 é uma composição de 32 bits (ex.: **11010001101001011100100000000001**) e, como pode ver, a sua leitura é difícil.

Por isso, os 32 bits são agrupados em quatro bytes de oito bits (ex.: **11010001.10100101.11001000.00000001**) chamados octetos.

Sua leitura ainda é difícil, assim, é comum representar os octetos em sua forma decimal (ex.: **209.165.200.1**).

---

##### Network and hosts:

O endereço IPv4 é hierárquico e contém duas partes, a network e host. A parte network é definida/identificada pela máscara de sub-rede, ex.: IPv4 address: 192.168.0.1; máscara: 255.255.255.0

Por quê hierárquico? Porque a porção network identifica a rede de cada endereço de host. Assim, os routers precisam saber como alcançar cada rede, ao invés de saber a localização exata de cada host.

O IPv4 possibilita a existência de várias redes lógicas numa mesma rede física.
