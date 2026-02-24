# 02 Lei dos Grandes Números (LLN)

## Enunciado

A Lei dos Grandes Números (LLN) afirma que a média amostral converge para a média populacional à medida que o tamanho da amostra cresce.

Formalmente, para uma população com média $\mu$ e para $\varepsilon > 0$:

$$
\lim_{n \rightarrow \infty} \Pr(\left|\overline{x}_n-\mu \right|<\varepsilon ) = 1
$$

Essa expressão diz que a probabilidade de a média amostral ficar arbitrariamente próxima de $\mu$ tende a 1 quando $n$ aumenta.

## Exemplo conceitual: lançamento de um dado

Considere um dado justo com resultados em $\{1,2,3,4,5,6\}$.

Para uma variável aleatória discreta $X$:

$$
\mu_X = \operatorname{E}[X] = \sum_x x \times \Pr(X=x)
$$

No caso do dado:

$$
\operatorname{E}[X] = 1\cdot\frac{1}{6}+2\cdot\frac{1}{6}+3\cdot\frac{1}{6}+4\cdot\frac{1}{6}+5\cdot\frac{1}{6}+6\cdot\frac{1}{6}=3.5
$$

Pela LLN, à medida que aumentamos o número de lançamentos, a média amostral tende a se aproximar de $3.5$.

## Declaração equivalente

Uma formulação comum da LLN é:

> A média amostral de $n$ variáveis aleatórias i.i.d. converge para a média populacional conforme $n$ cresce.

## Esboço de demonstração (Chebyshev)

A desigualdade de Chebyshev para uma variável aleatória com média $\mu$ e variância finita $\sigma^2$ é:

$$
\Pr(|X - \mu| \geq \varepsilon) \leq \frac{\sigma^2}{\varepsilon^2}
$$

Aplicando em $\overline{x}$ (média amostral):

$$
\Pr(\left|\overline{x}-\mu_{\overline{x}} \right|\geq \varepsilon ) \leq \frac{\sigma^{2}_{\overline{x}}}{\varepsilon ^{2}}
$$

Usando $\mu_{\overline{x}}=\mu$ e $\sigma^2_{\overline{x}}=\sigma^2/n$:

$$
\Pr(\left|\overline{x}-\mu \right|\geq \varepsilon ) \leq \frac{\sigma ^{2}}{n\varepsilon ^{2}}
$$

Então:

$$
\Pr(\left|\overline{x}-\mu \right|<\varepsilon ) \geq 1-\frac{\sigma ^{2}}{n\varepsilon^{2}}
$$

Como $n \to \infty$, o termo da direita tende a $1$, concluindo:

$$
\lim_{n \rightarrow \infty} \Pr(\left|\overline{x}-\mu \right|<\varepsilon ) = 1
$$
