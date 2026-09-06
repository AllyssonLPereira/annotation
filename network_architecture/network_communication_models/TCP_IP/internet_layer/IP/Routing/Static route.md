## O Que é uma rota estática

O roteamento estático é uma forma manual de indicar ao roteador como ele deve alcançar uma rede de destino. Em vez de utilizar protocolos dinâmicos que "conversam" entre si para descobrir caminhos, o administrador da rede insere manualmente na tabela de roteamento a informação de qual o caminho deve ser seguido para chegar a um destino específico. 

É um método que oferece controle total ao administrador, pois o caminho dos pacotes torna-se previsível e fixo, além de não consumir recursos de processamento ou largura de banda do roteador com mensagens de atualização, sendo ideal para redes menores ou pontos terminais onde o caminho é único.

## Default Static Route

A Rota Estática Padrão, frequentemente chamada de "gateway de último recurso", é um tipo especial de rota estática utilizada quando o roteador não possui uma instrução específica para o destino de um pacote. Em vez de descartar o pacote por falta de informação, o roteador consulta a rota padrão como uma alternativa de "último esforço". 

Ela é configurada com um endereço de rede e uma máscara que representam "qualquer lugar" (geralmente lida como 0.0.0.0 com máscara 0.0.0.0), funcionando como uma porta de saída universal.

Veja bem, 0.0.0.0/0 é um endereço que não tem porção de rede, apenas host; nele, temos todas as possibilidades possíveis de endereços, ou melhor, ele abrange todos os endereços nele. Logo, quando não há uma outra rota mais específica, ela será encaminhada para essa rota.

