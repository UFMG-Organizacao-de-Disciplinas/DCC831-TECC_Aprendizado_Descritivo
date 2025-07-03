# A

## B

### Slide: aula09-SD

#### Introdução

- Até o momento técnicas de aprendizado descritivo que encontravam padrões em dados não rotulados
- Essas técnicas buscavam regularidades locais nos dados sem a preocupação de aprender o conjunto como um todo
- Por outro lado, técnicas de aprendizado preditivo focam no aprendizado de modelos globais e, para isso, frequentemente fazem uso de dados rotulados
  - Intencionalmente, optam por não aprender pequenas regularidades nos dados
- Nesse sentido, parece existir uma dicotomia entre os dois tipos de aprendizado
- A área de aprendizado descritivo supervisionado se encontra na interseção das duas

  - De uma forma geral, o foco é encontrar regularidades descrevendo dados rotulados

- [JV]
  - Qual a vantagem de calcular essas métricas? Saber o que está acontecendo naquela base de dados.
  - Nem sempre a análise deve ser nas compras, mas sim nos clientes que fazem as compras.
  - Padrões em regiões ricas vs padrões em regiões pobres.
  - Teremos agora uma mistura do aprendizado supervisionado com a mineração de padrões.

#### Padrões locais x globais

- Para ilustrar essa diferença entre aprendizado descritivo supervisionado e algoritmos de classificação, consideremos o seguinte conjunto de dados rotulado

[Imagem: itens distribuídos aleatoriamente (os azuis mais na diagonal secundária, o vermelho mais na diagonal principal) e alguns mais frequentemente agrupados. Dois rótulos: quadrado azul e bola vermelha.]

---

- Árvores de decisão

[Imagem: árvore de decisão em si]

[Imagem]

---

- Padrões descritivos supervisionados

[Imagem]

- $\sigma_1 \equiv \in \lbrack 0.3, 0.7 ) \land x_2 \geq 0.9$
- $\sigma_2 \equiv \in \lbrack 0.275, 0.7 ) \land x_2 \leq 0.1$

- [JV]
  - "Ah, mas isso é detecção de anomalia". Não. É uma regularidade, excepcional.

#### Aprendizado descritivo supervisionado

- A área de aprendizado descritivo supervisionado evoluiu de forma isolada em três frentes:
  - Padrões contrastantes (contrast set mining)
  - Padrões emergentes (emerging pattern mining)
  - Descoberta de subgrupos (subgroup discovery)
    - [JV] Foram unificadas posteriormente
- O que há de comum e que une as três técnicas é o fato delas buscarem padrões locais com distribuições não usuais de alguma característica alvo
  - Normalmente, essa característica alvo é um atributo classe (rótulo das transações)
- Alguns autores referenciam essas técnicas como "descoberta de regras descritivas supervisionadas"
  - Ou Mineração supervisionada de padrões descritivos
    - [JV]
      - é o analista do problema que define quais as variáveis
      - O nome mais familiar é a descoberta de subgrupos

##### Contrast set mining

- Padrões contrastantes foram propostos por Bay e Pazzani (2001) como uma forma de encontrar padrões interessantes em dados rotulados
- Para eles, os objetos continuam sendo caracterizados por atributos categóricos/nominais, porém, agora, divididos em grupos
  - Os grupos são os rótulos dos objetos e são todos disjuntos entre si
- Eles definem que um itemset é um contrast set se existirem pelos menos dois grupos onde a probabilidade de ocorrência diverge

- [JV]
  - a diferença de frequência é relativamente grande.
  - As bases têm rótulos que são categóricos.

---

- Formalmente:
  - $\exists i j P(cset = True | G_i) \neq P(cset = True | G_j)$
    - [JV]
      - $cset:$ contrast set
      - $i, j:$ dois rótulo
        - O rótulo tende a ser mais frequente em um do que o outro.
      - Isso aqui diz respeito à relevância. Se um for diferente, "tá valendo"
  - $\max_{i j} | support(cset, G_i) - support(cset, G_j) | \geq \rho$
    - [JV]
      - A diferença de suporte entre os caras tem que ser maior que um valor mínimo.
- A ideia então é buscar padrões com suportes relativamente diferentes entre os grupos que sejam estatisticamente diferentes em confiança
  - Usam teste chi-quadrado para avaliar se as confianças são significativamente diferentes
- Tarefa adaptada para considerar apenas diferença de suporte

- Usa o algoritmo STUCCO

##### Emerging pattern mining

- Emerging pattern mining foi proposta por Dong e Li (1999)
  - [JV] Li foi membro da banca da tese de doutorado do Renato.
- A ideia dos autores era que seria necessário encontrar padrões que capturassem mudanças entre conjuntos de dados
- Um padrão emergente (emerging pattern) é definido como um itemset cujo suporte aumenta 'significativamente' de uma base de dados para outra
  - Nesse caso, são considerados explicitamente apenas dois grupos
- A medida de interesse é chamada de _growth rate_, sendo definida como:

$$
GR(X) =
\begin{cases}
  0, & \text{se } \sup_1(X) = 0 \text{ e } \sup_2(X) = 0 \\
  \infty, & \text{se } \sup_1(X) = 0 \text{ e } \sup_2(X) > 0 \\
  \frac{\sup_2(X)}{\sup_1(X)}, & \text{caso contrário} \\
\end{cases}
$$

- [JV]
  - Eles comparavam duas bases de dados
  - Esse infinito é chamado de "Jumping Emerging Pattern" e é muito interessante porque representa um que não acontecia de um lado e agora aparece no outro.
    - O problema é que ele só considera se for $> 0$, o que é muito aberto.
  - É interessante que isso é variante por direção.
  - (15/05/2025): E se testa do grupo A ou B, precisa testar também do B ao A? Não necessariamente. Eles buscam testar uma correlação entre grupos de dados distintos.

---

- Quando se fala em padrões emergentes, assume-se uma direção aonde eles 'emergem'
  - Pelo growth rate, um padrão é infinitamente interessante se ele não ocorre em uma base, mas ocorre pelo menos uma vez na outra
- Assim como na mineração de padrões frequentes, usualmente se estabelece um limiar de crescimento/emergência mínima
  - Um itemset $X$ é um padrão emergente se $GR(X) \geq \rho > 1$
- Podemos elencar diferentes tarefas considerando suporte e growth rate mínimos

---

- A figura ao lado, reproduzida de Dong e Li (1999), define o espaço de busca de padrões emergentes
- Cada itemset é representado por um ponto nesse espaço
  - Se $\sup_1(X) = s_1$ e $\sup_2(X) = s_2$, então $X$ é representado por $(s_1, s_2)$
- Os padrões emergentes são os itemsets abaixo da reta
- A interseção das retas que passam por $\alpha$ e $\beta$ é importante
  - $\beta = \alpha \times \rho$
  - O interesse é que esse ponto seja o mais próximo da origem possível

[Imagem] $\mathbb{R}^2: \sup_2(X) \times \sup_1(X)$

- Sobre a imagem:
  - Tudo da diagonal pra baixo é quem tem $\rho$ grande o bastante.
  - O ponto $(\alpha, \beta)$ representa
  - A inclinação é $1/\rho$
  - $\beta = \rho \cdot \alpha$
    - O ajuste de suporte mínimo vai depender desses três parâmetros.
  - $\alpha: minsup_1$
  - $\beta: minsup_2$
  - Qual a diferença entre A, B, C?
    - C: Frequentes em ambas as bases; GR acima do $\rho$, porém provavelmente algo já esperado
    - A: São os infrequentes. Padrões emergentes dentro dos infrequentes. São muito difíceis de calcular devido a abaixar o crivo do minsup
    - B: são os mais interessantes. Frequentes em 2 e infrequentes em 1. Aqueles com GR infinito.
  - O artigo foca em encontrar os padrões em B, porém com modificações consegue encontrar o C.

---

- Os polígonos A, B e C representam três tipos de tarefas associadas a mineração de padrões emergentes
- O triângulo A são itemsets infrequentes em ambos conjuntos de dados
  - **Tarefa:** mineração de padrões emergentes raros
  - Difícil execução pelo volume de padrões candidatos
- O triângulo C são itemsets frequentes em ambos conjuntos de dados
  - **Tarefa:** mineração de padrões emergentes frequentes
  - Possivelmente, trará padrões irrelevantes
  - Pode ser resolvido com pós-processamento nos itemsets frequentes de cada base
- O retângulo B são itemsets infrequentes na base 1 e frequente em 2
  - **Tarefa:** mineração de padrões emergentes
  - Padrões com maior potencial de relevância prática (i.e. maior aplicabilidade)
  - Pode-se aproveitar algoritmos já desenvolvidos anteriormente

[Imagem]

#### Descoberta de subgrupos (15/05/2025)

- Entende-se como descoberta de subgrupos a seguinte tarefa (Wrobel 1997):
  - > [...] given a so-called population of individuals (objects, customer, ...) and a property of those individuals we are interested in. The task of subgroup discovery is then to discover the subgroups of the population that are statistically "most interesting", i.e. are as large as possible and have the most unusual statistical (distributional) characteristics with respect to the property of interest
    - [JV]
      - Quer encontrar um grupo de elementos que desvia do comportamento esperado da população.
      - às vezes, é interessante analisar com todos aqueles que não têm determinada característica.
- Assim, compara-se a distribuição do atributo alvo no subgrupo e em seu complemento (ou população), verificando se elas são significativamente diferentes
  - [JV] Temos um atributo descritivo e um atributo alvo. O alvo é o que buscamos encontrar alguma característica.
  - Se o atributo alvo é a classe/rótulo dos objetos, então compara-se o suporte das classes no grupo e complemento, verificando se são diferentes
  - No caso de rótulos binários, verifica-se o suporte de uma das classes no grupo e complemento

---

- [JV] Baseline: ou a própria população, ou o complemento do subgrupo.

- O objetivo da tarefa então é encontrar padrões que discriminem as transações desses dois subconjuntos
- Os padrões podem ser itens como no caso de mineração de itemsets frequentes
  - Porém é mais comum se definir uma linguagem desses padrões
- A linguagem dos padrões é a conjunção de predicados definidos sobre os atributos da base
  - [JV]
    - Não é mais uma base de dados binária de "tem ou não tem", agora pode ser categórica, numérica, etc.
    - Esses abaixo são predicados criados. Pelo que entendi, a criação de predicados é tipo uma binarização dos dados.
    - Durante a execução do código pode-se tentar induzir quais devem ser esses valores pros predicados.
  - **Numéricos:** $\alpha \geq x; \alpha = x \dots$ (e.g. $idade \geq 10$)
  - **Categóricos:** $\alpha = x; \alpha \notin X$ (e.g. $cor=azul; cargo \in \{programador, analista\}$)
  - **Padrão:** $\alpha \geq x \land \beta \in X$ (e.g. $salario \geq 3K \land cargo \in \{programador, analista\}$)
    - [JV]
      - Um padrão seria uma conjunção de predicados.
      - Por que não disjunções? Porque explodiria fácil. Deixa de ser antimonotônica. Quanto mais adicionar, mais abrangente é.

---

- Duas das métricas de qualidade mais usadas para avaliar os padrões são:
  - $Q_g(X) = \frac{\sup^{+}(X)}{\sup^{-}(X) + g}$
    - [JV]
      - Tirando o g, é a ideia de padrões emergentes de Growth Rate
  - $WRAcc(X) = p(X) \cdot (p(+|X) - p(+))$
    - [JV]
      - Weighted Relative Accuracy/Unusualness/Descomunalidade
      - $p(X)$ é o suporte relativo de $X$
      - Acurácia: $p(+|X)$ dado que eu tenho a propriedade $X$, quantos têm a propriedade $+$?
      - $p(+)$ probabilidade dos itens $p(+)$ na população
      - $0.25 \leq WRAcc \leq 0.25$: Se for negativo, significa que
      - $X$ é a conjunção dos predicados.
  - onde
    - $\sup^{+}(X)$: é o suporte positivo (no subconjunto $D^{+}$)
    - $\sup^{-}(X)$: é o suporte negativo (no subconjunto $D^{-}$)
    - $p(.)$: é a probabilidade (proporção) da variável

---

- Note que, ao contrário do suporte, essas métricas não são anti-monotônicas.
  - [JV] Não dá pra usar o apriori pra isso.
- Assim, não podemos usar diretamente os algoritmos de mineração de itemsets frequentes para buscar esses padrões
- Existem alguns tipos de algoritmos para a tarefa:
  - **Exaustivos:** adaptações dos algoritmos clássicos (Apriori, FP-Growth) como Apriori-SD e SD-Map
    - [JV] não são tão usadas.
  - **Heurísticas gulosas:** algoritmo beam search como o algoritmo SD
    - [JV] Busca em feixe: Busca em largura com restrição de janela
  - **Heurísticas evolucionárias:** algoritmos genéticos, programação genética, como MESDIF, NMEEF, SSDP
    - [JV] MESDIF e NMEED: adaptações de algoritmos clássicos; SSDP: proposto por um aluno, bom para alta dimensionalidade
  - **Algoritmos de sampling:** MCTS4DM, MiSoSouP
    - [JV]
      - MCTS4DM (Monte Carlo Tree Search for Data Mining): tendo uma limitação de tempo, ele vai calculando de gradualmente; proposto
      - MiSoSouP: proposto por um italiano.

#### Equivalência entre as tarefas

- **Teorema**: Contrast set mining é compatível ('equivalente') a descoberta de subgrupos
- **Prova**:

  - $WRAcc(X) = p(X) \cdot [P(G_1|X) - P(G_1)]$
  - $= P(G_1 \cap X) - P(G_1) P(X)$
  - $= P(G_1 \cap X) - P(G_1) [P(G_2 \cap X) + P(G_1 \cap X)]$
  - $= P(G_1 \cap X) - P(G_1 \cap X) P(G_1) - P(G_1) P(G_2 \cap X)$
  - $= (1 - P(G_1)) P(G_1 \cap X) - P(G_2 \cap X) P(G_1)$
  - $= P(G_2) P(G_1 \cap X) - P(G_2 \cap X) P(G_1)$
  - $= P(G_2) P(G_1) P(X|G_1) - P(G_2) P(G_1) P(X|G_1)$
  - $= P(G_1) P(G_2) [P(X|G_1) - P(X|G_2)]$

- Como o tamanho das bases é constante, maximizar o $WRAcc$ é o mesmo que maximizar a diferença de suporte

---

- **Teorema:** Emerging pattern mining é equivalente a descoberta de subgrupos
- **Prova:** A definição de growth rate é equivalente à do $Q_g$ com $g = 0$
- Embora não tenha sido demonstrada a equivalência direta entre CSM e EPM, o fato de ambas serem compatíveis com SD nos permite deduzir tal equivalência.
- A tarefa de SD ganhou mais notoriedade na literatura que as demais. Grande parte dos estudos usa o termo Subgroup Discovery ao invés de qualquer outro
  - Alguns estudos usam a expressão supervised descriptive pattern mining, mas são mais raros
- Por essa razão, focaremos os estudos na tarefa de SD, lembrando que se trocarmos a função de qualidade, retornamos a qualquer uma das outras duas
  - [JV] Perguntei sobre a existência de uma Classe de Complexidade pra essas tarefas. Ele disse que acha que não fizeram isso.

#### Leitura

- Novak, P. K., Lavrač, N., & Webb, G. I. (2009). Supervised descriptive rule discovery: A unifying survey of contrast set, emerging pattern and subgroup mining. Journal of Machine Learning Research, 10(2).
- Ventura e Luna cap. 1
- Dong e Bailey cap. 1
