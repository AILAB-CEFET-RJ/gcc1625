# 02c Lei dos Grandes Números (LLN)

## Enunciado

A Lei dos Grandes Números (LLN) afirma que a média amostral converge para a média populacional à medida que o tamanho da amostra cresce.
Nesta seção, consideramos $X_1,\ldots,X_n$ i.i.d. com $\mu=\operatorname{E}[X_i]$ finita.

Nota de continuidade com o tópico anterior (TLC): as limitações associadas a caudas muito pesadas e ao caso de variância infinita foram discutidas em `02b_CLT.md`. Aqui focamos no mecanismo de convergência da média amostral sob as hipóteses explicitadas.

Formalmente (LLN fraca), para $\varepsilon > 0$:

$$
\lim_{n \rightarrow \infty} \Pr(\left|\overline{X}_n-\mu \right|<\varepsilon ) = 1
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

> A média amostral $\overline{X}_n$ de variáveis aleatórias i.i.d. converge em probabilidade para $\mu$ conforme $n$ cresce.

## Esboço de demonstração (Chebyshev)

A desigualdade de Chebyshev para uma variável aleatória com média $\mu$ e variância finita $\sigma^2$ é:

$$
\Pr(|X - \mu| \geq \varepsilon) \leq \frac{\sigma^2}{\varepsilon^2}
$$

Aplicando em $\overline{X}_n$ (média amostral):

$$
\Pr(\left|\overline{X}_n-\mu_{\overline{X}_n} \right|\geq \varepsilon ) \leq \frac{\sigma^{2}_{\overline{X}_n}}{\varepsilon ^{2}}
$$

Usando $\mu_{\overline{X}_n}=\mu$ e, pela independência, $\sigma^2_{\overline{X}_n}=\sigma^2/n$:

$$
\Pr(\left|\overline{X}_n-\mu \right|\geq \varepsilon ) \leq \frac{\sigma ^{2}}{n\varepsilon ^{2}}
$$

Então:

$$
\Pr(\left|\overline{X}_n-\mu \right|<\varepsilon ) \geq 1-\frac{\sigma ^{2}}{n\varepsilon^{2}}
$$

Como $n \to \infty$, o termo da direita tende a $1$, concluindo:

$$
\lim_{n \rightarrow \infty} \Pr(\left|\overline{X}_n-\mu \right|<\varepsilon ) = 1
$$

Este esboço prova a convergência em probabilidade no caso com variância finita, que é a forma mais usada na prática introdutória.

## Relação com o TLC

- A LLN descreve a **convergência do centro**: $\overline{X}_n \to \mu$ em probabilidade.
- O TLC descreve a **forma da distribuição amostral**: para $n$ grande, $\overline{X}_n$ é aproximadamente normal.
- Portanto, LLN e TLC são complementares: uma explica *para onde* a média vai; a outra explica *como* ela se distribui ao redor desse valor.

## Dúvida comum: "isso já não está no TLC?"

Pergunta típica: se o TLC também fala de $\overline{X}_n$, por que estudar LLN separadamente?

Resposta curta: LLN e TLC tratam de aspectos diferentes da média amostral.

- **LLN:** responde **para onde** $\overline{X}_n$ vai.
$$
\overline{X}_n \xrightarrow{P} \mu
$$
Isto é, a média amostral se aproxima do parâmetro populacional (consistência).

- **TLC:** responde **como** $\overline{X}_n$ oscila em torno de $\mu$ para $n$ grande.
$$
\frac{\overline{X}_n-\mu}{\sigma/\sqrt{n}} \xrightarrow{d} \mathcal{N}(0,1)
$$
Isto é, descreve a forma aproximada da distribuição do erro de estimação.

Sob hipóteses usuais (i.i.d. e variância finita), o TLC é mais forte e implica a mensagem central da LLN. Ainda assim, didaticamente é útil separar: a LLN fixa a ideia de convergência para o alvo; o TLC quantifica a flutuação ao redor do alvo.

---

> 📝 **Pergunta 02c.1**
>
> Considere a expressão
> $$
> \lim_{n \rightarrow \infty} \Pr\!\left(\left|\overline{X}_n-\mu \right|<\varepsilon \right)=1.
> $$
>
> **(a)** Explique, com suas palavras, o significado dessa expressão.
>
> **(b)** Por que essa afirmação não significa que, para um único $n$ finito, $\overline{X}_n=\mu$ com probabilidade 1?

---

> 📝 **Pergunta 02c.2**
>
> No esboço com Chebyshev, usa-se:
> $$
> \Pr\!\left(\left|\overline{X}_n-\mu\right|\ge \varepsilon\right)\le \frac{\sigma^2}{n\varepsilon^2}.
> $$
>
> **(a)** Identifique as hipóteses principais necessárias para essa desigualdade ser aplicada no contexto da média amostral.
>
> **(b)** O que acontece com o limite superior quando $n$ aumenta? Interprete esse resultado em termos da precisão de $\overline{X}_n$.

---

> 📝 **Pergunta 02c.3**
>
> Um colega afirma: "A LLN diz que, para $n$ grande, a distribuição de $\overline{X}_n$ é normal."
>
> **(a)** A afirmação está correta? Justifique.
>
> **(b)** Reescreva a frase separando claramente o papel da LLN e o papel do TLC.

---

> 📝 **Pergunta 02c.4**
>
> Considere uma variável com média finita, porém com distribuição bastante assimétrica.
>
> **(a)** O que a LLN ainda garante sobre $\overline{X}_n$?
>
> **(b)** Que cuidado metodológico você teria ao usar aproximação normal para tamanhos amostrais moderados?
