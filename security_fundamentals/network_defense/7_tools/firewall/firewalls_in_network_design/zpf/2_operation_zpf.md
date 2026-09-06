---
tags:
  - arquivo
---
## ZPF Actions

As políticas identificam ações que o ZPF executará no tráfego de rede. Três ações possíveis podem ser configuradas para processar o tráfego por protocolo, zonas de origem e destino — pares de zonas — e outros critérios.

- *`Inspect`* — Isso realiza inspeção de pacotes de estado de Cisco IOS.
- *`Drop`* — Isso é análogo a deny uma declaração em uma ACL. Opção log vai logar os pacotes rejeitados.
- *`Pass`* — Isso é análogo a uma declaração permit em uma ACL. A ação de aprovação não rastreia o estado das conexões ou das sessões no tráfego.

---
## Traffic rules

As regras dependem se as interfaces de entrada e saída e saída são membros da mesma zona:

- Se nenhuma das relações é um membro da zona, a seguir a ação resultante é passar o tráfego.
- Se ambas as relações são membros da mesma zona, a seguir a ação resultante é passar o tráfego.
- Se uma relação é um membro da zona, mas a outra não é, a seguir a ação resultante é deixar cair o tráfego apesar de um zona-par existir.
- Se ambas as relações pertencem ao mesmo zona-par e uma política existe, a seguir a ação resultante é inspecionar, permitir, ou cair conforme definido pela política.

A tabela resume essas regras.

| Interface de origem - membro da zona? | Interface de destino - membro da zona? | Zona-par existente? | Política existente? | Resultado   |
| ------------------------------------- | -------------------------------------- | ------------------- | ------------------- | ----------- |
| NÃO                                   | NÃO                                    | N/D                 | N/D                 | APROVADO    |
| SIM                                   | NÃO                                    | N/D                 | N/D                 | DESCARTAR   |
| NÃO                                   | SIM                                    | N/D                 | N/D                 | DESCARTAR   |
| SIM — PRIVADO                         | SIM — PÚBLICO                          | N/D                 | N/D                 | APROVADO    |
| SIM — PRIVADO                         | SIM — PÚBLICO                          | SIM                 | N/D                 | DESCARTAR   |
| SIM — PRIVADO                         | SIM  — PÚBLICO                         | SIM                 | NÃO                 | APROVADO    |
| SIM — PRIVADO                         | SIM  — PÚBLICO                         | SIM                 | SIM                 | INSPECIONAR |

---

