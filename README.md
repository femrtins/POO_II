**SIMULAÇÃO DE MÉTODOS DE EMBARQUE EM AVIÕES**

Fernanda Ribeiro Martins[^1] José Mateus Amaral[^2] Monique Ellen dos Santos[^3]

**RESUMO**

Para haver maior eficiência nos processos, e consequentemente menores perdas financeiras, a diminuição de atrasos é essencial. Este artigo examina as interferências entres os passageiros que resultam em atrasos no tempo de embarque de uma aeronave. Foi desenvolvido um algoritmo de criação de sequências de filas de embarque que a partir de força bruta, poderia encontrar a melhor sequência e diminuir atrasos em voos. Os resultados apontam que métodos específicos podem ser usados para aumentar a eficiência em embarques. Dessa forma, é possível diminuir o tempo de embarque utilizando o algoritmo, apesar de não levar em consideração aleatoriedades e espaço para bagagens.

**INTRODUÇÃO**

O processo de embarque em um avião envolve uma série de etapas que o torna um desafio logístico. O tempo gasto pelos passageiros se acomodarem em seus assentos tem impacto direto na eficiência e pontualidade dos voos. Atrasos no embarque resultam em inconvenientes para os passageiros e custos adicionais para as companhias aéreas.

No solo as empresas aéreas perdem receita e possuem custos para manter as aeronaves. Nos Estados Unidos, cada minuto pode potencialmente economizar 16.000.000,00 (dezesseis milhões) dólares, tendo em vista uma média de 1500 (mil e quinhentos) voos por ano. (STEFFEN; HOTCHKISS, 2011)

Nesse contexto, a utilização de ambientes simulados surge como uma abordagem promissora para otimizar o tempo de embarque, permitindo a análise e teste de diferentes estratégias antes de sua implementação em ambientes reais. A utilização de simuladores para testar esse tipo de situação já é conhecida e testada por Bazargan (2006) e Landeghem (2001), entretanto estes artigos não dispõem de uma ferramenta capaz de encontrar a melhor alternativa entre todas as possibilidades, utilizando somente os métodos conhecidos a partir de modelos matemáticos.

Este artigo tem como objetivo explorar a aplicação de um ambiente simulado na otimização do tempo que as pessoas demoram para embarcar em uma aeronave. Através do uso de técnicas de programação orientada a objetos e algoritmos de otimização, buscamos encontrar uma sequência de assentamento mais eficiente, considerando interferências de assentos e bagagem de mão.

**MATERIAL E MÉTODOS**

O código foi feito em Python 3.10, possui 7 classes (Figura 1), implementação em SQLite para armazenar as sequências.[^4]

![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.001.png)

**Figura 1-**Diagrama de classes do código. Fonte: Construção dos autores.

A primeira etapa do algoritmo consiste em definir uma representação adequada dos passageiros e dos assentos disponíveis na aeronave. Cada passageiro é tratado como um objeto individual, contendo as informações do número do assento e existência de bagagem. Os assentos também são representados como objetos, com características como localização, classe e disponibilidade.

Ao iniciarmos o algoritmo, é criado uma fila de pessoas. Cada passageiro na fila do avião anda para frente na fila, até que chegue na linha correspondente ao seu assento. Caso o passageiro tenha bagagem, ele precisará de tempo parado na fila, para que possa acomodar sua bagagem corretamente. As pessoas atrás na fila devem esperar até que essa ação seja realizada. Após realizada a ação, os demais passageiros estão livres para passar pela parte da fila onde o passageiro com a bagagem estava. Caso o passageiro não possua bagagem, ele irá sentar instantaneamente ao chegar no seu lugar, desta forma, não irá obstruir a passagem.

Cada vez que a simulação é executada, é gerada uma nova sequência de embarque. Uma variável importante neste processo é o caso de o passageiro ter bagagem ou não, pois, quando há bagagem, há interferência no andamento da fila por determinado período de tempo, causando um congestionamento. Outro fator que proporciona o bloqueio no corredor é quando existem pessoas sentadas entre o passageiro e seu assento.

O código armazena as sequências e seus respectivos tempo gasto. O algoritmo para encontrar a melhor maneira de embarque na aeronave é de ordem O(n!), ou seja,

em uma aeronave com 138 assentos precisa de um tempo correspondente a 1, 59277anos para encontrar a(s) melhor(es) sequências.

Para fins de comparação com outros estudos, as simulações foram calculadas com 72 assentos, sendo 6 fileiras e um corredor central (Figura 2). Também são considerados métodos de embarque, Steffen e Hotchkiss, (2011) apresentam cinco métodos de embarque que foram implementados no código, sendo:

![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.002.jpeg)

**Figura 2-**Visualização da simulação do avião. Fonte: STEFFEN; HOTCHKISS, 2011

- Aleatório: Os passageiros embarcam em qualquer ordem. Não há sequências determinadas.
- Por Blocos: Os passageiros são divididos em três grupos. As 4 últimas linhas do avião formam o primeiro grupo (9-12), as 4 linhas do meio formam o segundo grupo (05-08) e o último grupo é formado pelos passageiros das primeiras linhas (01-04).
- Back To Front: A ordem é pré definida, embarcam primeiro os passageiros da última linha, é ocupado primeiro os assentos das janelas, depois do meio e por último os do corredor.
- Método Wilma: Os passageiros são divididos em três grupos. O primeiro grupo é definido pelos que sentam nas janelas, o segundo grupo são os que ocupam as colunas do meio, e o terceiro grupo ocupam as fileiras do corredor.
- Método Steffen: A ordem de embarque é pré definida, já que os passageiros são prescritos a embarcar em uma ordem específica. Essa ordem incorpora o método de trás para frente e das janelas para o corredor. Na fila de embarque os passageiros são organizados de forma que ficam a uma distância de duas fileiras um do outro. (Figura 3)

![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.003.jpeg)

**Figura 3-**Ordem de embarque do método Steffen. Fonte: STEFFEN; HOTCHKISS, 2011

**RESULTADOS E DISCUSSÃO**

Ao comparar os resultados obtidos utilizando diferentes estratégias de embarque, observou-se que o algoritmo de otimização foi capaz de reduzir significativamente o tempo médio de assentamento em relação a abordagens convencionais. Isso indica que a sequência de assentamento determinada pelo algoritmo considerou efetivamente os critérios de otimização, levando a uma distribuição mais eficiente dos passageiros pela aeronave.

Utilizando uma ordem aleatória de embarque, em 100.000 simulações, a maior parte das sequências dura entre 150 e 170 unidades de tempo. É considerada uma unidade de tempo a locomoção de um passageiro para um lugar na frente da fila. Com o tempo menor do que 150 a curva no gráfico do tempo de embarque (Figura 4) se torna mais inclinada, o que implica em poucas sequências com esses valores. Assim como a curva fica mais inclinada assim que atinge os 170, indicando uma menor quantidade de simulações que atingem essa marca.

![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.004.jpeg)

**Figura 4-** Gráfico de Tempo de Embarque. Fonte: Construção dos autores.

Os métodos considerados para comparação com o aleatório apresentaram os seguintes tempos (Tabela 1).

**Tabela 1 –** Tempo de cada método para o embarque de passageiros

Métodos Tempo

Aleatório (tempo médio) 160 ![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.005.png)Blocks (tempo médio) 188 Back to Front (tempo fixo) 256 Método Wilma (tempo médio) 157 Método Wilma (ordem específica) 91 Método Steffen (tempo fixo) 114

Fonte: Construção dos autores.

Pode-se notar que o método de Blocks possui um tempo superior ao aleatório, isso pode ser explicado pelo fato de que dessa forma existem mais interferências durante o assentamento, já que são criados três setores menores que se comportam como um avião por si só.

O método de trás para frente possui um tempo alto em relação aos outros, já que sofre com muitas interferências na fila do corredor do avião, pois os passageiros vão sentar sempre na mesma linha.

O método Wilma utilizado de forma arbitrária possui um tempo médio abaixo do método aleatório.O método Steffen resultou em um tempo fixo de 114. Entretanto, utilizando uma ordem específica definida pelos autores baseada no método Wilma é possível diminuir o tempo para 91, tornando essa sequência mais rápida que o estipulado em Steffen (2011). Essa sequência começa de trás para frente, das fileiras da janela para as do corredor (Figura 5).

![](Aspose.Words.021752bd-4484-4042-a91d-aaa2fef7c45e.006.png)

**Figura 5-**Exemplo de sequência com tempo de 91. Fonte: Construção dos autores.

Esse resultado está de acordo com a pesquisa de Landeghem e Beuselinck, onde a ordem mais rápida é basicamente em ordem decrescente de linha e ordem de assento de fora para dentro.

Um ponto fraco deste algoritmo é que, conforme a quantidade de simulações testadas aumenta, maior é o tempo para testar novas simulações, pois precisamos realizar a verificação para não testar a mesma simulação mais de uma vez, o que causa um desperdício de processamento.

**CONSIDERAÇÕES FINAIS**

A simulação é uma ferramenta poderosa para testar diferentes estratégias de embarque, explorar cenários e coletar dados precisos sobre o desempenho do processo. A capacidade de repetir a simulação múltiplas vezes, ajustar variáveis e analisar os resultados de forma controlada e segura, possibilita uma análise aprofundada do impacto das estratégias de assentamento.

Os resultados obtidos na simulação demonstraram que a abordagem de otimização foi eficaz em reduzir o tempo médio de assentamento, melhorar o tempo de espera dos passageiros e aumentar a eficiência geral do embarque. No entanto, vale ressaltar que o trabalho apresenta algumas limitações. A simulação considerou um conjunto específico de variáveis, e é importante reconhecer que a complexidade do processo de assentamento pode variar em diferentes contextos e aeronaves. Portanto, é recomendado que futuras pesquisas explorem diferentes cenários e considerem uma variedade maior de variáveis para uma análise mais abrangente.

O simulador não considera o espaço das bagagens. O mais comum é quando o passageiro guarda a bagagem o mais próximo possível de seu assento, pode acontecer de o espaço mais próximo para guardar esteja a duas linhas a frente ou atrás de seu assento, o que proporciona um tempo maior de interferência na fila. Também não são levados em consideração aleatoriedades, como trocas de assentos e pessoas com maior dificuldade de locomoção.

Espera-se que este trabalho incentive pesquisas futuras nesta área, com a exploração de novas estratégias, aprimoramentos nos algoritmos de otimização e a consideração de aspectos adicionais que possam impactar o processo de assentamento dos passageiros.

**REFERÊNCIAS**

BAZARGAN, Massoud. A linear programming approach for aircraft boarding strategy. **European Journal Of Operational Research**. A, p. 394-411. 14 dez. 2006. Disponível em: https://courses.nus.edu.sg/course/cheld/internet/CN5111/Reference/LP/A%20linear%20 programming%20approach%20for%20aircraft%20boarding%20strategy.pdf. Acesso em: 12 jun. 2023.

STEFFEN, Jason H.; HOTCHKISS, Jon. **Experimental test of airplane boarding methods**. European Journal Of Operational Research. Blumenau, p. 64-67. jan. 2012. Disponível em: https://arxiv.org/abs/1108.5211. Acesso em: 12 jun. 2023.

LANDEGHEM, H.; BEUSELINCK, A.. **Reducing passenger boarding time in airplanes**: A simulation based approach. European Journal Of Operational Research 142. p. 294-308. out. 2002. Disponível em: https://www.researchgate.net/publication/222639981\_Reducing\_passenger\_boarding\_ti me\_in\_airplanes\_A\_simulation\_based\_approach. Acesso em: 12 jun. 2023.

[^1]: Aluna do Bacharelado de Ciência da Computação; fernandamartins.rm@gmail.com
[^2]: Aluno do Bacharelado de Ciência da Computação; josemateusamaral@gmail.com
[^3]: Aluna do Bacharelado de Ciência da Computação; moniqueellen1402@gmail.com
[^4]: Link do github:
