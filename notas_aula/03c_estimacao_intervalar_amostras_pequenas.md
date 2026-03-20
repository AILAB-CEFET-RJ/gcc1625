# 03c Estimação Intervalar para Amostras Pequenas

---

# Intervalos de confiança para amostras pequenas

Quando o tamanho da amostra é pequeno ($n \leq 30$), a construção de intervalos de confiança exige mais cuidado. Para a média $\mu$, quando a população é aproximadamente normal, a **distribuição t de Student** é a ferramenta clássica. Para proporções $p$, também existem métodos específicos para amostras pequenas — os principais são o intervalo exato de Clopper-Pearson e o intervalo de Wilson; ambos são abordados em seções posteriores. Nesta seção, focamos no caso da média com distribuição $t$.

---

## Distribuição $t$ de Student

A distribuição $t$ de Student foi proposta em um [artigo](https://www.york.ac.uk/depts/maths/histstat/student.pdf) publicado em 1908 por William Gosset. Seu objetivo era permitir realizar estudos estatísticos sobre **amostras pequenas**. Por questões de confidencialidade relacionadas à empresa para a qual trabalhava, William usou o pseudônimo *Student* nessa publicação.

<center>
<img src="../figs/william_sealy_gosset_800.jpg" width="150px"/>
</center>

Considere que $X_{1}, X_{2}, \cdots, X_{n}$ é uma amostra de tamanho $n$ retirada de uma população que segue (aproximadamente) uma distribuição normal com média $\mu$. Nessa amostra, calculam-se a média amostral (*sample mean*) e a variância amostral (*sample variance*):

$$
\begin{aligned}
	\overline{x}	=	{\frac {X_{1}+ X_2 + \cdots +X_{n}}{n}} \quad
	s^{2}		=	{\frac {1}{n-1}}\sum _{i=1}^{n}(X_{i}-{\overline{x}})^{2}.
\end{aligned}
$$

A estatística $T$ é definida por
$$
	T = \frac{\overline{x} - \mu}{s/\sqrt{n}}
$$

É possível provar que $T$ segue a distribuição de probabilidades denominada $t$ de Student, com $(n - 1)$ **graus de liberdade**. A função de densidade de probabilidade de uma variável que segue a distribuição $t$ é dada pela expressão matemática a seguir. Essa expressão usa a [função Gama](https://en.wikipedia.org/wiki/Gamma_function), denotada por $\Gamma$ na expressão abaixo.

$$
f(t) = \textstyle {\frac {\Gamma \left({\frac {\nu +1}{2}}\right)}{{\sqrt {\nu \pi }}\,\Gamma \left({\frac {\nu }{2}}\right)}}\left(1+{\frac {t^{2}}{\nu }}\right)^{-{\frac {\nu +1}{2}}}\!
$$

A quantidade de graus de liberdade, denotada por $\nu$ na expressão acima, é um parâmetro dessa distribuição. Um esboço da prova para derivar a expressão acima pode ser encontrado nesse [vídeo](https://youtu.be/jFOyzEJctUU). Uma derivação completa pode ser encontrada nesse outro [vídeo](https://youtu.be/XMfFxwZXHaI).

A distribuição $t$ com $n-1$ graus de liberdade é a distribuição amostral (*sampling distribution*) da estatística $T$.

Repare a semelhança da estatística $T$ com a estatística $Z$:
$$
	Z = \frac{\overline{x} - \mu}{\sigma/\sqrt{n}}
$$

É importante notar que, apesar da grande semelhança sintática entre as definições dessas duas estatísticas, $Z$ segue a distribuição normal, enquanto que $T$ não segue. De fato, a distribuição $t$ é usada em estudos estatísticos envolvendo amostras pequenas justamente para levar em consideração o correspondente maior grau de incerteza resultante de usar $s$ em vez de $\sigma$.

Sobre o conceito de *graus de liberdade*, usado na definição da distribuição $t$, esse [link](https://bluebox.creighton.edu/demo/modules/en-boundless-old/www.boundless.com/statistics/textbooks/boundless-statistics-textbook/measures-of-variation-6/describing-variability-26/degrees-of-freedom-136-4427/index.html) fornece uma descrição intuitiva.

---

### Principais características

Algumas características da distribuição $t$ são descritas a seguir.

- A forma da função de densidade da distribuição $t$ é controlada pelo parâmetro $\nu$, que é conhecido como a quantidade de graus de liberdade (*degrees of freedom*). (O símbolo $\nu$ é uma [letra grega](https://pt.wikipedia.org/wiki/Ν));

- A forma da função de densidade da distribuição $t$ é semelhante à da distribuição normal padrão. Em particular, a distribuição $t$ é simétrica em relação ao 0;

- Para uma amostra de tamanho $n$, o valor do parâmetro $\nu$ é definido com $\nu = n - 1$;

- Para valores pequenos de $n$, a curva da distribuição $t$ é mais espalhada do que a da normal padrão, mas o espalhamento diminui à medida que o número de graus de liberdade aumenta;

- Para $n$ em torno de 30 ou mais, a distribuição $t$ já se aproxima bastante da distribuição normal padrão — embora esse limiar seja uma heurística, não uma fronteira exata. Em aplicações práticas, recomenda-se sempre usar a distribuição $t$ quando $\sigma$ é desconhecido, independentemente do tamanho da amostra;

- No limite, quando $n \rightarrow \infty$, a distribuição $t$ converge para a distribuição normal padrão.

A figura a seguir ([fonte](https://en.wikipedia.org/wiki/Student%27s_t-distribution)) apresenta exemplos de diversas distribuições t para diferentes valores do parâmetro $\nu = n-1$.

<center>
<img src="../figs/student_t_pdf_1024.svg" width="500px"/>
</center>

---

A aplicação prática dessas ideias pode ser feita com funções numéricas da distribuição $t$ disponíveis em bibliotecas estatísticas.

---

Para fins de comparação, é útil sobrepor a curva da distribuição $t$ com a curva da normal padrão e variar os graus de liberdade (`df`). Para valores de `df` em torno de 30 ou maiores, as curvas tornam-se praticamente indistinguíveis — embora a convergência dependa do contexto e da precisão exigida.

---

### Funções do scipy relacionadas

Felizmente, não precisamos realizar cálculos diretamente com a expressão matemática da função de densidade de probabilidade da distribuição $t$. A maioria dos pacotes estatísticos fornecem funções para computar valores no contexto da distribuição $t$. Nesta seção, apresentamos algumas funções do pacote [scipy.stats](https://docs.scipy.org/doc/scipy/reference/stats.html) relacionadas à distribuição $t$.

Os exemplos de código abaixo pressupõem o seguinte import:

```python
from scipy.stats import t
```

---

#### t.ppf

A função ppf (abreviação de *percent point function*) permite computar valores correspondentes à inversa da função de distribuição acumulada. A função t.ppf apresenta a seguinte assinatura:

> `t.ppf(q, df)`

Na expressão acima, o argumento `df` é uma abreviação para degrees of freedom e corresponde ao parâmetro $\nu$ da distribuição $t$. Esse mesmo argumento aparece nas demais funções definidas no pacote scipy.stats.t.

Por exemplo, o comando `t.ppf(0.95, 30)` retorna um valor próximo de $1{,}697$, que é o valor do percentil 95 da distribuição $t$ com 30 graus de liberdade. Esse valor significa que 95% da área abaixo da curva dessa distribuição está à esquerda de $1{,}697$, e que apenas 5% está à direita.

---

#### t.cdf

Esta função retorna o valor da CDF, que é a probabilidade de ser gerado um número menor ou igual ao argumento x. A função cdf (abreviação de *cumulative distribution function*) apresenta a seguinte assinatura:

> `t.cdf(x, df)`

Por exemplo, a chamada `t.cdf(1.697, 30)` retorna um resultado próximo de 95%. Já que $1{,}697$ corresponde ao percentil 95, o valor resultante da chamada é de aproximadamente 95%.

---

#### t.pdf

A chamada à função `t.pdf` produz o valor da função de densidade de probabilidade em x. Esse valor produzido corresponde à altura da curva da distribuição no ponto x.

> `t.pdf(x, df)`

Por exemplo, considere que $\nu=30$. Para $x= 1{,}697$, o valor resultante é $0{,}096$, enquanto que para $x = 0$ é aproximadamente $0{,}396$.

---

### Exemplos

---

Exemplo 1: Encontre os percentis 2,5 e 97,5 da distribuição Student $t$ com 5 graus de liberdade.

> Solução. Podemos usar a função ppf aqui, passando as porcentagens correspondentes aos percentis desejados:
> ```python
> t.ppf(0.025, 5)  # → aproximadamente -2.571
> t.ppf(0.975, 5)  # → aproximadamente  2.571
> ```

---

Exemplo 2: Uma amostra aleatória de tamanho 10 é colhida a partir de uma população com distribuição normal com média $\mu=4$. Define-se a estatística T conforme a seguir:

$$
T = \frac{\overline{x} - 4}{s / \sqrt{10}}
$$

Qual é a probabilidade de que $T>1{,}833$?

> Solução. Por definição, essa estatística segue a distribuição $t$ de Student, com $\nu = 10-1 = 9$ graus de liberdade. Por meio da função `t.cdf`, podemos computar $\Pr(T > 1{,}833)$:
> ```python
> 1 - t.cdf(1.833, 9)  # → aproximadamente 0.05
> ```
> Portanto $\Pr(T > 1{,}833) \approx 0{,}05$.

---

Exemplo 3: Encontre o valor para a distribuição $t_{12}$ que delimita à sua direita uma área correspondente à probabilidade $0{,}025$.

> Solução. Basta usar a função `t.ppf`, passando como primeiro argumento o complemento de $0{,}025$, e como segundo argumento o valor 12 (quantidade de graus de liberdade):
> ```python
> t.ppf(0.975, 12)  # → aproximadamente 2.179
> ```

---

Exemplo 4: Determine o valor da variável aleatória que segue a distribuição $t_{14}$ para o qual a área da cauda inferior é de 0,01.

> Solução. O valor que delimita uma probabilidade de 1% na cauda inferior é negativo (por simetria da distribuição $t$):
> ```python
> t.ppf(0.01, 14)  # → aproximadamente -2.624
> ```

---

## Verificação da suposição de normalidade

O uso da distribuição $t$ para amostras pequenas requer que a população seja aproximadamente normal. Com $n$ pequeno, ferramentas como histogramas são pouco informativas. As abordagens mais indicadas para verificar essa suposição são:

- **Gráfico Q-Q (quantil-quantil):** plota os quantis da amostra contra os quantis teóricos da normal. Pontos alinhados próximos a uma reta diagonal indicam aderência à normalidade. Em Python, pode-se usar `scipy.stats.probplot` ou `statsmodels.graphics.gofplots.qqplot`.

- **Teste de Shapiro-Wilk:** teste formal de normalidade, especialmente adequado para amostras pequenas. Em Python: `scipy.stats.shapiro(dados)`. O resultado inclui a estatística $W$ e o p-valor; p-valores pequenos (convencionalmente $< 0{,}05$) indicam evidência contra a normalidade.

É importante lembrar que, para amostras muito pequenas ($n < 10$), mesmo esses diagnósticos têm poder limitado. Nesses casos, o conhecimento do processo gerador dos dados (contexto do problema) tende a ser mais informativo do que os testes.

---

## Intervalo de confiança para $\mu$

Quando o tamanho da amostra é grande, não importa qual é a distribuição da população para a determinação de uma estimativa intervalar para a média populacional. Isso porque o TLC garante que $\overline{x}$ será aproximadamente normalmente distribuída.

Porém, quando a amostra disponível é pequena ($n \leq 30$), a distribuição da população deve ser aproximadamente normal para que se possa fazer estimativas adequadas — e recomenda-se verificar essa suposição conforme descrito na seção anterior. Nesse caso, intervalos de confiança são construídos de forma semelhante ao caso em que $n>30$. A diferença é que o z-score (denotado por $z_{\alpha/2}$) é substituído por um valor da distribuição $t$ de Student, o t-score. Esse valor, denotado por $t_{n-1, \alpha/2}$, é aquele que delimita uma área de $\alpha / 2$ na cauda do lado direito da distribuição $t$.

> **Nota:** o limiar $n = 30$ é uma heurística amplamente usada para orientar a escolha entre $z$ e $t$, mas não é uma fronteira rígida. Na prática, sempre que $\sigma$ for desconhecido — independentemente de $n$ — o uso da distribuição $t$ é teoricamente mais adequado.

Para amostras pequenas, o procedimento geral para a determinação de um intervalo de confiança para $\mu$ é resumido a seguir.

---

### Procedimento de cálculo

Para construir um intervalo de confiança no nível de $(1-\alpha)$% para a média populacional $\mu$, considere que:
- $X_{1}, X_{2}, \ldots, X_{n}$ é a amostra aleatória de tamanho $n$ ($n \leq 30$);
- $(1-\alpha)$% é o nível de confiança definido para o estudo;
- a população é aproximadamente normal (verificar com Q-Q plot ou Shapiro-Wilk quando possível).

Procedimento:

> 1. Calcular a média da amostra:
$$
\overline{x} = \frac{\left(X_{1} + X_{2} + \cdots + X_{n}\right)}{n}
$$
> 2. Calcular o desvio padrão da amostra:
$$
s = \sqrt{{\frac {1}{n-1}}\sum _{i=1}^{n}{\big (}X_{i}-{\overline{x}}\,{\big )}^{2}}
$$
> 3. Determinar $t_{n-1, \alpha/2}$, o escore na distribuição $t$ de Student que delimita uma área de $\alpha/2$ no lado direito da curva da distribuição.
> 4. Computar os extremos do intervalo de confiança usando a expressão a seguir:
$$
\overline{x} \pm t_{n-1, \alpha/2} \times \frac{s}{\sqrt{n}}
$$

---

### Exemplo 1

> Um técnico em metalurgia está estudando um novo processo de soldagem. Ele fabrica 5 juntas soldadas usando esse processo e mede a resistência à deformação de cada uma. Os cinco valores (medidos em [ksi](https://en.wikipedia.org/wiki/Pounds_per_square_inch)) são
$$56{,}3 \quad 65{,}4 \quad 58{,}7 \quad 70{,}1 \quad 63{,}9$$
> Suponha que esses valores são uma amostra aleatória simples proveniente de uma população aproximadamente normal. Determine um intervalo de confiança no nível de 95% para a resistência média das soldaduras forjadas nesse processo.

**Solução**

A figura a seguir mostra a distribuição $t_4$ (curva em vermelho). Essa figura também apresenta uma área hachurada (em cor azul) que corresponde a 95% da área total sob a curva. Os limites dessa área hachurada são $x=-2{,}776$ e $x=2{,}776$.

Segue-se que, para 95% de todas as amostras que poderiam ter sido escolhidas, vale a seguinte desigualdade:

$$
-2{,}776 < \frac{\overline{x} - \mu}{s/\sqrt{n}} < 2{,}776
$$

Ao manipular essa desigualdade, obtemos:

$$
\overline{x} - 2{,}776\frac{s}{\sqrt{n}} < \mu < \overline{x} + 2{,}776\frac{s}{\sqrt{n}}
$$

A média e o desvio padrão da amostra são, respectivamente, $\overline{x} = 62{,}88$ e $s = 5{,}484$. O tamanho da amostra é $n = 5$. Ao fazermos a substituição de valores, descobrimos que um intervalo de confiança de 95% para $\mu$ é

$$
62{,}88 - 6{,}81 < \mu < 62{,}88 + 6{,}81
$$

ou $(56{,}07,\ 69{,}69)$.

Em Python:

```python
import numpy as np
from scipy.stats import t

dados = [56.3, 65.4, 58.7, 70.1, 63.9]
n = len(dados)
media = np.mean(dados)
s = np.std(dados, ddof=1)           # ddof=1 para desvio padrão amostral
t_critico = t.ppf(0.975, df=n-1)    # bicaudal 95%
margem = t_critico * s / np.sqrt(n)
print(media - margem, media + margem)  # → (56.07, 69.69)
```

---

Em implementações numéricas, é importante usar `ddof=1` para que a fórmula do desvio padrão amostral $s$ seja aplicada, e não a do desvio padrão populacional $\sigma$. Veja a diferença entre essas duas fórmulas:

$$
s = \sqrt{{\frac {1}{n-1}}\sum _{i=1}^{n}{\big (}X_{i}-{\overline{x}}\,{\big )}^{2}}
\qquad \text{vs} \qquad
\sigma = \sqrt{{\frac {1}{n}}\sum _{i=1}^{n}{\big (}X_{i}-{\mu}\,{\big )}^{2}}
$$

Veja a entrada da Wikipedia sobre a [correção de Bessel](https://en.wikipedia.org/wiki/Bessel%27s_correction) para entender a razão disso.

---

Para um melhor entendimento do significado do valor de t-score, considere a curva da distribuição $t$ com 4 graus de liberdade e a área central delimitada entre $-2{,}776$ e $+2{,}776$. Nesse caso, $2{,}776$ é o valor crítico (em módulo), e a área central correspondente é de 95%, exatamente o nível de confiança definido no Exemplo 1.

---

### Exemplo 2

> Uma amostra de 25 elementos tem média igual a 150 e desvio padrão igual a 10. Determine um intervalo de confiança em nível de 90% para a média populacional.

**Solução**

Como $\sigma$ é desconhecido, usamos a distribuição $t$ de Student. O número de graus de liberdade é $\nu = n - 1 = 24$.

O nível de confiança desejado é $(1 - \alpha) = 0{,}9$, portanto $\alpha = 0{,}1$ e $\alpha/2 = 0{,}05$.

```python
t_critico = t.ppf(0.95, df=24)  # → 1.7109
```

Construindo o intervalo:

$$
150 \pm 1{,}7109 \times \frac{10}{\sqrt{25}} = 150 \pm 3{,}42
$$

Intervalo de confiança: $(146{,}58,\ 153{,}42)$.

---

> 📝 **Pergunta 03c.1**
>
> Compare as estatísticas $Z$ e $T$:
>
> **(a)** Qual é a diferença entre suas fórmulas?
>
> **(b)** Por que essa diferença faz com que $T$ siga uma distribuição com caudas mais pesadas do que a normal padrão?

---

> 📝 **Pergunta 03c.2**
>
> Para cada situação abaixo, identifique o valor crítico $t_{n-1,\,\alpha/2}$ a ser usado na construção do IC:
>
> **(a)** $n = 10$, nível de confiança 95%
>
> **(b)** $n = 25$, nível de confiança 90%
>
> **(c)** $n = 5$, nível de confiança 99%

---

> 📝 **Pergunta 03c.3**
>
> No Exemplo 1 (soldagem), suponha que os dados fossem $n = 5$ observações de uma distribuição claramente assimétrica (por exemplo, com um valor muito discrepante). O procedimento de IC com distribuição $t$ ainda seria adequado? O que você faria antes de aplicá-lo?

---

> 📝 **Pergunta 03c.4**
>
> Um pesquisador afirma: *"Como minha amostra tem $n = 40$, posso usar $z$ em vez de $t$."* Avalie essa afirmação. Em que sentido ela está correta? Em que sentido poderia ser melhorada?