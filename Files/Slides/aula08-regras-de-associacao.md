# Slide: aula08-regras-de-associação [JV: Cheguei tarde]

## Aula 14 | 06/05/2025 | Descoberta de subgrupos

### Introdução (Aula 14)

- Como discutimos anteriormente, o processo de extração de regras de associação em base de dados envolve duas etapas:
  - A mineração de padrões frequentes (que vimos ao longo das últimas aulas); e
  - A geração de regras interessantes a partir dos padrões
- A definição de 'interesse' é naturalmente subjetiva, pois depende do domínio da aplicação.
- Pode-se usar métricas na tentativa de tornar a medida de interesse mais objetiva
- O suporte dos padrões é uma forma de evitar regras espúrias, já que exclui padrões que ocorrem por chance
- Assim o processo de geração de regras se torna relativamente trivial a partir dos padrões frequentes

### Regras de associação

- Uma regra de associação é uma implicação lógica do tipo $X \to Y$ em que $X$ e $Y$ são itemsets e $X \cap Y = \varnothing$
  - [JV]
    - O que tá na esquerda da seta é o antecedente. O que tá à direita é o consequente.
    - Se eles são vazios, nenhum deles é vazio $(X \neq Y \neq \varnothing)$
    - Quais são todas as possíveis regras de associação?
      - Sendo $A$ o conjunto de itens:
        - $|\mathcal{P}(A)| - \text{o maior item} - \varnothing$
        - $|A| = k$
        - $2^k - 2$
      - Exemplos
        - $\{a, b\} = \{\varnothing, a, b, ab\}$
        - $\{a, b, c\} = \{\varnothing, a, b, c, ab, ac, bc, abc\}$; seria 6;
- O interesse (representatividade) de uma regra é definida por:
  - Suporte: $sup(X \to Y) = \frac{sup(X \cup Y)}{|D|}$
  - Confiança: $conf(X \to Y) = \frac{sup(X \cup Y)}{sup(X)}$
- Uma regra é interessante se o suporte é maior que um limiar de suporte mínimo (minsup), e a confiança maior que uma confiança mínima $(minconf)$
- Enquanto o suporte mostra quão aplicável (frequente) a regra é na base de dados, a confiança mostra a força da associação entre os itemsets (quão provável é se observar os itens de $Y$ nas transações da cobertura de $X$)

- [JV]
  - Buscamos formas subjetivas de definir o grau de interesse.
  - O suporte da regra define quão frequente é a ocorrência de determinada regra numa base.
    - Ele é dado pela divisão da `quantidade de vezes em que determinadas regras X e Y ocorrem na base de dados` pelo `tamanho da base de dados`.
  - A confiança é: "Dentre as transações de X, quantas delas têm X e Y?"
    - **Exemplo:** $X=ab, Y=cd; X \cup Y = abcd$
  - É importante considerar que embora trabalhemos com uma implicação, é aceito a possibilidade de falhas nessa implicação.
  - **Dúvida:** por que que não usávamos $minconf$ no contexto de minerações de padrões?
  - **Resposta:** Porque aqui estamos associando duas coisas entre si. E para isso precisamos verificar quão forte é essa associação

---

- Como as regras interessantes são aquelas que satisfazem o suporte mínimo, elas podem ser geradas a partir dos itemsets frequentes
- Podem ser geradas $2^k - 2$ regras a partir de um k-itemset
  - $r(X) = \lbrace (X - Y) \to Y | Y \subseteq X \text{ e } 0 < |Y| < k \rbrace$
    - [JV]
      - Entender melhor o que isso daqui quer dizer.
      - Essa subtração é justamente para gerar uma regra, confirmando que o que está à esquerda da seta seja necessariamente disjunto de $Y$; ou seja, $|(X-Y) \cap Y| = 0$
  - Note que, como $X$ é frequente, o suporte dos antecedentes e consequentes da regra também são itemsets frequentes e, portanto, já tiveram suporte computado. Assim, não há necessidade de novas passadas na base de dados para computar a confiança da regra
- Embora não seja anti-monotônica, se $(X - Y) \to Y$ não satisfaz a restrição de confiança, então $(X - Y') \to Y'$ também não satisfaz para todo $Y' \supset Y$

  - [JV] Essa é tipo a propriedade do apriori: se um conjunto é infrequente, os maiores que ele também são infrequentes. De forma similar, se $Y'$ é maior e engloba $Y$, e Y não tem confiança, então $Y'$ é também não tem confiança o bastante.

- [JV]
  - Podemos usar os padrões frequentes para poder gerar as regras de associação.
  - $c((X-Y) \to Y) = \frac{sup(X)}{sup(X-Y)} < minconf$
  - $Y \subset Y'$
  - $sup(X-Y') \leq sup (X-Y)$

---

[image: ICCBased(RGB,sRGB IEC61966-2.1), width: 565, height: 370, bpc: 8 Retirado de Figura 6.15 de Tan et al.]

- [JV]
  - A ideia passada nessa imagem é a mesma lógica do apriori. O primeiro que tiver baixa confiança, removemos então todos os seus filhos.
  - Deve-se rodar o código para cada um dos itemsets frequentes. Ele é aquele que está no topo dessa imagem; Embora não possa haver regra de associação onde $Y = \varnothing$
  - Dúvida: Ora, e por que não tem por exemplo a regra $a \to b$?
    - Resposta: essa regra teria sido calculada para o itemset frequente $ab$, afinal, se $abcd$ é frequente, $ab$ também é.

---

- Dessa forma, a geração das regras pode ser sistematizada em um procedimento similar ao usado no Apriori

[image: ICCBased(RGB,sRGB IEC61966-2.1), width: 445, height: 340, bpc: 8 Retirado de Algoritmo 6.3 de Tan et al.]

- **Algoritmo 6.3** - Procedure `ap-genrules`$(f_k, H_m)$
  - $k = |f_k|$ `\\ {tamanho do itemset frequente}`
  - $m = |H_m|$ `\\ {tamanho do consequente da regra}`
  - **if** $k > m + 1$ **then**
    - $H_{m+1} = \text{apriori-gen}(H_m)$
    - **for each** $h_{m+1} \in H_{m+1}$ **do**
      - $conf = \sigma(f_k) / \sigma(f_k - h_{m+1})$
      - **if** $conf \geq minconf$ **then**
        - **output** the rule $(f_k - h_{m+1}) \to h_{m+1}$
      - **else**
        - **delete** $h_{m+1}$ from $H_{m+1}$
      - **end if**
    - **end for**
    - **call** ap-genrules($f_k, H_{m+1}$)
  - **end if**

Retirado de Algoritmo 6.3 de Tan et al.

- [JV]
  - Entendendo o Algoritmo:
    - É basicamente o apriori;
    - O Apriori gen é basicamente o apriori, porém passando os consequentes.
  - Professor:
    - Ah, mas poderia usar outro algoritmo para gerar?
    - Resposta: Nunca vi. Afinal, precisa passar por todos.
  - Pode-se fazer um pós-processamento para apresentar os que são confiantes: ordenando por consequente, por confiança, etc.
  - Nisso daqui, o usuário final vai precisar filtrar algumas regras encontradas.
  - Buscamos encontrar regras inesperadas.
  - Exemplo: $(Café, Leite) \to Pão$ é trivial. Não tem tanto interesse por parte de um suposto stakeholder.

### Medidas de interesse

- Apesar do suporte e confiança fornecerem um bom mecanismo para filtragem de regras desinteressantes, elas também apresentam falhas
- Como foi discutido anteriormente, o filtro por suporte pode excluir da análise itens altamente lucrativos porém raros
  - [JV] Se o suporte for muito alto, só a trivialidade vai passar.
  - Diminuir o limiar de suporte mínimo inviabiliza a mineração dos padrões (tanto computacionalmente quanto no número de padrões retornados)
- Os problemas relacionados à confiança são mais sutis

---

- Considere uma base de dados com a avaliação da preferência de bebidas quentes de um grupo de pessoas
- A regra $chá \to café$ parece uma regra interessante, já que tem suporte=15% e confiança=75%
  - A interpretação dessa regra é: 15% das pessoas bebem ambas as bebidas e 75% das que bebem chá também bebem café
- Essa interpretação induz a conclusão de que o fato da pessoa beber chá influencia ela a beber café
  - Porém 80% das pessoas bebem café, logo o fato delas beberem chá influenciam negativamente o consumo de café

| Tabela de Contingência | Café | !Café | $\sum$ Linha |
| ---------------------- | ---: | ----: | -----------: |
| Chá                    |  150 |    50 |          200 |
| !Chá                   |  650 |   150 |          800 |
| $\sum Coluna$          |  800 |   200 |         1000 |

- [JV]
  - **Tabela de Contingência:** tabulação das contagens. Para cada par de variáveis categóricas, dá pra fazer isso. Em Aprendizado Preditivo dá pra ver qual foi o erro da predição das categorias.
  - Embora a relação $Chá \to Café$ represente uma regra de associação aparentemente boa, o café sozinho já é 80% então na realidade está reduzindo a quantidade de pessoas (ou algo assim).
  - Dúvida: Mas afinal, e a ideia de "não comprar tal coisa implica em comprar tal outro" também existe?
    - Sim, é chamado de Negative itemsets mining. Mas aumenta muito o tamanho do problema e também muitas coisas espúrias.
    - Há quem adicione categorias aos itens e mineram padrões a partir disso

---

- O problema anterior nos leva a conclusão de que padrões envolvendo itens mutuamente independentes ou que cubram poucas transações são desinteressantes
- Assim, outras medidas de interesse podem ser utilizadas para complementar a informação trazida pelo arcabouço suporte-confiança
- O mais comum na literatura é usar métricas de correlação como medidas de interesse
  - [JV] Correlação de variável discreta.

### Lift

- O problema identificado com a confiança é que ela sugeria uma correlação positiva entre os itemsets, enquanto, na verdade, existia uma correlação negativa
- O $lift$ é uma medida que avalia a independência entre os itemsets ou o quanto a ocorrência de um itemset 'eleva' a ocorrência de outro
- Ela é definida por
  - $lift(X,Y) = \frac{sup(X \cup Y)}{P(X) P(Y)} = \frac{conf(X \to Y)}{sup(Y)}$
    - [JV]
      - Qual a probabilidade deles acontecerem juntos vs a probabilidade deles acontecerem independentemente.
      - $lift(X,Y) = \frac{sup(X \cup Y)}{P(X) P(Y)} = \frac{sup(X \cup Y)}{P(X)} \cdot \frac{1}{P(Y)} = conf(X \to Y) \cdot \frac{1}{sup(Y)} = \frac{conf(X \to Y)}{sup(Y)}$
- Veja que:
  - Se o $lift(X,Y) = 1$, então $X$ e $Y$ são independentes;
  - Se o $lift(X,Y) < 1$, então $X$ e $Y$ são negativamente correlacionados; e
    - [JV] Dúvida: se eles são negativamente correlacionados, significa que $Y \to X$ é melhor do que $X \to Y$? Não. Só tende a considerar que pior, tipo o caso do chá e do café.
  - Se o $lift(X,Y) > 1$, então $X$ e $Y$ são positivamente correlacionados
- Para o exemplo das bebidas, $lift(chá, café) = \frac{0.15}{0.2 \times 0.8} = 0.9375$, indicando a correlação negativa observada anteriormente

#### Limitações do Lift

- Embora o lift seja bastante útil na prática, ele também apresenta limitações
- Considere uma situação de mineração de textos em que palavras sejam itens. Podemos avaliar a co-ocorrência de _data mining_ e _compiler mining_ nos textos através da métrica
  - Espera-se que as duas primeiras estejam positivamente correlacionadas enquanto as duas últimas não
- Supondo as tabelas ao lado, temos que o lift de data mining é 1.02 e de compiler mining é 4.08 para nossa surpresa
  - Mas o primeiro tem suporte 88% contra 2% do segundo
  - A confiança das regras $data \to mining$ e $compiler \to mining$ são 94.6% e 28.5%, o que parece mais razoável
  - [JV]
    - O cálculo do lift sozinho não adianta muito.
    - [Dúvida] Então o Lift seria usado em paralelo com o $minconf$?
      - **Resposta:** Sim. Na prática usamos os algoritmos e eles já cospem as métricas.

| X         | $p$ | $\bar{p}$ |   XX |
| --------- | --: | --------: | ---: |
| $q$       | 880 |        50 |  930 |
| $\bar{q}$ |  50 |        20 |   70 |
| XX        | 930 |        70 | 1000 |

| X         | $r$ | $\bar{r}$ |   XX |
| --------- | --: | --------: | ---: |
| $s$       |  20 |        50 |   70 |
| $\bar{s}$ |  50 |       880 |  930 |
| XX        |  70 |       930 | 1000 |

### Mathews' Correlation Coefficient (MCC)

- A correlação de Pearson é amplamente usada para variáveis contínuas, porém ela não se aplica a dados categóricos
  - [JV]
    - Gera acurácia de modelos, mesmo em bases de dados desbalanceados.
- A correlação de dados categóricos é medida pelo coeficiente phi ou Mathews' Correlation Coefficient (MCC)
- O MCC é computado através da tabela de contingência da seguinte forma
  - $\phi(X, Y) = ((N_{XY} \times N_{!X!Y}) - (N_{!XY} \times N_{X!Y})) / (N_X \times N_Y \times N_{!X} \times N_{!Y})$
    - [JV]
      - Professor: nenhum lugar explica a intuição dela.
- O coeficiente varia entre $-1$ e $+1$, sendo
  - $-1$ indicativo de correlação negativa
  - $+1$ correlação positiva
  - $0$ independência
- No caso do exemplo das bebidas, o valor do coeficiente é $-0.0625$ (ligeiramente negativamente correlacionado)

- [JV] Exemplo abaixo:

| XXX | X   | !X  |
| --- | --- | --- |
| Y   | a   | b   |
| !Y  | c   | d   |

- $\phi (X, Y) = (ad - bc)/(abcd)$

#### Limitações do MCC

- No caso do exemplo das palavras, se computarmos os coeficientes para ambos os casos, chegamos ao mesmo valor $0.232$
- A razão é que o coeficiente dá o mesmo peso para co-ocorrências e co-ausências. Nesse caso, a medida é mais adequada para variáveis simétrica
- A medida também é sensível mesmo a mudanças proporcionais no tamanho da amostra
  - [JV]
    - É mais usado em regra de associação do que...?
    - Até então temos nos baseados apenas no suporte, mas existem outras métricas de qualidade.

| X         | $p$ | $\bar{p}$ |   XX |
| --------- | --: | --------: | ---: |
| $q$       | 880 |        50 |  930 |
| $\bar{q}$ |  50 |        20 |   70 |
| XX        | 930 |        70 | 1000 |

| X         | $r$ | $\bar{r}$ |   XX |
| --------- | --: | --------: | ---: |
| $s$       |  20 |        50 |   70 |
| $\bar{s}$ |  50 |       880 |  930 |
| XX        |  70 |       930 | 1000 |

## Aula 15 | 08/05/2025 | Descoberta de subgrupos

### Revisando a aula anterior

- Lift: verificar correlação entre conjuntos de itemsets.
  - Problema: podia gerar correlações espúrias
- MCC: Avalia co-ocorrências e co-não-ocorrências.

### Chi-quadrado

- O teste do $\chi^2$(chi-quadrado) é muito usado para avaliar a dependência entre variáveis categóricas
- O teste é computado a partir da tabela de contingência das variáveis
  - Faz-se uma tabulação cruzada e computa-se a número de ocorrências de cada combinação da variáveis

|    X | $B$       | $!B$       | X        |
| ---: | --------- | ---------- | -------- |
|  $A$ | $N_{AB}$  | $N_{A!B}$  | $N_A$    |
| $!A$ | $N_{!AB}$ | $N_{!A!B}$ | $N_{!A}$ |
|    X | $N_B$     | $N_{!B}$   | Total    |

- [JV]
  - Poderia ter várias categorias se correlacionando.
  - Analisa-se o quanto elas excedem com relação a se elas fossem independentes.

---

- O valor da estatística $\chi^2$ é obtido computando-se a proporção do desvio entre o valor observado e esperado em cada célula da matriz
  - $\chi^2 = \sum_{i=1}^{n} \sum_{j=1}^{n} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}$, onde $O_{ij}$ e $E_{ij}$ são respectivamente os valores observados e esperados para cada célula
- O valor esperado é obtido assumindo-se a independência das variáveis
  - $E_{ij} = \frac{N_{i} \cdot N_{j}}{Total}$

---

- Uma vez computado o valor da estatística, pode-se usar uma tabela de valores críticos para estimar a probabilidade de se observar valores tão extremos quanto o calculado
  - Caso essa probabilidade seja relativamente pequena, rejeitamos a hipótese nula de independência entre as variáveis
  - No caso das tabelas $2x2$, o grau de liberdade é $1$ e o valor crítico para uma probabilidade de $0.05$ é $3.84 (P (\chi^2 \geq 3.84) = 0.05)$
    - [JV] Graus de liberdade é $(|linhas|-1)\cdot (|colunas|-1)$, que seriam "quantas outras variáveis eu tenho e que posso alterar para mudar..."
- Finalmente, descartada a independência das variáveis, compara-se o valor observado com o esperado para concluir o tipo de correlação

- [JV] Ele não vai entrar nas minúcias do $\chi^2$ porque não convém à disciplina.

---

- A tabela do exemplo anterior foi atualizada com os valores esperados
- O valor da estatística é $\chi^2 = 3.906$, o que é maior que o valor crítico
- Portanto, as variáveis são dependentes
- Como o valor observado para chá e café é ligeiramente inferior, conclui-se que elas são negativamente correlacionadas

| X    |      Café |     !Café |    - |
| ---- | --------: | --------: | ---: |
| Chá  | 150 (160) |   50 (40) |  200 |
| !Chá | 650 (640) | 150 (160) |  800 |
| X    |       800 |       200 | 1000 |

- [JV] O número entre parênteses é o cálculo do $E_{ij}$ onde ele calcula: Somatório da linha vezes somatório da coluna, dividido pelo total

### Cosseno

- A similaridade de cosseno é amplamente usada em aprendizado de máquina, sobretudo em aplicações envolvendo texto
- A medida pode ser adaptada para itemsets se visualizarmos suas coberturas como vetores binários
- Ela é formalmente definida por:
  - $Cosseno(X, Y) = \frac{X \cup Y}{\sqrt{\sup(X) \cdot \sup(Y)}}$
  - Ela também pode ser vista como a média geométrica das confianças das regras $X \to Y$ e $Y \to X$
  - [JV] Poderia também usar a métrica de Jaccard
- Os valores do cosseno variam entre 0 e 1, e indicam maior relação entre os itemsets quando estiver mais próximo de 1
- A vantagem é que ela depende somente das proporções das ocorrências de $X$, $Y$ e $X \cup Y$ (a ausência não é levada em conta como no MCC)

- [JV]
  - Essa do Cosseno é a menos utilizada. As que melhor expressam são o Lift e $\chi^2$
  - O problema é que com confiança de 5%, 5% dos itens são descartados.
  - Ele comenta sobre alguns que são ao acaso mas foi dito que não eram.
  - Estou confuso de que forma isso se dá com relação a falsos positivos e falsos negativos. Perguntar no final da aula

### Comparação das medidas

| Data Set |     $mc$ | $\overline{m}c$ | $m\overline{c}$ | $\overline{mc}$ | $\chi^2$ | **lift** | **cosine** |
| -------- | -------: | --------------: | --------------: | --------------: | -------: | -------: | ---------: |
| $D_1$    | $10.000$ |         $1.000$ |         $1.000$ |       $100.000$ | $90.557$ |  $ 9,26$ |     $0,91$ |
| $D_2$    | $10.000$ |         $1.000$ |         $1.000$ |           $100$ |      $0$ |   $1,00$ |     $0,91$ |
| $D_3$    |    $100$ |         $1.000$ |         $1.000$ |       $100.000$ |    $670$ |   $8,44$ |     $0,09$ |
| $D_4$    |  $1.000$ |         $1.000$ |         $1.000$ |       $100.000$ | $24.740$ |  $25,75$ |     $0,50$ |
| $D_5$    |  $1.000$ |           $100$ |        $10.000$ |       $100.000$ |  $8.173$ |   $9,18$ |     $0,29$ |
| $D_6$    |  $1.000$ |            $10$ |       $100.000$ |       $100.000$ |    $965$ |   $1,97$ |     $0,10$ |

- [JV]
  - Todas têm falhas
  - $D_1$
    - tem mais frequente que pessoas gostem de leite em café do que a soma de $\bar{m}c$ e $m\bar{c}$
    - Eles confirmam
  - $D_2$
    - Esse agora apresenta ainda mais intensamente a correlação, isso porque ele tem ainda mais proporção de correlação de MC com o todo.
    - O $\chi^2$ falha e não deveria
    - Lift falha. 1 indica que não tem correlação
    - Esses dois falham justamente porque eles dão muito enfoque no $\overline{MC}$
  - $D_3$
    - $\chi^2$ e Lift mostram que...
  - $D_4$
    - Realmente independentes
  - $D_5$
    - "Analisem depois, é interessante o resultado."
- "Subjetividade do unusualness"
  - Será necessário avaliar todas as métricas para poder confirmar se é relevante ou não.

### Leitura (Aula 14)

- Seção 6.7 Tan et al.
- Seção 6.4 Han et al.
- Capítulo 12 Zaki e Meira
