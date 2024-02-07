# SIMULAÇÃO DE MÉTODOS DE EMBARQUE EM AVIÕES

## Autores:
- Fernanda Ribeiro Martins
- José Mateus Amaral
- Monique Ellen dos Santos

## RESUMO

Para haver maior eficiência nos processos, e consequentemente menores perdas financeiras, a diminuição de atrasos é essencial. Este artigo examina as interferências entre os passageiros que resultam em atrasos no tempo de embarque de uma aeronave. Foi desenvolvido um algoritmo de criação de sequências de filas de embarque que a partir de força bruta, poderia encontrar a melhor sequência e diminuir atrasos em voos. Os resultados apontam que métodos específicos podem ser usados para aumentar a eficiência em embarques. Dessa forma, é possível diminuir o tempo de embarque utilizando o algoritmo, apesar de não levar em consideração aleatoriedades e espaço para bagagens.

## INTRODUÇÃO

O processo de embarque em um avião envolve uma série de etapas que o torna um desafio logístico. O tempo gasto pelos passageiros se acomodarem em seus assentos tem impacto direto na eficiência e pontualidade dos voos. Atrasos no embarque resultam em inconvenientes para os passageiros e custos adicionais para as companhias aéreas.

No solo as empresas aéreas perdem receita e possuem custos para manter as aeronaves. Nos Estados Unidos, cada minuto pode potencialmente economizar 16.000.000,00 (dezesseis milhões) dólares, tendo em vista uma média de 1500 (mil e quinhentos) voos por ano. (STEFFEN; HOTCHKISS, 2011)

Nesse contexto, a utilização de ambientes simulados surge como uma abordagem promissora para otimizar o tempo de embarque, permitindo a análise e teste de diferentes estratégias antes de sua implementação em ambientes reais. A utilização de simuladores para testar esse tipo de situação já é conhecida e testada por Bazargan (2006) e Landeghem (2001), entretanto estes artigos não dispõem de uma ferramenta capaz de encontrar a melhor alternativa entre todas as possibilidades, utilizando somente os métodos conhecidos a partir de modelos matemáticos.

Este artigo tem como objetivo explorar a aplicação de um ambiente simulado na otimização do tempo que as pessoas demoram para embarcar em uma aeronave. Através do uso de técnicas de programação orientada a objetos e algoritmos de otimização, buscamos encontrar uma sequência de assentamento mais eficiente, considerando interferências de assentos e bagagem de mão.

## MATERIAL E MÉTODOS

O código foi feito em Python 3.10, possui 7 classes (Figura 1), implementação em SQLite para armazenar as sequências.

![Figura 1 - Diagrama de classes do código. Fonte: Construção dos autores.](https://link_para_a_imagem)

A primeira etapa do algoritmo consiste em definir uma representação adequada dos passageiros e dos assentos disponíveis na aeronave. Cada passageiro é tratado como um objeto individual, contendo as informações do número do assento e existência de bagagem. Os assentos também são representados como objetos, com características como localização, classe e disponibilidade.

Ao iniciarmos o algoritmo, é criada uma fila de pessoas. Cada passageiro na fila do avião anda para frente na fila, até que chegue na linha correspondente ao seu assento. Caso o passageiro tenha bagagem, ele precisará de tempo parado na fila, para que possa acomodar sua bagagem corretamente. As pessoas atrás na fila devem esperar até que essa ação seja realizada. Após realizada a ação, os demais passageiros estão livres para passar pela parte da fila onde o passageiro com a bagagem estava. Caso o passageiro não possua bagagem, ele irá sentar instantaneamente ao chegar no seu lugar, desta forma, não irá obstruir a passagem.

Cada vez que a simulação é executada, é gerada uma nova sequência de embarque. Uma variável importante neste processo é o caso de o passageiro ter bagagem ou não, pois, quando há bagagem, há interferência no andamento da fila por determinado período de tempo, causando um congestionamento. Outro fator que proporciona o bloqueio no corredor é quando existem pessoas sentadas entre o passageiro e seu assento.

O código armazena as sequências e seus respectivos tempos gastos. O algoritmo para encontrar a melhor maneira de embarque na aeronave é de ordem O(n!), ou seja, em uma aeronave com 138 assentos precisa de um tempo correspondente a 1, 59277 anos para encontrar a(s) melhor(es) sequências.

Para fins de comparação com outros estudos, as simulações foram calculadas com 72 assentos, sendo 6 fileiras e um corredor central (Figura 2). Também são considerados métodos de embarque, Steffen e Hotchkiss, (2011) apresentam cinco métodos de embarque que foram implementados no código, sendo:

![Figura 2 - Visualização da simulação do avião. Fonte: STEFFEN; HOTCHKISS, 2011](https://link_para_a_imagem)

- Aleatório: Os passageiros embarcam em qualquer ordem. Não há sequências determinadas.
- Por Blocos: Os passageiros são divididos em três grupos. As 4 últimas linhas do avião formam o primeiro grupo (9-12), as 4 linhas do meio formam o segundo grupo (05-08) e o último grupo é formado pelos passageiros das primeiras linhas (01-04).
- Back To Front: A ordem é pré definida, embarcam primeiro os passageiros da última linha, é ocupado primeiro os assentos das janelas, depois do meio e por último os do corredor.
- Método Wilma: Os passageiros são divididos em três grupos. O primeiro grupo é definido pelos que sentam nas janelas, o segundo grupo são os que ocupam as colunas do meio, e o terceiro grupo ocupam as fileiras do corredor.
- Método Steffen: A ordem de embarque é pré definida, já que os passageiros são prescritos a embarcar em uma ordem específica. Essa ordem incorpora o método de trás para frente e das janelas para o corredor. Na fila
