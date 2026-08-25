# Laboratório: Distribuições Amostrais, LLN e TLC

## Organização da atividade

- Formem grupos de 2 a 4 alunos.
- Tempo sugerido: 30 a 40 minutos.
- Entreguem um único notebook Jupyter por grupo, com os gráficos, a tabela e respostas breves às perguntas de interpretação.
- Usem uma semente fixa para que os resultados possam ser reproduzidos.

## Objetivo

Investigar, por simulação, o comportamento da média amostral quando a população de origem é assimétrica. Ao final, o grupo deve distinguir:

- as propriedades exatas da distribuição amostral da média;
- a concentração prevista pela Lei dos Grandes Números (LLN);
- a aproximação da forma normal fornecida pelo Teorema do Limite Central (TLC);
- o papel do erro padrão na regra empírica aplicada a médias amostrais.

## Situação-problema

Considere uma população modelada por uma distribuição Gamma com parâmetros:

$$
X \sim \operatorname{Gamma}(\text{shape}=2,\ \text{scale}=2).
$$

Essa população é assimétrica à direita. Seus parâmetros são:

$$
\mu = \operatorname{E}[X] = 4
\qquad\text{e}\qquad
\sigma^2 = \operatorname{Var}(X) = 8.
$$

Para cada tamanho amostral $n \in \{5, 30, 100\}$, gere $R=10\,000$ amostras i.i.d. e calcule uma média amostral para cada uma delas. Denote por `medias_n` o vetor das $R$ médias obtidas para um dado valor de $n$.

### Dicas iniciais de Python

- Crie um gerador reprodutível com `rng = np.random.default_rng(20260825)`.
- Gere todas as amostras de uma vez com `rng.gamma(shape=2, scale=2, size=(R, n))`.
- Calcule as médias de cada linha com `amostras.mean(axis=1)`.
- Guarde os resultados em um dicionário, por exemplo `medias_por_n[n] = medias_n`.

---

## Parte 1. Média e variância da distribuição amostral

Para cada valor de $n$, construa uma tabela com:

- a média empírica de `medias_n`;
- a variância empírica de `medias_n`;
- o valor teórico de $\operatorname{E}[\overline{X}_n]$;
- o valor teórico de $\operatorname{Var}(\overline{X}_n)$.

Em seguida, responda:

1. As médias empíricas estão próximas de $\mu=4$? O que isso ilustra?
2. Compare as variâncias empíricas com $8/n$. O que acontece com a variabilidade de $\overline{X}_n$ quando $n$ aumenta?
3. As fórmulas $\operatorname{E}[\overline{X}_n]=\mu$ e $\operatorname{Var}(\overline{X}_n)=\sigma^2/n$ são fornecidas pelo TLC ou são propriedades exatas sob observações i.i.d.?

### Dicas de Python

- Use `medias_n.mean()` para a média empírica.
- Use `medias_n.var()` para a variância empírica. Como as $R$ médias representam a distribuição simulada, use a convenção padrão `ddof=0` para compará-la a $8/n$.
- Calcule o valor teórico com `8 / n`.
- Uma tabela simples pode ser feita com uma lista de dicionários e `pandas.DataFrame(...)`.

---

## Parte 2. Forma da distribuição e TLC

Faça três histogramas, um para cada valor de $n$, mostrando a distribuição empírica de `medias_n`. Sobreponha, em cada gráfico, a densidade da normal com média $4$ e variância $8/n$.

Em seguida, responda:

4. Em qual histograma a aproximação normal parece menos adequada? Relacione sua resposta à assimetria da população de origem.
5. Como mudam a largura e a forma dos histogramas quando $n$ cresce?
6. Explique por que esses gráficos não dizem que a população Gamma “se tornou normal”.

### Dicas de Python

- Use `plt.hist(medias_n, bins=..., density=True, alpha=...)`.
- Para a curva normal, use `from scipy.stats import norm` e `norm.pdf(x, loc=4, scale=np.sqrt(8/n))`.
- Crie os valores de `x` com `np.linspace(...)`. Uma faixa útil é de `4 - 4*np.sqrt(8/n)` até `4 + 4*np.sqrt(8/n)`.
- Para organizar os gráficos, use `fig, axes = plt.subplots(1, 3, figsize=(...))` e selecione cada eixo com `axes[i]`.

---

## Parte 3. Convergência em probabilidade e LLN

Fixe $\varepsilon=0{,}25$. Para cada valor de $n$, estime por simulação:

$$
\Pr\left(\left|\overline{X}_n-4\right|<0{,}25\right).
$$

Em seguida, responda:

7. Como essa probabilidade se comporta nos três tamanhos amostrais?
8. Explique o resultado usando a expressão “converge em probabilidade”.
9. A LLN garante que a probabilidade estimada será estritamente maior em todo valor sucessivo de $n$ em uma simulação finita? Justifique brevemente.

### Dicas de Python

- Calcule os desvios com `np.abs(medias_n - mu)`.
- O evento de interesse é `np.abs(medias_n - mu) < epsilon`.
- Como `True` vale 1 e `False` vale 0 em cálculos numéricos, a probabilidade simulada é `evento.mean()` ou `np.mean(evento)`.
- Um gráfico simples pode usar `plt.plot(valores_n, probabilidades, marker='o')` e `plt.ylim(0, 1.05)`.

---

## Parte 4. Regra empírica e erro padrão

Considere apenas o caso $n=100$. Calcule o erro padrão teórico:

$$
\sigma_{\overline{X}_{100}} = \frac{\sigma}{\sqrt{100}}.
$$

Em seguida, estime a proporção de médias simuladas que pertence ao intervalo:

$$
\mu \pm 2\sigma_{\overline{X}_{100}}.
$$

Por fim, escolha uma das médias simuladas e calcule seu escore-z:

$$
z=\frac{\overline{x}-\mu}{\sigma/\sqrt{n}}.
$$

Responda:

10. Qual é o erro padrão para $n=100$? Qual é a faixa aproximada de 95% para as médias amostrais?
11. A proporção simulada ficou próxima de 95%? Por que esse resultado é uma aproximação neste problema?
12. Interprete o escore-z calculado: quantos erros padrão a média observada está distante de $\mu$?

### Dicas de Python

- O desvio-padrão populacional é `sigma = np.sqrt(8)`.
- Calcule o erro padrão com `erro_padrao = sigma / np.sqrt(100)`.
- Defina os limites com `limite_inferior = mu - 2 * erro_padrao` e `limite_superior = mu + 2 * erro_padrao`.
- A proporção simulada pode ser obtida com `np.mean((medias_100 >= limite_inferior) & (medias_100 <= limite_superior))`.
- Escolha, por exemplo, `xbar_observada = medias_100[0]` e calcule `z = (xbar_observada - mu) / erro_padrao`.

---

## Síntese final

Em um único parágrafo, expliquem a diferença entre as três afirmações abaixo:

1. $\operatorname{E}[\overline{X}_n]=\mu$ e $\operatorname{Var}(\overline{X}_n)=\sigma^2/n$;
2. $\overline{X}_n \xrightarrow{P} \mu$;
3. $\overline{X}_n \approx \mathcal{N}(\mu,\sigma^2/n)$ para $n$ grande.

O parágrafo deve identificar quais afirmações são exatas, qual descreve concentração em torno do alvo e qual descreve uma aproximação de forma.
