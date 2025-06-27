# Apresentação do [Artigo 5][Link_artigo]

- **Título:** Modeling Match Performance in Elite Volleyball Players: Importance of Jump Load and Strength Training Characteristics
- [Artigo][Link_artigo]
- [Apresentação][Slide_art5]

[Link_artigo]: https://doi.org/10.3390/s22207996
[Slide_art5]: https://ufmgbr-my.sharepoint.com/:p:/g/personal/rvimieiro_ufmg_br/EQlMXoDU67NJgy7N3rJy_tUBlESMKSnWfhPJnaIiK0Qh6A

## Apresentações

### Historiador: Grupo 3 (345612) - Representante - GUILHERME BUXBAUM MARINHO GUERRA

#### Objetivo

- Investigar as relações entre carga de treinamento, bem-estar e desempenho de atletas profissionais de vôlei utilizando XGBoost, Random Forest e descoberta de subgrupos
  - XGBoost
  - Random Forest
  - Descoberta de subgrupos

### Formalizador: Grupo 4 (456123) - Representante: DINÁ BEATRIZ XAVIER

- One-hot-encoding

### Metodologista: Grupo 5 (561234) - Representante: JUAN MARCOS BRAGA FARIA

#### Discussão

- Preditores mais importantes:
  - Melhor ataque: Carga de treinamento de força de membros inferiores (4 sem.) (maiores pulos)
  - Pior ataque: Altura dos saltos (4 sem.) (menores pulos) e Excesso de carga em parte superior (menos controle)
  - Pior passe: Altura média dos saltos (1 semana) ("reduced freshess")
  - Bem estar não teve impacto.
- Limitações e trabalhos futuros:
  - Número baixo de jogadores para coletar os dados
  - Os melhores modelos de aprendizado performaram tão bem quanto modelos que se baseavam na média dos scores do tipo da ação
  - Avaliar variações nos cronogramas de treinamento
  - Pesos para importância da partida ou nível do oponente

### Assessor social: Grupo 6 (612345) - Representante: KAEL SOARES AUGUSTO

#### Aplicação: Esportes

- O artigo mostra a aplicação de métodos de descoberta de subgrupos para o melhor desempenho de atletas, por meio de:
  - Personalização de treinos
  - Análise de performance
  - Delimitação de treinos úteis e menos úteis
  - Medidas de previsão de desempenho em partida a partir do treino
- **Como dito no resumo do artigo:**
  - > "Differences in findings with respect to passing and attack performance suggest that elite volleyball players can improve their performance if training schedules are adapted to the position of a player. "

#### Aplicação: Desempenho em geral

- Nota-se que não necessariamente precisamos limitar a análise para análise de esportes. Podemos, por exemplo, fazer as seguintes trocas:
  - Treino (peso, repetições, etc) -> Estudos; Tempo e forma de trabalho;
  - Resultados na partida -> Entregas de trabalhos e tarefas
- O algoritmo pode ser generalizado para ambientes de estudos, trabalhos e hobbies pessoais, permitindo uma análise de quais as melhores formas de dedicação para alcance de melhores resultados.
- > "Empregados que passaram 20% das horas em repouso, 55% das horas trabalhando e 15% das horas estudando tiveram entregas mais pontuais."
- > "Empregados que variavam bastante o seu horário de entrada e saída tendem a terem resultados piores na avaliação das entregas."

#### Risco: Controle

Na busca de terem os dados mais atualizados, empresas e organizações podem acabar usando os estudos analíticos como desculpa para controlarem funcionários e atletas. Considere o caso à direita como exemplo:

Isso leva ao descontentamento de funcionários, considere os seguintes comentários:

---

Imagens Reddit

#### Risco: Privacidade

- O monitoramento constante das pessoas pode afetar a sua privacidade, especialmente quando:
  - Os dados forem usados sem consentimento claro ou transparência.
  - Houver coleta em excesso (dados sensíveis, pessoais).
  - Os dados monitoram a pessoa de forma a remover a privacidade em ambiente privados.
  - Houver vazamento de dados pessoais.

### Hacker: Grupo 1 (123456) - Representante: HENRIQUE ROTSEN SANTOS FERREIRA

#### Tentando obter os dados

- O artigo menciona que os dados não podem ser compartilhados publicamente, pois são propriedade da NeVoBo (Federação Holandesa de Voleibol). No entanto, os dados estão disponíveis mediante solicitação ao autor correspondente.
  - No artigo tem somente o e-mail do primeiro autor: Arie-Willem de Leeuw
  - O professor mudou de universidade, então o e-mail não existe mais
  - Procuramos o e-mail atual do Arie-Willem de Leeuw: ainda sem resposta
- O detentor dos dados é o segundo autor: Rick van Baar, ele era treinador, mas saiu da instituição NeVoBo.
  - Após muita busca, foi encontrado o e-mail: ainda sem resposta

#### Tentando obter os algoritmos

- Embora os dados brutos não estejam abertos, talvez o código-fonte para o método (os algoritmos de aprendizado de máquina e a engenharia de recursos) possa estar em um repositório. O artigo menciona o uso de **XGBoost**, **random forest regression** e **subgroup discovery**.
  - Buscamos o repositório no GitHub, mas não obtivemos sucesso.
- Porém, o uso dos algoritmos pode ser exemplificado:
- Random Forest Artigo: [Link do artigo](http://doi.org/10.1023/A:1010933404324)
  - Git: [Link do git](https://github.com/scikit-learn/scikit-learn/blob/main/sklearn/ensemble/_forest.py)
  - Biblioteca Py: from sklearn.ensemble import RandomForestClassifier
  - Exemplo de uso: [Link do git](https://github.com/matheuslima29/ML_Random-Florest/blob/main/Treinamento_RandomFlorest.ipynb)
- XGBoostArtigo: [Link do artigo](https://github.com/matheuslima29/ML_Random-Florest/blob/main/Treinamento_RandomFlorest.ipynb)
  - Git: [Link do git](https://github.com/dmlc/xgboost)

#### Características dos dados originais

- **Desempenho de Partida:**
  - Avaliações de ações de voleibol (ataque, bloqueio, recepção...) em uma escala de 0 a 10.
- **Carga de Salto:**
  - Número de saltos e alturas de salto (total, baixos < 50cm, médios entre 50-65cm, altos > 65cm).
- **Treinamento de Força:**
  - Pesos de exercícios (em kg absolutos ou % de 1-RM) divididos em corpo inteiro, parte inferior e parte superior do corpo.
- **Carga de Treinamento Percebida (RPE):**
  - Usando a escala CR10 para sessões de voleibol e força.
- **Bem-estar Percebido (Wellness):**
  - Medidas de fadiga, qualidade do sono, horas dormidas e humor em uma escala Likert de 10 pontos.
- **Períodos de Agregação:**
  - Dados agregados em janelas de 7, 14 ou 28 dias anteriores à partida, com funções como primeiro quartil, média, terceiro quartil e desvio padrão.

#### Como reproduzir?

- Procure por conjuntos de dados de voleibol abertos e disponíveis publicamente que sejam similares em natureza aos dados usados no artigo.
- O objetivo não é replicar exatamente os resultados, mas demonstrar como o método poderia ser aplicado e os tipos de padrões que poderiam ser encontrados.
- Implementação do algoritmo não faz parte do escopo.

#### Simulando o Dataset

Imagens

#### [Link para o Colab](https://colab.research.google.com/drive/15R61oNN5Zd-iGZFAnTTejkz1zHnHu6ZM?usp=sharing)

### Relator: Grupo 2 (234561)

- ENILDA ALVES COELHO
- FABIO CESAR MARRA FILHO
- GABRIEL TONIONI DUARTE
- IASMIN CORREA ARAUJO
- JOSE VINICIUS DE LIMA MASSARICO
- LARISSA DUARTE SANTANA
- MARCELO LOMMEZ RODRIGUES DE JESUS

## Comentários sobre o artigo

- A quantidade de dados pequena já seria grande o bastante para um artigo?
  - Sim, mas as conclusões são para o escopo limitado do artigo.
- No ponto de vista da ciência, todo artigo deveria ser reprodutível, mas aparentemente nem sempre é o caso. Tem esse tipo de motivação pra UFMG?
- E afinal, é generalizável para as diversas posições? Pros jogadores?
