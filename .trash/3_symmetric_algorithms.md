---
tags:
  - arquivo
---
## OTP - One Time Pad

A chave é uma string de bits aleatórios, com pelo menos o mesmo tamanho da mensagem em si.

O algoritmo é muito rápido, porém necessita de chaves muito longas (do tamanho da mensagem!).

$$C = E(k,m) = K ⊕ m$$
#### Exemplo: C = E(k,m) = K ⊕ m

| mensagem | 1000110 |
| -------- | ------- |
| chave    | 1100011 |
| C:       | 0100101 |

#### Exemplo: M = D(k,c) = K ⊕ c

| texto cifrado | 0100101 |
| ------------- | ------- |
| chave         | 1100011 |
| mensagem      | 1000110 |

#### Exemplo OTP: prova

$$D(k,E(k,m) = D(k,k ⊕ m) = k ⊕ (k ⊕ m) = (k ⊕ k) ⊕ m = 0 ⊕ m = m$$
