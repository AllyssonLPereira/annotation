---
tags:
  - arquivo
---
## Perímetro de segurança

Em tempos passados, todos os dados, todas as pessoas e todos os endpoints ficavam em um só lugar, em um só edifício.

Portanto, toda a segurança era pensada ali. Basicamente, era construída um muralha em torno de tudo isso utilizando hardware e software para tornar aquele ambiente interno seguro de um mundo externo inseguro. Logo, tudo que estava ali dentro era confiável. 

Além disso, alguém ali dentro tinha uma visibilidade geral da rede e não só aquilo que ela de fato precisava e no nível que ela precisava.

Porém, o cenário atual é bem diferente. Temos o advento da cloud, na qual os dados não estão mais só no local (on premis)e, mas em núvens privadas e em núvens públicas. Ainda, há o trabalho remoto, com pessoas acessando sistemas, recursos e dados de diferentes lugares, de diferentes dispositivos (dispositivos seguros? Nem sempre). Por fim, temos o BYOD (Bring Your Own Device).

Sendo assim, o perímetro de rede deixou de ser um edifício, um campus... e passou a ser o globo terrestre. Deixou de ser algo simples e estático, passando a ser algo complexo e dinâmico. Com isso, a abordagem de defesa também precisava mudar.

E é aqui que entra o Zero Trust ou Zero Trust Network Access (ZTNA).

> ***OBS***: O perímetro não deixou de existir, ele apenas ficou granular. Hoje, o perímetro é cada usuário, cada dispositivo e cada aplicação individualmente.

## O que é Zero Trust?

> Só uma informação, toda essa segurança é pensada em camadas (defense in depth)

O Zero Trust é um filosofia de segurança, um pensamento, uma ideia e não uma aplicação ou sistema de defesa.

O Zero Trust se baseia em três coisas, que são:

- ***Nunca confiar, sempre verificar***: seja um usuário ou um dispositivo, devemos sempre verificar a sua **autenticidade** e suas **autorizações dentro do sistema**.

- ***Least Privilege***: Você só terá acesso aquilo que realmente precisa, nada mais além disso.

- ***Suponha que a rede foi invadida***: se o local foi invadido, certamente ficarei muito mais alerta a tudo, e a ideia é justamente essa, estar sempre alerta ainda que a rede não tenha sido invadida, mas hajo como se tivesse.


A fim de cumprir o Zero Trust, podemos fazer o seguinte: sempre verificar a identidade do usuário (usuário, senha e MFA), mas não somente isso, podemos condicionar o acesso de usuários e dispositivos a rede ao contexto (data e hora de acesso, geolocalização e na postura de segurança do dispositivo).

### Least privilege

É o conceito de que qualquer usuário, programa ou processo deve ter apenas os **privilégios estritamente necessários** para realizar sua função, e nada mais.

Tudo isso precisa ser gerenciado por um sistema. Então, de forma bem simples, teremos um sistema que vai garantir esse acesso no nível adequado.

Para as "contas comuns" (RH e outros) teremos o IAM. Já para contas privilegiadas, teremos o PAM (Privilege Access Management).

#### Sobre o PAM

Se eu sou alguém que tem funções e autorizações simplórias na rede, serei monitorado, será coletado logs sobre tudo que faço...

Porém, se eu for alguém como o chefe de segurança de rede de determinada organização, o nível de segurança aplicada sobre mim será bem maior, sendo exigido mais segurança, sendo coletados mais logs (e mais detalhados).

Além disso, podemos aplicar o **acesso Just-in-Time (JIT)**. Você só ganha poderes de administrador por 2 horas para fazer uma manutenção específica, depois disso, sua conta volta a ser "comum".

#### Método Kipling

Ademais, teremos método Kipling quando tratamos de Least Privilege.

O nome vem do poeta Rudyard Kipling, que escreveu sobre os "seis servos honestos" (Quem, O quê, Onde, Quando, Por que e Como).

Para definir uma regra de acesso segura, você deve responder a essas perguntas:

- **Quem (Who):** Quem é o usuário? (Validado por MFA/Identidade).

- **O quê (What):** Qual recurso ele quer acessar? (Um servidor específico, não a rede toda).

- **Quando (When):** Em que horário? (É normal o financeiro acessar o sistema às 3h da manhã de um domingo?).

- **Onde (Where):** De onde vem a conexão? (Brasil? Da rede interna? De um IP suspeito?).

- **Por que (Why):** Qual a justificativa? (O usuário pertence ao grupo que realmente precisa disso?).

- **Como (How):** Através de qual dispositivo? (O notebook está com antivírus em dia? É um celular pessoal?).


Tudo isso tem o objetivo de diminuir a superfície de ataque na rede. Então, a lógica é: para diminuir a **superfície de ataque**, aplicamos o **privilégio mínimo** em todos os acessos. Para as contas de alto risco, usamos o **PAM**. E para configurar as regras que permitem ou bloqueiam esses acessos, usamos o **método Kipling**.

### Outras formas de pensar o Zero Trust

- Ter um plano do que fazer para vários cenários possíveis de violação;

- Microssegmentação da LAN a fim de evitar a movimentação lateral;

- ACLs, NAC, ZTNA...
