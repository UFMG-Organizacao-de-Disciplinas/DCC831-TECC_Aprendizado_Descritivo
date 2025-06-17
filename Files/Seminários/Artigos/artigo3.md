# Apresentação do [Artigo 3][Link_artigo]

- **Título:** Finding Interpretable Class-Specific Patterns through Efficient Neural Search
- [Artigo][Link_artigo]
- [Apresentação][Slide_art3]

[Link_artigo]: https://doi.org/10.1609/aaai.v38i8.28756
[Slide_art3]: https://ufmgbr-my.sharepoint.com/:p:/g/personal/rvimieiro_ufmg_br/EW8h3xu3PZVAiPK7gVoI98YBNdUZGMz9aQORBipu-AqjbQ

## Apresentações

### Historiador: Grupo 5 (561234) - Representante

- CAIO JORGE CARVALHO LARA
- JUAN MARCOS BRAGA FARIA
- LUISA VASCONCELOS DE CASTRO TOLEDO
- LUIZA SODRE SALGADO
- MATEUS REIS EVANGELISTA
- SAMUEL HENRIQUE MIRANDA ALVES

### Formalizador: Grupo 6 (612345) - Representante

- ALEXIS DUARTE GUIMARAES MARIZ
- AMANDA MENDES PINHO
- GABRIEL CHAVES FERREIRA
- JOÃO VÍTOR FERNANDES DIAS
- **KAEL SOARES AUGUSTO**
- LUCAS XAVIER VENEROSO

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

### Metodologista: Grupo 1 (123456) - Representante

- ALEXANDRE CASSIMIRO SILVA ARAÚJO
- ARTHUR YOCHIO RODRIGUES CODAMA
- CAÍQUE BRUNO FORTUNATO
- HENRIQUE ROTSEN SANTOS FERREIRA
- VICTOR GABRIEL MOURA OLIVEIRA
- WESLEY MARQUES DANIEL CHAVES

### Assessor social: Grupo 2 (234561) - Representante

- ENILDA ALVES COELHO
- FABIO CESAR MARRA FILHO
- GABRIEL TONIONI DUARTE
- IASMIN CORREA ARAUJO
- JOSE VINICIUS DE LIMA MASSARICO
- LARISSA DUARTE SANTANA
- MARCELO LOMMEZ RODRIGUES DE JESUS

### Hacker: Grupo 3 (345612) - Representante

- DANIEL SCHLICKMANN BASTOS
- GABRIEL CASTELO BRANCO ROCHA ALENCAR PINTO
- GUILHERME BUXBAUM MARINHO GUERRA
- JOSE EDUARDO DUARTE MASSUCATO
- LEONARDO CAETANO GOMIDE
- LUCAS MESQUITA ANDRADE
- VINICIUS LEITE CENSI FARIA

### Relator: Grupo 4 (456123)

- BERNNARDO SERAPHIM BAPTISTA DE OLIVEIRA
- DINÁ BEATRIZ XAVIER
- GABRIEL ARCANJO CAMPELO FADOUL
- KÊNIA CAROLINA GONÇALVES
- LUCAS VITOR DA SILVA RAMOS
- OLUWATOYIN JOY OMOLE
- SAMUEL KFURI FERRAZ MARCUSSI
