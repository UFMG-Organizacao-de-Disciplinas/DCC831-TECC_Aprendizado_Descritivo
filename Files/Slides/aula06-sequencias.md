# Slide: aula06-sequencias (Aula 8, 9, 10)

## Aula 08 | 10/04/2025 | Mineração de sequências

### Introdução (Aula 08)

- Nessa aula, vamos discutir o problema de mineração de sequências em bases de dados
- Esse problema ocorre com frequência em diversas áreas
  - Identificar trajetórias dos alunos de computação
  - Identificar perfil (temporal) de compras dos clientes (celular $\to$ capa protetora $\to$ fone de ouvido)
  - Identificar padrões de genes e proteínas no genoma
- Enquanto itemsets são padrões intra-transações, aqui estamos buscando padrões inter-transações

- [JV]
  - Agora buscaremos ver as trajetórias usuais.
  - Talvez poderíamos avaliar quais disciplinas os alunos tendam a fazer mais frequentemente. Distintos da sequência usual.
  - Busca-se entender os comportamentos dos clientes.

---

- Para ilustrar, considere a seguinte base de dados
- Os clientes fazem diversas compras na loja
  - Mais de 1 item pode ser adquirido em uma transação
- Existe algum padrão de compras?
  - Determinados itens são comprados em sequência?
- Esse problema é conhecido como **mineração de sequências (frequentes)**

| **ID Cliente** | **Data** | **Transação**         | **JV: Enxugado** |
| :------------- | :------: | :-------------------- | :--------------- |
| 1              | 25/06/19 | aveia                 | a                |
| 1              | 30/06/19 | castanha              | c                |
| 2              | 10/06/19 | granola, mel          | gm               |
| 2              | 15/06/19 | aveia                 | a                |
| 2              | 20/06/19 | banana, suco, leite   | bsl              |
| 3              | 25/06/19 | aveia, iogurte, leite | ail              |
| 4              | 25/06/19 | aveia                 | a                |
| 4              | 30/06/19 | banana, leite         | bl               |
| 4              | 25/07/19 | castanha              | c                |
| 5              | 12/06/19 | castanha              | c                |
| 6              | 10/06/19 | aveia, granola        | ag               |
| 6              | 11/06/19 | leite                 | l                |
| 6              | 17/06/19 | banana, leite         | bl               |

### Definições

- A base de dados é um conjunto de transações consistindo em:
  - ID do cliente
  - Timestamp da transação
  - Itens 'comprados'
- Os itens da transação são um itemset de uma coleção de possíveis itens
- Uma **sequência** é uma **lista ordenada de itemsets**
  - Os itemsets também são chamados de elementos
- Para um conjunto de itens $I$, uma sequência $s = \langle s_1 s_2 \dots s_n \rangle$ em que cada $s_i \subseteq I$ é um itemset

  - Por definição, um item não pode aparecer mais de uma vez num itemset, mas pode aparecer várias vezes numa sequência

- [JV]
  - Exemplo de sequência: $\langle (gm) a (bsl) \rangle$
    - gm: granola e mel
    - a: aveia
    - bsl: banana, suco e leite
    - Cada grupinho faz parte de uma transação. Eles apenas estão ordenados temporalmente, não internamente. Tanto que $\langle gm \rangle \equiv \langle mg \rangle$.

---

- Por exemplo, a sequência $\langle (gm) a (bsl) \rangle$ representa a sequência de compras do cliente 2 na base de dados anterior
  - Itemsets são delimitados por parêntesis; itemsets unitários são representados sem parêntesis
- Uma sequência $\alpha = \langle a_1 a_2 \dots a_n \rangle$ é uma subsequência de uma sequência $\beta = \langle b_1 b_2 \dots b_m \rangle$, $\alpha \subseteq \beta$, se existe uma função $\phi: [1:n] \to [1:m]$ tal que
  - $a_1 \subseteq b_{\phi(1)}$; e
  - $\forall i, j [i < j \to \phi(i) < \phi(j)]$
- As sequências $\langle (gm) b \rangle$, $\langle mab \rangle$ e $\langle a \rangle$ são subsequências de $\langle (gm) a (bsl) \rangle$
- Note que a ordem é definida somente entre elementos, e não dentro dos itemsets

  - Contudo, vamos assumir que os elementos são dispostos conforme alguma ordem dentro dos itemsets (em nosso caso, a ordem que forma apresentados na base original)

- [JV]
  - Para simplificação de notação, sempre que uma transação tiver apenas um item, ele não fica englobado por parênteses. Se tiver 2 ou mais, tem.
  - Uma sequência é subsequência de outra se todos os itens de um subconjunto aparecem no outro, e mantém a mesma ordem, mesmo que não estejam nas mesmas posições, e não precisam ser necessariamente contíguos.
  - Então, uma forma de analisar é se cada um dos grupinhos de itens das transações é subconjunto das outras transações.
  - Eu ainda posso explicar isso aqui melhor. Eu entendi, mas não anotei legal.

---

- Podemos redefinir a base de dados como um conjunto de pares $(sid, s)$ em que sid é um identificador de sequência e s uma sequência
  - Cada identificador de cliente é um sid
  - As diferentes transações de um cliente ordenados pelo tempo formam a sequência
- Um cliente $(sid, s)$ suporta uma sequência $\alpha$ se $\alpha \subseteq s$ para
- Assim, definimos o suporte de uma sequência como
  - $sup(\alpha) = |\lbrace (sid, s) | \alpha \subseteq s \rbrace|$
- Exemplo:
  - $sup(\langle a \rangle) = 5$
  - $sup(\langle gb \rangle) = 2$
  - $sup(\langle l \rangle) = 4$

| **sid** | **s**                           |
| :-----: | :------------------------------ |
|    1    | $$\langle ac \rangle$$          |
|    2    | $$\langle (gm)a(bsl) \rangle$$  |
|    3    | $$\langle (ail) \rangle$$       |
|    4    | $$\langle a (bl) c \rangle$$    |
|    5    | $$\langle c \rangle$$           |
|    6    | $$\langle (ag) l (bl) \rangle$$ |

---

- Uma sequência $\alpha$ é frequente se $sup(\alpha) \geq minsup$
- Uma sequência $\alpha$ tem tamanho $k$ (é uma k-sequência) se $\sum |a_i| = k$
- Uma sequência frequente é dita máxima se não existe uma supersequência própria que seja frequente
- Ela é fechada se não existe uma supersequência própria com o mesmo suporte

## Aula 09 | 15/04/2025 | Mineração de grafos

### Introdução (Aula 09)

- Nessa aula, vamos discutir o problema de mineração de sequências em bases de dados
- Esse problema ocorre com frequência em diversas áreas
  - Identificar trajetórias dos alunos de computação
  - Identificar perfil (temporal) de compras dos clientes (celular $\to$ capa protetora $\to$ fone de ouvido)
  - Identificar padrões de genes e proteínas no genoma
- Enquanto itemsets são padrões intra-transações, aqui estamos buscando padrões inter-transações

---

- Para ilustrar, considere a seguinte base de dados
- Os clientes fazem diversas compras na loja
  - Mais de 1 item pode ser adquirido em uma transação
- Existe algum padrão de compras?
  - Determinados itens são comprados em sequência?
- Esse problema é conhecido como **mineração de sequências (frequentes)**

| **ID Cliente** | **Data** | **Transação**         | **JV: Enxugado** |
| :------------- | :------: | :-------------------- | :--------------- |
| 1              | 25/06/19 | aveia                 | a                |
| 1              | 30/06/19 | castanha              | c                |
| 2              | 10/06/19 | granola, mel          | gm               |
| 2              | 15/06/19 | aveia                 | a                |
| 2              | 20/06/19 | banana, suco, leite   | bsl              |
| 3              | 25/06/19 | aveia, iogurte, leite | ail              |
| 4              | 25/06/19 | aveia                 | a                |
| 4              | 30/06/19 | banana, leite         | bl               |
| 4              | 25/07/19 | castanha              | c                |
| 5              | 12/06/19 | castanha              | c                |
| 6              | 10/06/19 | aveia, granola        | ag               |
| 6              | 11/06/19 | leite                 | l                |
| 6              | 17/06/19 | banana, leite         | bl               |

### Definições (Aula 09)

- A base de dados é um conjunto de transações consistindo em:
  - ID do cliente
  - Timestamp da transação
  - Itens 'comprados'
- Os itens da transação são um itemset de uma coleção de possíveis itens
- Uma **sequência** é uma **lista ordenada de itemsets**
  - Os itemsets também são chamados de elementos
- Para um conjunto de itens $I$, uma sequência $s = \langle s_1 s_2 \dots s_n \rangle$ em que cada $s_i \subseteq I$ é um itemset
  - Por definição, um item não pode aparecer mais de uma vez num itemset, mas pode aparecer várias vezes numa sequência

---

- Por exemplo, a sequência $\langle (gm) a (bsl) \rangle$ representa a sequência de compras do cliente 2 na base de dados anterior
  - Itemsets são delimitados por parêntesis; itemsets unitários são representados sem parêntesis
- Uma sequência $\alpha = \langle a_1 a_2 \dots a_n \rangle$ é uma subsequência de uma sequência $\beta = \langle b_1 b_2 \dots b_m \rangle$, $\alpha \subseteq \beta$, se existe uma função $\phi: [1:n] \to [1:m]$ tal que
  - $a_1 \subseteq b_{\phi(1)}$; e
  - $\forall i, j [i < j \to \phi(i) < \phi(j)]$
- As sequências $\langle (gm) b \rangle$, $\langle mab \rangle$ e $\langle a \rangle$ são subsequências de $\langle (gm) a (bsl) \rangle$
- Note que a ordem é definida somente entre elementos, e não dentro dos itemsets

  - Contudo, vamos assumir que os elementos são dispostos conforme alguma ordem dentro dos itemsets (em nosso caso, a ordem que forma apresentados na base original)

- [JV]
  - Tentando explicar sobre as subsequências:

| Itemset $a$                    | Itemset $b$                    | $b$ é subsequência de $a$? |
| :----------------------------- | :----------------------------- | :------------------------: |
| $\langle (gm) a (bsl) \rangle$ | $\langle (gm) b \rangle$       |            Sim             |
| $\langle (mg) a (lsb) \rangle$ | $\langle (gm) a (bls) \rangle$ |            Sim             |
| $\langle (gm) a (bsl) \rangle$ | $\langle (gm) a \rangle$       |            Sim             |

...

---

- Podemos redefinir a base de dados como um conjunto de pares $(sid, s)$ em que sid é um identificador de sequência e s uma sequência
  - Cada identificador de cliente é um sid
  - As diferentes transações de um cliente ordenados pelo tempo formam a sequência
- Um cliente $(sid, s)$ suporta uma sequência $\alpha$ se $\alpha \subseteq s$ para
- Assim, definimos o suporte de uma sequência como
  - $sup(\alpha) = |\lbrace (sid, s) | \alpha \subseteq s \rbrace|$
- Exemplo:
  - $sup(\langle a \rangle) = 5$
  - $sup(\langle gb \rangle) = 2$
  - $sup(\langle l \rangle) = 4$

| **sid** | **s**                           |
| :-----: | :------------------------------ |
|    1    | $$\langle ac \rangle$$          |
|    2    | $$\langle (gm)a(bsl) \rangle$$  |
|    3    | $$\langle (ail) \rangle$$       |
|    4    | $$\langle a (bl) c \rangle$$    |
|    5    | $$\langle c \rangle$$           |
|    6    | $$\langle (ag) l (bl) \rangle$$ |

- [JV]
  - Essa representação é similar à representação horizontal.
  - Nessa definição ignoramos o timestamp. Focamos apenas na sequência cronológica.
  - Nesse caso o tempo apenas é usado pra ordenar, mas não é considerado na sequência.
  - Cobertura: todos os elementos do qual o itemset é subsequência.
  - O suporte é o tamanho da cobertura.

---

- Uma sequência $\alpha$ é frequente se $sup(\alpha) \geq minsup$
- Uma sequência $\alpha$ tem tamanho $k$ (é uma k-sequência) se $\sum |a_i| = k$
- Uma sequência frequente é dita máxima se não existe uma supersequência própria que seja frequente
- Ela é fechada se não existe uma supersequência própria com o mesmo suporte

- [JV]
  - $\sum |a_i| = k$: conta o total de itens. Sem se preocupar com repetição ou não.

### Mineração de sequências frequentes - (Aula 09)

- O problema de mineração de sequências frequentes consiste em encontrar todas as sequências cujo suporte esteja acima de um limiar mínimo definido pelo usuário
- Existem abordagens tanto para minerar todo o conjunto de sequências frequentes quanto para representações compactas desse conjunto
- Nessa aula veremos apenas as abordagens para minerar todo o conjunto de sequências frequentes
- Essas abordagens são extensões dos principais algoritmos para mineração de conjuntos de itens frequentes

- [JV]
  - Não veremos as maximais e fechadas das sequências. Nem as formas densas, embora existam.

### Generalized Sequential Patterns (GSP)

- O GSP é um algoritmo baseado no Apriori para minerar sequências frequentes
- Ele também foi proposto por Agrawal e Srikant em 1996
- Por ser baseado no Apriori, o algoritmo adota a estratégia de busca em largura
- O algoritmo usa sequências frequentes de tamanho $k-1$ para gerar candidatas de tamanho $k$ e avaliar o suporte,
- Ele também emprega a propriedade de antimonotonicidade do suporte para podar o espaço de busca

- [JV]
  - Se uma sequência é infrequente, qualquer supersequência dela também será infrequente.

---

- Assim como o Apriori, o algoritmo faz diversas passadas sobre a base de dados
- Na primeira passada, o algoritmo verifica o suporte de cada item
  - Os itens individualmente são sequências simples de tamanho 1
- Pela propriedade do Apriori, somente os itens frequentes são mantidos e servem de base para a geração dos candidatos de tamanho 2
- Cada par $\langle x \rangle$ e $\langle y \rangle$ de sequências de tamanho 1 dá origem a duas sequências de tamanho 2
  - $\langle xy \rangle$
  - $\langle (xy) \rangle$
- A exceção se dá quando $x=y$, nesse caso somente a primeira é gerada
- Logo, o conjunto de candidatos de tamanho 2 é:

  - $C^{(2)} = \lbrace  \langle xy \rangle | (x, y) \in F^{(1)} \times F^{(1)}  \rbrace \cup \lbrace  \langle (xy) \rangle | (x, y) \in F^{(1)} \times F^{(1)} \wedge x \neq y \rbrace$

- [JV]
  - Primeiro calcula o suporte de cada item individual.
  - Depois, à partir de cada sequência, geram-se três candidatos
    - Ex: $\langle a \rangle$ e $\langle b \rangle$ geram:
      - $\langle ab \rangle$, $\langle ba \rangle$, $\langle (ab) \rangle$.
    - Ou dois candidatos, se desconsiderarmos que $\langle ba \rangle$ será gerado em outra iteração.
  - Todos de tamanho dois não verificamos a propriedade apriori.

---

- Os candidatos que possuam subsequências de tamanho $k-1$ infrequentes são removidos do conjunto
- Então, o suporte dos candidatos é computado com uma passada na base, e os infrequentes são descartados
- A partir de $k=3$, os candidatos são gerados da seguinte forma:
  - Sejam $s_1$ e $s_2$ duas sequências frequentes de tamanho $k-1$ tais que ambas sejam idênticas após a remoção do primeiro item de $s_1$ e do último item de $s_2$
  - As sequências são unidas para gerar uma candidata de tamanha k
    - A nova candidata será a sequência $s_1$ estendida com o último item de $s_2$
  - O último item será um elemento separado se ele era um elemento separado em $s_2$, ou será agregado ao último elemento de $s_1$ caso contrário
- O algoritmo repete o processo enquanto houverem candidatos no próximo nível

- [JV]
  - Esse daqui foi muito confuso
  - ga+(am) = g(am)
  - ga+am = gam
  - (ga)+am = (ga)m
  - (ga)+(am) = (gam)
  - aba+bab = abab
  - bab+aba = baba

### Sequential Pattern Discovery using Equivalence classes (Spade)

- Outra abordagem para mineração de sequências frequentes foi proposta por Zaki em 2001
- O algoritmo Spade é baseado no Eclat
- Assim como o Eclat, ele utiliza uma representação da base de dados similar à vertical e divide o espaço de busca de acordo com o prefixo das sequências

---

- Para obter a representação vertical, vamos associar a cada item $i$ uma tupla $(sid, pos(i))$
  - $pos(i)$ é a lista de todos os elementos em que $i$ ocorre na sequência referente ao cliente $sid$
- A lista de todos os pares sequência-posição de um item é chamada de **poslist** e é denotada por $\mathcal{L}(i)$
- Exemplos:
  - $\mathcal{L}(l) = \lbrace  (2, \lbrace 3 \rbrace), (3, \lbrace 1 \rbrace), (4, \lbrace 2 \rbrace), (6, \lbrace 2, 3 \rbrace )  \rbrace$
  - $\mathcal{L}(g) = \lbrace  (2, \lbrace 1 \rbrace), (6, \lbrace 1 \rbrace)  \rbrace$
- A representação vertical da base pode ser obtida pelas poslists de todos os itens
  - Note que $sup(i) = |\mathcal{L}(i)|$

| **sid** | **s**                           |
| :------ | :------------------------------ |
| 1       | $$\langle ac \rangle$$          |
| 2       | $$\langle (gm)a(bsl) \rangle$$  |
| 3       | $$\langle (ail) \rangle$$       |
| 4       | $$\langle a (bl) c \rangle$$    |
| 5       | $$\langle c \rangle$$           |
| 6       | $$\langle (ag) l (bl) \rangle$$ |

| **item** | **pos(item)**                         |
| :------- | :------------------------------------ |
| a        | { (1,1), (2,2), (3,1), (4,1), (6,1) } |
| b        | { (2,3), (4,2), (6,3) }               |
| c        | { (1,2), (4,3), (5,1) }               |
| g        | { (2,1), (6,1) }                      |
| i        | { (3,1) }                             |
| l        | { (2,3), (3,1), (4,2), (6,23) }       |
| s        | { (2,3) }                             |

- [JV]
  - No caso do l, o 23, na verdade é uma lista $[2, 3]$

---

- Zaki demonstrou que novas sequências podem ser geradas a partir da **junção temporal** de duas sequências que pertençam a uma mesma classe de equivalência (compartilham um prefixo de tamanho $k-1$)
- O suporte pode ser computado pela interseção das poslists
- Supondo que as sequências a serem unidas compartilham um prefixo P, três situações podem ocorrer:
- Juntar duas sequências (Px) e (Py): resulta em (Pxy)
- Juntar duas sequências (Px) e Py: resulta em (Px)y
- Juntar duas sequências Px e Py: pode resultar em Pxy, Pyx e P(xy) dependendo da ordem temporal de x e y; um caso particular ocorre quando x=y, nesse caso, a junção só pode resultar em Pxx

---

- Juntar duas sequências (Px) e (Py): resulta em (Pxy)
  - Sejam $\mathcal{L}(Px)$ e $\mathcal{L}(Py)$ as poslists de (Px) e (Py). A poslist de (Pxy) é gerada da seguinte forma: $\mathcal{L}((Pxy)) = \left{ \left( i, pos((Px)) \cap pos((Py)) \right) | \left( i, pos((Px)) \right) \in \mathcal{L}((Px)) \wedge \left( i, pos((Py)) \right) \in \mathcal{L}((Py)) \wedge pos((Px)) \cap pos((Py)) \neq \emptyset \right}$
  - Ou seja, é o conjunto de sequência-posições em que ambos ocorrem ao mesmo tempo
  - O caso P(xy) é análogo a esse
- Juntar duas sequências (Px) e Py: resulta em (Px)y

  - $\mathcal{L}((Px)y) = \left{ \left( i, \left{ v \in pos(Py) | \exists u \in pos((Px)) u < v \wedge \left( i, pos(Py) \right) \in \mathcal{L}(Py) \wedge \left( i, pos((Px)) \right) \in \mathcal{L}((PX)) \right} \right) \right}$;
  - Ou seja, são todas as sequências em que ambas acontecem, porém agora somente as posições em que $y$ ocorre temporalmente após $x$ são mantidas
  - O caso é equivalente a Pxy e Pyx

- [JV]
  - Agora veremos os dois prefixos. E apenas consideraremos o último item. Não a última transação.
  - Se considerarmos Py, onde P ocorreu na posição 1, e y está na posição 6;
  - E temos Px, onde P ocorreu na posição 2, e x está na posição 2;
  - Se gerarmos Pyx, teríamos que o y está antes do x, mas temporalmente deveria estar depois. Logo, consideramos que ele será infrequente, podendo então podar.

## Aula 10 | 17/04/2025 | Mineração de grafos

### Sequential Pattern Discovery using Equivalence classes (Spade) (Aula 10)

- Para obter a representação vertical, vamos associar a cada item $i$ uma tupla $(sid, pos(i))$
  - $pos(i)$ é a lista de todos os elementos em que $i$ ocorre na sequência referente ao cliente $sid$
- A lista de todos os pares sequência-posição de um item é chamada de **poslist** e é denotada por $\mathcal{L}(i)$
- Exemplos:
  - $\mathcal{L}(l) = \lbrace  (2, \lbrace 3 \rbrace), (3, \lbrace 1 \rbrace), (4, \lbrace 2 \rbrace), (6, \lbrace 2, 3 \rbrace )  \rbrace$
  - $\mathcal{L}(g) = \lbrace  (2, \lbrace 1 \rbrace), (6, \lbrace 1 \rbrace)  \rbrace$
- A representação vertical da base pode ser obtida pelas poslists de todos os itens
  - Note que $sup(i) = |\mathcal{L}(i)|$

| **sid** | **s**                           |
| :------ | :------------------------------ |
| 1       | $$\langle ac \rangle$$          |
| 2       | $$\langle (gm)a(bsl) \rangle$$  |
| 3       | $$\langle (ail) \rangle$$       |
| 4       | $$\langle a (bl) c \rangle$$    |
| 5       | $$\langle c \rangle$$           |
| 6       | $$\langle (ag) l (bl) \rangle$$ |

| **item** | **pos(item)**                                         |
| :------- | :---------------------------------------------------- |
| a        | $\lbrace  (1,1), (2,2), (3,1), (4,1), (6,1)  \rbrace$ |
| b        | $\lbrace  (2,3), (4,2), (6,3)  \rbrace$               |
| c        | $\lbrace  (1,2), (4,3), (5,1)  \rbrace$               |
| g        | $\lbrace  (2,1), (6,1)  \rbrace$                      |
| i        | $\lbrace  (3,1)  \rbrace$                             |
| l        | $\lbrace  (2,3), (3,1), (4,2), (6,23)  \rbrace$       |
| s        | $\lbrace  (2,3)  \rbrace$                             |

- [JV Anotação no quadro]
  - $ms = minsup = 3$
  - itens com suporte mínimo: $\lbrace a, b, c, l \rbrace$
  - Checa com o
  - $P_a:$
    - Verifica naquela lista ali de trás de $pos(item)$, e vai verificando se os itens aparecem nessa ordem para os dois itens nas transações de um mesmo cliente.
    - $\emptyset a - \emptyset a:$ aa | ~~(aa)~~ (Como os dois são o mesmo item, é descartado)
      - $aa:$ Infrequente
    - $\emptyset a - \emptyset b: ab | (ab)$
      - $ab: pos = \lbrace  (2,3), (4,2), (6,3)  \rbrace$
      - $(ab):$ Infrequente
    - $\emptyset a - \emptyset c: ac | (ac)$
      - $ac: pos = \lbrace  (1,2), (4,3)  \rbrace$ Infrequente
      - $(ac):$ Infrequente
    - $\emptyset a - \emptyset l: al|(al)$
      - $al: pos = \lbrace  (2,3), (4,2), (6, 23)  \rbrace$
      - $(al):$ Infrequente
  - Então, os frequentes são: $\lbrace  ab, al \rbrace$
  - $P_{ab}$
    - $ab - ab: abb$
    - $ab - al: abl|a(bl)$
      - $a(bl): pos = (2,3), (4,2), (6,3)  \rbrace$
  - Então os frequentes são: $\lbrace  a(bl)  \rbrace$
  - $P_{a(bl)}$
    - $a(bl) - a(bl): a(bl)l$ Isso daqui eu não entendi.
  -

---

- Zaki demonstrou que novas sequências podem ser geradas a partir da **junção temporal** de duas sequências que pertençam a uma mesma classe de equivalência (compartilham um prefixo de tamanho $k-1$)
- O suporte pode ser computado pela interseção das poslists
- Supondo que as sequências a serem unidas compartilham um prefixo P, três situações podem ocorrer:
- Juntar duas sequências (Px) e (Py): resulta em (Pxy)
- Juntar duas sequências (Px) e Py: resulta em (Px)y
- Juntar duas sequências Px e Py: pode resultar em Pxy, Pyx e P(xy) dependendo da ordem temporal de x e y; um caso particular ocorre quando x=y, nesse caso, a junção só pode resultar em Pxx

---

- Juntar duas sequências (Px) e (Py): resulta em (Pxy)
  - Sejam $\mathcal{L}(Px)$ e $\mathcal{L}(Py)$ as poslists de (Px) e (Py). A poslist de (Pxy) é gerada da seguinte forma: $\mathcal{L}((Pxy)) = \left{ \left( i, pos((Px)) \cap pos((Py)) \right) | \left( i, pos((Px)) \right) \in \mathcal{L}((Px)) \wedge \left( i, pos((Py)) \right) \in \mathcal{L}((Py)) \wedge pos((Px)) \cap pos((Py)) \neq \emptyset \right}$
  - Ou seja, é o conjunto de sequência-posições em que ambos ocorrem ao mesmo tempo
  - O caso P(xy) é análogo a esse
- Juntar duas sequências (Px) e Py: resulta em (Px)y

  - $\mathcal{L}((Px)y) = \lbrace \left( i, \lbrace v \in pos(Py) | \exists u \in pos((Px)) u < v \wedge ( i, pos(Py) ) \in \mathcal{L}(Py) \wedge ( i, pos((Px)) ) \in \mathcal{L}((PX)) \rbrace \right) \rbrace$
  - Ou seja, são todas as sequências em que ambas acontecem, porém agora somente as posições em que $y$ ocorre temporalmente após $x$ são mantidas
  - O caso é equivalente a Pxy e Pyx

- [JV]
  - Agora veremos os dois prefixos. E apenas consideraremos o último item. Não a última transação.
  - Se considerarmos Py, onde P ocorreu na posição 1, e y está na posição 6;
  - E temos Px, onde P ocorreu na posição 2, e x está na posição 2;
  - Se gerarmos Pyx, teríamos que o y está antes do x, mas temporalmente deveria estar depois. Logo, consideramos que ele será infrequente, podendo então podar.

---

- Sejam as sequências $\langle gb \rangle$ e $\langle gl \rangle$ pertencentes à classe de equivalência de $g$, e suas respectivas poslists $\mathcal{L}(gb) = \lbrace  (2,3), (6,3)  \rbrace$ e $\mathcal{L}(gl) = \lbrace  (2,3), (6,3)  \rbrace$
  - $\mathcal{L}(g(bl)) = \lbrace  (2,3), (6,3)  \rbrace$
  - $\mathcal{L}(gbl) = \emptyset$
  - $\mathcal{L}(glb) = \emptyset$
- O algoritmo segue explorando o espaço de busca enquanto as classes de equivalência não forem vazias

---

- **ALGORITHM 10.2. Algorithm SPADE**
  - `// Initial Call:` $\mathcal{F} \gets \emptyset, k \gets 0, P \gets \lbrace \langle s, \mathcal{L}(s) \rangle | s \in \sum, sup(s) \geq minsup \rbrace$
  - **SPADE** $(P, minsup, \mathcal{F}, k)$
    - **foreach** $r_a \in P$ **do**
      - $\mathcal{F} \gets \mathcal{F} \cup \lbrace (r_a, sup(r_a)) \rbrace$
      - $P_a \gets \emptyset$
      - **foreach** $r_b \in P$ **do**
        - $r_{ab} = r_a + r_b$
        - $\mathcal{L}(r_{ab}) = \mathcal{L}(r_a) \cap \mathcal{L}(r_b)$
        - **if** $sup(r_{ab}) \geq minsup$ **then**
          - $P_a \gets P_a \cup \lbrace \langle r_{ab}, \mathcal{L}(r_{ab}) \rangle \rbrace$
      - **if** $P_a \neq \emptyset$ **then** SPADE $(P, minsup, \mathcal{F}, k+1)$

### Leitura (Aula 10)

- Seções 10.1 e 10.2 Zaki e Meira
- Capítulo 11 Aggarwal e Han
- [Link_2001][Link_2001] Zaki, M.J. SPADE: An Efficient Algorithm for Mining Frequent Sequences. Machine Learning 42, 31-60 (2001).
- [Link_1996][Link_1996] Srikant R., Agrawal R. (1996) Mining sequential patterns: Generalizations and performance improvements. In: Apers P., Bouzeghoub M., Gardarin G. (eds) Advances in Database Technology — EDBT '96. EDBT 1996. Lecture Notes in Computer Science, vol 1057. Springer, Berlin, Heidelberg.

[Link_2001]: https://doi.org/10.1023/A:1007652502315
[Link_1996]: https://doi.org/10.1007/BFb0014140
