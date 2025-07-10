# Apresentação do projeto

| Data de Apresentação |  ID | Integrantes                       |
| :------------------- | --: | --------------------------------- |
| 03/07/2025           |  01 | Daniel Schlickmann Bastos         |
| 03/07/2025           |  01 | Leonardo Caetano Gomide           |
| 03/07/2025           |  01 | Lucas Mesquita Andrade            |
| 03/07/2025           |  07 | Caio Jorge Carvalho Lara          |
| 03/07/2025           |  07 | José Eduardo Duarte Massucato     |
| 03/07/2025           |  07 | Vinícius Leite Censi Faria        |
| 03/07/2025           |  08 | Samuel Henrique Miranda Alves     |
| 03/07/2025           |  09 | Alexis Duarte                     |
| 03/07/2025           |  09 | Bernnardo Seraphim                |
| 03/07/2025           |  09 | Gabriel Castelo                   |
| 03/07/2025           |  09 | Henrique Rotsen                   |
| 03/07/2025           |  09 | Luisa Toledo                      |
| 08/07/2025           |  02 | Arthur Codama                     |
| 08/07/2025           |  02 | Caíque Fortunato                  |
| 08/07/2025           |  02 | Fabio Marra                       |
| 08/07/2025           |  02 | Victor Gabriel                    |
| 08/07/2025           |  02 | Wesley Marques                    |
| 08/07/2025           |  03 | Alexandre Cassimiro Silva Araújo  |
| 08/07/2025           |  03 | Diná Beatriz Xavier               |
| 08/07/2025           |  03 | Enilda Alves Coelho               |
| 08/07/2025           |  03 | Kael Soares Augusto               |
| 08/07/2025           |  03 | Mateus Reis Evangelista           |
| 08/07/2025           |  06 | Kênia Carolina Gonçalves          |
| 10/07/2025           |  04 | Gabriel Arcanjo Campelo Fadoul    |
| 10/07/2025           |  04 | Iasmin Correa Araujo              |
| 10/07/2025           |  04 | José Vinicius de Lima Massarico   |
| 10/07/2025           |  04 | Juan Marcos Braga Faria           |
| 10/07/2025           |  04 | Luiza Sodre Salgado               |
| 10/07/2025           |  10 | Guilherme Buxbaum Marinho Guerra  |
| 10/07/2025           |  10 | Lucas Xavier Veneroso             |
| 10/07/2025           |  10 | Marcelo Lommez Rodrigues de Jesus |
| 10/07/2025           |  10 | Oluwatoyin Joy Omole              |
| 10/07/2025           |  10 | Samuel Kfuri Ferraz Marcussi      |
| 10/07/2025           |  11 | Amanda Mendes Pinho               |
| 10/07/2025           |  11 | Gabriel Tonioni Duarte            |
| 10/07/2025           |  11 | João Vítor Fernandes Dias         |
| 10/07/2025           |  11 | Larissa Duarte Santana            |

## 03/07/2025

### ID 01

### ID 07

- Kaggle
- Filtragem
- Execução dupla do Beam Search
- WRAcc
- Mineração de Padrões Frequentes
- Países envolvidos e desenvolvidosz

### ID 08

- Estudo de caso de ITBI em BH
- Encontrar os grupos de imóveis que apresentaram valorizações atípicas

### ID 09

- Aluguel nos EUA
- 100k anúncios de apartamentos
- Mineração de itemsets nas amenidades
- Remoção de outliers por estado
- Itemsets de maior suporte
- Regras de associação
- Usaram Pysubgroup
  1. BeamSearch
  2. Pre-processamento das variáveis alvo
     - Análise de desvio padrão
  3. Modificação do algoritmo de Beam Search
     - Similaridade de Jaccard
     - Métrica de qualidade
- Aluguel, aluguel. Não é AirBnB

## 08/07/2025

### ID 06 - Kênia

- Twitch: entender de que forma as crianças e adolescentes se inserem no contexto da Twitch
- Content Classification Labels (CCLs) e Branded Content
  - CCL: Gambling, Violência, Mature não-sei-oq
  - Branded Content: Conteúdo Propocional
- Avaliou as informações de recomendações do Twitch
- Criou 3 personas USA e 3 personas BR. Idades distribuídas. Definiu os jogos mais recorrentes.

#### Sumarização de dados

- 9 de abril a 13 de maior
- 8h, 12h, 16h, 20h, 0h e 4h (Horário de Brasília)

#### Perguntas norteadoras

- Padrão de recomendação de streams por perfil?
- As recomendação são por localidade e/ou idade?

#### Frequência das streams recomendadas

- Itemset frequente - FP-Growth
  - BR_13
    - Minsup 0.1
    - 156 Mature
    - 162 Profanity
    - 411 Mature
  - US_13
  - BR_15
  - US_15

#### Similaridade entre os itemsets das personas

- Similaridade simples de Jaccard

#### Spade - minsup = 0.6 - Insucesso

#### Alguma coisa

- 30% alguma coisa

#### Subgrupos com propagandas

- Com target pra propaganas...

#### Trabalhos futuros

Pretende mudar para poder reanalisar verificando o jogo buscado.

- Analisar re-runs, verificar os canais.
- Fazer one-hot encoding para distribuir as tags em colunas+

### ID 02 - Arthur Codama; Caíque Fortunato; Fabio Marra; Victor Gabriel; Wesley Marques

#### Introdução

- Aplicar FP-Growth e ... para analisar dados sobre abuso doméstico, violência, estupro, etc.

#### Metodologia

- Dados públicos do Governo de MG.
- 61.000 registros
- Processamento pelo Colab
- Dados disponibilizados em excel com erros em datas
- Separou por dias da semana também: Seg~Dom e Final de Semana vs Meio da semana

##### Base de Dados

- Descrevem os atributos.
- BH; Metropolitana não-bh; interior
- Tentado ou consumado
- Quantidade de vítimas
- Fim de Semana = (1, 0)
- Reincidência: se o mesmo crime ocorreu no mesmo município
- FP-Growth

##### FP-Growth

- 3 descritores categóricos
- MLXtent
- Suporte de 0.05
- Lift e confiança como Métricas

###### Resultados

- Lift superiores a 7

#### SD - Descoberta de subgrupos

- One hot encoding para analisar atributos
- Métrica de qualidade WRAcc

Maior reincidência

#### Conclusão

- Reincidência e consumação é alta no final de semana
- Limitações e comentários
  - Pode conter subnotificações ou inconsistências
  - Não considerou os perfis demográficos
  - FP-Growth foca nos frequentes e desconsidera os infrequentes e relevantes
  - Chance de encontrar correlações expúrias
- Trabalhos futuros:
  - Adicionar novos dados.
  - Utilizar aprendizado de máquina interpretável

#### Comentários - ID2

- Se é Contagem, sempre é região metropolitana. Então acabam gerando regras triviais
  - Isso é o que ocorre quando há correlação forte entre as variáveis

### ID 03 - Alexandre Cassimiro Silva Araújo; Diná Beatriz Xavier; Enilda Alves Coelho; Kael Soares Augusto; Mateus Reis Evangelista

- Título: Análise categórica não supervisionada de gases do efeito estufa
- Our world in data

#### Roteiro

- Entendendo os dados
- Análise e preparação
- Algoritmo escolhido
- Resultados
- Considerações finais

#### Entendendo os dados

- Sempre em constante atualização
- 50k linhas; 79 atributos
- Análise exploratória estatística
- Dados estranhos e nulos:
  - A coluna `country` não eram necessariamente países. Alguns eram agrupamentos geopolíticos, etc.
  - Decidiram focar apenas nos países

#### Análise e exploração

- Limpeza dos dados: cobertura de dados x ano
  - Fizeram um gráfico temporal por linhas.
  - Um ponto de corte bom é ter 80% dos dados preenhidos. E os dados eram mais completos depois de 1900 e alguma coisa
- Remoção de Outliers
  - Distribuiram em quartis para encontrar entre os quartis
- Correlações de dados: CO_2 com a emissão de gases de efeito estufa. Etc.
- Clusterização dos dados: agrupar por países para buscar os padrões

#### Algoritmos utilizados

- MLXtend
- Suporte...

#### Resultados finais

- Sankey Diagram
- Suporte 10%
- Países com PIBs altos e altas emissões eram fortemente associados a alto consumo energético.
- Países com maiores variações de temperatura, têm também maiores emissões de gás.
- Discretizaram as colunas em 5 variações, o que possa ter causado a perda em associações inesperadas

#### Tentativa Falha: EMM

- Não conseguiram encontrar padrões excepcionais.

#### Conclusões

- Trabalharam bastante e em equipe
- Metodologia CRISP-DM é uma das mais utilizadas e funciona bem.

#### Imprevistos

- Dados muito fortemente correlacionados.
- Tentaram remover as colunas com correlações muito fortes.

#### Evaluation

- Críticas
  - Acabaram gerando regras bem simples
- Escolha final
  - Ainda assim usaram FP-Growth
- Deployment: GitHub: apresentação, notebook e artigo

#### Comentários - ID3

- Comentaram sobre Outliers
- Renato perguntou sobre o que eles tentaram com EMM

## 10/07/2025

### ID 04 - Gabriel Arcanjo Campelo Fadoul; Iasmin Correa Araujo; José Vinicius de Lima Massarico; Juan Marcos Braga Faria; Luiza Sodre Salgado

### ID 10 - Guilherme Buxbaum Marinho Guerra; Lucas Xavier Veneroso; Marcelo Lommez Rodrigues de Jesus; Oluwatoyin Joy Omole; Samuel Kfuri Ferraz Marcussi

### ID 11 - Amanda Mendes Pinho; Gabriel Tonioni Duarte; João Vítor Fernandes Dias; Larissa Duarte Santana
