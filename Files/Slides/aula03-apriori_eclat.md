# Slide: aula03-apriori_eclat (Aula 3, 4) - Mineração de itens frequentes: Apriori e Eclat

## Aula 03 | 25/03/2025 | Mineração de conjuntos de itens - Faltei - Mineração de itens frequentes: Apriori e Eclat

### Introdução (Aula 03)

- Como vimos na aula anterior, o principal problema do algoritmo ingênuo para mineração de conjuntos de itens frequentes era a replicação de esforços para avaliar o suporte dos candidatos
- As múltiplas passadas no conjunto de dados (armazenado em memória secundária) torna o algoritmo impraticável até mesmo para pequenos volumes
- Os algoritmos que veremos hoje exploram propriedades do problema para amortizar o custo da computação de suporte, e evitar retrabalho na avaliação dos candidatos

- [JV]
  - O que é mesmo o suporte? 🤔
  - Recapitulando da aula anterior, o Suporte é a quantidade de vezes que determinado item aparece no conjunto de dados; já o "Suporte Mínimo" ($minsup$) é o limiar que define se determinado item é frequente o bastante ou não.
  - Esse valor é dado pela seguinte fórmula:
    - $sup(X) = |c(X)|$, onde $c(X)$ é a cobertura do itemset $X$.
  - Mas o que é mesmo a cobertura?
    - A cobertura é o conjunto de transações que contém um itemset $X$. Ou seja, é o conjunto de transações que contém todos os itens do itemset $X$.

### Apriori

- O Apriori foi proposto por Rakesh Agrawal e Ramakrishnan Srikant em 1994
  - O artigo possui mais de 30K citações
- Os autores à época trabalhavam no projeto da IBM para o Wal-Mart
- A ideia central é evitar computações desnecessárias para candidatos infrequentes
- Isso é viabilizado pela propriedade de **anti-monotonicidade** da função suporte
- Essa é uma das propriedades mais importantes para a área

- Autores: Rakesh Agrawal (Data Insights Labs) e Ramakrishnan Srikant (Google Fellow) (1994)

#### Anti-monotonicidade do suporte

- Considere dois itemsets $A$ e $B$ quaisquer. Se $A \subseteq B$, então $sup(A) \geq sup(B)$.
- Essa observação nos diz que a cobertura de conjuntos de itens é, no máximo, tão grande quanto a de seus subconjuntos
  - No caso mais simples, um conjunto de dois itens não pode ocorrer em mais transações que cada um dos itens individualmente
- Consequentemente, se o itemset A é infrequente, B também será.
- Isso define a propriedade de anti-monotonicidade da função suporte, também conhecida como a propriedade do Apriori

  - **Todo superconjunto de um conjunto infrequente é infrequente**
  - **Todo subconjunto de um conjunto frequente é frequente**

- [JV]
  - Muito interessante isso daí de cima.
  - Basicamente entendemos que $sup(X=\lbrace A, B \rbrace) \geq sup(Y=\lbrace A, B, C \rbrace)$ com isso, se X é frequente, nada garante que Y também seja. Porém, se Y é frequente, isso garante que todos os possíveis subconjuntos de Y também serão frequentes.

### Apriori [2]

- O Apriori utiliza uma busca em largura no espaço de busca para minerar os padrões
  - Frequentemente, o termo usado na literatura é abordagem por níveis (level-wise approach)
- A busca inicia com a identificação dos itens frequentes
- Depois, os conjuntos de tamanho $k$ são explorados antes dos de tamanho $k+1$
- Assim como o algoritmo ingênuo, ele também opera em duas etapas:
  - Geração de candidatos
  - Cômputo do suporte e eliminação dos infrequentes

---

- A geração dos candidatos é feita a partir dos conjuntos frequentes encontrados na fase anterior
- Conjuntos compartilhando um prefixo de $k-1$ itens são combinados para gerar candidatos de tamanho $k+1$
  - Novamente, assume-se que eles são ordenados pela ordem lexicográfica
- Candidatos que possuam algum subconjunto infrequente são descartados imediatamente
  - A propriedade do Apriori é empregada
- Os suportes dos candidatos são atualizados com uma única passada no conjunto de dados
  - Subconjuntos de tamanho $k$ de cada transação são usados para atualizar o suporte dos candidatos

---

- **APRIORI** $(D, \mathcal{I}, minsup)$:
  - $\mathcal{F} \gets \emptyset$
  - $\mathcal{C}^{(1)} \gets \lbrace \emptyset \rbrace$ `// Initial prefix tree with single items`
  - **foreach** $i \in \mathcal{I}$ **do** Add $i$ as child of $\emptyset$ in $\mathcal{C}^{(1)}$ with $sup(i) \gets 0$
  - $k \gets 1$ `// k denotes the level`
  - **while** $\mathcal{C}^{(k)} \neq \emptyset$ **do**
    - **ComputeSupport** $(\mathcal{C}^{(k)}, D)$
    - **foreach** _leaf_ $X \in \mathcal{C}^{(k)}$ **do**
      - **if** $sup(X) \geq minsup$ **then** $\mathcal{F} \gets \mathcal{F} \cup \lbrace (X, sup(X)) \rbrace$
      - **else** remove $X$ from $\mathcal{C}^{(k)}$
    - $\mathcal{C}^{(k+1)} \gets$ ExtendPrefixTree($\mathcal{C}^{(k)}$)
    - $k \gets k+1$
  - **return** $\mathcal{F}^{(k)}$

---

- **ComputeSupport** $(\mathcal{C}^{(k)}, D)$:

  - **foreach** $\langle t, i(t) \rangle \in D$ **do**
    - **foreach** k-subset $X \subseteq i(t)$ **do**
      - **if** $X \in \mathcal{C}^{(k)}$ **then** $sup(X) \gets sup(X) + 1$

- **ExtendPrefixTree** $(\mathcal{C}^{(k)})$:
  - **foreach** leaf $X_a \in \mathcal{C}^{(k)}$ **do**
    - **foreach** leaf $X_b \in SIBLING(X_a)$, such that $b > a$ **do**
      - $X_{ab} \gets X_a \cup X_b$ `// prune candidate if there are any infrequent subsets`
      - **if** $X_j \in \mathcal{C}^{(k)}$, **for all** $X_j \subset X_{ab}$, such that $|X_j| = |X_{ab}|-1$ **then**
        - Add $X_{ab}$ as child of $X_a$ with $sup(X_{ab}) \gets 0$
    - **if** _no extensions from_ $X_a$ **then**
      - Remove $X_a$, and all ancestors of $X_a with no extensions, from $\mathcal{C}^{(k)}$
  - **return** $\mathcal{C}^{(k)}$

---

- Exemplo $(minsup=3)$:

$$
\begin{bmatrix}
  TID & Muesli & Oats & Milk & Yoghurt & Biscuits & Tea \\
  1   &      1 &    0 &    1 &       1 &        0 &   1 \\
  2   &      0 &    1 &    1 &       0 &        0 &   0 \\
  3   &      0 &    0 &    1 &       0 &        1 &   1 \\
  4   &      1 &    0 &    0 &       1 &        0 &   0 \\
  5   &      0 &    1 &    1 &       0 &        0 &   1 \\
  6   &      1 &    0 &    1 &       0 &        0 &   1 \\
\end{bmatrix}
\Rightarrow
\begin{bmatrix}
  TID & Muesli & Milk & Tea \\
    1 &      1 &    1 &   1 \\
    2 &      0 &    1 &   0 \\
    3 &      0 &    1 &   1 \\
    4 &      1 &    0 &   0 \\
    5 &      0 &    1 &   1 \\
    6 &      1 &    1 &   1 \\
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
- O custo da contagem e verificação pode ser atenuado, usando estruturas de dados mais 'sofisticadas'
- Existem duas abordagens mais comuns:
  - Usar uma árvore hash
  - Usar uma árvore de prefixos (Trie)
- Na primeira abordagem, cada nó folha armazena um conjunto de candidatos/conjuntos frequentes
  - O número de comparações é reduzido
- Na segunda abordagem, os nós da Trie armazenam os candidatos/conjuntos frequentes. Os subconjuntos das transações são usadas para indexá-la e atualizar o suporte

---

- A redução do suporte mínimo tem um impacto muito grande no custo computacional do algoritmo
  - O tamanho dos candidatos aumenta $\to$ Mais candidatos são avaliados em cada nível $\to$ o tamanho dos conjuntos frequentes aumenta $\to$ mais níveis são explorados

[Imagem(a): Number of candidate itemsets]

[Imagem(b): Number of frequent itemsets]

---

- A densidade da base de dados também tem muito impacto no custo
  - Transações passam a ter mais itens
  - Isso tem duas implicações: tamanho médio dos itemsets aumentam; mais subconjuntos são gerados durante a contagem do suporte $\binom{|t|}{k}$

[Imagem(a): Number of candidate itemsets]

[Imagem(b): Number of frequent itemsets]

### Eclat - Próxima aula

## Aula 04 | 27/03/2025 | Mineração de conjuntos de itens

### Aula passada

- Algoritmo Apriori
- Frequente, infrequente.
- Como calcula o suporte

  - A partir dos itens frequentes: tabelas de 0 e 1.
  - Pra isso usava árvore de prefixos
  - Para cada transação gerava os itemsets de tamanho k, ia na árvore de prefixos
  - E incrementava o suporte daquela chave

- [JV: escrevi o que ele tá falando, mas não tô entendendo]
  - Duas coisas influenciam o desempenho do algoritmo
    1. Ele falou algo
    2. Se o BD é denso, as transações são mais largas.
       - $\binom{|t|}{k}$
       - Quando é esparso, funciona bem. Quando é denso que começa a dar problema.
  - Eu tô achando que se eu compro $J = \lbrace A, B, C \rbrace$, Então o conjunto potência dele é $P(J) = \lbrace \emptyset, A, B, C, AB, AC, BC, ABC \rbrace$, e então, incrementaria 1 para um desses grupos
  - Cálculo de suporte:
    - Para cada um dos itemsets tem que verificar se ele tá na árvore K(?)
  - Se os itemsets estão em memória...
  - Se quero gerar o itemset $XY$ partindo de $X \cup Y$, posso dizer que o suporte será $|c(X) \cap c(Y)|$

### Eclat (Equivalence Class Transformation)

- Dadas as deficiências do Apriori, M. Zaki propôs, em 2000, o algoritmo Equivalence Class Transformation (Eclat)
- A proposta do algoritmo é 'eliminar' a necessidade de passadas no conjunto de dados para computar o suporte
- Para isso, ele parte de uma representação vertical dos dados, e se baseia no fato de que a cobertura da união de dois itemsets é a interseção de suas coberturas

- [JV]
  - Dada a representação vertical dos dados, consigo calcular o suporte por essa intercessão.
  - Problema: como mantenho todos os itemsets gerados em memória?

---

- Ou seja, a ideia central do algoritmo tentar manter os tidsets em memória principal para computar o suporte dos itemsets através de interseções desses conjuntos
- Contudo, todos os tidsets podem não caber na memória principal. Assim, é necessário algum mecanismo que possibilite a divisão do espaço de busca em subproblemas independentes que caibam na memória
- A divisão é feita conforme uma relação de equivalência estabelecida sobre os candidatos

- [JV]
  - Tenta manter tudo na memória principal
  - A ideia é partir o problema em subproblemas e trazer esses subproblemas pra memória.
  - Surgiu através da criação de uma relação de equivalência entre os itemsets

---

- Seja $p: P(I) \times \mathbb{N} \rightarrow P(I)$ uma função prefixo. $p(X, k) = X[1:k]$.
- A relação $\theta_k \subseteq P(I) \times P(I), A \theta_k B \equiv p(A, k) = p(B, k)$, é uma relação de equivalência
- Dessa forma, ela induz uma partição dos conjuntos de itens em classes de equivalência, onde todos os elementos compartilham um certo prefixo
- Por exemplo, todos os conjuntos que contêm o item Muesli pertencem à classe de equivalência $[Muesli]_{\theta_1}$
- Intuitivamente, essas classes servem como projeções do conjunto de dados, em que somente as transações contendo aquele prefixo são consideradas

- [JV]
  - Cria-se uma relação de equivalência pelos prefixos.
  - Diz-se que dois itemsets são equivalentes se o prefixos dos dois são iguais.
  - Consideremos que temos o seguinte conjunto potência: $\mathcal{P}(I) = \lbrace \emptyset, A, B, C, AB, AC, BC, ABC \rbrace$. Na forma de representação, seria como se agrupássemos os dados em grupos de prefixos:
    - $\emptyset: \lbrace \emptyset, A, B, C, AB, AC, BC, ABC \rbrace$
    - $A: \lbrace A, AB, AC, ABC \rbrace$
    - $B: \lbrace B, BC \rbrace$
    - $C: \lbrace C \rbrace$
  - E então seriam varridos de C para A (ou o $\emptyset$).
  - Poderia-se também fazer subgrupos de subgrupos, dependendo do tamanho do conjunto de prefixos.

---

- Durante a busca em profundidade, o algoritmo particiona os conjuntos de itens conforme a relação de equivalência e o nível da árvore
- O particionamento pode ser encerrado tão logo os tidsets caibam na memória e as interseções possam ser computadas facilmente
- Contudo, a estratégia pode ser usada durante toda a execução do algoritmo
- O cálculo do suporte no algoritmo se restringe a calcular o tamanho do tidset

- [JV]
  - Ele faz uma busca em profundidade (DFS)
  - Ele faz subpartições até que o número de transações seja pequeno o suficiente para caber na memória.

---

- **ALGORITHM 8.3. Algorithm ECLAT**
- // Initial Call: $\mathcal{F} \gets \emptyset, P \gets \lbrace  \langle i, t(i) \rangle | i \in \mathcal{I}, |t(i)| \geq minsup  \rbrace$
- **ECLAT** $(P, minsup, \mathcal{F})$:
  - **foreach** $\langle X_a, t(X_a) \rangle \in P$ **do**
    - $\mathcal{F} \gets \mathcal{F} \cup \lbrace (X_a, sup(X_a)) \rbrace$
    - $P_a \gets \emptyset$
    - **foreach** $\langle X_b, t(X_b) \rangle \in P$, with $X_b > X_a$ **do**
      - $X_{ab} = X_a \cup X_b$
      - $t(X_{ab}) = t(X_a) \cap t(X_b)$
      - **if** $sup(X_{ab}) \geq minsup$ **then**
        - $P_a \gets P_a \cup \lbrace  \langle X_{ab}, t(X_{ab}) \rangle  \rbrace$
    - **if** $P_a \neq \emptyset$ **then** ECLAT $(P_a, minsup, \mathcal{F})$

[JV: Droga, foquei em transcrever brevemente e esqueci de prestar atenção na explicação do professor]

- [JV]
  - P guarda todos os frequentes da chamada anterior. porque ele filtrou todos que são infrequentes pelo minsup
  - para cada um dos frequentes dos candidatos, armazena no conjunto de itens frequentes globais
  - e a partir dele gera em profundidade a combinação dele com todos os outros que vêm pra frente.
  - Evitam redundância: 1. partições; 2. Ordem sistemática de combinação dos itens.
    1. A B C
    2. A com B e C: AB AC
    3. AB com AC: ABC
    4. B com C: BC

#### Representações de conjuntos de dados (Aula 4)

$$
\begin{bmatrix}
  TID & Muesli & Oats & Milk & Yoghurt & Biscuits & Tea \\
  1 & 1 & 0 & 1 & 1 & 0 & 1\\
  2 & 0 & 1 & 1 & 0 & 0 & 0\\
  3 & 0 & 0 & 1 & 0 & 1 & 1\\
  4 & 1 & 0 & 0 & 1 & 0 & 0\\
  5 & 0 & 1 & 1 & 0 & 0 & 1\\
  6 & 1 & 0 & 1 & 0 & 0 & 1\\
\end{bmatrix}
\Rightarrow
[\emptyset]_{\theta_0}
\begin{bmatrix}
  X      & c(x)  \\
  Muesli & 146   \\
  Milk   & 12356 \\
  Tea    & 1356  \\
\end{bmatrix}
$$

- [JV]
  - Pelo que eu tô entendendo:
    1. Começa pegando todos os itens que tenham uma quantidade de transações maior que o minsup (o valor mínimo aceitável para que consideremos relevante)
    2. Depois disso, começamos fazendo a intercessão das transações entre o primeiro conjunto de itens que passou pela comparação com o segundo conjunto.
    3. Depois disso, vê se o resultado dessas intercessões é grande o bastante.
  - Se $A \subseteq B$, então $c(B) \subseteq c(A)$ (Cobertura)

### Eclat (Equivalence Class Transformation) [2]

- O custo computacional do algoritmo está diretamente relacionado ao tamanho dos tidsets
  - O tempo de execução depende do cálculo da interseção dos tidsets
- O custo de espaço também é dependente do tamanho. Quanto mais denso o conjunto de dados, mais largos serão os tidsets
- Há duas formas de se implementar o algoritmo:
  - Usando vetores de bits
  - Usando vetores de Ids
- Os vetores de bits são interessantes para o cálculo do suporte
  - Eles facilitam a computação da interseção e o cálculo do tamanho do tidset pode ser feito usando uma tabela auxiliar (palavras de 16bits mapeadas para valores)
- Contudo, se o conjunto for esparso, isso representará um desperdício muito grande de espaço. Então vetores de Ids se tornam mais interessantes.
  - As computações de interseção são feitas como na função merge do mergesort

#### Diffsets e dEclat [Próxima aula]

- Percebendo o problema de se manter os tidsets em memória, Zaki e Gouda propuseram em 2001 (o artigo só foi publicado em 2003) uma solução alternativa
- Eles propuseram armazenar as diferenças entre os tidsets dos membros de uma classe e dos prefixos que a definem
- Eles chamaram esse conjunto de **diffset**
- Formalmente, para um prefixo P e um itemset PX, o diffset de X, $d(PX) = c(P) - c(PX)$
- Seriam armazenados, portanto, o suporte do itemset e seu diffset

- [JV]
  - Em bases de dados densos, varia bem pouco o suporte entre os itens. Então, faria mais sentido guardar só a diferença ao invés de guardar o todo.
  - Ao invés de chamar de tidset, passaram a chamar de diffset.
  - ...
  - Pode-se armazenar em vetores de bits ao invés de vetores de inteiros.
  - Usando o vetor de bits, é como se fosse:
    - $A = [00110, 01001, 01100, 00011]$
  - E para calcular o suporte (?) cobertura(?)
  - basta fazer um cálculo rápido de 0 a 255 para dizer quantos bits estão ativos, e então fazer a contagem de bits ativos somando esses valores.
    - $0 \to 1$
    - $1 \to 1$
    - $2 \to 1$
    - ...
    - $255 \to ...$
  - Outra forma de condensar é: Se sei que um determinado conjunto é grande o bastante, posso inferir que todos os que são menores que eles também são grandes o bastante.
  - Se só é guardado o valor das diferenças, acaba sendo um problema fazer as intercessões.

---

- [JV]

  - Por definição, $d(PXY) = c(PX) - c(PXY) = c(PX) - c(PY)$
  - Podemos adicionar, ao conjunto acima, o conjunto vazio $(c(P) - c(P))$ sem alterá-lo
  - Logo, $d(PXY) = c(PX) - c(PY) + c(P) - c(P) - c(P) = (c(P)-c(PY)) - (c(P) - c(PX)) = d(PY) - d(PX)$
  - Em outras palavras, podemos usar os diffsets dos conjuntos base para calcular o diffset do novo candidato
  - A variante do Eclat que usa diffsets ficou conhecida como dEclat

  - $C(PX) - C(PY)$
  - $C(PX) - C(PY) \cup C(P) - C(P)$
  - $C(PX) \cap \overline{C(PY)} \cup C(P) \cap \overline{C(P)}$
  - $C(PX) \cup \overline{C(P)} \cap C(P) \cup \overline{C(P)}$

## Aula 05 | 01/04/2025 | Mineração de conjuntos de itens

### Diffsets e dEclat [Aula 05]

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

- Por definição, $d(PXY) = c(PX) - c(PXY) = c(PX) - c(PY)$
- Podemos adicionar, ao conjunto acima, o conjunto vazio $(c(P) - c(P))$ sem alterá-lo
- Logo, $d(PXY) = c(PX) - c(PY) + c(P) - c(P) - c(P) = (c(P)-c(PY)) - (c(P) - c(PX)) = d(PY) - d(PX)$
- Em outras palavras, podemos usar os diffsets dos conjuntos base para calcular o diffset do novo candidato
- A variante do Eclat que usa diffsets ficou conhecida como dEclat

- [JV]
  - $d(PXY) = c(PX) - c(PY) = c(PX) - c(PXY)$
  - $c(PXY) = c(PX) \cap c(PY)$
    - "Diferença é a mesma coisa que interseção com complemento"
    - - $d(PXY) = ...$
  - Ele fez um monte de igualdades com operações de conjuntos.
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
  - $d(PX) = ...$
  - Outro exemplo:
    - $P = \lbrace 1, 2, 3, 4, 5 \rbrace$
    - $X = \lbrace 1, 3, 5 \rbrace$
    - $Y = \lbrace 2, 3, 4 \rbrace$
    - $PX = \lbrace 1, 3, 5 \rbrace$
    - $PY = \lbrace 2, 3, 4 \rbrace$
    - $\overline{PY} = \lbrace 1, 5 \rbrace$
    - $PX \cap \overline{PY} = \lbrace 1, 5 \rbrace$

---

- **ALGORITHM 8.4. Algorithm dEclat**
  - //`Initial Call:` $\mathcal{F} \gets \emptyset, P \gets \lbrace  \langle i, d(i), sup(i) \rangle | i \in \mathcal{I}, d(i) = \mathcal{T}\\t(i), sup(i) \geq minsup  \rbrace$
  - **dEclat** $(P, minsup, \mathcal{F})$:
    - **foreach** $\langle X_a, d(X_a), sup(X_a) \rangle \in P$ **do**
      - $\mathcal{F} \gets \mathcal{F} \cup \lbrace (X_a, sup(X_a)) \rbrace$
      - $P_a \gets \emptyset$
      - **foreach** $\langle X_b, d(X_b), sup(X_b) \rangle \in P$, with $X_b > X_a$ **do**
        - $X_{ab} = X_a \cup X_b$
        - $d(X_{ab}) = d(X_b) \setminus d(X_a)$
        - $sup(X_{ab}) = sup(X_a) - |d(X_{ab})|$
        - **if** $sup(X_{ab}) \geq minsup$ **then**
          - $P_a \gets P_a \cup \lbrace  \langle X_{ab}, d(X_{ab}), sup(X_{ab}) \rangle  \rbrace$
      - **if** $P_a \neq \emptyset$ **then** dEclat $(P_a, minsup, \mathcal{F})$

---

- Essa abordagem se mostrou muito eficiente para conjuntos densos
- Porém, em conjuntos esparsos, o algoritmo original é a melhor opção

- [JV]
  - Para bases esparsas: Eclat; para bases densas: dEclat

[Imagem (a): Minimun Support (%) - Connect]

[Imagem (b): Minimun Support (%) - pumsb*]

[Imagem (c): Minimun Support (%) - T40I10D100K]

### Leitura (Aula 05)

- Seções 8.1, 8.2 (Zaki e Meira)
- Seções 6.1, 6.2 (Introduction to Data Mining)
- Mohammed Javeed Zaki: Scalable Algorithms for Association Mining. IEEE Trans. Knowl. Data Eng. 12(3): 372-390 (2000)
- Zaki, M.J., Gouda, K.: Fast vertical mining using diffsets. Technical Report 01-1, Computer Science Dept., Rensselaer Polytechnic Institute (March 2001) 10
- Christian Borgelt. Efficient Implementations of Apriori and Eclat. Workshop of Frequent Item Set Mining Implementations (FIMI 2003, Melbourne, FL, USA).

- [JV]
  - Boa parte da explicação estão nos artigos. A implementação tá no Borgelt.
