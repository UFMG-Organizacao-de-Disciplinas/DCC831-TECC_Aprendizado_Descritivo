# A

## B

### **Slide:** aula12-SSDP - Algoritmos evolucionários para descoberta de subgrupos

#### Introdução

- Como vimos, as abordagens heurísticas são necessárias em situações em que os algoritmos exaustivos falham
- Frequentemente, essa situação ocorre em bases de dados com muitos atributos (alta dimensionalidade)
- Nesses casos, o espaço de busca cresce muito rapidamente, mesmo considerando linguagens com seletores mais simples
- Um dos problemas do beam search é que o resultado final é bastante redundante, apesar da medidas implementadas para combater a redundância

---

- A figura abaixo mostra a cobertura dos 100 melhores subgrupos encontrados em uma base de dados de benchmark
- Como pode ser visto, existem essencialmente duas classes de padrões
  - Uma do 1-60 que cobrem uma parte das amostras
  - Outra do 60-100 que cobrem uma parte disjunta
  - Mas os subgrupos de cada parte cobrem essencialmente os mesmos objetos

[Imagem: Fig. extraída de Van Leeuwen e Knobbe (2012) | Tuples X Subgroups]

---

- Usando o exemplo de van Leeuwen e Knobbe (2012), assuma uma base de dados com os atributos à esquerda, sendo os melhores individuais como na coluna do meio, e segundo nível do beam search com beam width = 4 à direita
- Percebemos que, já no segundo nível, o beam é dominado por combinações dos melhores seletores

- $fatalities$: positive integer
- $nature$: $\{ fatal, injured, damage\ only \}$
- $time$: $\{ day, night \}$
- $cost$: positive real

===

1. $fatalities \geq 1$
2. $nature = fatal$
3. $fatalities \geq 2$
4. $nature damage\ only$
5. $time = night$
6. $\dots \dots$

===

1. $fatalities \geq 1 \land nature = fatal$
2. $fatalities \geq 1 \land nature  \neq damage\ only$
3. $fatalities \geq 1 \land fatalities \geq 2$
4. $nature = fatal /land cost \geq 123.4$

---

- Assim, o grande esforço computacional dispendido na busca dos padrões é usado para encontrar combinações dos melhores seletores
- Outra abordagem muito usada em problemas de otimização são heurísticas baseadas em computação natural (em particular, abordagens evolucionárias)
- Abordagens evolucionárias usam metáforas da natureza para construção de algoritmos heurísticos
  - Nesse caso, a teoria de evolução das espécies
- Esses algoritmos possuem aplicações em vários contextos, obtendo bons resultados por sua capacidade de balancear exploração e explotação do espaço de busca
- Vamos ver dois métodos para descoberta de subgrupos baseados em algoritmos genéticos

#### Algoritmos Genéticos

- Os algoritmos genéticos (GA) se baseiam nos processos biológicos de seleção natural para evolução de espécies
- Intuitivamente, os indivíduos de uma população se cruzam, trocando material genético, o qual pode sofrer mutações para produzir novos indivíduos na população
- Considerando-se que os recursos disponíveis são limitados, apenas os indivíduos mais aptos sobrevivem, passando seu material genético para as novas gerações
- A heurística computacional se baseia nesses princípios para navegar no espaço de busca

---

- O primeiro passo na construção de um algoritmo genético é definir a representação dos cromossomos dos indivíduos
  - O mais comum é a representação binária, em que cada bit (gene) representa a inclusão ou exclusão de um valor
  - Outras representações mais complexas também podem ser usadas
- O segundo passo é definir uma função de aptidão (fitness), que corresponde à função objetivo que queremos otimizar
- Em seguida, o algoritmo entra em um ciclo onde a população evolui até que um critério de parada seja alcançado

---

- De uma forma geral, os GAs possuem a seguinte estrutura:
- [Algoritmo]
  - Início
    - $t \gets 1$
    - **Inicializar** a população $P(t)$
    - **Avaliar** a população $P(t)$
    - **Enquanto** não atingir critério de parada:
      - **Selecionar** indivíduos para reprodução em $P(t)$
      - **Aplicar** operadores genéticos para produzir população $P(t+1)$
      - **Avaliar** $P(t+1)$
      - $t \gets t + 1$
    - Fim **Enquanto**
  - Fim

---

- Existem diferentes abordagens para a seleção dos indivíduos que serão usados na reprodução
  - Seleção proporcional ao fitness (método da roleta)
  - Seleção por torneio
- Os demais operadores genéticos são cruzamento e mutação
  - Esses operadores são aplicados com probabilidades estabelecidas pelo usuário
- No cruzamento, um par de indivíduos selecionados pelo operador de seleção trocam seu material genético para construir dois novos indivíduos
  - Existem diferentes formas de combinar esses indivíduos, algumas sendo específicas para alguns tipos de representação
- A mutação altera de forma aleatória um ou mais genes do indivíduo, gerando uma nova solução (indivíduo)
  - Esse operador também é desenhado conforme a aplicação em questão
- Após a geração dos novos indivíduos, a próxima geração é selecionada para continuar a evolução

#### SSDP

- O algoritmo Simple Search Discriminative Patterns (SSDP) foi proposto por Pontes, Vimieiro e Ludermir em 2016
- O SSDP é uma heurística evolucionária para encontrar top-k subgrupos em bases de dados de alta dimensionalidade
- O algoritmo foi desenhado especificamente para encontrar padrões em bases com essa característica, onde, os outros métodos do estado da arte falhavam
- Dado o grande número de atributos, os autores optaram por simplificar a linguagem de descrição, considerando apenas seletores da forma atributo=valor
  - São aceitos somente dados categóricos

---

- Quanto ao atributo alvo, inicialmente foi previsto somente dados categóricos. Contudo, não há restrições caso a função de fitness seja ajustada para medidas de qualidade numéricas
- Como a ideia do algoritmo era ser simples de usar, vários parâmetros comuns a algoritmos genéticos foram ajustados automaticamente
  - A taxa de mutação e cruzamento são adaptativas e determinadas pelo algoritmo
  - O tamanho da população é fixo, determinado pelo número de seletores da base
  - O usuário tem que determinar o valor de $k$, e a função de qualidade desejada

---

- O algoritmo mantém dois conjuntos de subgrupos paralelos ao longo da execução
  - Os $k$ melhores subgrupos
  - A população atual do GA
- A população é inicializada com todos os possíveis seletores
  - Isso permite que mais soluções candidatas sejam exploradas pelo algoritmo, uma vez que o espaço de busca é muito grande
- Como os primeiros indivíduos são seletores únicos, houve a necessidade de se criar um operador de cruzamento específico para a primeira geração
  - Esse operador é equivalente ao gerador de candidatos do Apriori
- A partir da segunda geração, foi utilizado cruzamento uniforme
- O operador de mutação consiste em 3 ações distintas equiprováveis
  - Troca de um seletor por outro
  - Remoção de um seletor
  - Inclusão de um seletor
- O operador de seleção é torneio binário

---

- A cada iteração, os $k$ melhores indivíduos **relevantes** tentam substituir os atuais subgrupos em $P_k$
- Caso não haja melhoria, a taxa de cruzamento é decrementada e mutação aumenta em 0.2
  - As taxas de mutação e cruzamento devem sempre somar a 1
- Se a mutação chegar em 1 e não houver melhora por 3 gerações, a população é reinicializada
  - 10% aleatória com os seletores dos $k$ melhores subgrupos
  - 90% aleatória contendo de 1 à média de seletores por indivíduo na população atual
- Se a população for reinicializada por 3 vezes, a busca é interrompida

---

- **Require:** $k, metricEvaluation$
  - $P \gets \{ \{i_1\}, \{i_2\}, \dots, \{i_{|I|}\} \}$
  - $P_k \gets kBestRelevants(P)$
  - $reinializationCount \gets 0$
  - $mutationRate \gets 0.4$
  - $crossoverRate \gets 0.6$
- **While** $reinializationCount < 2$ **do**
  - **While** $P_k$ not improve three consecutive generations keeping $mutationRate == 1.0$ **do**
    - **If** $generation == 1$ **then**
      - $Pnew \gets crossoverAND(P)$
    - **Else** {generation > 1}
      - $P_{new} \gets evolutionaryOperator(P, mutationRate, crossoverRate)$
    - **End if**
    - $P* \gets best(P, P_{new})$
    - $P_k \gets kBestRelevants(P_k, P_{*})$
    - $update(mutationRate, crossoverRate)$
    - $P \gets P_{*}$
  - **End while**
  - $reinializationCount ++$
  - $P \gets restart$
- **End while**
- **Return** $P_k$

---

| **Name**    | **$\mid D\mid$** | **$\mid D^{+}\mid$** | **$\mid D^{-}\mid$** | **Attributes** |
| :---------- | ---------------: | -------------------: | -------------------: | -------------: |
| Alon        |               62 |                   40 |                   22 |           2000 |
| Borovecki   |               31 |                   17 |                   14 |          22283 |
| Burczynski  |              127 |                   59 |                   68 |          22283 |
| Chiaretti   |              128 |                   74 |                   54 |          12625 |
| Chin        |              118 |                   75 |                   43 |          22215 |
| Chowdary    |              104 |                   62 |                   42 |          22283 |
| Christensen |              217 |                  113 |                  104 |           1413 |
| Golub       |               72 |                   47 |                   25 |           7129 |
| Gordon      |              181 |                  150 |                   31 |          12533 |
| Gravier     |              168 |                  111 |                   57 |           2905 |
| Khan        |               63 |                   23 |                   40 |           2308 |
| Nakayama    |              105 |                   21 |                   84 |         220283 |
| Pomeroy     |               60 |                   39 |                   21 |           7128 |
| Shipp       |               77 |                   58 |                   19 |           7129 |
| Singh       |              102 |                   52 |                   50 |          12600 |
| Sorlie      |               85 |                   32 |                   53 |            456 |
| Subramanian |               50 |                   33 |                   17 |          10100 |
| Sun         |              180 |                   81 |                   99 |          54613 |
| Tian        |              173 |                  137 |                   36 |          12625 |
| West        |               49 |                   25 |                   24 |           7129 |
| Yeoh        |              248 |                   79 |                  169 |          12625 |

WRAcc, k, time, number of tests and patterns obtained by SSDP and NMEEF-1k-1M algorithms in 10 microarray databases.

| Base        | Algorithm   | $WRAcc_{normalized}$ | $k$ | $Time(s)$ | $Tests (10^6)$ |
| :---------- | :---------- | -------------------: | --: | --------: | -------------: |
| Alon        | NMEEF-1k-1M |                0.260 |   3 |      1984 |              1 |
| Burczynski  | NMEEF-1k-1M |                0.000 |   0 |     63697 |              1 |
| Chiaretti   | NMEEF-1k-1M |                0.000 |   0 |     36882 |              1 |
| Chin        | NMEEF-1k-1M |                0.388 |   1 |     31301 |              1 |
| Christensen | NMEEF-1k-1M |                0.592 |   1 |      3408 |              1 |
| Gravier     | NMEEF-1k-1M |                0.232 |   1 |      5745 |              1 |
| Nakayama    | NMEEF-1k-1M |                0.000 |   0 |     58419 |              1 |
| Tian        | NMEEF-1k-1M |                0.000 |   0 |     43218 |              1 |
| Yeoh        | NMEEF-1k-1M |                0.000 |   0 |    104533 |              1 |
| Sun         | NMEEF-1k-1M |                    - |   - |         - |              - |
| ---         | ---         |                  --- | --- |       --- |            --- |
| Alon        | SSDP        |                0.572 |   5 |     0.422 |          0.116 |
| Burczynski  | SSDP        |                0.684 |   5 |     8.254 |          1.247 |
| Chiaretti   | SSDP        |                0.584 |   5 |     4.789 |          0.808 |
| Chin        | SSDP        |                0.624 |   5 |     5.928 |          0.799 |
| Christensen | SSDP        |                0.896 |   5 |     0.297 |          0.056 |
| Gravier     | SSDP        |                0.440 |   5 |     0.905 |          0.185 |
| Nakayama    | SSDP        |                0.600 |   5 |     7.893 |          1.515 |
| Tian        | SSDP        |                0.296 |   5 |     4.072 |          0.505 |
| Yeoh        | SSDP        |                0.848 |   5 |     8.798 |          0.782 |
| Sun         | SSDP        |                0.186 |   5 |    36.315 |          3.386 |

#### SSDP+

- Embora as medidas implantadas garantiam certo nível de eliminação de redundância, o que foi observado na prática é que a cobertura global ainda poderia ser melhorada caso outras medidas fossem implementadas
- Essas medidas, além de controlar a redundância, permitiam que padrões alternativos fossem encontrados e apresentados ao usuário. Esses padrões, por sua vez, podem ser mais úteis ao usuário
- Assim, Lucas, Vimieiro e Ludermir (2018) apresentaram uma extensão do SSDP para incluir outras formas de controle de redundância

---

- O algoritmo SSDP+ introduziu o conceito de cache para os padrões
- O conjunto $P_k$ dos $k$ melhores padrões passou a ser tratado como uma lista ordenada
- Ao preencher essa lista, o algoritmo verifica a similaridade de cobertura do novo padrão com respeito aos já inseridos, sequencialmente
- Caso o novo subgrupo $s'$ seja similar a algum subgrupo s já inserido, verifica-se se $s'$ possui qualidade inferior a s, se for o caso, então $s'$ é inserido no cache de s
  - Como o cache é limitado, ele deve substituir o de pior qualidade
- Se $s'$ for similar, mas possui maior qualidade, então ele assume o papel de $s$, e o cache é recriado (os elementos são reinserido em $P_k$)
- Se $s'$ não é similar a nenhum dos subgrupos já inseridos em $P_k$, ele é inserido à lista se o número de elementos presente for menor que k, e descartado caso contrário

---

- $item_{dom} = \max \{ count(i) / k \}$
  - $count(i) = | \{ X \in P_k | i \in X \} |$
- $SUPP^{+} = \bigcup_{X \in P_k} c^{+} (X) | / N$

[Tabelas]

#### Leitura

- [Link][Vimieiro_2018] T. Lucas, R. Vimieiro and T. Ludermir, "SSDP+: A Diverse and More Informative Subgroup Discovery Approach for High Dimensional Data," 2018 IEEE Congress on Evolutionary Computation (CEC), Rio de Janeiro, Brazil, 2018, pp. 1-8.
- [Link][Vimieiro_2017] Tarcísio Lucas, Túlio C.P.B. Silva, Renato Vimieiro, and Teresa B. Ludermir. 2017. A new evolutionary algorithm for mining top-k discriminative patterns in high dimensional data. Appl. Soft Comput. 59, C (October 2017), 487–499.
- [Link][Vimieiro_2016] T. Pontes, R. Vimieiro and T. B. Ludermir, "SSDP: A Simple Evolutionary Approach for Top-K Discriminative Patterns in High Dimensional Databases," 2016 5th Brazilian Conference on Intelligent Systems (BRACIS), Recife, Brazil, 2016, pp. 361-366.

[Vimieiro_2018]: https://doi.org/10.1109/CEC.2018.8477855
[Vimieiro_2017]: https://doi.org/10.1016/j.asoc.2017.05.048
[Vimieiro_2016]: https://doi.org/10.1109/BRACIS.2016.072
