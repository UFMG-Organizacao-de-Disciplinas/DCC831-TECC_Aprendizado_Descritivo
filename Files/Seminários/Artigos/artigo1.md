# Apresentação do [Artigo 1][Link_artigo]

- **Título:**
  - Differentiable Pattern Set Mining

[Link_artigo]: https://doi.org/10.1145/3447548.3467348

- [Apresentação](https://ufmgbr-my.sharepoint.com/:p:/g/personal/rvimieiro_ufmg_br/ESSM0mBDMNZFj7vzopqACYIBKOi3ChX9tsyje_2RroiT4Q)

## Apresentações

### Historiador: Grupo 1 (123456) - Representante: HENRIQUE ROTSEN SANTOS FERREIRA

- Contextualização
- Minerações de padrões vistos em aula
- Comparação Histórica
- Explicou sobre Asso, Slim e Desc.
  - SVD: fatoração de matrizes que reduz a matriz que consegue gerar a original.

---

- Ele comentou que sentiu falta do artigo não falando sobre a perda do gradiente.

### Formalizador: Grupo 2 (234561) - Representante: FABIO CESAR MARRA FILHO

- Autoencoders e BinaPs
  - Busca reduzir dimensionalidade
  - Explicou de que forma é diferenciável.
  - A transformação de entrada e saída é a mesma matriz, só que transposta.
  - Faz-se a binarização dos pesos.
  - O que significa a ativação do neurônio?
- Codificação
  - Existem vários neurônios na camada oculta?
  - Entender melhor o que significa essa sequência.
- Funcionamento do algoritmo
  - Aprende no Forward pass e ajusta no Backward propagation.
  - "Round é desnecessário"... será?
  - O padrão é montado na matriz de pesos.
- Atualização dos pesos e bias
  - Se a matriz for muito esparsa, ele tenderá a botar mais zeros.
  - Se a matriz for muito densa, ele tenderá a botar mais uns.
  - Nos dois casos se beneficiará com isso.
  - A função de perda faz o comparativo entre a matriz original e a reconstruída.
  - Ele estima o gradiente usando a base teórica do Bengio.
  - Porém, restringindo pra não punir os neurônios que não estavam ativos, logo, não sendo responsáveis pelo erro de reconstrução.
  - Porém, se ele foi ativado e o resultado foi positivo, então ele é recompensado.
  - A função Clamp é para definir os limites inferiores e superiores.

### Metodologista: Grupo 3 (345612) - Representante: LEONARDO CAETANO GOMIDE

- Experimentos
  - 4 neurônios: rodam mais rápido.
  - Comparativo com Asso, Slim e Desc.
  - Ele paraleliza esses 3 anteriores com... algo que ele julgou desbalanceado
- Dados sintéticos
  - 100k amostras, 20k colunas
  - As duas primeiras imagens comparam as features com a quantidade dos datasets
  - no início, tem 25% de chance de gerar um padrão que não existe
  - Ele sentiu falta de informações sobre intervalo de confiança, mas como os resultados são bem discrepantes, não tem tanto problema.
- Dados Reais
  - Asso, Desc e Slim não conseguiram rodar em bases de dados reais
- Dados Densos
  - BinaPS e Asso encontraram...
  - Slim e Desc...
- Resultados Qualitativos
  - Instacart
    - BinaPS: padrões densos e ruidosos
  - Genomes
    - Encontrou padrões que existem mas não necessariamente fazem sentido.
    - Também citou conjuntos que condizem com o que já é estudado e sabido.
- Análise Crítica
  - Min-average...
  - Não é diferenciável em 0, o que pode dar um problema pra rede.
  - min-square-error poderia ser uma função de ativação mais derivável.
  - Eles falaram sobre a quantidade de neurônios iguais ao tamanho de entrada, mas o artigo não falou muito sobre isso.
  - Trabalhos futuros:
    - Como achar padrões... (de um tipo específico que não entendi)

### Assessor social: Grupo 4 (456123) - Representante: KÊNIA CAROLINA GONÇALVES

- Crítica geral: o artigo é muito técnico e não apresenta o impacto social de forma clara.

- Impacto Social
  - Consegue propor padrões identificáveis.
  - A personalização do algoritmo é algo positivo pela maleabilidade que traz.
  - Risco de falsa objetividade.
- Cenários
  - Saúde
  - Cidades inteligentes
  - Educação
  - Comércio
  - Governos
- Problemas com privacidade, equidade, discriminação e igualdade​
  - Exemplo 1: concessão de crédito discriminatória.
  - Exemplo 2: Precificação de seguros e planos de saúde. Algoritmos que conseguiriam identificar as pessoas baseados no padrão de comportamento.
- Outros possíveis danos
  - Método de poisoning: se sei como o algoritmo funciona, consigo agir de forma maliciosa e forçar o algoritmo a se comportar de um jeito específico que desejo.
  - Aspecto ético...

---

- Essa parte de ética é pouquíssimo explorada.
- Não se financia tanto quem analisa os efeitos e impactos sociais no mundo.
- Acabam surgindo problemas por falta de multidisciplinaridade que ajudaria a resolver alguns problemas.
- Em termos técnicos, um dos problemas é a falta de explicabilidade das redes neurais.

### Hacker: Grupo 5 (561234) - Representante: ?

- CAIO JORGE CARVALHO LARA
- JUAN MARCOS BRAGA FARIA
- LUISA VASCONCELOS DE CASTRO TOLEDO
- LUIZA SODRE SALGADO
- MATEUS REIS EVANGELISTA
- SAMUEL HENRIQUE MIRANDA ALVES

Falarão do passo a passo pra instalar.

- Instalação e Dependências
  - Têm a base de dados sintéticos e o genômico.
  - O download dos dados genômicos é sugerido que rode em um computador com 1Tb de RAM
  - Eles conseguiram rodar o de gerar dados sintéticos com apenas 16Gb de RAM.
  - Usaram PyTorch para gerar as redes neurais.
  - Usaram também R para fazer alguma coisa que não entendi.
- Hacker
  - Apresentaram outros passos para rodar o código, e também uma tabela com os parâmetros
- Geração dos Dados de Entrada
  - O arquivo DAT é um arquivo de transações. Cada linha contém os elementos em que estão na transação.
  - Disse que é a representação horizontal da base de dados.
  - Dados sintéticos geraram em torno de 100k linhas
- Execução
  - Cada uma das épocas demoraram cerca de 1 minuto.
  - A Average Loss aparentemente deve ser a Total Loss.
  - Acurácia de 0%, por que? Idealmente a saída deve ser igual à entrada.
  - Apenas reconstruiu perfeitamente 30 dos 9971 padrões.
  - Porém essa acurácia pífia não é um problema, afinal, não é esse o objetivo.
  - Supp_full: se todos os itens acontecem no padrão, computa 1
  - Supp_half: se pelo menos metade dos elementos aparecem no padrão, computa 1
  - Os dois suportes sempre resultavam em valores bem próximos, o que revela uma confiança bem grande dentro dos padrões.
  - Isso (?) é uma tentativa de interpretar o que os padrões revelam sobre as bases de dados.

### Relator: Grupo 6 (612345)

- ALEXIS DUARTE GUIMARAES MARIZ
- AMANDA MENDES PINHO
- GABRIEL CHAVES FERREIRA
- **JOÃO VÍTOR FERNANDES DIAS**
- **KAEL SOARES AUGUSTO**
- LUCAS XAVIER VENEROSO

#### Termos desconhecidos

- neural autoencoder
  - An autoencoder is a neural network consisting of task-specific encoding layers that end in an embedding layer, and a symmetric decoder to reconstruct the input from the embedding layer.
- BinaPs
  - R: Binary Pattern Networks
- MDL (Minimum Description Length) principle
- acrually
- Clamping function

#### Dúvidas

- This solves one problem, but creates another: the search space for pattern sets is even larger than that of patterns alone - doubly exponential in the number of features
- Pattern Set mining approaches:
  - Tiling
  - Boolean Matrix Factorization
- information theoretic approaches that use the MDL principle
- > at the cost of a twice exponential search space that does **not expose any easy to exploit** structure
  - Significa que não há uma estrutura que facilite a exploração do espaço de busca?
- O que seria a presença de ruído nos dados?
- > continuous versions of the weights
  - Como algo em computação pode ser contínuo?
- > each neuron in the hidden layer corresponds to a pattern p, while all neurons together correspond to the pattern set P.
  - > Ué, mas como?
- > To ensure that the hidden neurons correspond to actual patterns, and that such patterns are interpretable,
  - Ora, se são escondidos como podem ser interpretáveis?

#### Comentários

In this paper we propose a radically different strategy to pattern set mining that scales extremely well in both $n$ and $m$, naturally handles noise, and copes equally well with sparse and dense data.

- Renato
  - 1/m tende a zero, porque m tende a ser um número muito grande.
  - Outro ponto positivo é conseguir reduzir a dimensionalidade dos dados.
