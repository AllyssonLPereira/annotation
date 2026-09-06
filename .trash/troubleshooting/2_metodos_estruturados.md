---
tags:
  - arquivo
---
### Métodos Estruturados de Solução de Problemas

Existem várias abordagens estruturadas de solução de problemas que podem ser usadas. Qual usar dependerá da situação. Cada abordagem tem suas vantagens e desvantagens.


- [Bottom-Up]:

	Na solução de problemas de baixo para cima, você começa com os componentes físicos da rede e sobe pelas camadas do modelo OSI até que a causa do problema seja identificada.

	A identificação e solução de problemas bottom-up é um bom método a ser usado quando há suspeita de que o problema seja físico. *A maioria dos problemas de rede reside nos níveis inferiores, portanto, a implementação da abordagem bottom-up é frequentemente eficaz.

	A desvantagem da abordagem de identificação e solução de problemas bottom-up é o fato de que ela requer a verificação de todos os dispositivos e interfaces na rede, até encontrar a possível causa do problema. 


- [Top-Down]:

	A solução de problemas de cima para baixo começa com os aplicativos do usuário final e desce pelas camadas do modelo OSI até que a causa do problema seja identificada.

	Os aplicativos de usuário final de um sistema final são testados antes da abordagem das partes de rede mais específicas. *Use essa abordagem para problemas mais simples ou quando você achar que o problema está em um componente de software.

	A desvantagem da abordagem top-down é que ela requer a verificação de todos os aplicativos de rede até que seja encontrada a causa possível do problema. É necessário documentar todas as conclusões e possibilidades.


- [Divide-and-conquer]:

	O administrador de rede seleciona uma camada e testa em ambos os sentidos a partir dessa camada.
	
	Na identificação e solução de problemas divide-and-conquer, *você começa com a coleta das experiências do usuário em relação ao problema, documenta os sintomas e depois, de posse dessas informações, faz uma dedução inteligente sobre em qual camada OSI começar a investigação.* 

	Após a confirmação do funcionamento correto de uma camada, é possível pressupor que as camadas abaixo estejam funcionando. 

	O administrador pode trabalhar as camadas OSI desse ponto para cima. Se uma camada não estiver funcionando da forma correta, o administrador pode aplicar o modelo de camada OSI.


- [Siga o caminho]:

	Esta é uma das técnicas de solução de problemas mais básicas. *A abordagem primeiro descobre o caminho de tráfego real da origem até o destino. 

	O escopo da solução de problemas é reduzido apenas para os links e dispositivos que estão no caminho de encaminhamento. 

	O objetivo é eliminar os links e dispositivos que são irrelevantes para a tarefa de solução de problemas em mãos. Esta abordagem geralmente complementa uma das outras abordagens.


- [Substituição]:

	Essa abordagem também é chamada de [troca do componente] porque você troca fisicamente o dispositivo problemático por um conhecido e funcional. 

	Em situações específicas, *esse pode ser um método ideal para a rápida resolução de problemas, como em um único ponto crítico de falha.* 


