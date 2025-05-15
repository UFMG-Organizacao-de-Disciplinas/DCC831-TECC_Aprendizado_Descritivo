# Resumo por aula

## Slide 08, Aula 14 - Regras de associação e métricas de interesse

## Introdução

Para extrair regras de associação, primeiro precisamos minerar padrões frequentes, e depois gerar as regras de interesse à partir dos padrões.

O "interesse" é subjetivo e varia conforme a aplicação; para medi-lo usam-se métricas. Uma delas tem sido o uso do suporte, que nos assegura o uso de padrões frequentes.

## Regras de associação

- "Uma regra de associação é uma implicação lógica do tipo $X \to Y$ em que $X$ e $Y$ são itemsets"

Antes de seguirmos para as próximas informações, elaboremos mais com algumas informações que ele deu em aula e que não foram apresentadas até então nos slides:

Nessa implicação lógica, o primeiro termo é chamado de **antecedente**, enquanto que o segundo é chamado de **consequente**.

Agora algumas regrinhas gerais:

1. $X \neq Y \neq \varnothing$
2. Considerando que $A$ é o conjunto de itens, a maior quantidade possível de regras de associação é dada pela fórmula $2^k - 2$
   1. $|A| = k; |\mathcal{P}(A)| = 2^k$
      1. Obs.: $\mathcal{P}(A) =$ o conjunto potência de A, ou seja, o conjunto de todos os possíveis subconjuntos entre os itens de A, sem repetições e contendo o conjunto vazio.
   2. Porém, como o menor item é $\varnothing$ e isso não pode ocorrer; Além disso, digamos que $X = \varnothing$. Isso implicaria que $Y = a_1 a_2 \dots a_k$
   3. Sendo assim, de todo o conjunto potência, excluem-se dois itens extremos: o menor ($\varnothing$) e o maior ($a_1 a_2 \dots a_k$)
   4. Assim resultando em $2^k - 2$

Com isso voltemos ao conteúdo

Agora são apresentados duas métricas de interesse/representatividade:

- Suporte: $sup(X \to Y) = \frac{sup(X \cup Y)}{|D|}$
  - Podemos entendê-lo como sendo "Qual a frequência de aparição simultânea dos itens de X e Y em todas as transações?"
    - Ilustrando a união: $X=ab, Y=cd; X \cup Y = abcd$
- Confiança: $conf(X \to Y) = \frac{sup(X \cup Y)}{sup(X)}$
  - Podemos entendê-lo como sendo "Qual a frequência de aparição simultânea dos itens de $X$ e $Y$ dado o número de aparições de $X$?"
  - Com isso, surge também o $minconf$ que é o valor mínimo de confiança que se precisa ter para considerar que há confiança em determinada implicação.

Embora as métricas ajudem a guiar para regras valorosas, ainda assim elas podem gerar falsos positivos.

---

Usualmente, um dos crivos que uma regra precisa satisfazer é a do suporte mínimo, e portanto, geralmente se avaliam apenas os itemsets frequentes.

Para a geração de regras, consideramos a seguinte equação:

- $r(X) = \lbrace (X - Y) \to Y | Y \subseteq X \text{ e } 0 < |Y| < k \rbrace$
- $r(it\_freq) = \{ (it\_freq - conseq) \to conseq | conseq \subseteq it\_freq \text{ e } 0 < |conseq| < |it\_freq| \}$
  - Onde:
    - $it\_freq:$ um dos itemsets frequentes gerados pela mineração de padrões frequentes.
    - $conseq:$ é o consequente, aquele que buscamos verificar a implicação
- Entendimento geral dessa função: para determinado item frequente passado como parâmetro, para cada um dos possíveis subconjuntos
