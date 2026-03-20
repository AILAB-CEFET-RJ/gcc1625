# 02 Teorema do Limite Central (TLC)

## Propriedades da distribuição amostral de $\overline{x}$

Antes de enunciar o TLC, é importante registrar duas propriedades **exatas** da média amostral — válidas para **qualquer tamanho de amostra** $n$, desde que as observações sejam i.i.d. com média $\mu$ e variância finita $\sigma^2$:

- A esperança da média amostral é igual à média populacional:
$$
\mu_{\overline{x}} = \operatorname{E}[\overline{x}] = \mu
$$

- A variância da média amostral é:
$$
\sigma^2_{\overline{x}} = \operatorname{Var}[\overline{x}] = \frac{\sigma^2}{n}
$$

Essas igualdades decorrem diretamente da linearidade da esperança e da independência entre as observações — não dependem de $n$ ser grande nem do TLC.

## Enunciado do TLC

Considere amostras aleatórias i.i.d. retiradas de uma população com média $\mu$ e variância finita $\sigma^2$. O Teorema do Limite Central declara que, conforme o tamanho amostral $n$ cresce, a **distribuição amostral** da média amostral $\overline{x}$ **aproxima-se** de uma normal com os parâmetros exatos acima:

$$
\overline{x} \xrightarrow{d} \mathcal{N}\left(\mu,\ \frac{\sigma^2}{n}\right)
$$

Em outras palavras, o TLC afirma algo sobre a **forma** da distribuição de $\overline{x}$ — que ela se torna aproximadamente normal para $n$ grande — enquanto as propriedades de média e variância apresentadas acima já valiam exatamente para qualquer $n$.

---

> 📝 **Pergunta 02b.1**
>
> Sobre o enunciado do TLC e as propriedades da distribuição amostral de $\overline{x}$:
>
> **(a)** Qual resultado descreve uma **aproximação de forma de distribuição** e quais descrevem **momentos exatos** (média e variância) de $\overline{x}$?
>
> **(b)** Explique, em uma frase, por que não há contradição entre "aproximação normal" e "igualdades exatas para média e variância".
>
> **(c)** Em termos práticos, por que separar essas ideias ajuda a interpretar resultados de simulação?

## Intuição e observações

- A aproximação normal ocorre independentemente da forma da distribuição da população, para $n$ suficientemente grande (desde que as hipóteses do TLC sejam atendidas).
- Populações muito assimétricas ou com caudas pesadas demandam amostras maiores para boa aproximação.
- Em populações aproximadamente simétricas, a aproximação costuma funcionar com tamanhos menores.
- Regra prática comum: para muitos cenários, $n > 30$ já produz boa aproximação. **Atenção:** essa é uma heurística grosseira. Ela pode falhar em distribuições com forte assimetria, caudas pesadas ou variância muito elevada. Sempre que possível, verifique a adequação da aproximação para a distribuição específica do problema.

## Limite importante das hipóteses

O TLC clássico apresentado aqui depende de variância populacional finita ($\sigma^2 < \infty$).  
Quando a distribuição tem caudas muito pesadas, essa hipótese pode falhar, e a aproximação normal para $\overline{x}$ pode deixar de ser adequada mesmo com amostras grandes.

Intuição didática: "variância infinita" não significa valores infinitos observados na amostra; significa que eventos extremos têm peso suficiente para impedir a estabilização do segundo momento.

---

> 📝 **Pergunta 02b.6**
>
> Com base na seção **Limite importante das hipóteses**:
>
> **(a)** Qual hipótese do TLC clássico pode falhar em distribuições com caudas muito pesadas?
>
> **(b)** Se essa hipótese falhar, qual consequência o texto aponta para a aproximação normal de $\overline{x}$?
>
> **(c)** Explique, em uma frase, por que "variância infinita" não significa observar valores infinitos na amostra.

---

> 📝 **Pergunta 02b.2**
>
> Considere duas populações: A (aproximadamente simétrica) e B (fortemente assimétrica).
>
> **(a)** Em qual delas você esperaria precisar de maior tamanho amostral para obter boa aproximação normal da distribuição de $\overline{x}$? Justifique com base no texto.
>
> **(b)** A regra prática "$n > 30$" pode falhar em qual situação e por quê?
>
> **(c)** Com base no que você já sabe sobre fenômenos reais ou distribuições estudadas anteriormente, dê um exemplo de variável que você suspeitaria ter alta assimetria. Explique brevemente por quê.

## Relações importantes

Em termos de desvio-padrão, a raiz quadrada de $\sigma^2_{\overline{x}}$ é chamada de **erro padrão** (*standard error*) da média:

$$
\sigma_{\overline{x}} = \frac{\sigma}{\sqrt{n}}
$$

Essa relação mostra que o erro padrão decresce com $\sqrt{n}$: para reduzir a variabilidade de $\overline{x}$ à metade, é necessário quadruplicar o tamanho da amostra.

---

> 📝 **Pergunta 02b.3**
>
> Uma população tem desvio-padrão $\sigma = 12$.
>
> **(a)** Calcule $\sigma_{\overline{x}}$ para $n=9$, $n=36$ e $n=144$.
>
> **(b)** O que acontece com a variabilidade de $\overline{x}$ quando quadruplicamos $n$?
>
> **(c)** Se o objetivo é reduzir o erro padrão pela metade, como o tamanho amostral deve ser alterado?

## Exemplo conceitual (dado de 6 lados)

Se $X$ é uniforme discreta entre $a=1$ e $b=6$, com $k = b - a + 1 = 6$ valores igualmente prováveis:

$$
\mu = \operatorname{E}[X] = \frac{a+b}{2} = 3.5
$$

$$
\sigma^2 = \operatorname{Var}[X] = \frac{k^2 - 1}{12} = \frac{36 - 1}{12} = \frac{35}{12} \approx 2.9167
$$

Esses valores são parâmetros populacionais. A simulação computacional no notebook prático mostra que as distribuições amostrais das médias convergem para os comportamentos previstos pelo TLC.

---

> 📝 **Pergunta 02b.4**
>
> No experimento do dado justo, considere $X \in \{1,2,3,4,5,6\}$.
>
> **(a)** Quais são os valores teóricos de $\mu$ e $\sigma^2$? Use as fórmulas apresentadas no texto.
>
> **(b)** Para $n=36$, qual é o valor teórico de $\operatorname{Var}(\overline{X})$?
>
> **(c)** Uma simulação com muitas repetições produziu média de $\overline{X}$ igual a 3.48. Sabendo que $\operatorname{E}[\overline{X}] = \mu = 3.5$, o valor 3.48 está próximo do esperado? O que o TLC diz sobre o comportamento de $\overline{X}$ em torno de $\mu$ conforme $n$ cresce?

---

> 📝 **Pergunta 02b.5**
>
> Um grupo simulou a distribuição amostral de $\overline{X}$ para $n=5$ e para $n=100$.
>
> **(a)** Em qual caso você espera histograma mais "concentrado"? Justifique com a fórmula de $\sigma_{\overline{x}}$.
>
> **(b)** Em qual caso a forma do histograma deve parecer mais próxima de uma curva em forma de sino? Justifique com base no TLC.
>
> **(c)** Descreva o que você esperaria observar visualmente ao comparar os dois histogramas lado a lado: o que mudaria na largura, na simetria e no formato geral de cada um?
