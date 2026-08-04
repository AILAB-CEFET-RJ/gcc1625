# 02 Distribuições Amostrais

## Definição

Considere uma população com parâmetro de interesse $\theta$ e uma estatística $T$
calculada sobre amostras de tamanho $n$.

A **distribuição amostral** (*sampling distribution*) de $T$ é a distribuição dos
valores de $T$ quando consideramos todas as possíveis amostras de tamanho $n$
extraídas dessa população.

Para tornar isso concreto, imagine o seguinte experimento mental: extraia uma
amostra de tamanho $n$, calcule $T$, registre o valor, devolva a amostra à
população e repita indefinidamente. O histograma dos valores registrados converge
para a distribuição amostral de $T$. Cada valor individual de $T$ varia de amostra
para amostra porque cada amostra é diferente, e é exatamente essa variabilidade
que a distribuição amostral descreve.

Existem duas formas de obter (ou aproximar) essa distribuição:

- A versão **teórica** é derivada analiticamente, considerando todas as amostras
  possíveis. Em geral, requer conhecimento da distribuição populacional e resulta
  em fórmulas fechadas, como veremos no caso da média amostral.
- A versão **empírica** aproxima a teórica por simulação: geram-se muitas amostras
  de tamanho $n$, calcula-se $T$ em cada uma, e o histograma resultante serve como
  aproximação. Essa abordagem é explorada no notebook prático.

---

> 📝 **Pergunta 02a.1***
>
> **(a)** O texto descreve um experimento mental para construir a
> distribuição amostral de uma estatística $T$ qualquer. Descreva como você
> aplicaria esse mesmo experimento para construir a distribuição amostral da
> **mediana** de tempos de atendimento em uma fila. O que mudaria em relação ao
> experimento descrito no texto?
>
> **(b)** O texto afirma que o histograma das repetições "converge"
> para a distribuição amostral de $T$. O que impede que esse histograma seja
> exato após um número finito de repetições? Em que sentido a versão empírica
> é sempre uma **aproximação**?
>
> **(c)** Por que o valor de $T$ muda a cada repetição do experimento, se a
> população é sempre a mesma?
>
> **(d)** Qual a diferença entre a versão **teórica** e a versão **empírica** da
> distribuição amostral? Em qual situação a versão empírica seria preferível?

---

## Distinção importante

Os termos em inglês são próximos e frequentemente confundidos, mas referem-se a
objetos completamente diferentes:

- *sample distribution* — **distribuição da amostra**: descreve os valores
  observados em **uma única amostra específica**. É um conjunto fixo de $n$
  números.
- *sampling distribution* — **distribuição amostral**: descreve os valores que
  uma **estatística** assume ao longo de **muitas amostras diferentes**. É uma
  distribuição de probabilidades.

Um exemplo ajuda a fixar a distinção. Suponha que medimos a altura de 40 alunos
(uma amostra) e calculamos a média $\overline{x}$. O histograma das 40 alturas
observadas é a *distribuição da amostra*. Se repetíssemos esse processo com outras
40 turmas e construíssemos um histograma das 40 médias obtidas, estaríamos
aproximando a *distribuição amostral* de $\overline{x}$.

---

> 📝 **Pergunta 02a.2**
>
> Um pesquisador coletou o tempo de atendimento (em minutos) de 50 clientes em uma
> agência bancária e registrou os 50 valores. Em seguida, ele repetiu a coleta em
> outras 99 agências diferentes, obtendo ao todo 100 amostras de tamanho 50.
>
> **(a)** O histograma dos 50 tempos da primeira agência é um exemplo de
> *sample distribution* ou *sampling distribution*? Justifique.
>
> **(b)** O pesquisador calculou a média $\overline{x}$ de cada uma das 100
> amostras e construiu um histograma dessas 100 médias. Esse histograma é um
> exemplo de qual dos dois conceitos? Justifique.
>
> **(c)** O objeto descrito no item (b) é uma distribuição de probabilidades ou
> um conjunto fixo de números? O que isso implica sobre sua natureza como variável
> aleatória?

---

## Distribuição amostral da média

Quando a estatística de interesse é a média amostral:

$$
\overline{x}_{n}=\frac{1}{n}(x_{1}+x_{2}+\cdots +x_{n})
$$

a distribuição dos valores de $\overline{x}_n$ ao longo de muitas amostras de
tamanho $n$ é chamada de **distribuição amostral da média amostral**.

Algumas propriedades dessa distribuição podem ser derivadas diretamente das
propriedades da esperança e da variância, sem nenhuma hipótese sobre a forma da
distribuição populacional — basta que as observações sejam i.i.d. com média $\mu$
e variância $\sigma^2$ finita:

$$
\operatorname{E}[\overline{x}_n] = \mu
\qquad \text{e} \qquad
\operatorname{Var}[\overline{x}_n] = \frac{\sigma^2}{n}
$$

A primeira igualdade diz que $\overline{x}$ é um estimador **não-viesado** de
$\mu$: em média, ao longo de muitas amostras, o estimador acerta o alvo. A segunda
diz que a variabilidade de $\overline{x}$ em torno de $\mu$ **diminui com $n$**:
quanto maior a amostra, mais concentrada é a distribuição amostral em torno do
parâmetro verdadeiro.

A quantidade $\sigma_{\overline{x}} = \sigma/\sqrt{n}$ é chamada de **erro padrão**
(*standard error*) da média e mede a precisão típica do estimador: para reduzir o
erro padrão à metade, é necessário quadruplicar o tamanho da amostra.

A distribuição amostral da média é central para a inferência estatística porque
conecta três ideias fundamentais:

1. **Variabilidade amostral**: amostras diferentes produzem médias diferentes; a
   distribuição amostral quantifica esse fenômeno.
2. **Precisão de estimativas**: o erro padrão indica o quanto $\overline{x}$ pode
   se afastar de $\mu$ em uma amostra típica.
3. **Comportamento assintótico**: o Teorema do Limite Central (próxima seção)
   descreve a *forma* dessa distribuição conforme $n$ cresce, completando o quadro.

---

> 📝 **Pergunta 02a.3**
>
> Uma população tem média $\mu = 80$ e desvio-padrão $\sigma = 20$.
>
> **(a)** Calcule o erro padrão da média amostral para $n = 16$, $n = 100$ e
> $n = 400$.
>
> **(b)** Com base nos valores calculados, o que acontece com a concentração da
> distribuição amostral de $\overline{x}$ em torno de $\mu$ conforme $n$ aumenta?
>
> **(c)** Um colega afirma: *"Se coletarmos uma amostra grande o suficiente,
> $\overline{x}$ será exatamente igual a $\mu$."* Essa afirmação está correta?
> Justifique com base nas propriedades apresentadas no texto.

---

> 📝 **Pergunta 02a.4**
>
> **(a)** O texto afirma que $\overline{x}$ é um estimador **não-viesado** de
> $\mu$. O que essa afirmação significa em termos do experimento mental de extrair
> muitas amostras e calcular $\overline{x}$ em cada uma?
>
> **(b)** Não-viés é uma propriedade de uma única amostra ou do comportamento do
> estimador ao longo de muitas amostras? Justifique.
>
> **(c)** O texto lista três razões pelas quais a distribuição amostral da média é
> central para a inferência estatística. Reescreva cada uma delas com suas próprias
> palavras, sem usar os termos técnicos do texto.
