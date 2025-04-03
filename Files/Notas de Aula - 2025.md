# Aprendizado Descritivo - Renato Vimieiro - 2025

## Aula 01 | 18/03/2025 | Apresentação do curso - [JV: Cheguei atrasado]

### Slide 1

#### Introdução

...

#### Aprendizado Preditivo

- O que desejamos é receber informações e conseguir retornar um rótulo.
- Nem todos de aprendizado de máquina levam em consideração os rótulos.
- Aprendizado supervisionado preditivo
- [JV: não anotei sobre o que seria o supervisionado]
- Se tiver que explicar como funciona, aí é a área de Explanable AI.
- Aqui é mais importante o resultado do que o processo.

---

- Queremos um modelo que seja fiel à realidade.

---

[(Tratamento)] --> Contrução --> Avaliação --> Uso (Modelo)
Avaliação --> [(Validação)]

```mermaid
flowchart TD
  Trat[(Tratamento)]
  Cons[Construção]
  Ava[Avaliação]
  Uso[Uso (Modelo)]
  Val[(Validação)]
  Trat --> Cons
  Cons --> Ava
  Ava --> Uso
  Ava --> Val
```

- Aqui, não queremos obter nenhum entendimento sobre o que já vimos antes, mas sim, ter meios de prever como serão classificados os próximos itens que veremos.

---

- Exemplo: câncer de mama
  - Separando mulheres cuja quimioterapia foram eficazes e as que não foram.
  - Analisar quais os mapeamentos genéticos delas
  - Verificar de que forma há uma relação entre os mapeamentos genéticos e a eficácia da quimioterapia.
  - E com isso, tentar predizer se a quimioterapia será eficaz ou não para uma nova paciente.
- No aprendizado não supervisionado não há rótulos.
- Uma tarefa de aprendizado não-supervisionado bastante popular é a de agrupamento (clustering)
  - Um dos mais conhecidos é o k-menas

#### Aprendizado Descritivo

- > A premissa é "eu não sei nada sobre os dados", "então preciso encontrar um modelo que descreva os dados"
- "Estatística não é boa para descrever grafos"
- O Descritivo é tão importante quanto prever coisas, mas atuam em momentos diferentes.

---

- O aprendizado descritivo leva a descoberta en ovos conhecimentos. Estando entre mineração de dados e aprendizado de máquina.
- Busca responder "o quê aconteceu?"
- Descrevem situações passadas e com isso auxiliam no processo de **tomada de decisão**.

- 4 paradigmas científicos
  - Indução, teórico, ...
- Antes viam o fenômenos, criavam teorias, tentavam provar que as teorias se aplicavam.
- Atualmente usamos um modelo baseado em dados
  - Veem como os dados se comportas, criam teorias e tentam provar que os dados se comportam de acordo com a teoria.

---

- Uma das coisas feitas nessa disciplina é a busca por regularidades de acontecimentos em conjuntos.
- Há uma interseção bem grande entre aprendizado descritivo e Mineração de Dados.

---

- > What Wal-Mart knows about Customers' Habits
- Eles avaliaram de que forma os usuários se comportavam em relação a desastres naturais e o que compravam nas cidades que tavam para ser afetadas.
  - A decisão trivial era considerar que faria sentido estocar pilha, água mineral, lanterna e produtos não específicos.
  - Eles descobriram que houve um aumento de 7x nas vendas de Pop Tarts sabor morando, e o campeão dos aumentos foi a cerveja.
  - Nessa situação eles mais queriam descrever o passado do que predizer o futuro.
- Embora seja abordado como preditivo, na prática seria um exemplo de aprendizado descritivo supervisionado.
- Exceptional Model Mining
  - Busca-se encontrar quais conjuntos de itens são não-usualmente comprados qunado algum evento ocorre.

Dúvida: Como fazer para discernimos se um aumento, como no caso do Pop Tarts foi de fato devido aos furacões ou se calhou de, nesses dois mesmos intervalos de tempo, foram veículados anúncios desse produto; sendo então apenas uma coincidência?

Resposta: Dá para tentar refinar a forma de análise e o cálculo da função objetivo. Porém, devido ao caráter qualitativo, é difícil de se ter certeza de que essa atipicidade nessa busca por padrões atípicos sejam separados.

#### Aprendizado Descritivo X Preditivo

...

---

...

---

No modelo Preditivo, tenta-se definir limites para que próximos itens sejam classificados de acordo com o que foi visto anteriormente.

Já no Descritivo, tenta-se encontrar padrões que descrevam o que foi visto anteriormente.

---

No exemplo apontado pode-se separar as distribuições dos pontos em 4 quadrantes, isso baseado na estimativa do que já ocorreu antes, busca então estimar onde estarão posicionados os quadradinhos azuis e as bolinhas vermelhas.

É importante também identificar quais são as regularidades existentes em certos padrões irregulares.

---

Às vezes usa-se o mesmo modelo entre preditivo e descritivo, porém, um pra descrever e o outro pra predizer.

---

#### Comentários sobre o curso

Nesse curso busca-se a parte teoria dos algoritmos, não necessariamente em sua aplicação.

Ela é teórica, densa em algoritmo, e a aplicação em código é mínimo.

Busca-se "botar uma lupa" sobre a descoberta de padrões.

A primeira parte será toda não-supervisionada.

A busca de padrões em grafos pode ser usada na área de fármacos para encontrar quais sub-estruturas são as mais frequentes em determinados remédios para determinada infermidade?

A segunda parte será de aprendizado supervisionado.

Por volta de 20 de maio tem uma prova.

Haverá um tipo de "roleplaying" das atividades. Ele separou as salas em 8 grupos. Um grupo era o "historiador" (buscava entender qual era o contexto), o outro era o "metodologista" (tentatva entender como o algoritmo funcionava), "Aplicações", "Coletar as apresentações e redigir", "Publicar o resumo em um site da turma". O "hacker" é quem busca os códigos existentes, tenta entender, fazer funcionar e documentar como fez funcionar.

"Daqui para baixo é a parte mais recente, talvez mais pós graduação, ou coisas que não estão nos livros".

Cada grupo vai rotacionar em cada uma das tarefas. Serão 9 artigos no total que leremos.

Os Seminários (aplicações), veremos de fato aplicações

O que ele quer com o projeto? Uma interação maior com o professor. A parte mais prática da disciplina.

Na parte de ... será o ... que foi quem inventou.

Na parte de supervisionado: Sebastian Ventura e José Maria Luna 2018; Guozhu Dong and James Bailey 2012;

## Aula 02 | 20/03/2025 | Aprendizado descritivo x preditivo

### Slide - Aprendizado Descritivo

#### Introdução - Aula 2

- Mineração de itens alguma coisa

---

- Kosinski (2013) coletavam dados das personalidades através do MyPersonality.
  - Escândalo do Cambridge Analytica
- Buscava predizer a personalidade baseado nas curtidas feitas no Facebook

---

- Provost e Foster (2013) utilizaram os dados para demonstrar a modelagem descritiva e as informações úteis.
- Alguns exemplos de regras:
  - Selena Gomez -> Demi Lovato
  - Linking Park & Disturbed & System of a Down & Korn -> Slipknot
  - SpongeBob SquarePants & Converse [JV: empresa do All Stars] -> Patrick Star
  - Skittles & Mountain Dew -> Gatorade

[JV: Offtopic: o diretor da Google daqui fez doutorado no PPGCC]

---

- A ideia de itens em cesta de compra pode ser generalizada para itens virtuais
- Busca-se encontrar co-ocorrências de itens de análise
- Dados os limites éticos, pode-se usar essa análise para se atingir diversos objetivos.

##### Itemset e Tidsets

- Os "produtos" da cesta de compras são chamados de "Itens".
  - $I = {x_1, x_2, \dots, x_m}$
- Esses elementos serão as **variáveis de análise**
- Um conjunto $X \subseteq I$ é chamado de **Itemset**
- Um itemset de tamanho $k$ é chamado de **k-itemset**
- Denotamos o conjunto de todos os **k-itemsets** por $I^(k)$
- Todas as "Transações" serão identificadas por IDs, ou então, **TID** (Transaction ID)
- O conjunto $T = {t_1, t_2, \dots, t_n}$ é o conjunto das transações.

---

- O Conjunto $Y \subseteq T$ é chamado de **Tidset**
- É válido assumir que _itemsets_ e _tidsets_ são ordenados por ordem lexicográfica dos itens e transações. (Não importa qual ordem, mas estão de algum modo ordenados)
- Cada transação consiste de um identificador (TID) e um conjunto de itens
  - Então, cada transação é um par $(t, X)$ em que $t \in T$ e $X \subseteq I$
- Formalmente, um conjunto de dados será uma tripla $(T, I, D)$
  - T: Transações ou objetos
  - I: Atributos ou itens
  - D: Relação binária entre eles.
  - $T$ e $I$ são os conjuntos de tids e itens
  - $D \subsetq T \times I$ é a relação binária em que $(t, i) \in D$...

---

- Podemos estender a definição também para conjuntos de itens
- Dizemos que $t$ contém um itemset X sse $\forall i \in X (t, i) \in D$

Ou seja: $t$ contém $X$ se $|X - t| = 0$

---

- Dado um itemset $X$, podemos querer saber o conjunto de transações que o contém.
- Esse conjunto é chamado de **extensão** ou **cobertura** de $X$
- Ele é definido pela seguinte função:
  - $c: P(I) \to P(T)$
  - $c(X) = {t \in T | \forall i \in X(t, i) \in D}$
- Dado um tidset Y, podemos querer saber o maior conjunto de itens comuns às transações de Y.
- Esse conjunto é chamado de **intensão** (Não é intenção!) de Y.
- Ele é definido por
  - $i: P(T) \to P(I)$
  - $i(Y) = {x \in I | \forall t \in Y(t, x) \in D}$

O uso de extensão e intensão vêm da ideia filosófica e semiótica de que a extensão é o conjunto de coisas que se encaixam em uma definição, enquanto a intensão é a definição em si.

---

|  TID | Muesli | Oats | Milk | Yoghut | BIscuits |  Tea |
| ---: | -----: | ---: | ---: | -----: | -------: | ---: |
|    1 |      1 |    0 |      |        |          |    1 |
|    2 |      0 |    1 |      |        |          |    0 |
|    3 |      0 |    0 |      |        |          |    1 |
|    4 |      1 |    0 |      |        |          |    0 |
|    5 |      0 |    1 |      |        |          |    1 |
|    6 |      1 |    0 |      |        |          |    1 |

Intensão: conjunto de itens comuns a todos os elementos de um determinado conjunto de transações.

Extensão: o conjunto de transações que contenham um determinado conjunto de itens.

Intensão: a interseção das linhas
Extensão: a interseção das colunas

##### Representações de conjuntos de dados

- Podemos enxergar o conjunto de dados como um conjunto de transações e suas respectivas intensões
  - Conjunto de $(t, i(t))$
  - Essa representação é chamada de **Horizontal**
- Similarmente podemos enxergar o conjunto de dados como um conjunto de itens e suas cobrerturas
  - Conjunto de $(x, c(x))$
  - Essa representação é chamada de **Vertical**

---

- Horizontal

|    t |                       i(t) |
| ---: | -------------------------: |
|    1 | Muesli, Milk, Yoghurt, Tea |
|    2 |                 Oats, Milk |
|    3 |        Milk, Biscuits, Tea |
|    4 |            Muesli, Yoghurt |
|    5 |            Oats, Milk, Tea |
|    6 |          Muesli, Milk, Tea |

- Vertical

|    x |  Muesli | Oats |          Milk | Yoghurt | Biscuits |        Tea |
| ---: | ------: | ---: | ------------: | ------: | -------: | ---------: |
| t(x) | 1, 4, 6 | 2, 5 | 1, 2, 3, 5, 6 |    1, 4 |        3 | 1, 3, 5, 6 |

|        x |          t(x) |
| -------: | ------------: |
|   Muesli |       1, 4, 6 |
|     Oats |          2, 5 |
|     Milk | 1, 2, 3, 5, 6 |
|  Yoghurt |          1, 4 |
| Biscuits |             3 |
|      Tea |    1, 3, 5, 6 |

##### Conjuntos de itens frequentes e Regras de Associação

- A identificação de regras tais como as que vimos no exemplo no início da aula, em geral, envolvem duas etapas
  - Mineração de conjuntos de itens frequentes
  - Descoberta de regras de associações interessantes
- A primeira tende a ser computacionalmente mais intensa. Por este motivo recebe mais atenção dos pesquisadores.
- Nos concentraremos nessa tarefa.

##### Mineração de Conjuntos de itens frequentes

- Uma definição de "regra interessante" é ela ocorrer com certa frequência.
- Então é necessário definir um limiar entre o que é frequente e o que é infrequente
  - Esse limiar é chamado de suporte mínimo (minsup)
- O suporte de um itemset é o tamanho de sua cobertura
  - sup(X) = |c(X)|
- Como essa definição é dependente do contexto, admite-se também a definição do suporte relativo
  - rsup(X) = |c(X)| / |T|

---

Dessa forma, dizemos que um itemset é frequente sse $sup(X) \geq minsup$

---

Relação de ordem parcial: $X \subseteq Y \leftrightarrow X \leq Y$

Conjunto potência: é o conjunto de todos os possíveis subconjuntos de um conjunto.

```mermaid
flowchart TD
  null[["\null"]]
  null --> A & B & C
  A --> AB & AC
  B --> AB & BC
  C --> AC & BC
```

- O espaço de busca do problema é o conjunto potência do conjunto de itens
- Se considerarmos a relação de subconjuntos como uma relação de ordem parcial, temos que o espaço de busca é estruturado como um reticulado
  - Esse reticulado pode ser visualizado como um grafo, onde somente as relações diretas são representadas
  - Ou seja, se $A \subseteq B \land |A| = |B| - 1$, então existe uma aresta entre A e B no diagrama

Aquele diagrama explica bastante o que que isso quis dizer. Basicamente, no conjunto potência, cada nível vai ter um elemento a mais que o nível anterior.

- ...

###### Algoritmo Ingênuo

Complexidade do algoritmo: $O(2^I \cdot T \cdot I)$

- // ALGORITHM 8.1. Algoritm BruteForce
- int BruteForce(D, I, minsup):
  - F \leftarrow // set of frequent itemsets
    - for each X \subseteq I do
      - sup(X) \leftarrow ComputeSupport (X, D)
      - if sup(X) \leq minsup then
        - F \leftarrow F \cup {(X, sup(X))}
    - return F

- ComputeSupport(X, D):
  - sup(X) \leftarrow 0
  - for each (t, i(t)) \in D do
    - if X \subseteq i(t) then
      - sup(X) \leftarrow sup(X) + 1
- return sup(X)

---

...

---

- A complexidade do espaço de busca é inerente ao problema. Contudo o algoritmo é ineficiente mesmo em espaços pequenos
- Note que o conjunto de dados não é mantido em memória, portanto a computação do suporte torna o algoritmo impraticável
- Os algoritmos mais "sofisticados" atacam majoritariamente o problema de computação de suporte, evitando computações desnecessáris, e/ou adotando estratégias mais eficientes para computá-lo.

Então temos dois problemas principais: reduzir o espaço de busca e reduzir a complexidade para calcular o suporte.

##### Leitura

- Seções 8.1 e 8.2 Zaki e Meira
- Seções 6.1 e 5.2 (Introduction to Data Mining)

## Aula 03 | 25/03/2025 | Mineração de conjuntos de itens - Faltei - Mineração de itens frequentes: Apriori e Eclat

### Slide: aula03-apriori_eclat (Aula 03)

#### Introdução (Aula 03)

- Como vimos na aula anterior, o principal problema do algoritmo ingênuo para mineração de conjuntos de itens frequentes era a replicação de esforços para avaliar o suporte dos candidatos
- As múltiplas passadas no conjunto de dados (armazenado em memória secundária) torna o algoritmo impraticável até mesmo para pequenos volumes
- Os algoritmos que veremos hoje exploram propriedades do problema para amortizar o custo da computação de suporte, e evitar retrabalho na avaliação dos candidatos

---
---

O que é mesmo o suporte? 🤔

- Recapitulando da aula anterior, o Suporte aparantemente é um encurtamento para o "Suporte Mínimo" (minsup) que é o limiar que define se determinado item é frequente o bastante ou não.
  - Esse valor é dado pela seguinte fórmula:
    - $sup(X) = |c(X)|$, onde $c(X)$ é a cobertura do itemset X.

Mas o que é mesmo a cobertura?

- A cobertura é o conjunto de transações que contém um itemset X. Ou seja, é o conjunto de transações que contém todos os itens do itemset X.

#### Apriori [1]

- O Apriori foi proposto por Rakesh Agrawal e Ramakrishnan Srikant em 1994
  - O artigo possui mais de 30K citações
- Os autores à época trabalhavam no projeto da IBM para o Wal-Mart
- A ideia central é evitar computações desnecessárias para candidatos infrequentes
- Isso é viabilizado pela propriedade de **anti-monotonicidade** da função suporte
- Essa é uma das propriedades mais importantes para a área

##### Anti-monotonicidade do suporte

- Considere dois itemsets $A$ e $B$ quaisquer. Se $A \subseteq B$, então $sup(A) \geq sup(B)$.
- Essa observação nos diz que a cobertura de conjuntos de itens é, no máximo, tão grande quanto a de seus subconjuntos
  - No caso mais simples, um conjunto de dois itens não pode ocorrer em mais transações que cada um dos itens individualmente
- Consequentemente, se o itemset A é infrequente, B também será.
- Isso define a propriedade de anti-monotonicidade da função suporte, também conhecida como a propriedade do Apriori
  - **Todo superconjunto de um conjunto infrequente é infrequente**
  - **Todo subconjunto de um conjunto frequente é frequente**

---
---

Muito interessante isso daí de cima.

Basicamente entendemos que $sup(X=\{A, B\}) \geq sup(Y=\{A, B, C\})$ com isso, se X é frequente, nada garante que Y também seja. Porém, se Y é frequente, isso garante que todos os possíveis subconjuntos de Y também serão frequentes.

#### Apriori [2]

- O Apriori utiliza uma busca em largura no espaço de busca para minerar os padrões
  - Frequentemente, o termo usado na literatura é abordagem por níveis (level-wise approach)
- A busca inicia com a identificação dos itens frequentes
- Depois, os conjuntos de tamanho k são explorados antes dos de tamanho k+1
- Assim como o algoritmo ingênuo, ele também opera em duas etapas:
  - Geração de candidatos
  - Cômputo do suporte e eliminação dos infrequentes

---

- A geração dos candidatos é feita a partir dos conjuntos frequentes encontrados na fase anterior
- Conjuntos compartilhando um prefixo de k-1 itens são combinados para gerar candidatos de tamanho k+1
  - Novamente, assume-se que eles são ordenados pela ordem lexicográfica
- Candidatos que possuam algum subconjunto infrequente são descartados imediatamente
  - A propriedade do Apriori é empregada
- Os suportes dos candidatos são atualizados com uma única passada no conjunto de dados
  - Subconjuntos de tamanho k de cada transação são usados para atualizar o suporte dos candidatos

---

- **APRIORI** $(D, \mathcal{I}, minsup)$:
  - $\mathcal{F} \leftarrow \emptyset$
  - $\mathcal{C}^{(1)} \leftarrow \{\emptyset\}$ // Initial prefix tree with single items
  - **foreach** $i \in \mathcal{I}$ **do** Add $i$ as child of $\emptyset$ in $\mathcal{C}^{(1)}$ with $sup(i) \leftarrow 0$
  - $k \leftarrow 1$ // $k$ denotes the level
  - **while** $\mathcal{C}^{(k)} \neq \emptyset$ **do**
    - ComputeSupport $(\mathcal{C}^{(k)}, D)$
    - **foreach** _leaf_ $X \in \mathcal{C}^{(k)}$ **do**
      - **if** $sup(X) \geq minsup$ **then** $\mathcal{F} \leftarrow \mathcal{F} \cup \{(X, sup(X))\}$
      - **else** remove $X$ from $\mathcal{C}^{(k)}$
    - $\mathcal{C}^{(k+1)} \leftarrow$ ExtendPRefixTree($\mathcal{C}^{(k)}$)
    - $k \leftarrow k+1$
  - **return** $\mathcal{F}^{(k)}$

---

- ComputeSupport $(C^{(k)}, D)$:
  - ...

- ExtendPrefixTree $()$:
  - ...
  - **return** $C^{(k)}$

---

Exemplo (minsup=3):

$$
\begin{bmatrix}
  TID & Muesli & Oats & Milk & Yoghurt & Biscuits & Tea \\
  1 & 1 & 0 & 1 & 1 & 0 & 1 \\
  2 & 0 & 1 & 1 & 0 & 0 & 0 \\
  3 & 0 & 0 & 1 & 0 & 1 & 1 \\
  4 & 1 & 0 & 0 & 1 & 0 & 0 \\
  5 & 0 & 1 & 1 & 0 & 0 & 1 \\
  6 & 1 & 0 & 1 & 0 & 0 & 1 \\
\end{bmatrix}
\Rightarrow
\begin{bmatrix}
  TID & Muesli & Milk & Tea \\
  1 & 1 & 1 & 1 \\
  2 & 0 & 1 & 0 \\
  3 & 0 & 1 & 1 \\
  4 & 1 & 0 & 0 \\
  5 & 0 & 1 & 1 \\
  6 & 1 & 1 & 1 \\
\end{bmatrix}
$$

---

- O número de passadas é drasticamente reduzido em relação ao algoritmo ingênuo
  - $O(2^I) \rightarrow O(I)$
- As podas baseadas na anti-monotonicidade do suporte também são bastante efetivas na prática
- O algoritmo também apresenta alguns problemas:
  - Busca em largura requer que todos os candidatos de um nível sejam mantidos em memória. Esse custo é proibitivo em alguns (muitos) casos
  - Tanto a contagem do suporte quanto a poda do Apriori podem ser consideravelmente caras, dependendo da implementação

---

- O custo de memória é inerente à abordagem, e não podemos fazer muita coisa para melhorá-lo
- O custo da contagem e verificação pode ser atenuado, usando estruturas de dados mais ‘sofisticadas’
- Existem duas abordagens mais comuns:
  - Usar uma árvore hash
  - Usar uma árvore de prefixos (Trie)
- Na primeira abordagem, cada nó folha armazena um conjunto de candidatos/conjuntos frequentes
  - O número de comparações é reduzido
- Na segunda abordagem, os nós da Trie armazenam os candidatos/conjuntos frequentes. Os subconjuntos das transações são usadas para indexá-la e atualizar o suporte

---

- A redução do suporte mínimo tem um impacto muito grande no custo computacional do algoritmo
  - O tamanho dos candidatos aumenta -> Mais candidatos são avaliados em cada nível -> o tamanho dos conjuntos frequentes aumenta -> mais níveis são explorados

---

- A densidade da base de dados também tem muito impacto no custo
  - Transações passam a ter mais itens
  - Isso tem duas implicações: tamanho médio dos itemsets aumentam; mais subconjuntos são gerados durante a contagem do suporte $\binom{|t|}{k}$

## Aula 04 | 27/03/2025 | Mineração de conjuntos de itens

### Aula passada

- Algoritmo apriori
- Frequente, infrequente.
- Como calcula o suporte
  - A partir dos itens frequentes: tabelas de 0 e 1.
  - Pra isso usaca árvore de ???
  - Para cada transação gerava os itemsets de tamanho k, ia na árvore ???
  - E incrementava o suporte daquela chave

[JV: escrevi o que ele tá falando, mas não tô entendendo]

- Duas coisas influenciam o desempenho do algoritmo
  1. Ele falou algo
  2. Se o BD é denso, as transações são mais largas.
- $\binom{|t|}{k}$
- Quando é esparso, funciona bem. Quando é denso que começa a dar problema.

Eu tô achando que se eu compro $J = {A, B, C}$, Então o conjunto potência dele é $P(J) = {\emptyset, A, B, C, AB, AC, BC, ABC}$, e então, incrementaria 1 para um desses grupos

- Cálculo de suporte:
  - Para cada um dos itemsets tem que verificar se ele tá na árvore K(?)

- Se os itemsets estão em memória...
- Se quero gerar o itemset XY partindo de $X \cup Y$, posso dizer que o suporte será $|c(X) \cap c(Y)|$

### Slide: aula03-apriori_eclat (Aula 04)

#### Eclat (Equivalence Class Transformation)

Dada a representação vertical dos dados, consigo calcular o suporte por essa intercessão.

- Dadas as deficiências do Apriori, M. Zaki propôs, em 2000, o algoritmo Equivalence Class Transformation (Eclat)
- A proposta do algoritmo é ‘eliminar’ a necessidade de passadas no conjunto de dados para computar o suporte
- Para isso, ele parte de uma representação vertical dos dados, e se baseia no fato de que a cobertura da união de dois itemsets é a interseção de suas coberturas

Problema: como mantenho todos os itemsets gerados em memória?

---

- Ou seja, a ideia central do algoritmo tentar manter os tidsets em memória principal para computar o suporte dos itemsets através de interseções desses conjuntos
- Contudo, todos os tidsets podem não caber na memória principal. Assim, é necessário algum mecanismo que possibilite a divisão do espaço de busca em subproblemas independentes que caibam na memória
- A divisão é feita conforme uma relação de equivalência estabelecida sobre os candidatos

Tenta manter tudo na memória principal

A ideia é partir o problema em subproblemas e trazer esses subproblemas pra memória.

Surgiu através da criação de uma relação de equivalência entre os itemsets

---

Cria-se uma relação de equivalência pelos prefixos.

Diz-se que dois itemsets são equivalentes se o prefixos dos dois são iguais.

Consideremos que temos o seguinte conjunto potência: $P(I) = {\emptyset, A, B, C, AB, AC, BC, ABC}$. Na forma de representação, seria como se agrupássemos os dados em grupos de prefixos:

- A: {A, AB, AC, ABC}
- B: {B, BC}
- C: {C}

E então seriam varridos de C para A.

Poderia-se também fazer subgrupos de subgrupos, dependendo do tamanho do conjunto de prefixos.

---

Ele faz uma busca em profundidade (DFS)

Ele faz subpartições até que o número de transações seja pequeno o suficiente para caber na memória.

---

- Algoritmo 8.3 - Algoritmo ECLAT
- // Initial Call: $F \leftarrow 0, P \leftarrow {}$
- ECLAT (P, minsup, F):
- foreach
  - F
  - P0
  - foreach
    - X
    - ?
    - if sup()
      - po
  - if p neq 0 then ...

[JV: Droga, foquei em transcrever brevemente e esqueci de prestar atenção na explicação do professor]

P guarda todos os frequentes da chamada anterior. porque ele filtro toudos que são infrequentes pelo minsup

para cada um dos frequentes dos candidatos, armazena no ocnjunto de itens frequentes globais

e a partir dele gera em profundidade a combinação dele com todos os outros que vêm pra frente.

Evitam redundância: 1. partições; 2. Ordem sistemática de combinação dos itens.

1. A B C
2. A com B e C: AB AC
3. AB com AC: ABC
4. B com C: BC

##### Representações de conjuntos de dados - Aula 4

Pelo que eu tô entendendo:

1. Começa pegando todos os itens que tenham uma quantidade de transações maior que o minsup (o valor mínimo aceitável para que consideremos relevante)
2. Depois disso, começamos fazendo a intercessão das transações entre o primeiro conjunto de itens que passou pela comparação com o segundo conjunto.
3. Depois disso, vê se o resultado dessas intercessões é grande o bastante.

Se $A \subseteq B$, então $c(B) \subseteq c(A)$ (Cobertura)

---

##### Diffsets e dEclat

Em bases de dados densos, varia bem pouco o suporte entre os itens. Então, faria mais sentido guardar só a diferença ao invés de guardar o todo.

Ao invés de chamar de tidset, passaram a chamar de diffset.

...

Pode-se armazenar em vetores de bits ao invés de vetores de inteiros.

Usando o vetor de bits, é como se fosse:

A = [00110, 01001, 01100, 00011]

E para calcular o suporte (?) cobetura(?)

basta fazer um cálculo rápido de 0 a 255 para dizer quantos bits estão ativos, e então fazer a contagem de bits ativos somando esses valores.

0 -> 1
1 -> 1
2 -> 1
...
255 -> ...

Outra forma de condensar é: Se sei que um determinado conjunto é grande o bastante, posso inferir que todos os que são menores que eles também são grandes o bastante.

Se só é guardado o valor das diferenças, acaba sendo um problema fazer as intercessões.

---

- $C(PX) - C(PY)$
- $C(PX) - C(PY) \cup C(P) - C(P)$
- $C(PX) \cap \overline{C(PY)} \cup C(P) \cap \overline{C(P)}$
- $C(PX) \cup \overline{C(P)} \cap C(P) \cup \overline{C(P)}$

## Aula 05 | 01/04/2025 | Mineração de conjuntos de itens

### Slide: aula03-apriori_eclat (Aula 05)

#### Diffsets e dEclat [Aula 05]

- Percebendo o problema de se manter os tidsets em memória, Zaki e Gouda propuseram em 2001 (o artigo só foi publicado em 2003) uma solução alternativa
- Eles propuseram armazenar as diferenças entre os tidsets dos membros de uma classe e dos prefixos que a definem
- Eles chamaram esse conjunto de **diffset**
- Formalmente, para um prefixo $P$ e um itemset $PX$, o diffset de $X$, $d(PX) = c(P) - c(PX)$
- Seriam armazenados, portanto, o suporte do itemset e seu diffset

---

- O fato é que, se somente os diffsets são armazenados, o suporte não é mais obtido como a cardinalidade desse conjunto
- Dessa forma, como calcular o suporte de um itemset $PXY$ obtido a partir de outros dois $PX$ e $PY$, usando somente seus diffsets?
- O suporte de $PX$ é calculado pela diferença entre o suporte de $P$ e o diffset de $PX$, $sup(PX) = sup(PX) - |d(PXY)|$
  - Portanto, $sup(PXY) = sup(PX) - |d(PXY)|$
- A solução passa por computar o diffset de $PXY$. Porém, temos somente os diffsets de $PX$ e $PY$

---

- Por definição, 𝑑 𝑃𝑋𝑌 = 𝑐 𝑃𝑋 − 𝑐 𝑃𝑋𝑌 = 𝑐 𝑃𝑋 − 𝑐 𝑃𝑌
- Podemos adicionar, ao conjunto acima, o conjunto vazio (𝑐 𝑃 − 𝑐 𝑃 ) sem alterá-lo
- Logo, 𝑑 𝑃𝑋𝑌 = 𝑐 𝑃𝑋 − 𝑐 𝑃𝑌 + 𝑐 𝑃 − 𝑐 𝑃 = 3 4 𝑐 𝑃 − 𝑐 𝑃𝑌 − 𝑐 𝑃 − 𝑐 𝑃𝑋 = 𝑑 𝑃𝑌 − 𝑑(𝑃𝑋)
- Em outras palavras, podemos usar os diffsets dos conjuntos base para calcular o diffset do novo candidato
- A variante do Eclat que usa diffsets ficou conhecida como dEclat

---
---

- $d(PXY) = c(PX) - c(PY) = c(PX) - c(PXY)$
- $c(PXY) = c(PX) \cap c(PY)$

"Diferença é a mesma coisa que interseção com complemento"

- $d(PXY) = ...$

Ele fez um monte de igualdades com operações de conjuntos.

- $d(PXY) =$
- $c(PX) - c(PY) =$
- $c(PX) - c(PXY) =$
- $[c(PX) - c(PXY)] \cup [c(P) - c(P)] =$
- $[c(PX) \cap \overline{c(PXY)}] \cup [c(P) \cap \overline{c(P)}]$
- $[c(PX) \cup c(P)] \cap [\overline{c(PY)} \cup \overline{c(P)}] \cap \overline{d(PX)}$
- $(c(PX) \cap \overline{c(PY)}) \cup (c(P) \cap \overline{c(P)}) \cup (c(P) \cap \overline{c(PY)}) \cup (c(P) \cap \overline{c(P)} \cap \overline{d(PX)})$
- $(Q \subseteq d(PY)) \cup (\emptyset) \cup (d(PY)) \cup (\emptyset) \cap (\overline{d(PX)})$
- $d(PY) \cap \overline{d(PX)} =$
- $d(PY) - d(PX)$

---

- $d(PX) = ...$

---

- $P = \{1, 2, 3, 4, 5\}$
- $X = \{1, 3, 5\}$
- $Y = \{2, 3, 4\}$
- $PX = \{1, 3, 5\}$
- $PY = \{2, 3, 4\}$
- $\overline{PY} = \{1, 5\}$
- $PX \cap \overline{PY} = \{1, 5\}$

---

- ALGORITHM 8.4. Algorithm dEclat
  - ...

---

- Essa abordagem se mostrou muito eficiente para conjuntos densos
- Porém, em conjuntos esparsos, o algoritmo original é a melhor opção

Para bases esparsas: eClat; para bases densas: dEclat

#### Leitura (Aula 05)

- Seções 8.1, 8.2 (Zaki e Meira)
- Seções 6.1, 6.2 (Introduction to Data Mining)
- Mohammed Javeed Zaki: Scalable Algorithms for Association Mining. IEEE Trans. Knowl. Data Eng. 12(3): 372-390 (2000)
- Zaki, M.J., Gouda, K.: Fast vertical mining using diffsets. Technical Report 01-1, Computer Science Dept., Rensselaer Polytechnic Institute (March 2001) 10
- Christian Borgelt. Efficient Implementations of Apriori and Eclat. Workshop of Frequent Item Set Mining Implementations (FIMI 2003, Melbourne, FL, USA).

Boa parte da explicação estão nos artigos. A implementação tá no Borgelt.

### Slide: aula04-FPGrowth (Aula 05)

#### Recapitulando

- Apriori: reduzir o número de passsadas em disco
- Eclat: trazer pra memória e assim reduzir o número de passadas em disco, tendendo a zero.

#### Introdução (Aula 05)

- Nessa aula, veremos outro algoritmo que usa projeções para reduzir o número de passadas para computação dos conjuntos de itens frequentes
- O algoritmo FP-Growth (Frequent Pattern Growth) adota uma estratégia dividir-e-conquistar para reduzir o custo computacional
- Ele, ao contrário do Apriori, não se baseia na geração de candidatos
- Os padrões são construídos ao longo do processamento em profundidade
- Esse algoritmo é, talvez, o algoritmo sequencial mais eficiente para busca de conjuntos de itens frequentes

A ideia é evitar ter que computar os candidatos.

#### FP-Growth

- O FP-Growth foi proposto em 2000 por Jiawei Han, Jian Pei e Yiwen Yin
- O algoritmo atacou dois problemas presentes nas abordagens iniciais:
  1. Repetidas passadas sobre a base de dados; e
  2. Geração de candidatos [Mais crítico]
- O primeiro problema, como já discutimos, é crítico pelo custo computacional inerente à leitura em memória secundária
- O segundo problema está relacionado à geração de candidatos desnecessários
  - Muitos são descartados pela propriedade do Apriori

##### FP-Tree [Árvore de Prefixos]

- O FP-Growth possui algumas similaridades ao Eclat:
  - Ambos adotam a estratégia de busca em profundidade
  - Ambos adotam projeções dos dados com o intuito de trazê-los para memória principal e reduzir o custo computacional
- O FP-Growth, no entanto, usa uma estrutura de dados diferente para suportar a busca pelos padrões
  - Uma árvore de prefixos chamada FP-Tree
- A busca pelos padrões se dá inteiramente através da árvore sem a necessidade de se voltar à base de dados
- Dessa forma, a primeira tarefa do algoritmo é construir essa estrutura

"A partir da Base de Dados, como fazer a árvore de prefixos?"

---

- A construção da FP-Tree ocorre em duas fases
- Primeiro, o algoritmo varre a base de dados para computar a frequência individual de cada item
  - Itens infrequentes são descartados, uma vez que não podem formar padrões frequentes
- Segundo, o algoritmo percorre novamente a base processando as transações ordenadas pela frequência dos itens
  - Os itens nas transações são ordenados em ordem decrescente de frequência e os infrequentes são filtrados
- As transações são então inseridas na árvore enquanto processadas
  - Itens são nós da árvore
  - Cada nó armazena um item e sua frequência (número de transações que o contém)

Basicamente, ele limpa os infrequentes, e depois disso, vai inserindo as transações em uma árvore.

---

- Para facilitar a busca pelos padrões, a árvore é equipada com uma estrutura adicional para localizar a ocorrência dos itens e sua frequência
- Exemplo

$$
\begin{bmatrix}
  TID & Muesli (a) & Oats (b) & Milk (c) & Yoghurt (d) & Biscuits (e) & Tea (f) \\
  1 & 1 & 0 & 1 & 1 & 0 & 1\\
  2 & 0 & 1 & 1 & 0 & 0 & 0\\
  3 & 0 & 0 & 1 & 0 & 1 & 1\\
  4 & 1 & 0 & 0 & 1 & 0 & 0\\
  5 & 0 & 1 & 1 & 0 & 0 & 1\\
  6 & 1 & 0 & 1 & 0 & 0 & 1\\
\end{bmatrix}
$$

minsup = 2

Em ordem de maior suporte pra menor suporte: cfabd

1. cfad
2. cb
3. cf
4. ad
5. cfb
6. cfa

Obs.: Ignoram-se os itens infrequentes.

#### Mineração dos padrões [Aula 05]

- A mineração dos padrões se inicia uma vez que a FP-Tree tenha sido construída
- A construção agora ocorre aumentando-se prefixos dos padrões em ordem crescente de suporte
- As transações que satisfaçam (contém) o padrão sendo construído são projetadas em uma nova árvore
- Itens podem se tornar infrequentes nessa nova base e são descartados
- Os padrões encontrados nessa nova árvore devem incluir o prefixo que a gerou
- O algoritmo segue com as extensões recursivamente até que um único ramo seja obtido
  - Se a árvore possui um único ramo, os padrões obteníveis são todas as combinações dos nós

Para se minerar as transações de volta, percorremos a lista de itens e então subimos dele até a raiz.

Partindo do item menos frequente e indo pro item mais frequente, fazemos projeções da árvore.

Essas projeções são sub-árvores da árvore original.

No caso do d, percorrerei todos os nós da lista encadeada de de d's, indo dele até a raiz. A junção de todos os nós que eu passar, formará uma nova árvore. E essa será a projeção do item d.

Mas ainda não entendi o que precisa ser feito após essa primeira projeção.

---

- Exemplo

$$
\begin{bmatrix}
  Item & Freq & Link
  c & 5 & \\
  f & 4 & \\
  a & 3 & \\
  b & 2 & \\
  d & 2 & \\
\end{bmatrix}
$$

```mermaid
flowchart LR
  Vazio(("`$\emptyset$`")) --> C((c:5))
  C --> F((f:4))
  F --> A2((a:2))
  A2 --> D1((d:1))
  F --> B1((b:1))
  C --> B2((b:1))
  Vazio --> A1((a:1))
  A1 --> D2((d:1))
```

Há também uma lista encadeada para todos os nós com ocorrências de um mesmo item.

A lista encadeada serve para podermos percorrer todos os nós de um mesmo item e calcularmos sua frequência.

...

#### Questões de implementação

- E se a FP-tree não couber na memória?
  - A solução é particionar/projetar a base de dados em memória secundária antes de iniciar a construção da árvore
- Como construir a FP-tree de forma eficiente?
  - Solução proposta por Christian Borgelt otimiza memória e tempo
  - Representação básica dos dados: lista de vetores de inteiros
  - Dados (projeções) são carregados inteiramente para memória
  - Lista é seccionada com base no k-ésimo item; um nó é criado para cada seção
  - Nós têm tamanho fixo (20 bytes em 32bits; 40 em 64bits)
    - 1x identificador de item
    - 1x contador de frequência
    - 1x ponteiro para nó pai
    - 1x ponteiro para próxima ocorrência do item
    - 1x ponteiro para nó auxiliar

---

- Implementação tradicional, conforme descrição do algoritmo, evita carregar dados para memória
  - Porém, nós terão tamanho variável ou desperdiçam memória (ponteiros para filhos que nunca ocorrem)
  - Melhora gerenciamento de memória; grandes blocos podem ser alocados de uma vez e gerenciados internamente
  - Além disso, ponteiros para pais são mais úteis que ponteiros para filhos durante execução

---

- Projeções são executadas com dois laços
  - Um laço externo percorre o nível mais baixo (elemento condicionante da projeção)
  - Laço interno percorre a os ramos originários do nó folha
- A nova árvore é construída como uma ‘sombra’ da original
  - Nós são duplicados conforme são visitados (ponteiro auxiliar mantém elo de ligação entre original e cópia para atualizações necessárias durante construção)
  - Frequência do nó folha é propagada para cima
- A sombra é destacada da árvore original em uma segunda passada pelos nós
- Nós infrequentes podem ser removidos e nós com mesmo rótulo mesclados

---

...

---

#### Leitura [Aula 05]

- Seção 6.6 Intro to Data Mining
- Seção 8.2.3 Zaki e Meira
- [Borgelt, C. (2005) An Implementation of the FP-growth Algorithm][LinkFPGrowth]

[LinkFPGrowth]: <https://borgelt.net/papers/fpgrowth.pdf>

## Aula 06 | 03/04/2025 | Mineração de conjuntos de itens

## Aula 07 | 08/04/2025 | Mineração de sequências

### Aula 08 | 10/04/2025 | Mineração de sequências

### Aula 09 | 15/04/2025 | Mineração de grafos

### Aula 10 | 17/04/2025 | Mineração de grafos

### Aula 11 | 22/04/2025 | Regras de associação e métricas de qualidade

### Aula 12 | 24/04/2025 | Aprendizado descritivo supervisionado: padrões emergentes, contrastantes e descoberta de subgrupos

### Aula 13 | 29/04/2025 | Descoberta de subgrupos

### Aula 14 | 06/05/2025 | Descoberta de subgrupos

### Aula 15 | 08/05/2025 | Descoberta de subgrupos

### Aula 16 | 13/05/2025 | Mineração de modelos excepcionais

### Aula 17 | 15/05/2025 | Mineração de modelos excepcionais

### Aula 18 | 20/05/2025 | Mineração de modelos excepcionais

### Aula 19 | 22/05/2025 | Seminários (Padrões Frequentes)

### Aula 20 | 27/05/2025 | Seminários (Padrões Frequentes)

### Aula 21 | 29/05/2025 | Seminários (Padrões Frequentes)

### Aula 22 | 03/06/2025 | Seminários (SD)

### Aula 23 | 05/06/2025 | Seminários (SD)

### Aula 24 | 10/06/2025 | Seminários (SD)

### Aula 25 | 12/06/2025 | Seminários (aplicações)

### Aula 26 | 17/06/2025 | Seminários (aplicações)

### Aula 27 | 24/06/2025 | Seminários (aplicações)

### Aula 28 | 26/06/2025 | Projeto

### Aula 29 | 01/07/2025 | Projeto

### Aula 30 | 03/07/2025 | Projeto
