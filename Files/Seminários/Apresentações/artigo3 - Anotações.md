# Apresentação do [Artigo 3][Link_artigo]

- **Título:** Finding Interpretable Class-Specific Patterns through Efficient Neural Search
- [Artigo][Link_artigo]
- [Apresentação][Slide_art3]

[Link_artigo]: https://doi.org/10.1609/aaai.v38i8.28756
[Slide_art3]: https://ufmgbr-my.sharepoint.com/:p:/g/personal/rvimieiro_ufmg_br/EW8h3xu3PZVAiPK7gVoI98YBNdUZGMz9aQORBipu-AqjbQ

## Apresentações

### Historiador: Grupo 5 (561234) - Representante: CAIO JORGE CARVALHO LARA

- Descoberta de subgrupos (Subgroup Discovery)

#### Motivação e Justificativa

#### Trabalhos Relacionados

- **CART:** ...
- **SPUMANTE:** explode por algo relacionado ao teste de hipótese
- **PREMISE:** busca conjunto não redundante de padrões
- **CLASSY:** foca mais em previsão do que descrição
- **RLL:** foca na precisão da classificação

Benefício do **DiffNaps:** ...

#### Comparação com Métodos Clássicos

[Tabela Maneira]
### Formalizador: Grupo 6 (612345) - Representante: KAEL SOARES AUGUSTO

#### DiffNaps in a Nutshell

- AutoEncoder

#### DiffNaps in Detail

- Alguma coisa relacionada ao número de $k$, $p$ e classes.

#### Forward Pass

- $\lambda_E$: Função de binarização
- ...

#### Objective Function

- A objective function é uma loss function.
- Cross Entropy Loss: compara o Ground-Truth com o que foi encontrado.
- W-shaped regularizer
    - Só um outro artigo fala sobre. E tem duas variáveis. Provavelmente uma varia a barriga do W e a outra varia a angulação do W.

#### Back Propagation - Simplified

- Usa derivadas parciais, mas com a ...
- Não penaliza neurônios desativados.

---

$$
\boxed{
  \mathbb{P}(p \mid k) = \frac{supp_k(p)}{n_k}
}
\text{\quad e \quad}
\boxed{
  \mathbb{P}(k \mid p) = \frac{supp_k(p)}{supp(p)}
}
\\
\begin{align*}
\mathbb{P}(p \mid k) &= \frac{supp_k(p)}{n_k}, \\
\mathbb{P}(k \mid p) &= \frac{supp_k(p)}{supp(p)}.
\end{align*}
$$

---

$$
z = f_E(x) = \lambda_E(f_{W^E_b} (x))
\\
\hat{x} = f_D(z) = \lambda_D(f_{W^D_b} (z))
$$

$$
l_e(x, \hat{x}) = \sum_{j=1}^m \left( (1 - x_j)\alpha + x_j(1 - \alpha) \right) |x_j - \hat{x}_j|
$$

$$
l_c(y, \hat{y}) = \sum_{k=1}^K y_k \log(\hat{y}_k)
$$

$$
r_s(W) = \sum_{i=1}^m \left( \sum_{j=1}^h W_{i,j} \right)^2
$$

$$
r_b(W) = \sum_{w \in W} \min \left\{ r(w),\ r(w - 1) \right\}
$$

$$
r(w) = \kappa \|w \|_1 + \lambda \|w\|_2^2
$$

$$
\mathcal{L}(X, Y; \theta) = \sum_{i=1}^n l_e(y_i, \hat{y}_i) + \lambda_c \, l_c(x_i, \hat{x}_i) + r_s(W^E) + r_b(\theta)
$$

$$
\frac{\partial f_{W^E_b}}{\partial W^E} := g_u x^{\top}
$$

$$
\frac{\partial f_{W^E_b}}{dx} := (W^E)^{\top} g_u
$$

$$
\frac{\partial \lambda_E}{\partial b} :=
\begin{cases}
g_u & \text{se } \lambda_E(x) = 1 \\
0 & \text{se } \lambda_E(x) = 0
\end{cases}
$$

$$
\frac{\partial \lambda_E}{\partial x} :=
\begin{cases}
g_u & \text{se } \lambda_E(x) = 1 \\
\max(0, g_u) & \text{se } \lambda_E(x) = 0
\end{cases}
$$

### Metodologista: Grupo 1 (123456) - Representante: VICTOR GABRIEL MOURA OLIVEIRA

#### Estratégia experimental: baseline

#### Estratégia experimental: dados sintéticos

- Usa a similaridade de Jacard, F1.

#### Análise Quantitativa

### Assessor social: Grupo 2 (234561) - Representante: ENILDA ALVES COELHO

#### Inovação Tecnológica

#### Cenários de uso

- Genomas
- Salvar vidas

---

- O artigo menciona sobre casos de uso em uma nota de rodapé.
- Encontrar os padrões de dados pode resultar em economia

#### Potenciais riscos e danos à sociedade

- Reidentificação de indivíduos
- Reforço de viéses
- Desigualdades
- Limitação dos dados

### Hacker: Grupo 3 (345612) - Representante: LUCAS MESQUITA ANDRADE

---

#### Rodar

1. Clonar o Repositório​
2. Baixar Dependências​
3. Atualizar a base de Dados dentro da arquitetura​
4. Rodar os Arquivos Python

#### Limitações

- 40Gb GPU
- 2Tb

Para resolver, usou o Colab e passou a criar dados sintéticos

- Exp1: 74 Gb de RAM
- Exp2: 75 Gb de RAM
- Exp3: 16 min
    - Roda CSV com métricas
    - Roda 5 testes
    - Cada 30 segundos por dado por época
    - Cada um dos experimentos, 5 épocas
- Exp4: Um monte de métricas

#### Conclusões finais

- Recursos caríssimos. O laboratório do SPEED não tankaria rodar.
- Não tá 100% atualizado
- Base difícil de recriar
- Mas deu bom 👍

### Relator: Grupo 4 (456123)

- BERNNARDO SERAPHIM BAPTISTA DE OLIVEIRA
- DINÁ BEATRIZ XAVIER
- GABRIEL ARCANJO CAMPELO FADOUL
- KÊNIA CAROLINA GONÇALVES
- LUCAS VITOR DA SILVA RAMOS
- OLUWATOYIN JOY OMOLE
- SAMUEL KFURI FERRAZ MARCUSSI

## Discussão

- **Renato:** ao invés de usar os dados dele, se usasse dados de alguma base, poderia?
    - **Resposta:** parece que os dados dele já são bem tratados para o caso específico
- **Renato:** foi fácil usar o DiffNaps sem os dados de estresse?
    - **Resposta:** Pra você conseguir usar o código dele precisa entender bem o que tá rolando.
    - Algumas partes usam configurações muito específicas do Torch.
- Aplicação da Lâmina de Ockham: o menor modelo que classifica o que queremos (?)
- Talvez os padrões são redundantes, ou não.
- "'Conjunto, lista ou buscar padrões' pra mim é a mesma coisa"
- A qualidade desse artigo é muito melhor que o de quinta.
- "O artigo que fundou o KDD, foi publicado no 3AI (AAAI)"
- Sugestão: fazer código que automaticamente já cospe as imagens estatísticas.
- "Daqui 5 anos teremos um datacenter"