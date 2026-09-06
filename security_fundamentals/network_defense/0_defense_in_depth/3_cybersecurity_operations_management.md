---
tags:
  - arquivo
---
## Configuration management

O gerenciamento de configuração refere-se à identificação, controle e auditoria da implementação/alterações feitas à linha de base estabelecida de um sistema.

> *A configuração da linha de base inclui todas as definições para um sistema que fornecem a base para todos os sistemas semelhantes, como um tipo de modelo.*

Por exemplo, os responsáveis pela implantação de estações de trabalho do Windows para usuários devem instalar os aplicativos necessários e definir as configurações do sistema de acordo com uma configuração documentada. Essa é a configuração de linha de base para as estações de trabalho Windows nessa empresa.

Os recursos de configuração documentados podem incluir o seguinte:

- Mapas de rede, diagramas de cabeamento, especificações de configuração da aplicação;
- Convenções de nomenclatura padrão usadas para computadores;
- Esquema IP para rastrear endereços IP.


> *O reforço do sistema operacional é uma parte importante para garantir que os sistemas tenham configurações seguras. A configuração de arquivos de log junto com a auditoria, a alteração de nomes de conta e senhas e a implementação de políticas de conta e controle de acesso no nível de arquivo são usados para criar um sistema operacional seguro.*

---
## Log files

Um log registra todos os eventos que ocorrem. Entradas de log compõem um arquivo de log e uma entrada de log contém todas as informações relacionadas a um evento específico. *Registros precisos e completos são muito importantes na segurança digital*.

Por exemplo, um log de auditoria rastreia as tentativas de autenticação do usuário e um log de acesso fornece todos os detalhes sobre as solicitações para arquivos específicos de um sistema. O monitoramento dos logs do sistema pode determinar como um ataque ocorreu e se as defesas implantadas foram bem-sucedidas.

Com o aumento do número de arquivos de log gerados para fins de segurança do computador, a empresa deve considerar um processo de gerenciamento de logs. O gerenciamento de dados do log de segurança do computador deve determinar os procedimentos para o seguinte:

- Gerando arquivos de log;
- Transmissão de arquivos de log;
- Armazenamento de arquivos de log;
- Análise de dados;
- Descartando dados de log.


- Logs do sistema operacional:

	O sistema operacional registra eventos de registro que estão vinculados a ações relacionadas ao sistema operacional. Eventos do sistema incluem o seguinte:

	1. Solicitações do cliente e respostas do servidor, como autenticações de usuário bem-sucedidas.

	2. Informações de uso que contêm o número e o tamanho das transações em um determinado período de tempo.


- *Segurança de aplicações*:

	As empresas usam software de segurança pela rede ou pelo sistema para detectar atividade mal-intencionada.

	Esse software gera um log de segurança para fornecer dados de segurança do computador. Os logs são úteis para a realização de análise de auditoria e para a identificação de tendências e de problemas no longo prazo. 

	Os logs também permitem que uma empresa forneça documentação que mostre que está em conformidade com as leis e os requisitos regulatórios.

---
## Packet analyzers

Os *packet analyzers* — analisadores de pacotes — interceptam e registram o tráfego de rede.

O packet analyzer captura cada pacote, mostra os valores de vários campos no pacote e analisa o conteúdo. Um sniffer pode capturar o tráfego em redes com e sem fio.

Packet analyzers executam as seguintes funções:

- Log de tráfego;
- Análise de problemas de rede;
- Detecção de uso indevido da rede;
- Detecção de tentativas de invasão da rede;
- Isolamento do sistema explorado.

![[network_defense-ativos_vulnerabilidades_ameacas-analisadores_de_protocolos.png]]