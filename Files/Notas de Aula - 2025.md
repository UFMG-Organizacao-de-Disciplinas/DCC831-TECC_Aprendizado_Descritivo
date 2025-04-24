# Aprendizado Descritivo - Renato Vimieiro - 2025.1

<!-- ‘’ -->

## Aula 01 | 18/03/2025 | Apresentação do curso - [JV: Cheguei atrasado]

### Slide 1 - aula01-intro

#### Introdução

- Quando falamos sobre aprendizado de máquina e mineração de dados, frequentemente associamos essas expressões a predição de valores
- Mais especificamente, temos a ideia de que aprendizado de máquina (AM) se resume a, dada uma entrada X, encontrar uma função f(X) que retorne o valor de uma variável alvo Y
  - Quando a variável alvo Y é categórica, chamamos o problema de **classificação**
  - Quando a variável alvo Y é contínua, chamamos o problema de **regressão**
- Assim, o senso comum define AM como aprender uma função f capaz de predizer valores para dados ainda não coletados
- Essa definição, embora restritiva, é correta para a classe de tarefas elencadas acima, chamadas de **aprendizado preditivo**

#### Aprendizado Preditivo

- Mais especificamente ainda, esse imaginário popular define o que conhecemos por aprendizado supervisionado de modelos preditivos
- De maneira mais formal, o objetivo dessas técnicas é aprender uma função cujo domínio é um conjunto de instâncias $\mathcal{X}$, e contradomínio um conjunto de saídas $\mathcal{Y}$
- Para tal, o algoritmo recebe um conjunto de pares $(x, l(x)) \in \mathcal{X} \times \mathcal{L}$
  - A função $l(x)$ retorna o valor de saída esperado para a instância x
- Como o algoritmo obtém o modelo guiado por esse conjunto de entrada (treinamento), a tarefa é classificada como 'supervisionada', já que $l(x)$ faz o papel de 'professor'
- Da mesma forma, como o modelo aprendido é usado para predizer valores de saída de novas instâncias, ele é chamado de preditivo

- JV
  - O que desejamos é receber informações e conseguir retornar um rótulo.
  - Nem todos de aprendizado de máquina levam em consideração os rótulos.
  - Aprendizado supervisionado preditivo
  - [JV: não anotei sobre o que seria o supervisionado]
  - Se tiver que explicar como funciona, aí é a área de Explanable AI.
  - Aqui é mais importante o resultado do que o processo.

---

- Como queremos que o modelo seja fiel à realidade e, portanto, consiga capturar a relação entre instância (entrada) e saída, é comum, nesse cenário, avaliarmos sua qualidade comparando os valores obtidos com os verdadeiros para um conjunto de instâncias chamado de conjunto de validação
- Ou seja, nesse tipo de tarefa temos o seguinte fluxo de trabalho:

---

```mermaid
flowchart LR
  Trat[(Tratamento)]
  Cons[Construção]
  Ava[Avaliação]
  Uso["Uso (Modelo)"]
  Val[(Validação)]
  Trat --> Cons
  Cons --> Ava
  Ava --> Uso
  Ava --> Cons
  Val --> Ava
```

Aqui, não queremos obter nenhum entendimento sobre o que já vimos antes, mas sim, ter meios de prever como serão classificados os próximos itens que veremos.

---

- Embora métodos de regressão e classificação (aprendizado supervisionado) sejam os -ais populares em AM, existem outras abordagens preditivas que não requerem a variável -lvo para ajustarem modelos
- Técnicas que não utilizam essas variáveis são classificadas como **não-supervisionadas**
- Uma tarefa de aprendizado não-supervisionado bastante popular é a de agrupamento (clustering)
- Essa tarefa consiste em encontrar subgrupos de elementos homogêneos nos dados

---

---

- [JV]
  - Exemplo: câncer de mama
    - Separando mulheres cuja quimioterapia foram eficazes e as que não foram.
    - Analisar quais os mapeamentos genéticos delas
    - Verificar de que forma há uma relação entre os mapeamentos genéticos e a eficácia da quimioterapia.
    - E com isso, tentar predizer se a quimioterapia será eficaz ou não para uma nova paciente.
  - No aprendizado não supervisionado não há rótulos.
  - Uma tarefa de aprendizado não-supervisionado bastante popular é a de agrupamento (clustering)
    - Um dos mais conhecidos é o k-menas

---

- Em outras palavras, a tarefa de agrupamento consiste em detectar grupos de instâncias que sejam mais parecidas entre si do que com as de outros grupos
- Sob a ótica de aprendizado preditivo, a tarefa consiste em encontrar uma função $q: \mathcal{X} \rightarrow \mathcal{C}$, cujo domínio $\mathcal{X}$ é um conjunto de instâncias, e o contradomínio 𝒞 um conjunto de grupos (clusters)
- Note que a tarefa se assemelha à de classificação (já que os rótulos dos grupos são categóricos), porém o ajuste do modelo não leva em consideração rótulos pré-definidos
- Um exemplo de método aprendizado preditivo não-supervisionado é o K-Means
  - O modelo são os centroides e a distância euclidiana
  - Novas instâncias são alocadas nos clusters de cujos centroides elas sejam mais próximas de acordo com a distância euclidiana

#### Aprendizado Descritivo

- Aprendizado descritivo tem como objetivo central obter uma descrição para os dados
  - Isto é, o objetivo é encontrar um **modelo descritivo** para os dados
- Dessa forma, podemos apontar a primeira diferença para aprendizado preditivo:
  - Não temos mais a necessidade de dividir o conjunto de instâncias em treinamento e validação
- A divisão entre treinamento e validação não faz mais sentido, pois queremos obter um modelo para os dados que temos em mãos
- Consequentemente, a avaliação dos resultados (modelos) se torna mais difícil, já que não temos mais uma 'verdade absoluta' para compararmos as saídas

- JV
  - > A premissa é "eu não sei nada sobre os dados", "então preciso encontrar um modelo que descreva os dados"
  - "Estatística não é boa para descrever grafos"
  - O Descritivo é tão importante quanto prever coisas, mas atuam em momentos diferentes.

---

- Por outro lado, segundo Flach (2012), _o aprendizado descritivo leva à descoberta genuína de novos conhecimentos, e, dessa forma, está situado entre as áreas de mineração de dados e aprendizado de máquina_
- O objetivo de se buscar um modelo descritivo dos dados se justifica nas situações em que se quer responder perguntas do tipo “o quê aconteceu?”
- Ou seja, esses modelos descrevem situações passadas e, assim, auxiliam no processo de tomada de decisão Aprendizado

- JV

  - O aprendizado descritivo leva a descoberta e novos conhecimentos. Estando entre mineração de dados e aprendizado de máquina.
  - Busca responder "o quê aconteceu?"
  - Descrevem situações passadas e com isso auxiliam no processo de **tomada de decisão**.

  - 4 paradigmas científicos
    - Indução, teórico, ...
  - Antes viam o fenômenos, criavam teorias, tentavam provar que as teorias se aplicavam.
  - Atualmente usamos um modelo baseado em dados
    - Veem como os dados se comportas, criam teorias e tentam provar que os dados se comportam de acordo com a teoria.

---

- Considere a seguinte situação em que um grande _Market place_ deseja reduzir os custos de distribuição dos produtos que ele vende
- Uma prática muito utilizada atualmente é manter centros de distribuição regionais para estocar produtos vendidos frequentemente, reduzindo o custo e tempo de transporte, e, consequentemente, aumentando a satisfação dos clientes
- Apesar da estocagem de produtos populares nas regionais ser uma decisão trivial, ela pode ser aprimorada analisando-se o histórico de vendas
- Nesse histórico, podemos encontrar itens menos populares que, com certa frequência, são adquiridos junto com os mais populares

  - Isso nos permite decidir estocar também esses produtos menos populares, em menor quantidade, mas evitando, assim, um custo maior de se enviar tais produtos individualmente de centros mais distantes

- JV
  - Uma das coisas feitas nessa disciplina é a busca por regularidades de acontecimentos em conjuntos.
  - Há uma interseção bem grande entre aprendizado descritivo e Mineração de Dados.

---

- Considere um segundo caso real em que executivos do Wal-Mart utilizaram de AM para aumentar as vendas diante da ameaça do furação Frances em 2004
- Enquanto o furacão atravessava o Caribe, os executivos queriam prever os produtos que seus clientes consumiam diante de catástrofes

- JV
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

---

- O objetivo dos executivos do Wal-Mart era abastecer as lojas da Flórida, que estava no caminho do furacão, e assim aumentar as vendas
- Novamente, a decisão trivial seria aumentar o estoque de pilhas, água mineral, lanternas, e produtos não perecíveis
- A análise do histórico de vendas, nesse caso, poderia retornar que as lojas venderam todo o estoque de DVDs de um gênero específico de filmes
- No entanto, ao analisar os dados, eles chegaram à conclusão de que havia um aumento de 7x nas vendas de Pop Tarts sabor morango, e o campeão do aumento de vendas era cerveja

---

- Apesar do caso ter sido abordado como um exemplo de aprendizado preditivo na matéria, ele é um exemplo claro de aprendizado descritivo supervisionado
- Especificamente, ele é um caso claro da aplicação de excepcional model mining
  - Queremos encontrar padrões de vendas não usuais, isto é, detectar aumento da venda de produtos que esteja correlacionado positivamente a um evento de interesse
- O único porém é que essa tarefa foi inicialmente proposta somente em 2008, 4 anos após o evento!

#### Aprendizado Descritivo X Preditivo

- Os exemplos ilustram bem a aplicabilidade do aprendizado descritivo:
  - Como dito, eles revelam o que ocorreu no passado e auxiliam na tomada de decisão de eventos futuros
- De forma análoga, os modelos preditivos utilizam dados históricos para prever o comportamento de dados futuros
- Note que a diferença, portanto, é bem tênue entre as duas abordagens
  - A diferença mais aparente é a intervenção humana no primeiro, contra um certo automatismo da segunda

---

- Um exemplo dessa diferença tênue entre as duas abordagens é justamente a tarefa de agrupamento
- Incialmente apresentamos clustering como uma tarefa de aprendizado preditivo não-supervisionado
- A mesma tarefa, porém, pode ser apresentada como descritiva
- O objetivo no agrupamento descritivo é obter uma função $q: \mathcal{D} \to \mathcal{C}$, que mapeia as instâncias coletadas no conjunto de dados $\mathcal{D}$ a grupos específicos (clusters) $\mathcal{C}$
  - A diferença aqui é que assumimos como domínio apenas o conjunto de instâncias em mãos, e não toda população de instâncias possíveis
  - Ou seja, o resultado do nosso agrupamento é 'apenas' uma divisão das instâncias em grupos, permitindo a análise de similaridade entre elas; não estamos interessados em alocar novas instâncias aos grupos encontrados

---

[Imagem: Agrupamento preditivo//Agrupamento Descritivo]

No modelo Preditivo, tenta-se definir limites para que próximos itens sejam classificados de acordo com o que foi visto anteriormente.

Já no Descritivo, tenta-se encontrar padrões que descrevam o que foi visto anteriormente.

---

- Considere agora um exemplo mais relacionado ao segundo estudo de caso discutido anteriormente
- Suponha que nosso conjunto de entrada rotulado seja o seguinte
- Podemos traçar dois objetivos aqui:
  - Separar círculos de quadrados, para classificar novos pontos como um ou outro
  - Buscar padrões nos dados para entender as diferenças entre círculos e quadrados

[Imagem: Distribuição de quadrados azuis e círculos vermelhos]

No exemplo apontado pode-se separar as distribuições dos pontos em 4 quadrantes, isso baseado na estimativa do que já ocorreu antes, busca então estimar onde estarão posicionados os quadradinhos azuis e as bolinhas vermelhas.

É importante também identificar quais são as regularidades existentes em certos padrões irregulares.

---

- O primeiro objetivo induz uma abordagem preditiva
- Logo, o abordamos como um problema de classificação

Às vezes usa-se o mesmo modelo entre preditivo e descritivo, porém, um pra descrever e o outro pra predizer.

[Imagem: Distribuição dos pontos]

---

- O segundo objetivo induz a uma abordagem descritiva
- Logo, abordamos o problema como uma tarefa de descoberta de subgrupos
- [JV]
  - $\sigma_1 \equiv x_1 \in [0.3, 0.7) \wedge x_2 \geq 0.9$
  - $\sigma_2 \equiv x_1 \in [0.275, 0.7) \wedge x_2 \leq 0.1$

[Imagem: Definindo grupo independente]

---

- Esse último exemplo mostra uma característica que frequentemente diferencia as duas abordagens
- As abordagens preditivas buscam ajustar modelos que aprendam as regularidades globais dos dados
  - No exemplo, encontrar as fronteiras que separam círculos de quadrados
- As abordagens descritivas, por outro lado, ajustam modelos que aprendam regularidades locais dos dados, i.e., padrões válidos apenas a subgrupos específicos
  - No exemplo, intervalos das variáveis que descrevem subgrupos com uma distribuição não usual de círculos e quadrados Leitura

#### Leitura - Aula 01

- Capítulo 3, Flach (2012)

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

### Slide - aula02-FIM

#### Introdução - Aula 2

- Hoje iremos focar num dos modelos mais conhecidos de aprendizado descritivo: mineração de regras de associação
- O problema foi inicialmente proposto pelos executivos do Wal-Mart para descoberta de padrões de consumo nos supermercados
- Por essa razão, muitas vezes a área é também conhecida, sobretudo em inglês, como _Market basket analysis_
- Contudo, diversas aplicações podem tirar proveito desse tipo de modelo
- Antes de entrarmos nos detalhes técnicos, vamos analisar um estudo de caso

---

- Kosinski et al. (2013), um grupo de pesquisadores da Universidade de Cambridge, -oletaram dados sobre a personalidade e gostos de usuários do Facebook através do aplicativo MyPersonality
- O objetivo do trabalho foi demonstrar que 'curtidas' do Facebook poderiam ser usadas -ara predizer com acurácia informações sensíveis dos usuários
- O app posteriormente foi relacionado ao escândalo do Cambridge Analytica; e os dados em si são carregados de controvérsia
- Embora seja um exemplo negativo, ele ilustra bem a utilidade da tarefa que estudaremos hoje

- JV
  - Kosinski (2013) coletavam dados das personalidades através do MyPersonality.
    - Escândalo do Cambridge Analytica
  - Buscava predizer a personalidade baseado nas curtidas feitas no Facebook

---

- Em resumo, os desenvolvedores do app coletaram uma série de dados de voluntários, mas, em particular suas 'curtidas' no site
- Provost e Foster (2013) utilizaram esses dados para demonstrar como a modelagem descritiva traz informações úteis
- Seguem alguns exemplos de regras:

- JV
  - Provost e Foster (2013) utilizaram os dados para demonstrar a modelagem descritiva e as informações úteis.
  - Alguns exemplos de regras:
    - Selena Gomez -> Demi Lovato
    - Linking Park & Disturbed & System of a Down & Korn -> Slipknot
    - SpongeBob SquarePants & Converse [JV: empresa do All Stars] -> Patrick Star
    - Skittles & Mountain Dew -> Gatorade

[JV: Offtopic: o diretor da Google daqui fez doutorado no PPGCC]

---

- Note que a ideia de itens em uma cesta de compras da aplicação original pode ser generalizada para itens virtuais
- O objetivo aqui é encontrar co-ocorrências de itens de análise que sejam interessantes
- O exemplo traz novamente padrões de consumo
  - Majoritariamente de consumo de músicas, mas, como intencionado pelo estudo original, revela traços de personalidade dos usuários
- Respeitados os limites éticos e legais, essas informações são úteis em diversos contextos: campanhas de marketing, desenvolvimento de produtos, ...

- JV
  - A ideia de itens em cesta de compra pode ser generalizada para itens virtuais
  - Busca-se encontrar co-ocorrências de itens de análise
  - Dados os limites éticos, pode-se usar essa análise para se atingir diversos objetivos.

#### Itemset e Tidsets

- Chamamos os elementos do conjunto $I = \{x_1, x_2, \dots, x_m\}$ de itens
- Esses elementos são as variáveis de análise que estamos considerando
- Um conjunto $X \subseteq I$ é chamado de _itemset_
- Um itemset de tamanho k é chamado de k-itemset
- Denotamos o conjunto de todos os k-itemsets por $I^{(k)}$
- Similarmente, como estamos lidando com 'transações', vamos identificá-las individualmente por IDs, que serão chamados de tids
- Logo, o conjunto $T = \{t_1, t_2, \dots, t_n\}$ é o conjunto de transações consideradas, identificadas pelos seus respectivos tids

- JV
  - Os "produtos" da cesta de compras são chamados de "Itens".
    - $I = \{x_1, x_2, \dots, x_m\}$
  - Esses elementos serão as **variáveis de análise**
  - Um conjunto $X \subseteq I$ é chamado de **Itemset**
  - Um itemset de tamanho $k$ é chamado de **k-itemset**
  - Denotamos o conjunto de todos os **k-itemsets** por $I^(k)$
  - Todas as "Transações" serão identificadas por IDs, ou então, **TID** (Transaction ID)
  - O conjunto $T = \{t_1, t_2, \dots, t_n\}$ é o conjunto das transações.

---

- O conjunto $Y \subseteq T$ é chamado de _tidset_
- É conveniente assumir que tanto os itemsets quanto os tidsets são sempre armazenados ordenados pela ordem lexicográfica dos itens e transações (seja ela qual for)
- Cada transação consiste de um identificador (tid) e um conjunto de itens
  - Ou seja, cada transação é um par $(t, X)$ em que $t \in T$ e $X \subseteq I$
- Formalmente, um conjunto de dados será uma tripla $(T, I, D)$

  - T e I são os conjuntos de tids e itens
  - $D \subseteq T \times I$ é uma relação binária em que $(t, i) \in D \bicond i \in X$ na transação $(t, X)$
  - Dizemos que a transação t **contém** o item i

- JV
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

- Exemplo:
  - I = {muesli, oats, milk, yoghurt, biscuits, tea}
  - T = {1,2,3,4,5,6}
  - (1, {muesli, milk, yoghurt, tea})
  - 5 contém {milk, tea}

Ou seja: $t$ contém $X$ se $|X - t| = 0$

| TID | Muesli | Oats | Milk | Yoghurt | Biscuits | Tea |
| --: | -----: | ---: | ---: | ------: | -------: | --: |
|   1 |      1 |    0 |    1 |       1 |        0 |   1 |
|   2 |      0 |    1 |    1 |       0 |        0 |   0 |
|   3 |      0 |    0 |    1 |       0 |        1 |   1 |
|   4 |      1 |    0 |    0 |       1 |        0 |   0 |
|   5 |      0 |    1 |    1 |       0 |        0 |   1 |
|   6 |      1 |    0 |    1 |       0 |        0 |   1 |

---

- Dado um itemset $X$, podemos querer saber o conjunto de transações que o contém.
- Esse conjunto é chamado de **extensão** ou **cobertura** de $X$
- Ele é definido pela seguinte função:
  - $c: P(I) \to P(T)$
  - $c(X) = \{t \in T | \forall i \in X(t, i) \in D\}$
- Dado um tidset Y, podemos querer saber o maior conjunto de itens comuns às transações de Y.
- Esse conjunto é chamado de **intensão** (Não é intenção!) de Y.
- Ele é definido por
  - $i: P(T) \to P(I)$
  - $i(Y) = \{x \in I | \forall t \in Y(t, x) \in D\}$

O uso de extensão e intensão vêm da ideia filosófica e semiótica de que a extensão é o conjunto de coisas que se encaixam em uma definição, enquanto a intensão é a definição em si.

---

- Exemplos:
  - $i(\{1, 5, 6\}) = \{milk, tea\}$
  - $c(\{milk, tea\}) = \{1, 3, 5, 6\}$
  - $c(\{muesly, oats\}) = ?$
  - $i({4, 5}) = ?$

| TID | Muesli | Oats | Milk | Yoghurt | Biscuits | Tea |
| --: | -----: | ---: | ---: | ------: | -------: | --: |
|   1 |      1 |    0 |    1 |       1 |        0 |   1 |
|   2 |      0 |    1 |    1 |       0 |        0 |   0 |
|   3 |      0 |    0 |    1 |       0 |        1 |   1 |
|   4 |      1 |    0 |    0 |       1 |        0 |   0 |
|   5 |      0 |    1 |    1 |       0 |        0 |   1 |
|   6 |      1 |    0 |    1 |       0 |        0 |   1 |

Intensão: conjunto de itens comuns a todos os elementos de um determinado conjunto de transações.

Extensão: o conjunto de transações que contenham um determinado conjunto de itens.

Intensão: a interseção das linhas
Extensão: a interseção das colunas

#### Representações de conjuntos de dados

- As funções de intensão e cobertura permitem representar de diferentes formas a definição de conjunto de dados apresentada anteriormente
- Por exemplo, podemos enxergar o conjunto de dados como um conjunto de transações e suas respectivas intensões
  - Ou seja, ele é um conjunto de $(t, i(t))$
  - Essa representação é chamada de **horizontal**
- Similarmente, podemos enxergar o conjunto de dados como um conjunto de itens e suas coberturas
  - Ou seja, como um conjunto de $(x, c(x))$
  - Essa representação é chamada de **vertical**

---

- Horizontal

| **t** |                   **i(t)** |
| ----: | -------------------------: |
|     1 | Muesli, Milk, Yoghurt, Tea |
|     2 |                 Oats, Milk |
|     3 |        Milk, Biscuits, Tea |
|     4 |            Muesli, Yoghurt |
|     5 |            Oats, Milk, Tea |
|     6 |          Muesli, Milk, Tea |

|    **t** | 1                          | 2          | 3                   | 4               | 5               | 6                 |
| -------: | -------------------------- | ---------- | ------------------- | --------------- | --------------- | ----------------- |
| **i(t)** | Muesli, Milk, Yoghurt, Tea | Oats, Milk | Milk, Biscuits, Tea | Muesli, Yoghurt | Oats, Milk, Tea | Muesli, Milk, Tea |

- Vertical

|    **x** |  Muesli | Oats |          Milk | Yoghurt | Biscuits |        Tea |
| -------: | ------: | ---: | ------------: | ------: | -------: | ---------: |
| **t(x)** | 1, 4, 6 | 2, 5 | 1, 2, 3, 5, 6 |    1, 4 |        3 | 1, 3, 5, 6 |

|    **x** |      **t(x)** |
| -------: | ------------: |
|   Muesli |       1, 4, 6 |
|     Oats |          2, 5 |
|     Milk | 1, 2, 3, 5, 6 |
|  Yoghurt |          1, 4 |
| Biscuits |             3 |
|      Tea |    1, 3, 5, 6 |

#### Conjuntos de itens frequentes e Regras de Associação

- A identificação de regras tais como as que vimos no exemplo no início da aula, em geral, envolvem duas etapas
  - Mineração de conjuntos de itens frequentes
  - Descoberta de regras de associação interessantes
- A primeira parte é computacionalmente mais intensa e, por esta razão, é a que recebeu mais atenção dos pesquisadores
- Por isso, vamos inicialmente nos concentrar nessa tarefa

#### Mineração de Conjuntos de itens frequentes

- Uma definição de "regra interessante" é ela ocorrer com certa frequência.
- Então é necessário definir um limiar entre o que é frequente e o que é infrequente
  - Esse limiar é chamado de suporte mínimo (minsup)
- O suporte de um itemset é o tamanho de sua cobertura
  - $sup(X) = |c(X)|$
- Como essa definição é dependente do contexto, admite-se também a definição do suporte relativo
  - $rsup(X) = |c(X)| / |T|$

---

- Dessa forma, dizemos que um itemset é frequente sse $sup(X) \geq minsup$
- Exemplos, considerando $minsup=2$:
  - $\{milk\}; sup(\{milk\}) = 5$
  - $\{milk, tea\}; sup(\{milk, tea\}) = 4$
  - $\{muesli, oats, milk\}$?
  - $\{muesli, milk\}$?

| TID | Muesli | Oats | Milk | Yoghurt | Biscuits | Tea |
| --: | -----: | ---: | ---: | ------: | -------: | --: |
|   1 |      1 |    0 |    1 |       1 |        0 |   1 |
|   2 |      0 |    1 |    1 |       0 |        0 |   0 |
|   3 |      0 |    0 |    1 |       0 |        1 |   1 |
|   4 |      1 |    0 |    0 |       1 |        0 |   0 |
|   5 |      0 |    1 |    1 |       0 |        0 |   1 |
|   6 |      1 |    0 |    1 |       0 |        0 |   1 |

---

- O espaço de busca do problema é o conjunto potência do conjunto de itens
- Se considerarmos a relação de subconjuntos como uma relação de ordem parcial, temos que o espaço de busca é estruturado como um reticulado
  - Esse reticulado pode ser visualizado como um grafo, onde somente as relações diretas são representadas
  - Ou seja, se $A \subseteq B \wedge |A| = |B| - 1$, então existe uma aresta entre A e B no diagrama
- Assim, a mineração de conjunto de itens frequentes é resolvida por uma 'simples' busca no reticulado associado
- Essa busca pode ser tanto uma busca em largura quanto em profundidade
  - De fato, existem abordagens baseadas em ambas as buscas
- No entanto, a maioria das abordagens compartilham a mesma estrutura de busca:
  - Identificam candidatos navegando o espaço de busca
  - Computam o suporte desses candidatos, descartando os infrequentes

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

- JV
  - O espaço de busca do problema é o conjunto potência do conjunto de itens
  - Se considerarmos a relação de subconjuntos como uma relação de ordem parcial, temos que o espaço de busca é estruturado como um reticulado
    - Esse reticulado pode ser visualizado como um grafo, onde somente as relações diretas são representadas
    - Ou seja, se $A \subseteq B \land |A| = |B| - 1$, então existe uma aresta entre A e B no diagrama

Aquele diagrama explica bastante o que que isso quis dizer. Basicamente, no conjunto potência, cada nível vai ter um elemento a mais que o nível anterior.

#### Algoritmo Ingênuo

- Vamos considerar uma abordagem ingênua para a mineração de itens frequentes, antes de explorarmos outros mecanismos
- Independentemente da escolha da forma de busca, devemos enumerar os possíveis candidatos, e, em seguida, computar seu suporte
- Especificamente, devemos enumerar cada itemset possível; e depois verificar no conjunto de dados quais transações contêm esse itemset

---

Complexidade do algoritmo: $O(2^I \cdot T \cdot I)$

- **// ALGORITHM 8.1. Algoritm BruteForce**

  - **BruteForce** $(D, \mathcal{I}, minsup)$:

    - $\mathcal{F} \leftarrow \emptyset$ // set of frequent itemsets
      - **foreach** $X \subseteq \mathcal{I}$ **do**
        - $sup(X) \leftarrow ComputeSupport (X, D)$
        - **if** $sup(X) \leq minsup$ **then**
          - $\mathcal{F} \leftarrow \mathcal{F} \cup {(X, sup(X))}$
      - **return** $\mathcal{F}$

  - **ComputeSupport** $(X, D)$:
    - $sup(X) \leftarrow 0$
    - **foreach** $\langle t, i(t) \rangle \in D$ **do**
      - **if** $X \subseteq i(t)$ **then**
        - $sup(X) \leftarrow sup(X) + 1$
  - **return** $sup(X)$

---

- A computação do suporte de um itemset requer uma passada sobre o conjunto de dados, ou seja, requer tempo $O(|T|)$
- Verificar se uma dada transação contém um itemset requer tempo $O(|I|)$
- Portanto, o custo total de computação do suporte é $O(|T|)$
- O espaço de busca, por sua vez, é o conjunto potência de $I$. Logo, a complexidade do algoritmo ingênuo é $O(2^I \cdot I \cdot T)$

---

- A complexidade do espaço de busca é inerente ao problema. Contudo o algoritmo é ineficiente mesmo em espaços pequenos
- Note que o conjunto de dados não é mantido em memória, portanto a computação do suporte torna o algoritmo impraticável
- Os algoritmos mais "sofisticados" atacam majoritariamente o problema de computação de suporte, evitando computações desnecessáris, e/ou adotando estratégias mais eficientes para computá-lo.

Então temos dois problemas principais: reduzir o espaço de busca e reduzir a complexidade para calcular o suporte.

#### Leitura - Aula 02

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
    - $sup(X) = |c(X)|$, onde $c(X)$ é a cobertura do itemset $X$.

Mas o que é mesmo a cobertura?

- A cobertura é o conjunto de transações que contém um itemset $X$. Ou seja, é o conjunto de transações que contém todos os itens do itemset $X$.

#### Apriori

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
  - $\mathcal{F} \leftarrow \emptyset$
  - $\mathcal{C}^{(1)} \leftarrow \{\emptyset\}$ `// Initial prefix tree with single items`
  - **foreach** $i \in \mathcal{I}$ **do** Add $i$ as child of $\emptyset$ in $\mathcal{C}^{(1)}$ with $sup(i) \leftarrow 0$
  - $k \leftarrow 1$ `// k denotes the level`
  - **while** $\mathcal{C}^{(k)} \neq \emptyset$ **do**
    - ComputeSupport $(\mathcal{C}^{(k)}, D)$
    - **foreach** _leaf_ $X \in \mathcal{C}^{(k)}$ **do**
      - **if** $sup(X) \geq minsup$ **then** $\mathcal{F} \leftarrow \mathcal{F} \cup \{(X, sup(X))\}$
      - **else** remove $X$ from $\mathcal{C}^{(k)}$
    - $\mathcal{C}^{(k+1)} \leftarrow$ ExtendPrefixTree($\mathcal{C}^{(k)}$)
    - $k \leftarrow k+1$
  - **return** $\mathcal{F}^{(k)}$

---

- ComputeSupport $(\mathcal{C}^{(k)}, D)$:

  - **foreach** $\langle t, i(t) \rangle \in D$ **do**
    - **foreach** k-subset $X \subseteq i(t)$ **do**
      - **if** $X \in \mathcal{C}^{(k)}$ **then** $sup(X) \leftarrow sup(X) + 1$

- ExtendPrefixTree $(\mathcal{C}^{(k)})$:
  - **foreach** leaf $X_a \in \mathcal{C}^{(k)}$ **do**
    - **foreach** leaf $X_b \in SIBLING(X_a)$, such that $b > a$ **do**
      - $X_{ab} \leftarrow X_a \cup X_b$ `// prune candidate if there are any infrequent subsets`
      - **if** $X_j \in \mathcal{C}^{(k)}$, **for all** $X_j \subset X_{ab}$, such that $|X_j| = |X_{ab}|-1$ **then**
        - Add $X_{ab}$ as child of $X_a$ with $sup(X_{ab}) \leftarrow 0$
    - **if** _no extensions from_ $X_a$ **then**
      - Remove $X_a$, and all ancestors of $X_a with no extensions, from $\mathcal{C}^{(k)}$
  - **return** $\mathcal{C}^{(k)}$

---

- Exemplo (minsup=3):

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
  - O tamanho dos candidatos aumenta -> Mais candidatos são avaliados em cada nível -> o tamanho dos conjuntos frequentes aumenta -> mais níveis são explorados

[Imagem(a): Number of candidate itemsets]

[Imagem(b): Number of frequent itemsets]

---

- A densidade da base de dados também tem muito impacto no custo
  - Transações passam a ter mais itens
  - Isso tem duas implicações: tamanho médio dos itemsets aumentam; mais subconjuntos são gerados durante a contagem do suporte $\binom{|t|}{k}$

[Imagem(a): Number of candidate itemsets]

[Imagem(b): Number of frequent itemsets]

#### Eclat - Próxima aula

## Aula 04 | 27/03/2025 | Mineração de conjuntos de itens

### Aula passada

- Algoritmo apriori
- Frequente, infrequente.
- Como calcula o suporte
  - A partir dos itens frequentes: tabelas de 0 e 1.
  - Pra isso usava árvore de prefixos
  - Para cada transação gerava os itemsets de tamanho k, ia na árvore de prefixos
  - E incrementava o suporte daquela chave

[JV: escrevi o que ele tá falando, mas não tô entendendo]

- Duas coisas influenciam o desempenho do algoritmo
  1. Ele falou algo
  2. Se o BD é denso, as transações são mais largas.
- $\binom{|t|}{k}$
- Quando é esparso, funciona bem. Quando é denso que começa a dar problema.

Eu tô achando que se eu compro $J = \{A, B, C\}$, Então o conjunto potência dele é $P(J) = \{\emptyset, A, B, C, AB, AC, BC, ABC\}$, e então, incrementaria 1 para um desses grupos

- Cálculo de suporte:

  - Para cada um dos itemsets tem que verificar se ele tá na árvore K(?)

- Se os itemsets estão em memória...
- Se quero gerar o itemset $XY$ partindo de $X \cup Y$, posso dizer que o suporte será $|c(X) \cap c(Y)|$

### Slide: aula03-apriori_eclat (Aula 04)

#### Eclat (Equivalence Class Transformation)

Dada a representação vertical dos dados, consigo calcular o suporte por essa intercessão.

- Dadas as deficiências do Apriori, M. Zaki propôs, em 2000, o algoritmo Equivalence Class Transformation (Eclat)
- A proposta do algoritmo é 'eliminar' a necessidade de passadas no conjunto de dados para computar o suporte
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

- Seja $p: P(I) \times \mathbb{N} \rightarrow P(I)$ uma função prefixo. $p(X, k) = X[1:k]$.
- A relação $\theta_k \subseteq P(I) \times P(I), A \theta_k B \equiv p(A, k) = p(B, k)$, é uma relação de equivalência
- Dessa forma, ela induz uma partição dos conjuntos de itens em classes de equivalência, onde todos os elementos compartilham um certo prefixo
- Por exemplo, todos os conjuntos que contêm o item Muesli pertencem à classe de equivalência $[Muesli]_{\theta_1}$
- Intuitivamente, essas classes servem como projeções do conjunto de dados, em que somente as transações contendo aquele prefixo são consideradas

Cria-se uma relação de equivalência pelos prefixos.

Diz-se que dois itemsets são equivalentes se o prefixos dos dois são iguais.

Consideremos que temos o seguinte conjunto potência: $P(I) = \{\emptyset, A, B, C, AB, AC, BC, ABC\}$. Na forma de representação, seria como se agrupássemos os dados em grupos de prefixos:

- $A: \{A, AB, AC, ABC\}$
- $B: \{B, BC\}$
- $C: \{C\}$

E então seriam varridos de C para A.

Poderia-se também fazer subgrupos de subgrupos, dependendo do tamanho do conjunto de prefixos.

---

Ele faz uma busca em profundidade (DFS)

Ele faz subpartições até que o número de transações seja pequeno o suficiente para caber na memória.

- Durante a busca em profundidade, o algoritmo particiona os conjuntos de itens conforme a relação de equivalência e o nível da árvore
- O particionamento pode ser encerrado tão logo os tidsets caibam na memória e as interseções possam ser computadas facilmente
- Contudo, a estratégia pode ser usada durante toda a execução do algoritmo
- O cálculo do suporte no algoritmo se restringe a calcular o tamanho do tidset

---

- **ALGORITHM 8.3. Algorithm ECLAT**
- // Initial Call: $\mathcal{F} \leftarrow \emptyset, P \leftarrow \{ \langle i, t(i) \rangle | i \in \mathcal{I}, |t(i)| \geq minsup \} $
- **ECLAT** $(P, minsup, \mathcal{F})$:
  - **foreach** $\langle X_a, t(X_a) \rangle \in P$ **do**
    - $\mathcal{F} \leftarrow \mathcal{F} \cup \{(X_a, sup(X_a))\}$
    - $P_a \leftarrow \emptyset$
    - **foreach** $\langle X_b, t(X_b) \rangle \in P$, with $X_b > X_a$ **do**
      - $X_{ab} = X_a \cup X_b$
      - $t(X_{ab}) = t(X_a) \cap t(X_b)$
      - **if** $sup(X_{ab}) \geq minsup$ **then**
        - $P_a \leftarrow P_a \cup \{ \langle X_{ab}, t(X_{ab}) \rangle \}$
    - **if** $P_a \neq \emptyset$ **then** ECLAT $(P_a, minsup, \mathcal{F})$

[JV: Droga, foquei em transcrever brevemente e esqueci de prestar atenção na explicação do professor]

P guarda todos os frequentes da chamada anterior. porque ele filtro toudos que são infrequentes pelo minsup

para cada um dos frequentes dos candidatos, armazena no ocnjunto de itens frequentes globais

e a partir dele gera em profundidade a combinação dele com todos os outros que vêm pra frente.

Evitam redundância: 1. partições; 2. Ordem sistemática de combinação dos itens.

1. A B C
2. A com B e C: AB AC
3. AB com AC: ABC
4. B com C: BC

##### Representações de conjuntos de dados (Aula 4)

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

Pelo que eu tô entendendo:

1. Começa pegando todos os itens que tenham uma quantidade de transações maior que o minsup (o valor mínimo aceitável para que consideremos relevante)
2. Depois disso, começamos fazendo a intercessão das transações entre o primeiro conjunto de itens que passou pela comparação com o segundo conjunto.
3. Depois disso, vê se o resultado dessas intercessões é grande o bastante.

Se $A \subseteq B$, então $c(B) \subseteq c(A)$ (Cobertura)

#### Eclat (Equivalence Class Transformation) [2]

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

##### Diffsets e dEclat [Próxima aula]

- Percebendo o problema de se manter os tidsets em memória, Zaki e Gouda propuseram em 2001 (o artigo só foi publicado em 2003) uma solução alternativa
- Eles propuseram armazenar as diferenças entre os tidsets dos membros de uma classe e dos prefixos que a definem
- Eles chamaram esse conjunto de **diffset**
- Formalmente, para um prefixo P e um itemset PX, o diffset de X, $d(PX) = c(P) - c(PX)$
- Seriam armazenados, portanto, o suporte do itemset e seu diffset

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

- Por definição, $d(PXY) = c(PX) - c(PXY) = c(PX) - c(PY)$
- Podemos adicionar, ao conjunto acima, o conjunto vazio $(c(P) - c(P))$ sem alterá-lo
- Logo, $d(PXY) = c(PX) - c(PY) + c(P) - c(P) - c(P) = (c(P)-c(PY)) - (c(P) - c(PX)) = d(PY) - d(PX)$
- Em outras palavras, podemos usar os diffsets dos conjuntos base para calcular o diffset do novo candidato
- A variante do Eclat que usa diffsets ficou conhecida como dEclat

$C(PX) - C(PY)$

$C(PX) - C(PY) \cup C(P) - C(P)$

$C(PX) \cap \overline{C(PY)} \cup C(P) \cap \overline{C(P)}$

$C(PX) \cup \overline{C(P)} \cap C(P) \cup \overline{C(P)}$

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

- Por definição, $d(PXY) = c(PX) - c(PXY) = c(PX) - c(PY)$
- Podemos adicionar, ao conjunto acima, o conjunto vazio $(c(P) - c(P))$ sem alterá-lo
- Logo, $d(PXY) = c(PX) - c(PY) + c(P) - c(P) - c(P) = (c(P)-c(PY)) - (c(P) - c(PX)) = d(PY) - d(PX)$
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

---

---

- **ALGORITHM 8.4. Algorithm dEclat**
  - //`Initial Call:` $\mathcal{F} \leftarrow \emptyset, P \leftarrow \{ \langle i, d(i), sup(i) \rangle | i \in \mathcal{I}, d(i) = \mathcal{T}\\t(i), sup(i) \geq minsup \}$
  - **dEclat** $(P, minsup, \mathcal{F})$:
    - **foreach** $\langle X_a, d(X_a), sup(X_a) \rangle \in P$ **do**
      - $\mathcal{F} \leftarrow \mathcal{F} \cup \{(X_a, sup(X_a))\}$
      - $P_a \leftarrow \emptyset$
      - **foreach** $\langle X_b, d(X_b), sup(X_b) \rangle \in P$, with $X_b > X_a$ **do**
        - $X_{ab} = X_a \cup X_b$
        - $d(X_{ab}) = d(X_b) \\ d(X_a)$
        - $sup(X_{ab}) = sup(X_a) - |d(X_{ab})|$
        - **if** $sup(X_{ab}) \geq minsup$ **then**
          - $P_a \leftarrow P_a \cup \{ \langle X_{ab}, d(X_{ab}), sup(X_{ab}) \rangle \}$
      - **if** $P_a \neq \emptyset$ **then** dEclat $(P_a, minsup, \mathcal{F})$

---

- Essa abordagem se mostrou muito eficiente para conjuntos densos
- Porém, em conjuntos esparsos, o algoritmo original é a melhor opção

Para bases esparsas: eClat; para bases densas: dEclat

[Imagem (a): Minimun Support (%) - Connect]

[Imagem (b): Minimun Support (%) - pumsb*]

[Imagem (c): Minimun Support (%) - T40I10D100K]

#### Leitura (Aula 05)

- Seções 8.1, 8.2 (Zaki e Meira)
- Seções 6.1, 6.2 (Introduction to Data Mining)
- Mohammed Javeed Zaki: Scalable Algorithms for Association Mining. IEEE Trans. Knowl. Data Eng. 12(3): 372-390 (2000)
- Zaki, M.J., Gouda, K.: Fast vertical mining using diffsets. Technical Report 01-1, Computer Science Dept., Rensselaer Polytechnic Institute (March 2001) 10
- Christian Borgelt. Efficient Implementations of Apriori and Eclat. Workshop of Frequent Item Set Mining Implementations (FIMI 2003, Melbourne, FL, USA).

Boa parte da explicação estão nos artigos. A implementação tá no Borgelt.

### Slide: aula04-FPGrowth (Aula 05)

#### Recapitulando (Aula 05)

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

| **TID** | **Muesli (a)** | **Oats (b)** | **Milk (c)** | **Yoghurt (d)** | **Biscuits (e)** | **Tea (f)** |
| :------ | :------------: | :----------: | :----------: | :-------------: | :--------------: | :---------: |
| 1       |       1        |      0       |      1       |        1        |        0         |      1      |
| 2       |       0        |      1       |      1       |        0        |        0         |      0      |
| 3       |       0        |      0       |      1       |        0        |        1         |      1      |
| 4       |       1        |      0       |      0       |        1        |        0         |      0      |
| 5       |       0        |      1       |      1       |        0        |        0         |      1      |
| 6       |       1        |      0       |      1       |        0        |        0         |      1      |

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
  Item & Freq & Link \\
  c & 5 & \\
  f & 4 & \\
  a & 3 & \\
  b & 2 & \\
  d & 2 & \\
\end{bmatrix}
$$

```mermaid
flowchart LR
  Vazio(("$$\emptyset$$")) --> C(("$$c:5$$"))
  C --> F(("$$f:4$$"))
  F --> A2(("$$a:2$$"))
  A2 --> D1(("$$d:1$$"))
  F --> B1(("$$b:1$$"))
  C --> B2(("$$b:1$$"))
  Vazio --> A1(("$$a:1$$"))
  A1 --> D2(("$$d:1$$"))
```

Há também uma lista encadeada para todos os nós com ocorrências de um mesmo item.

A lista encadeada serve para podermos percorrer todos os nós de um mesmo item e calcularmos sua frequência.

#### Continua na próxima aula

## Aula 06 | 03/04/2025 | Mineração de conjuntos de itens

### Slide: aula04-FPGrowth (Aula 06)

#### FP-Growth (Aula 06)

- O FP-Growth foi proposto em 2000 por Jiawei Han, Jian Pei e Yiwen Yin
- O algoritmo atacou dois problemas presentes nas abordagens iniciais:
  1. Repetidas passadas sobre a base de dados; e
  2. Geração de candidatos [Mais crítico]
- O primeiro problema, como já discutimos, é crítico pelo custo computacional inerente à leitura em memória secundária
- O segundo problema está relacionado à geração de candidatos desnecessários
  - Muitos são descartados pela propriedade do Apriori

##### FP-Tree [Árvore de Prefixos] (Aula 06)

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

| **TID** | **Muesli (a)** | **Oats (b)** | **Milk (c)** | **Yoghurt (d)** | **Biscuits (e)** | **Tea (f)** |
| :------ | :------------: | :----------: | :----------: | :-------------: | :--------------: | :---------: |
| 1       |       1        |      0       |      1       |        1        |        0         |      1      |
| 2       |       0        |      1       |      1       |        0        |        0         |      0      |
| 3       |       0        |      0       |      1       |        0        |        1         |      1      |
| 4       |       1        |      0       |      0       |        1        |        0         |      0      |
| 5       |       0        |      1       |      1       |        0        |        0         |      1      |
| 6       |       1        |      0       |      1       |        0        |        0         |      1      |

#### Mineração dos padrões [Aula 05] (Aula 06)

- A mineração dos padrões se inicia uma vez que a FP-Tree tenha sido construída
- A construção agora ocorre aumentando-se prefixos dos padrões em ordem crescente de suporte
- As transações que satisfaçam (contém) o padrão sendo construído são projetadas em uma nova árvore
- Itens podem se tornar infrequentes nessa nova base e são descartados
- Os padrões encontrados nessa nova árvore devem incluir o prefixo que a gerou
- O algoritmo segue com as extensões recursivamente até que um único ramo seja obtido
  - Se a árvore possui um único ramo, os padrões obteníveis são todas as combinações dos nós

---

- Exemplo

$$
\begin{bmatrix}
  Item & Freq & Link \\
  c & 5 & \\
  f & 4 & \\
  a & 3 & \\
  b & 2 & \\
  d & 2 & \\
\end{bmatrix}
$$

```mermaid
flowchart LR
  Vazio(("$$\emptyset$$")) --> C(("$$c:5$$"))
  C --> F(("$$f:4$$"))
  F --> A2(("$$a:2$$"))
  A2 --> D1(("$$d:1$$"))
  F --> B1(("$$b:1$$"))
  C --> B2(("$$b:1$$"))
  Vazio --> A1(("$$a:1$$"))
  A1 --> D2(("$$d:1$$"))
```

Há também uma lista encadeada para todos os nós com ocorrências de um mesmo item.

A lista encadeada serve para podermos percorrer todos os nós de um mesmo item e calcularmos sua frequência.

- [JV] Explicação do Algoritmo
  - Para se minerar as transações de volta, percorremos a lista de itens e então subimos dele até a raiz.
  - Partindo do item menos frequente e indo pro item mais frequente, fazemos projeções da árvore.
  - Essas projeções são sub-árvores da árvore original.
  - No caso do d, percorrerei todos os nós da lista encadeada de de d's, indo dele até a raiz. A junção de todos os nós que eu passar, formará uma nova árvore. E essa será a projeção do item d.
  - Mas ainda não entendi o que precisa ser feito após essa primeira projeção.
- [JV] Explicação 2
  - Primeiro filtra pelos itens frequentes, removendo os infrenquentes.
    - Ex: minsup = 2
  - Depois disso, ele faz a... "transposição horizontal(?)", ou seja, para cara transação, ele lista todos os itens frequentes que estão presentes nela.
  - Então ordena cada um desses itens por seu suporte.
    - Ex:
      - Em ordem de maior suporte pra menor suporte: cfabd; Obs.: Ignoram-se os itens infrequentes.
      1. cfad
      2. cb
      3. cf
      4. ad
      5. cfb
      6. cfa
  - Depois disso, ele vai inserindo esses itens em uma árvore de prefixos, em sequência: do primeiro TID até o último TID, depois do primeiro item até o último item.
  - Dúvida JV: Qual é a sequência para se percorrer as transações? Da primeira pra última? Poderíamos ordenar as transações por suporte, e depois fazer a inserção na árvore? Haveria benefício ao fazermos isso?
    - Resposta: Sim, a ideia é percorrer as transações na ordem em que elas aparecem. Porém, existe sim benefício em ordenar, mas não direi agora.
  - À medida em que insere, atualiza a tabela de frequência dos itens.
  - Depois de todos preenchidos, ele percorrerá a tabela das frequências, partindo do item menos frequente
  - Agora, percorrendo a lista encadeada do item menos frequente, ele vai subindo até a raiz, e então vai criando uma nova árvore de prefixos, que será a projeção dos sufixos do item menos frequente.
  - Porém, ao invés de fazer uma lista dos sufixos, ele faz uma sub-árvore que representa todos os sufixos do item que estamos percorrendo. Porém, omitindo o item em si.
  - Após criada essa sub-árvore, podaremos os itens que não são frequentes, segundo a sub-tabela de frequências dessas sub-árvores.
  - Então é feito um merge dos ramos que sobraram, somando os suportes dos itens que sobraram.
    - Eu estimo que esse merge seja feito partindo da raiz, e conferindo se todos os seus filhos não diferentes entre si. Caso sejam iguais, eles são mesclados e seus filhos também, assim somando e unindo recursivamente.
  - Agora sim são gerados os itemsets de padrões frequentes ao gerar todas as possibilidades partindo do conjunto vazio que é a raiz, e parando em cada um dos nós que sobraram.
    - **OBS.: ESSA ETAPA SÓ OCORRE CASO A ÁRVORE TENHA SOMENTE UM RAMO. SE A ÁRVORE TIVER MAIS DE UM RAMO, O ALGORITMO SE REPETE RECURSIVAMENTE, ATÉ QUE A ÁRVORE TENHA SOMENTE UM RAMO.**
    - Suponho também que, na última recursão, o algoritmo, mesmo que sejam podados todos os nós visíveis (não considerando o $\emptyset$), ele ainda assim gere os padrões frequentes, sendo ele o item da qual a árvore é projeção.

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

- [JV] Explicação da criação
  - Ao invés de fazer a FP-Tree, ele primeiro ordena todos as transações, ele, recursivamente:
    - agrupa elas pelo prefixo inicial. Cada prefixo inicial será um nó apontando ao seu pai. Inicialmente sendo o pai o nó raiz, o $\emptyset$.
    - E então repete isso para cada um dos sufixos que sobraram, até que não haja mais sufixos.

---

- Implementação tradicional, conforme descrição do algoritmo, evita carregar dados para memória
  - Porém, nós terão tamanho variável ou desperdiçam memória (ponteiros para filhos que nunca ocorrem)
  - Melhora gerenciamento de memória; grandes blocos podem ser alocados de uma vez e gerenciados internamente
  - Além disso, ponteiros para pais são mais úteis que ponteiros para filhos durante execução

---

- Projeções são executadas com dois laços
  - Um laço externo percorre o nível mais baixo (elemento condicionante da projeção)
  - Laço interno percorre a os ramos originários do nó folha
- A nova árvore é construída como uma 'sombra da original
  - Nós são duplicados conforme são visitados (ponteiro auxiliar mantém elo de ligação entre original e cópia para atualizações necessárias durante construção)
  - Frequência do nó folha é propagada para cima
- A sombra é destacada da árvore original em uma segunda passada pelos nós
- Nós infrequentes podem ser removidos e nós com mesmo rótulo mesclados

---

[Imagem (a): FP-Growth VS Eclat VS Apriori - Chess]

[Imagem (b): FP-Growth VS Eclat VS Apriori - Mushroom]

Figuras retiradas de Borgelt, C. An Implementation of the FP-growth Algorithm

#### Leitura [Aula 05]

- Seção 6.6 Intro to Data Mining
- Seção 8.2.3 Zaki e Meira
- [Borgelt, C. (2005) An Implementation of the FP-growth Algorithm][LinkFPGrowth]

[LinkFPGrowth]: https://borgelt.net/papers/fpgrowth.pdf

### Slide: aula05-repr-compactadas (Aula 06)

#### Introdução (Aula 06)

- Nessa aula, vamos discutir representações compactas para o conjunto de todos os conjuntos de itens frequentes de uma base de dados
- Representações compactas são subconjuntos a partir dos quais é possível derivar todos os conjuntos de itens frequentes
- Para motivar a necessidade dessas representações, considere uma base de dados com somente duas transações e 100 itens:
  - $D = \{(0, a_{1}, a_{2}, \dots, a_{50}), (1, a_{1}, a_{2}, \dots, a_{100})\}$
- Se considerarmos um minsup=1, essa base terá

  - $\binom{100}{1} + \binom{100}{2} + \dots + \binom{100}{100} = 2^{100} - 1 \approx 1.27E^{30}$

- [JV]
  - Podemos considerar que:
    - $01 = a_{1}a_{2}\dots a_{50}$
    - $ 1 = a*{1}a*{2}\dots a\_{100}$
  - O que seriam representações compactas do conjunto de itemsets frequentes

---

- Nesse caso, o problema se torna incomputável por qualquer das abordagens que vimos anteriormente
- Embora esse seja um caso extremo, não é raro que situações similares a essa ocorram na prática
  - É possível, por exemplo, que um subconjunto das transações e itens apresentem esse comportamento em uma base de dados maior
- Note que podemos particionar os itemsets frequentes em duas classes de equivalência:
  - Os que ocorrem em ambas as transações; e
  - Os que ocorrem somente na segunda

---

- Os que ocorrem em ambas as transações, possuem cobertura $c(X)=01$, e, portanto, são equivalentes a $a_{1}a_{2}\dots a_{50}$
- Os que ocorrem somente na segunda transação, possuem cobertura $c(X)=1$, e, portanto, são equivalentes a $a_{1}a_{2}\dots a_{100}$
  - Além disso, se estivéssemos somente interessados nos itemsets frequentes sem a informação da frequência, todos seriam equivalentes a esse itemset
- Em outras palavras, os mais de $10^{30}$ itemsets que seriam retornados por qualquer dos algoritmos vistos poderiam ser representados somente por esses dois conjuntos
- Esses conjuntos formam, dessa forma, uma **representação compacta** de todo o conjunto de itemsets frequentes
- Em particular, eles estão relacionados a dois tipos de representações compactas que veremos nessa aula
  - Conjuntos frequentes **máximos**
  - Conjuntos frequentes **fechados**

#### Representações compactas

- O particionamento dos itemsets no exemplo anterior se deu pelos tidsets que compunham suas extensões
- De fato, o raciocínio se aplica a qualquer base de dados. Ou seja, podemos particionar os itemsets conforme sua cobertura
- Dentro de cada classe de equivalência, podemos ordenar os elementos conforme a relação de subconjunto
  - O maior elemento da classe é chamado de conjunto fechado ou **closed itemset**
    - [JV:] O maior item possível dos itemsets. Exemplo: $a_{1}a_{2}\dots a_{50}$ || $P = c(i(P))$
  - Os menores elementos da classe são chamados de **minimal generators**
    - [JV:] Exemplo: cada um dos itenzinhos que foram concatenados. ($a_{1}, a_{2}, \dots, a_{50}$) || $X = i(c(X))$
- Os maiores elementos entre todos os conjuntos fechados são chamados de conjuntos frequentes máximos (**maximal itemsets**)
  - [JV:] O maior itemset possível entre todos os conjuntos fechados. Exemplo: $a_{1}a_{2}\dots a_{100}$ || "São os maiores itemsets frequentes"

---

- Os conjuntos máximos são os maiores itemsets frequentes
- Eles definem a 'borda entre o que é frequente e infrequente
- Como, por definição, não existem conjuntos frequentes maiores que eles, **todos os conjuntos frequentes podem ser derivados a partir dos conjuntos máximos**
- No entanto, o cálculo do suporte não pode ser obtido diretamente desses itemsets, sendo necessária uma nova passada na base de dados para computá-lo
- O itemset $a_{1}a_{2} \dots a_{100}$ no nosso exemplo inicial é um conjunto frequente máximo

---

- Essa necessidade de novas passadas na base de dados para computar o suporte dos itemsets frequentes a partir dos máximos torna a representação incompleta
- Os conjuntos fechados, por outro lado, são uma representação completa, já que tanto os itemsets quanto seu suporte podem ser derivados desses conjuntos
- Como dito, todo conjunto fechado dá origem a uma classe de equivalência
  - $[X] = \{Y \subseteq I | c(Y) = c(X)\} = \{Y \subseteq I | i(c(Y)) = X\}$
- Assim, podemos verificar o suporte de um itemset frequente a partir dos conjuntos fechados da seguinte forma
  - $sup(𝑋) = max \{sup(Y) | Y \in \mathcal{C} \wedge X \subseteq Y\}$
  - Em outras palavras, basta encontrarmos a classe de equivalência à qual o itemset pertence; todo itemset frequente ou é fechado ou pertence à classe de equivalência de algum conjunto fechado, como o suporte é anti-monotônico, se ele não for fechado, ele pertence à classe do de maior suporte.

---

- Exemplo: minsup=1

| TID | Muesli (m) | Oats (o) | Milk (m) | Yoghurt (y) |
| :-- | :--------: | :------: | :------: | :---------: |
| 1   |     1      |    0     |    1     |      1      |
| 2   |     0      |    1     |    1     |      0      |
| 3   |     0      |    0     |    1     |      0      |
| 4   |     1      |    0     |    0     |      1      |
| 5   |     0      |    1     |    1     |      0      |
| 6   |     1      |    0     |    1     |      0      |

---

```mermaid
flowchart LR

  %% Styles
  classDef Infrequent fill:#ffffff, color:#000000;
  classDef Frequent fill:#fffba6, color:#000000;
  classDef Maximal fill:#fffba6, color:#000000, stroke-width:5px, stroke:#000000;

  %% Vértices
  MOKY(("MOKY $$\{\}$$")):::Infrequent
  MOK(("MOK $$\{\}$$")):::Infrequent
  MOY(("MOY $$\{\}$$")):::Infrequent
  MKY(("MKY $$1$$")):::Maximal
  OKY(("OKY $$\{\}$$")):::Infrequent
  MO(("MO $$\{\}$$")):::Infrequent
  MK(("MK $$16$$")):::Frequent
  MY(("MY $$14$$")):::Frequent
  OK(("OK $$25$$")):::Maximal
  OY(("OY $$\{\}$$")):::Infrequent
  KY(("KY $$\{\}$$")):::Infrequent
  M(("M $$146$$")):::Frequent
  O(("O $$25$$")):::Frequent
  K(("K $$12356$$")):::Frequent
  Y(("Y $$14$$")):::Frequent
  Vazio(("$$\emptyset$$")):::Frequent

  %% Label
  Freq[Frequent Itemsets]:::Infrequent
  Infreq[Infrequent Itemsets]:::Frequent
  Max[Maximal Itemsets]:::Maximal

  %% Arestas
  MOKY --- MOK & MOY & MKY & OKY
  MOK --- MO & MK & OK
  MOY --- MO & MY & OY
  MKY --- MK & MY & KY
  OKY --- OK & OY & KY
  MO --- M & O
  MK --- M & K
  MY --- M & Y
  OK --- O & K
  OY --- O & Y
  KY --- K & Y
  M --- Vazio
  O --- Vazio
  K --- Vazio
  Y --- Vazio
```

---

```mermaid
flowchart LR

  %% Styles
  classDef Infrequent fill:#ffffff, color:#000000;
  classDef Frequent1 fill:#fffba6, color:#000000;
  classDef Frequent2 fill:#fffba6, color:#000000;
  classDef Frequent3 fill:#fffba6, color:#000000;
  classDef Maximal fill:#fffba6, color:#000000, stroke-width:5px, stroke:#000000;

  %% Vértices
  MOKY(("MOKY $$\{\}$$")):::Infrequent
  MOK(("MOK $$\{\}$$")):::Infrequent
  MOY(("MOY $$\{\}$$")):::Infrequent
  MKY(("MKY $$1$$")):::Maximal
  OKY(("OKY $$\{\}$$")):::Infrequent
  MO(("MO $$\{\}$$")):::Infrequent
  MK(("MK $$16$$")):::Frequent
  MY(("MY $$14$$")):::Frequent
  OK(("OK $$25$$")):::Maximal
  OY(("OY $$\{\}$$")):::Infrequent
  KY(("KY $$\{\}$$")):::Infrequent
  M(("M $$146$$")):::Frequent
  O(("O $$25$$")):::Frequent
  K(("K $$12356$$")):::Frequent
  Y(("Y $$14$$")):::Frequent
  Vazio(("$$\emptyset$$")):::Frequent

  %% Label
  Freq[Frequent Itemsets]:::Infrequent
  Infreq[Infrequent Itemsets]:::Frequent
  Max[Maximal Itemsets]:::Maximal

  %% Arestas
  MOKY --- MOK & MOY & MKY & OKY
  MOK --- MO & MK & OK
  MOY --- MO & MY & OY
  MKY --- MK & MY & KY
  OKY --- OK & OY & KY
  MO --- M & O
  MK --- M & K
  MY --- M & Y
  OK --- O & K
  OY --- O & Y
  KY --- K & Y
  M --- Vazio
  O --- Vazio
  K --- Vazio
  Y --- Vazio
```

Os azuis e verdes são classes de equivalência.

#### Algoritmos para encontrar representações compactas

- Os exemplos mostram que as representações compactas apresentam vantagens sobre o conjunto de todos os itemsets frequentes
- No entanto, se usarmos os algoritmos vistos anteriormente para encontrar essas representações, não temos ganho computacional algum em relação ao problema anterior
  - Pode ser que a mineração desses padrões continue inviável
- Existem diversos algoritmos específicos para mineração de itemsets máximos e fechados
- Veremos um representante de cada desses algoritmos

"Você consegue encontrar todos ..."

##### DCI_Closed - Próxima aula

## Aula 07 | 08/04/2025 | Mineração de sequências - Faltei pq tava passando mal

### Slide: aula05-repr-compactadas (Aula 07)

#### Algoritmos para encontrar representações compactas (Aula 07)

##### DCI_Closed (Aula 07)

- O algoritmo DCI_Closed foi proposto em 2004 por C. Lucchese, S. Orlando e R. Perego
- Ele também adota uma representação vertical da base de dados para facilitar a verificação dos conjuntos fechados
- O algoritmo explora o espaço de busca usando uma estratégia dividir- e-conquistar
- Os autores demonstraram que o problema pode ser decomposto em subproblemas independentes, permitindo inclusive uma solução paralela

---

- A ideia central do algoritmo é 'escalar' o reticulado de itemsets, percorrendo cada classe de equivalência uma única vez
- Somente um candidato de cada classe é avaliado para computar o seu conjunto fechado
- Novamente, assume-se uma ordem lexicográfica sobre os itens da base, e sua extensão sobre os itemsets
  - Qualquer ordem serve, inclusive a ordem sobre os rótulos dos itens
  - Essa ordem será representado por $\prec$
- Novos candidatos são gerados a partir dos conjuntos fechados obtidos, estendendo-os com itens ainda não investigados
  - Esses candidatos são chamados de **geradores**
  - Formalmente, um gerador é um conjunto $X = Y_i$, para um conjunto fechado $Y$ e um item $i$

---

- Um gerador $X = Y_i$ é dito **ordem-conservante** sse $i \prec (i(c(X)) - X)$
  - Em palavras, $X$ é ordem-conservante se todo item que tiver que ser adicionado a X para obter o conjunto fechado for maior que $i$
- Teorema 1: Para todo conjunto fechado $Y \neq i(c(\emptyset))$, existe uma sequência de $n \geq 1$ extensões (items) $i_0 \prec i_1 \prec \dots \prec i_{n-1}$ tais que $gen_0 = Y_0i_0$, $gen_1 = Y_1i_1$, $gen_{n-1} = Y_{n-1}i_{n-1}$, em que todos os $gen_k$ são ordem- conservantes, $Y_0 = i(c(\emptyset))$, $Y_{j+1} = i(c(Y_ji_j))$ e $Y_n=Y$.
- Corolário: Essa sequência é única.

---

- O problema agora é verificar se um gerador é ordem-conservante
- Lema 1: Seja $gen = Y_i$, para um conjunto fechado $Y$ e item $i$. Se $\exists j \prec i [j \notin gen \wedge c(gen) \subseteq c(j)]$, então $gen$ não é ordem-conservante.
  - Intuitivamente, $c(gen) \subseteq c(j)$ implica em $j \in i(c(gen))$, e como $j \notin gen$, $j \in i(c(gen)) - gen$; ou seja, $i \nprec i(c(gen)) - gen$
- Sendo assim, basta mantermos uma lista de elementos menores que $i$ não pertencentes a $gen$ para verificarmos se ele é ordem-conservante durante a execução do algoritmo
  - Essa lista é chamada de **pre-set**
  - Não há necessidade de manter os conjuntos fechados em memória!
- O espaço de busca pode ser percorrido a partir de $i(c(\emptyset))$ e todos os itens frequentes como possíveis extensões
  - Os geradores são avaliados conforme a ordem lexicográfica
  - Se encontrarmos um gerador não ordem-conservante, podamos o ramo
  - Após explorar o ramo com um item $i$, ele é colocado no **pre-set**

---

- **procedure** $DCI\_Closed_d$ (CLOSED_SET, PRE_SET, POST_SET)
  - **while** POST_SET $neq \emptyset$ **do**
    - $i \leftarrow min_{\prec}$ (POST_SET)
    - POST_SET $leftarrow$ POST_SET \ $i$
    - $new\_gen \leftarrow$ CLOSED_SET $\cup i$ \\\\ Build a new generator
    - **if** $supp(new\_gen) \geq minsupp$ **then**
      - $\neg$ is_dup (new_gen, PRE_SET) **then** \\\\ if $new\_gen$ is both frequent and order preserving
      - CLOSED*SET $*{New} \leftarrow new_gen$
      - POST*SET $*{New} \leftarrow \emptyset$
      - **for all** $j \in$ POST_SET **do** \\\\ Compute closure of $new\_gen$
        - **if** $g(new\_gen) \subseteq g(j)$ **then**
          - CLOSED*SET $*{New} \leftarrow$ CLOSED*SET $*{New} \cup j$
        - **else**
          - POST*SET $*{New} \leftarrow$ POST*SET$*{New} \cup j$
        - **end if**
      - **end for**
      - **Write Out** CLOSED*SET $*{New}$ _and its support_
      - DCI*Closed $_d$ CLOSED_SET $*{New}$, PRE_SET, POST_SET $_{New}$
      - PRE_SET $leftarrow$ PRE_SET $\cup i$
    - **end if**
  - **end while**
- **end procedure**

---

- **function** $is\_dup$ ($new\_gen$, PRE_SET) \\ Duplicate check
  - **for all** $j \in$ PRE_SET **do**
    - **if** $g(new\_gen) \subseteq g(j)$ **then**
      - **return** TRUE \\ $new\_gen$ is not order preserving
    - **end if**
  - **end for**
  - **return** FALSE
- **end function**

---

- Exemplo: minsup = 2

| **TID** | **Muesli (a)** | **Oats (b)** | **Milk (c)** | **Yoghurt (d)** | **Biscuits (e)** | **Tea (f)** |
| :------ | :------------: | :----------: | :----------: | :-------------: | :--------------: | :---------: |
| 1       |       1        |      0       |      1       |        1        |        0         |      1      |
| 2       |       0        |      1       |      1       |        0        |        0         |      0      |
| 3       |       0        |      0       |      1       |        0        |        1         |      1      |
| 4       |       1        |      0       |      0       |        1        |        0         |      0      |
| 5       |       0        |      1       |      1       |        0        |        0         |      1      |
| 6       |       1        |      0       |      1       |        0        |        0         |      1      |

##### MAFIA: Maximal Frequent Itemset Algorithm - Próxima aula

## Aula 08 | 10/04/2025 | Mineração de sequências

### Slide: aula05-repr-compactadas (Aula 08)

#### Algoritmos para encontrar representações compactas (Aula 08)

##### MAFIA: Maximal Frequent Itemset Algorithm

- O algoritmo MAFIA foi proposto em 2001 por D. Burdick, M. Calimlim e J. Gehrke
- A ideia geral do algoritmo é a de explorar o reticulado de itemsets com uma abordagem best-first/branch-and-bound
- Assim como o Eclat, o MAFIA também assume uma representação vertical dos dados usando vetores de bits
- O algoritmo também assume uma ordem lexicográfica sobre os itens e a ordem parcial de subconjuntos entre os itemsets durante a exploração

Se eu quero minimizar a quantidade de itens mostrados pro usuário, posso mostrar os maximais.

Existem vários algoritmos que encontram os maximais.

Nessa época dos anos 2000, assim como hoje é com IA e Deep Learning, na época era essa mineração de itens frequentes.

"Os maximais estão na fronteira"

"A maioria dos artigos na época costumava usar vetores de bits para representar itemsets" Isso por causa dos benefícios de velocidade de processamento para uniões e interseções.

Na notação vertical, a primeira coluna são os itens, e a segunda é a lista das transações que possuem esse item. Para calcular rapidamente o suporte é manter em uma estrutura auxiliar a quantidade de bits ativos.

---

- Durante a exploração do espaço de busca, o algoritmo divide os itens em dois grupos
  - **Head**: contendo o rótulo do nó corrente (itemset) na exploração
  - **Tail**: os itens que são maiores que o maior elemento do Head (possíveis extensões para o itemset)
- O conjunto de todos os itens que podem aparecer numa dada subárvore é a união entre o head e o tail (chamado de **HUT** - head union tail - pelos autores)
- Ao invés de adotar uma exploração puramente em profundidade, em cada nó, o algoritmo avalia os filhos imediatos para remover possíveis extensões do tail

  - Eles chamam essa estratégia de **reordenamento dinâmico (dynamic reordering)**

- [JV]

  - O conjunto de itens será dividido em dois:
    - Head: itemset que já visitei
    - Tail: itens que ainda vou considerar
  - HUT: Maior itemset que pode ser obtido a partir da sub árvore explorada.
  - "Posso podar se encontrar algum que seja maior do que o já encontrado"

- [JV]
  - Algoritmo
    - No nível que eu tô, ele calcula o suporte de todos os filhos. Então ele pode podar todos os que forem infrequentes.
    - Dúvida: se todos os items de determinado nível fossem infrequentes, isso implicaria na head ser infrequente também?
      - Não. Isso porque sempre estamos indo do mais geral pro menos geral.

---

- Ao explorar o nó P na figura ao lado
  - Head = 1
  - Tail = 234
  - HUT = 1234
- Antes de explorar em profundidade o nó, o algoritmo avalia os filhos 12, 13 e 14
- Como só 12 é frequente, 3 e 4 podem ser removidos do tail porque qualquer candidato dessa subárvore que inclua esses itens será infrequente
  - O ramo de 12 é podado

[Imagem]

- [JV]
  - Sempre descarta os itens que são infrequentes.
  - Se o HUT encontrado é subconjunto de um maximal já encontrado, posso podar todo o HUT.
  - Algoritmo:
    - Começa gerando todas as combinações simples do item do head com os itens do tail.
    - Poda todos os que forem infrequentes.
    - Depois de remover os infrequentes, remove também do tail.
    - Obs.: Mesmo que um item frequente seja composto por diversos conjuntos infrequentes, ainda assim ele permanece sendo frequente.
      - Ex.: Se eu compro AB, compro AC, compro AD. Embora apenas exista uma ocorrência de AB, uma de AC e uma de AD, ainda assim, A foi comprado 3 vezes, logo, é frequente.
    - Obs.: Best-First Search: Procura sempre o melhor. Procura sempre o caminho com maior estimativa de lucro. Parece um pouco com o conceito do algoritmo de Prim.
    - Ao final dessa análise, após podado o que deve ser podado, as folhas representam os conjuntos maximais.

---

- Note que, sempre que uma folha é visitada, um candidato a itemset máximo é encontrado
  - Ele será incluído na solução final somente se não possuir um superconjunto já incluído
  - A visitação em ordem lexicográfica em profundidade garante que conjuntos não tenham que ser removidos da solução final
- Outra poda vem do fato de que itemsets máximos são também fechados e que, portanto, para um itemset $X$ (head) e $y \in X.tail$:
  - Se $c(X) \subseteq c(y)$, então $X_y \subseteq i(c(X))$ (isto é, $y$ pertence ao conjunto fechado da classe à qual $X$ pertence)
  - Nesse caso, $y$ pode ser incorporado ao head e removido do tail
- Essa poda é chamada de Parent Equivalence Pruning (PEP)

- [JV]
  - "Sempre entra, nunca sai"
  - "Todo itemset maximal, é também um itemset fechado"
  - Itemset fechado: O maior itemset de uma classe de equivalência.
    - Ele explicou um pouco mais. Tem algo sobre checar todos os que têm a mesma cobertura e verificar qual o maior ou algo assim.

---

- Finalmente, podemos usar a propriedade do Apriori para descartar um ramo baseado no HUT
  - Lembrando que HUT é a união do head com o tail e representa o maior itemset que pode ser obtido a partir dessa subárvore
- Se o HUT for subconjunto de algum itemset máximo já descoberto anteriormente, sabemos que ele e todos os seus subconjuntos são frequentes, e, além disso, não podem ser máximos. Portanto, podemos podar a subárvore.

---

- Pseudocode: _MAFIA_ (**C**, **MFI**, Boolean **IsHUT**)

  - name **HUT** = **C**.head $\cup$ **C**.tail
  - if **HUT** is in **MFI**
    - Stop generation of children and return
  - Count all children, use PEP to trim the tail, and reorder by increasing support
    - For each item **i** in **C**.trimmed_tail
      - **IsHUT** = whether **i** is in the first item in the trail
      - **newNode** = **C** $\cup$ **I**
      - _MAFIA_ (**newNode, MFI, IsHUT**)
    - if (**IsHUT** and all extensions are frequent)
      - Stop search and go back up subtree
    - if (**C** is a leaf and **C**.head is not in **MFI**)
      - Add **C**.head to **MFI**

- [JV]
  - Algoritmo
    - Faz o HUT
    - Faz a poda do apriori
    - Faz a poda do PEP para poder o Tail
    - E para cada item vai procurando usando o Best-First
  - No artigo tem os pseudo-códigos dos outros sub-códigos.
  - A maior crítica a esse método é que não tem muito uma métrica de qualidade. O que temos é a definição do suporte e se ele é bom o bastante pro usuário.
- [Quadro]
  - $MFI \subseteq FCI \subseteq FIM$
  - Apriori: $FIM =  \{ X \subseteq I | sup (x) \geq minsup \}$
  - DCI: $FCI = \{ X \subseteq I | X = i(c(x)) \wedge sup (x) \geq minsup \}$
  - MAFIA: $MFI = \{ X \subseteq I | sup (x) \geq minsup \wedge \nexists Y \supseteq X \wedge sup (y) \geq minsup \}$

---

- Exemplo: minsup = 2

| **TID** | **Muesli (a)** | **Oats (b)** | **Milk (c)** | **Yoghurt (d)** | **Biscuits (e)** | **Tea (f)** |
| ------: | -------------: | -----------: | -----------: | --------------: | ---------------: | ----------: |
|       1 |              1 |            0 |            1 |               1 |                0 |           1 |
|       2 |              0 |            1 |            1 |               0 |                0 |           0 |
|       3 |              0 |            0 |            1 |               0 |                1 |           1 |
|       4 |              1 |            0 |            0 |               1 |                0 |           0 |
|       5 |              0 |            1 |            1 |               0 |                0 |           1 |
|       6 |              1 |            0 |            1 |               0 |                0 |           1 |

##### Leitura (Aula 08)

- Seção 9.1 Zaki e Meira
- Seção 6.2.6 Han et al.
- Burdick, D., Calimlim, M., & Gehrke, J. (2001, April). Mafia: A maximal frequent itemset algorithm for transactional databases. In Proceedings 17th international conference on data engineering (pp. 443-452). IEEE.
- Lucchese, C., Orlando, S., & Perego, R. (2004, November). DCI Closed: A Fast and Memory Efficient Algorithm to Mine Frequent Closed Itemsets. In FIMI.

- [JV]
  - É interessante, agora que já entendeu como o algoritmo funciona, ler e entender a narrativa do artigo.

### Slide: aula06-sequencias (Aula 08)

#### Introdução (Aula 08)

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

#### Definições

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
  - $sup(\alpha) = |\{(sid, s) | \alpha \subseteq s\}|$
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

### Slide: aula06-sequencias (Aula 09)

#### Introdução (Aula 09)

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

#### Definições (Aula 09)

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
  - $sup(\alpha) = |\{(sid, s) | \alpha \subseteq s\}|$
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

#### Mineração de sequências frequentes - (Aula 09)

- O problema de mineração de sequências frequentes consiste em encontrar todas as sequências cujo suporte esteja acima de um limiar mínimo definido pelo usuário
- Existem abordagens tanto para minerar todo o conjunto de sequências frequentes quanto para representações compactas desse conjunto
- Nessa aula veremos apenas as abordagens para minerar todo o conjunto de sequências frequentes
- Essas abordagens são extensões dos principais algoritmos para mineração de conjuntos de itens frequentes

- [JV]
  - Não veremos as maximais e fechadas das sequências. Nem as formas densas, embora existam.

#### Generalized Sequential Patterns (GSP)

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

  - $C^{(2)} = \{ \langle xy \rangle | (x, y) \in F^{(1)} \times F^{(1)} \} \cup \{ \langle (xy) \rangle | (x, y) \in F^{(1)} \times F^{(1)} \wedge x \neq y\}$

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

#### Sequential Pattern Discovery using Equivalence classes (Spade)

- Outra abordagem para mineração de sequências frequentes foi proposta por Zaki em 2001
- O algoritmo Spade é baseado no Eclat
- Assim como o Eclat, ele utiliza uma representação da base de dados similar à vertical e divide o espaço de busca de acordo com o prefixo das sequências

---

- Para obter a representação vertical, vamos associar a cada item $i$ uma tupla $(sid, pos(i))$
  - $pos(i)$ é a lista de todos os elementos em que $i$ ocorre na sequência referente ao cliente $sid$
- A lista de todos os pares sequência-posição de um item é chamada de **poslist** e é denotada por $\mathcal{L}(i)$
- Exemplos:
  - $\mathcal{L}(l) = \{ (2, \{3\}), (3, \{1\}), (4, \{2\}), (6, \{2, 3\} ) \}$
  - $\mathcal{L}(g) = \{ (2, \{1\}), (6, \{1\}) \}$
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

### Slide: aula06-sequencias (Aula 10)

#### Sequential Pattern Discovery using Equivalence classes (Spade) (Aula 10)

- Para obter a representação vertical, vamos associar a cada item $i$ uma tupla $(sid, pos(i))$
  - $pos(i)$ é a lista de todos os elementos em que $i$ ocorre na sequência referente ao cliente $sid$
- A lista de todos os pares sequência-posição de um item é chamada de **poslist** e é denotada por $\mathcal{L}(i)$
- Exemplos:
  - $\mathcal{L}(l) = \{ (2, \{3\}), (3, \{1\}), (4, \{2\}), (6, \{2, 3\} ) \}$
  - $\mathcal{L}(g) = \{ (2, \{1\}), (6, \{1\}) \}$
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

| **item** | **pos(item)**                             |
| :------- | :---------------------------------------- |
| a        | $\{ (1,1), (2,2), (3,1), (4,1), (6,1) \}$ |
| b        | $\{ (2,3), (4,2), (6,3) \}$               |
| c        | $\{ (1,2), (4,3), (5,1) \}$               |
| g        | $\{ (2,1), (6,1) \}$                      |
| i        | $\{ (3,1) \}$                             |
| l        | $\{ (2,3), (3,1), (4,2), (6,23) \}$       |
| s        | $\{ (2,3) \}$                             |

- [JV Anotação no quadro]
  - $ms = minsup = 3$
  - itens com suporte mínimo: $\{a, b, c, l\}$
  - Checa com o
  - $P_a:$
    - Verifica naquela lista ali de trás de $pos(item)$, e vai verificando se os itens aparecem nessa ordem para os dois itens nas transações de um mesmo cliente.
    - $\emptyset a - \emptyset a:$ aa | ~~(aa)~~ (Como os dois são o mesmo item, é descartado)
      - $aa:$ Infrequente
    - $\emptyset a - \emptyset b: ab | (ab)$
      - $ab: pos = \{ (2,3), (4,2), (6,3) \}$
      - $(ab):$ Infrequente
    - $\emptyset a - \emptyset c: ac | (ac)$
      - $ac: pos = \{ (1,2), (4,3) \}$ Infrequente
      - $(ac):$ Infrequente
    - $\emptyset a - \emptyset l: al|(al)$
      - $al: pos = \{ (2,3), (4,2), (6, 23) \}$
      - $(al):$ Infrequente
  - Então, os frequentes são: $\{ ab, al\}$
  - $P_{ab}$
    - $ab - ab: abb$
    - $ab - al: abl|a(bl)$
      - $a(bl): pos = (2,3), (4,2), (6,3) \}$
  - Então os frequentes são: $\{ a(bl) \}$
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

  - $\mathcal{L}((Px)y) = \left{ \left( i, \left{ v \in pos(Py) | \exists u \in pos((Px)) u < v \wedge \left( i, pos(Py) \right) \in \mathcal{L}(Py) \wedge \left( i, pos((Px)) \right) \in \mathcal{L}((PX)) \right} \right) \right}$;
  - Ou seja, são todas as sequências em que ambas acontecem, porém agora somente as posições em que $y$ ocorre temporalmente após $x$ são mantidas
  - O caso é equivalente a Pxy e Pyx

- [JV]
  - Agora veremos os dois prefixos. E apenas consideraremos o último item. Não a última transação.
  - Se considerarmos Py, onde P ocorreu na posição 1, e y está na posição 6;
  - E temos Px, onde P ocorreu na posição 2, e x está na posição 2;
  - Se gerarmos Pyx, teríamos que o y está antes do x, mas temporalmente deveria estar depois. Logo, consideramos que ele será infrequente, podendo então podar.

---

- Sejam as sequências $\langle gb \rangle$ e $\langle gl \rangle$ pertencentes à classe de equivalência de $g$, e suas respectivas poslists $\mathcal{L}(gb) = \{ (2,3), (6,3) \}$ e $\mathcal{L}(gl) = \{ (2,3), (6,3) \}$
  - $\mathcal{L}(g(bl)) = \{ (2,3), (6,3) \}$
  - $\mathcal{L}(gbl) = \emptyset$
  - $\mathcal{L}(glb) = \emptyset$
- O algoritmo segue explorando o espaço de busca enquanto as classes de equivalência não forem vazias

---

- **ALGORITHM 10.2. Algorithm SPADE**
  - `// Initial Call:` $\mathcal{F} \leftarrow \emptyset, k \leftarrow 0, P \leftarrow \left{ \langle s, \mathcal{L}(s) \rangle | s \in \sum, sup(s) \geq minsup \right}$
  - **SPADE** $(P, minsup, \mathcal{F}, k)$
    - **foreach** $r_a \in P$ **do**
      - $\mathcal{F} \leftarrow \mathcal{F} \cup \left{ (r_a, sup(r_a)) \right}$
      - $P_a \leftarrow \emptyset$
      - **foreach** $r_b \in P$ **do**
        - $r_{ab} = r_a + r_b$
        - $\mathcal{L}(r_{ab}) = \mathcal{L}(r_a) \cap \mathcal{L}(r_b)$
        - **if** $sup(r_{ab}) \geq minsup$ **then**
          - $P_a \leftarrow P_a \cup \left{ \langle r_{ab}, \mathcal{L}(r_{ab}) \rangle \right}$
      - **if** $P_a \neq \emptyset$ **then** SPADE $(P, minsup, \mathcal{F}, k+1)$

#### Leitura (Aula 10)

- Seções 10.1 e 10.2 Zaki e Meira
- Capítulo 11 Aggarwal e Han
- [Link][Link_2001] Zaki, M.J. SPADE: An Efficient Algorithm for Mining Frequent Sequences. Machine Learning 42, 31–60 (2001).
- [Link][Link_1996] Srikant R., Agrawal R. (1996) Mining sequential patterns: Generalizations and performance improvements. In: Apers P., Bouzeghoub M., Gardarin G. (eds) Advances in Database Technology — EDBT '96. EDBT 1996. Lecture Notes in Computer Science, vol 1057. Springer, Berlin, Heidelberg.

[Link_2001]: https://doi.org/10.1023/A:1007652502315
[Link_1996]: https://doi.org/10.1007/BFb0014140

### Slide: aula07-grafos (Aula 10)

#### Introdução - Aula 10

- Nessa aula, vamos discutir o problema de mineração de subgrafos frequentes em bases de dadASDos de grafos.
- A mineração de subgrafos frequentes tem ganhado destaque nos últimos anos com aplicações em diversas áreas:
  - Quimioinformática: descoberta de princípios ativos de fármacos
  - Bioinformática: padrões de interação em redes de proteínas
  - Engenharia de Software: análise do fluxo de controle de aplicações

---

- Considerando o contexto de quimioinformática, temos o seguinte exemplo:

Cafeína, Teobromina (chocolate), Teofilina (tratamento de asma), Sildenafil (Viagra)

(Imagens de estruturas químicas omitidas)

#### Definições (Aula 10)

- Um grafo é uma quádrupla $(V, E, l, L)$ em que:

  - $V$ é um conjunto de vértices;
  - $E$ é um conjunto de arestas;
  - $l: V \rightarrow \Sigma_v$ é uma função que determina o rótulo dos vértices;
  - $L: E \rightarrow \Sigma_e$ é uma função que determina o rótulo das arestas.

- [JV]
  - Grafo Rotulado/Grafo com atributos
  - Aqui consideramos que esses rótulos são strings

(Imagem de um grafo)

---

- Sejam $G_1$ e $G_2$ dois grafos rotulados com os mesmos alfabetos $\Sigma_v$ e $\Sigma_e$.
- Dizemos que $G_1$ é subgrafo isomorfo a $G_2$, representado por $G_1 \subseteq G_2$, se existe uma função injetora $\upvarphi: V_1 \rightarrow V_2$ tal que:
  - $(u, v) \in E_1 \Leftrightarrow (\upvarphi(u), \upvarphi(v)) \in E_2$
  - $\forall u \in V_1,\ l(u) = l(\upvarphi(u))$
  - $\forall (u, v) \in E_1,\ L(u,v) = L(\upvarphi(u), \upvarphi(v))$
- [JV]
  - É isomorfo se eu consigo mapear tanto os vértices quanto os rótulos.

(Três imagens de grafos: $G_1$, $G_3$ e $G_4$)

Nessa imagem, o $G_3$ é subgrafo isomorfo de $G_1$, mas $G_4$ não.

---

- Uma base de dados $D = \{G_1, G_2, \dots, G_n\}$ é um conjunto de grafos rotulados.
- O suporte de um grafo (padrão) $G$ é o número de grafos em $D$ em que $G$ está contido:

  - $\text{sup}(G) = |\{G_i \in D\ |\ G \subseteq G_i\}|$

- Um padrão $G$ é frequente se $\text{sup}(G) \geq minsup$

(Imagem de vários subgrafos)

- [JV]
  - Esse conceito de conjunto de grafos rotulados tá mais próximo do problema de moléculas.
  - No caso de redes sociais como Facebook e Instagram, é mais parecido com um grafo monolitão.
  - O Suporte é calculado pegando um subgrafo e checando se ele encaixaria em um dos grafos. Ou algo assim.

---

- O problema de mineração de subgrafos frequentes consiste em encontrar todos os **subgrafos conexos** que satisfaçam o suporte mínimo definido pelo usuário.
- Comparado aos problemas vistos até agora, esse é o mais difícil em termos computacionais.
  - O problema de isomorfismo é NP-difícil.
- Um grafo com $m$ vértices possui $O(m^2)$ arestas.
- O número de subgrafos com $m$ vértices é, portanto, $2^{O(m^2)}$.
- Considerando grafos rotulados com $|\Sigma_v| = |\Sigma_e| = s$, $s^m$ rotulações diferentes de vértices e $s^{m^2}$ rotulações de arestas.
- Logo, o espaço de busca do problema é $2^{O(m^2)} \left(s^{O(m)}\right) \left(s^{O(m^2)}\right)$.

- [JV]
  - Ele colocou a mesma quantidade de rotulações de arestas e vértices com o mesmo valor só pra simplificar.
  - Tem gente que vai pra mineração de grafos distribuídos.

## Aula 11 | 22/04/2025 | Regras de associação e métricas de qualidade

### Slide: aula07-grafos (Aula 11)

#### Mineração de subgrafos frequentes

- Assim como aconteceu com os problemas anteriores, existem duas categorias de algoritmos:
  - Baseados no 'Apriori' (geração de candidatos)
  - Baseados no 'FP-Growth' (crescimento de padrões)
- Os algoritmos baseados no Apriori se subdividem em mais grupos:
  - Os baseados no aumento do número de vértices; e
  - Os baseados no aumento do número de arestas.
- Os baseados em crescimento de padrões frequentemente utilizam extensões de arestas para crescê-los.

- [JV]
  - O de Vértices tende a ser pior que o de arestas.

##### Geração de candidatos (AGM)

- A geração de candidatos com aumento do número de vértices é usada no algoritmo AGM (Apriori-based Graph Mining) proposto por Inokuchi et al. em 2000
- A ideia é juntar dois grafos com k vértices que compartilhem um núcleo com k-1 vértices para formar um candidato com k+1 vértices

- [JV]
  - É calculado calcular suporte por ter que procurar isomorfismo de grafos.
    - Automorfismo é mais fácil que isomorfismo
  - Prioridade do apriori: antimonotonicidade
    - Se um grafo é infrequente, qualquer supergrafo dele também será infrequente.
  - Algoritmo
    - Buscar o isomorfismo entre os dois grafos
      - Pega a matriz de adjacência de um grafo e compara com o outro
      - Caso removidas as colunas (i,i), ela não resulte numa matriz de adjacência isomorfa, entre ambos, então tente todas as remanescentes permutações
      - Se for isomorfo
        - remove as últimas linhas e colunas das duas, e cria um novo candidato misturando a linha e coluna do primeiro com a linha e coluna do segundo.
          - Porém, não se sabe qual o rótulo existente, ou não, entre os dois vértices adicionados.
          - Então, criam-se candidatos com todos os possíveis rótulos, inclusive a inexistência de rótulo.
      - Comparam-se também os rótulos, mas isso não ficou tão claro.
    - Pra calcular o suporte, gerando a sub-estrutura, confere se ela é subgrafo de outra
  - Não faz sentido falar de ordem lexicográfica de strings
    - Representação canônica de uma matriz de adjacência
    - Tipo uma identidade, um hash

##### Geração de candidatos (FSG)

- A geração de candidatos com aumento no número de arestas é usada pelo algoritmo FSG, proposto por Kuramochi e Karypis em 2001.
- Dois padrões com $k$ arestas são juntados se eles compartilham um núcleo (possuem um mesmo subgrafo) com $k-1$ arestas.
  - Ou seja, $G_1$ e $G_2$ são juntados se existe uma aresta em $G_1$ e uma aresta em $G_2$ tais que a remoção das duas torna os subgrafos isomorfos entre si.
  - Consequentemente, o candidato terá as arestas de $G_1$ mais essa aresta de $G_2$.
- Ao contrário do que ocorre com o método baseado em vértices, aqui o candidato resultante pode não ter um número maior de vértices que os padrões do qual foi gerado

- [JV]
  - FSG - Frequent Sub Graph (?)

---

- Um conceito importante para a geração de candidatos é o de vértices topologicamente equivalentes
  - [JV]
    - Topologicamente equivalentes:
      - Grafos que mantém a mesma estrutura geral.
      - Pra comparar, pode-se comparar entre possibilidades de novas arestas a novos vértices e/ou a arestas existentes.
      - Lembrando também da comparação dos rótulos.
      - É uma equivalência estrutural entre vértices de dois grafos distintos.
      - É isomorfo se consegue-se fazer um mapeamento 1:1 entre os vértices e arestas de um pro outro.
- Considere os grafos abaixo

(Imagens de grafos)

---

- Para entender o processo de geração de candidatos, vamos considerar dois grafos genéricos $G_1$ e $G_2$ com $k$ arestas que compartilham um núcleo comum com $k-1$ arestas
  - Na figura, o núcleo é omitido e somente as arestas não compartilhadas são ilustradas; os vértices dentro da caixa fazem parte do núcleo.
  - Se $a$ é topologicamente equivalente a $c$, dizemos que $a=c$
  - Se $b$ e $d$ possuem o mesmo rótulo, dizemos que $b=d$
  - [JV]
    - Nesse caso estão sendo definidos dois tipos de igualdades que serão representados com o mesmo símbolo de igualdade.
- Temos 4 possíveis situações
  - [JV]
    - Quando definimos esse núcleo, é como se as arestas que saem dele vão para os vértices externos fossem perdidas.

| X          | $a=c$ | $a \neq c$ |
| ---------- | :---: | :--------: |
| $b=d$      |   1   |     4      |
| $b \neq d$ |   2   |     3      |

---

- Situação 1 [$a \neq c$ e $b \neq d$]: Nesse caso, somente um candidato pode ser gerado, já que a 'nova' aresta incide em vértices distintos
  - [JV]
    - Obs.:
      - A imagem dele é meio confusa. G1 e G2 são os grafos inteiros. O quadradinho apenas representa o núcleo desses grafos. O que eu havia entendido antes e está errado é que o núcleo se chamava G1 e o núcleo se chamava G2.
      - Outro detalhe, os vértices $a$ e $c$ são vértices contidos no núcleo de um grafo grafo omitido;

---

- Situação 2 [$a=c$ e $b \neq d$]: Nesse caso, temos duas possibilidades:
  - A 'nova' aresta incide sobre vértices distintos como na situação 1
  - A 'nova' aresta incide sobre o vértice equivalente a $a$ (ou $c$)
  - [JV]
    - Uma análise interessante é observarmos que se apenas houver um mesmo vértice $a$ que seja topologicamente equivalente a $c$, então, apenas o segundo caso ocorre, visto que não há um segundo vértice para se anexar a aresta.

---

- Situação 3 [$a \neq c$ e $b=d$]: Nesse caso, temos duas possibilidades:
  - A 'nova' aresta incide sobre vértices distintos como na situação 1
  - A 'nova' aresta incide sobre o vértice equivalente a $b$ (ou $d$)

---

- Situação 4 [$a=c$ e $b=d$]: Nesse caso, qualquer das possibilidades anteriores pode ocorrer; ou seja, pelo menos 3 candidatos são gerados.

- [JV]
  - Foi comentado sobre o "pelo menos 3 candidatos". Ele disse não saber porque escreveu assim, e considera que serão sempre 3, ou talvez, "no máximo 3".

---

- Além dessas situações, dois grafos podem compartilhar múltiplos núcleos. Cada um deles pode gerar candidatos distintos.

  - Podem existir até $k-1$ núcleos distintos para dois padrões de tamanho $k$.

[Imagens de grafos]

---

- Naturalmente, muitos desses candidatos serão isomorfos entre si, devendo, portanto, serem descartados exceto uma cópia
- O controle de isomorfismo é feito atribuindo-se um código (string) a partir de cada matriz de adjacências
- Grafos com mesmo código são isomorfos
- Os detalhes são omitidos, mas podem ser consultados no artigo original

- [JV]
  - Geração de versão canônica de string da matriz de adjacência. Feito na força bruta.
    - Da matriz triangular superior, coluna a coluna, lineariza-se todos os rótulos.
    - Gera-se todas as as permutações dessa string e a mais lexicograficamente mais ordenada, é a versão canônica.

## Aula 12 | 24/04/2025 | Aprendizado descritivo supervisionado: padrões emergentes, contrastantes e descoberta de subgrupos

### Slide: aula07-grafos (Aula 12)

#### Mineração de subgrafos frequentes (Aula 12)

##### Crescimento de padrões (gSpan)

- De maneira similar ao que acontece com itemsets, os algoritmos baseados em geração de candidatos possuem desempenho inferior aos baseados em crescimento de padrões, já que muitos candidatos são podados
- Em 2002, Yan e Han (FP-Growth) propuseram o algoritmo gSpan (Graph-based Substructure Pattern Mining)
- O algoritmo estende os padrões acrescentando arestas, uma por vez, de forma similar ao comportamento do FP-Growth
- Os autores também propuseram representar grafos por sequências de strings
  - Isso, de certa forma, mapeia o problema de mineração de grafos para mineração de sequências; levando ao aproveitamento de ideias propostas na última
- Cada aresta do grafo é representada pela string:

  - $\langle v_i, v_j, l(v_i), l(v_j), L(v_i, v_j) \rangle$
    - [JV]
      - $v_i$ e $v_j$ são os vértices que compõem a aresta
      - $l(v_i)$ e $l(v_j)$ são os rótulos dos vértices
      - $L(v_i, v_j)$ é o rótulo da aresta

- [JV]
  - Começa com um grafo vazio e vai aumentando o grafo.
  - Projeta uma Base
  - Analisa todas as arestas possíveis para expandir

---

- A extensão dos padrões proposta por Yan e Han se baseia na árvore geradora da busca em profundidade
  - [JV] Baseado na ordem em que encontrou.
- Os vértices do grafo são ordenados conforme a ordem de visitação de uma busca em profundidade no grafo
  - Vértices visitados no início são menores que os visitados no fim
  - Subscritos dos vértices indicam a ordem de visitação
- O caminho mais curto entre o primeiro vértice e o último é chamado de **caminho mais à direita (rightmost path)**
- Considerando a busca em profundidade, as arestas são divididas em dois conjuntos:
  - **Fordward edges**: arestas que fazem parte da árvore geradora da DFS
  - **Backward edges**: demais arestas
    - [JV]
      - Arestas de retorno que vão para aresta já visitada antes.
      - $\langle v_i, v_j, \dots \rangle$ é uma aresta de retorno se $v_i < v_j$, ou seja, $v_i$ foi visitado antes de $v_j$ na DFS

---

- As arestas podem ser ordenadas dentro dos respectivos conjuntos da seguinte forma:
  - **Forward edges**: $e_1 = \left( v_{i_1}, v_{j_1} \right)$, $e_2 = \left( v_{i_2}, v_{j_2} \right)$, $e_1 \preceq_F e_2 \leftrightarrow j_1 < j_2$
    - [JV]
      - $j_1$ e $j_2$ representam a sequência de visitação dos vértices.
      - $\preceq_F$: é definida a ordem de precedência entre arestas de avanço.
  - **Backward edges**: $e_1 \preceq_B e_2 \leftrightarrow [i_1 < i_2 \lor (i_1 = i_2 \land j_1 < j_2)]$
    - [JV]
      - "Uma aresta (2, 0) vem antes de (3, 1)"; (3, 1) vem antes de (3, 2)
      - $\preceq_B$: é definida a ordem de precedência entre arestas de retorno.
  - [JV]
    - resumindo essa questão de ordenação de arestas: Estamos rodando a DFS e depois ~~ordenando lexicograficamente, primeiro pela origem, depois pela chegada.~~
    - Esse entendimento superior é falso. Na verdade, estamos ordenando justamente a sequência das arestas visitadas. E a sequência de comparações é bem esquisita mesmo.
- Adicionalmente comparamos arestas dos conjuntos da seguinte forma:
  - $e_1 \preceq_{BF} e_2$ sse:
    - $e_1$ é uma aresta de retorno; $e_2$ é uma aresta de árvore; e $i_1 < j_2$
    - $e_1$ é uma aresta de árvore; $e_2$ é uma aresta de retorno; e $j_1 \leq i_2$
- Combinando a ordem dos vértices, com a ordem sobre as arestas e a ordem lexicográfica definida sobre os rótulos (de vértices e arestas), definimos uma ordem total sobre as arestas (códigos)
- Dessa forma, os grafos podem ser representados como sequências de strings (códigos) referentes às suas arestas

---

```mermaid
flowchart LR
  A
```

- [JV]

  - Arestas:

    - $e_x = \langle v_i, v_j, l(v_i), l(v_j), L(v_i, v_j) \rangle$
    - $e_1 = \langle 0, 1, a, a, q \rangle$
    - $e_2 = \langle 1, 2, a, a, r \rangle$
    - $e_3 = \langle 2, 0, a, a, r \rangle$
    - $e_4 = \langle 1, 3, a, b, r \rangle$
    - Ordem: $e_1 \preceq e_2 \preceq e_3 \preceq e_4$

  - Uma comparação que causou muita dúvida, foi:
    - $e_4 = \langle 1, 3, a, b, r \rangle$
    - $e_4 = \langle 0, 3, a, b, r \rangle$
    - Entre elas, qual é menor?
    - Resposta: a primeira

```mermaid
flowchart LR
  0 --- 1
  1 --- 2
  1 --- 3
  0 --- 3
```

- Exemplo:
  - Retirado da Figura 11.6 Zaki e Meira

(Imagem de grafos com arestas rotuladas)

- [JV] Exercício: fazer as representações de arestas de todos os 3 grafos e ver que o G1 de fato é menor.

---

- Note que diferentes buscas geram diferentes representações
- Podemos estender a ordem lexicográfica das arestas para as representações (grafos)
- Chamamos de **representação canônica** a menor dentre todas as representações de um grafo
- Dois grafos são isomorfos se possuem a mesma representação canônica
- Assim, o problema de encontrar subgrafos frequentes é equivalente a enumerar suas representações canônicas
  - Uma vez que as representações são sequências, o problema é essencialmente um problema de mineração de sequências

---

- O gSpan explora em profundidade o espaço de busca estendendo prefixos (subgrafos) com arestas no caminho mais à direita
  - O artigo original demonstra que representações canônicas só podem ser geradas por arestas seguindo o caminho mais à direita
- Ele inicia com o prefixo vazio e o estende com cada uma das arestas em ordem
  - As possíveis extensões são determinadas a partir dos caminhos mais à direita dos grafos em que o prefixo ocorre
- O suporte das extensões são computados e, caso sejam frequentes e canônicas, são exploradas recursivamente

---

- **ALGORITHM 11.1. Algorithm gSpan**
  - // Initial Call: $C \leftarrow \emptyset$
  - **gSpan** $(C, D, minsup)$:
    - $\epsilon \leftarrow RightMostPath-Extensions(C, D)$ `// extensions and supports`
    - **foreach** $(t, sup(t)) \in \epsilon$ do
      - $C' \leftarrow C \cup t$ `// extend the code with extended edge tuple t`
      - $sup(C') \leftarrow sup(t)$ `// record the support of new extension`
      - `// recursively call gSpan if code is frequent and canonical`
      - **if** $sup(C') \geq minsup$ **and** IsCanonical $(C')$ **then**
        - **gSpan** $(C', D, minsup)$

---

- Exemplo: $D = \{G_1, G_2\}, minsup=2$

#### Extensões do problema

- Assim como ocorre com sequências e itemsets, o número de subgrafos frequentes pode ser bastante elevado em uma base
  - Isso acaba dificultando a análise dos resultados
- Existem abordagens, como o CloseGraph proposto por Yan e Han, que mineram padrões fechados
- Pode-se também buscar padrões contrastantes: com suporte mínimo em um subconjunto e máximo em outro
  - Exemplo: subgrafos que ocorrem com frequência no conjunto de moléculas que potencializam um efeito desejado; e que sejam infrequentes no conjunto de moléculas que apresentem efeitos adversos
  - Essa abordagem foi sugerida por Borgelt e Berthold no algoritmo chamado MoFa
  - Suporte mínimo é usado para podar o espaço de busca, enquanto o máximo usado para filtrar padrões indesejados
- Na linha de algoritmos, existem abordagens heurísticas para o problema, dado seu alto custo computacional
- Outras linhas de pesquisa incluem uso de abordagens distribuídas como o Fractal proposto por Dias et al. em 2019

#### Leitura

- Capítulo 11 Zaki e Meira
- Seção 7.5 Tan et al.
- Capítulo 5 Mining Graph Data, Diane Cook e Lawrence Holder
- Akihiro Inokuchi, Takashi Washio, and Hiroshi Motoda. 2000. An Apriori-Based Algorithm for Mining
  Frequent Substructures from Graph Data. In Proceedings of the 4th European Conference on Principles of
  Data Mining and Knowledge Discovery (PKDD '00). Springer-Verlag, Berlin, Heidelberg, 13–23.
- Michihiro Kuramochi and George Karypis. 2001. Frequent Subgraph Discovery. In Proceedings of the 2001
  IEEE International Conference on Data Mining (ICDM '01). IEEE Computer Society, USA, 313–320.
- Xifeng Yan and Jiawei Han. 2002. GSpan: Graph-Based Substructure Pattern Mining. In Proceedings of the
  2002 IEEE International Conference on Data Mining (ICDM '02). IEEE Computer Society, USA, 721.
- Xifeng Yan and Jiawei Han. 2003. CloseGraph: mining closed frequent graph patterns. In Proceedings of the
  ninth ACM SIGKDD international conference on Knowledge discovery and data mining (KDD '03). Association
  for Computing Machinery, New York, NY, USA, 286–295. <https://doi.org/10.1145/956750.956784>
- Christian Borgelt and Michael R. Berthold. 2002. Mining Molecular Fragments: Finding Relevant
  Substructures of Molecules. In Proceedings of the 2002 IEEE International Conference on Data Mining
  (ICDM '02). IEEE Computer Society, USA, 51

### Slide: aula08-regras-de-associação

## Aula 13 | 29/04/2025 | Descoberta de subgrupos

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
