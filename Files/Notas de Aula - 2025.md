# Aprendizado Descritivo - Renato Vimieiro - 2025

## Aula 1 - 18/03/2025 - [JV: Cheguei atrasado]

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
