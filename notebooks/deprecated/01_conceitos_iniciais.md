# 01 Conceitos Iniciais

# Conceitos básicos da Inferência Estatística

---

## População e amostra


* **População** (*population*) é a totalidade de elementos ou resultados (escores, pessoas, medidas, etc) que estão sob discussão e dos quais se deseja inferir alguma informação. Na Estatística, o termo "população" tem um significado ligeiramente diferente daquele que lhe é atribuído no discurso comum. Não precisa se referir apenas a pessoas ou a outros seres vivos - a população da Grã-Bretanha, por exemplo, ou a população de cães de Londres. Os estatísticos também usam o termo população para denotar coleções de objetos, eventos ou procedimentos ou observações, incluindo coisas como as quantidades de colesterol medidas no sangue de um grupo de indivíduos, visitas ao médico ou operações cirúrgicas.


* **Amostra** (*sample*) é qualquer subconjunto de uma população. Dado um inteiro positivo $n$, uma amostra corresponde aos resultados de $n$ experimentos nos quais a mesma quantidade é medida. Por exemplo, se queremos estimar a altura média dos membros de uma determinada população, inicialmente medimos a altura de $n$ indivíduos.

<p align="center">
  <img src="../figs/simple_random_sampling_300.png" />
</p>

---

População e amostra (exemplo 01) - Considere uma escola de 5.000 alunos. Se quisermos fazer um estudo das estaturas (e.g., qual a estatura média?), podemos colher uma amostra de, digamos, 40 alunos e estudar o comportamento da **varíavel estatura** apenas nesses alunos. A variável a ser estudada poderia ser inteligência, número de irmãos, número de cáries, notas em história ou renda familiar, dentre outras.

---

> 📝 **Pergunta 01.1**
>
> Uma empresa fabrica 200.000 parafusos por dia e quer estimar a taxa de defeitos na produção.
>
> **(a)** Identifique a **população** e descreva o que seria uma **amostra** nesse contexto.
>
> **(b)** Por que seria inviável — ou até destrutivo — analisar a população inteira?
>
> **(c)** A variável "quantidade de defeitos por parafuso" é um exemplo de qual tipo de dado (quantitativo discreto, quantitativo contínuo ou qualitativo)? Justifique brevemente.

---

## Parâmetros versus estatísticas


* Um **parâmetro** é uma medida usada para descrever uma característica de uma população. É uma medida numérica, normalmente não observável, que descreve uma característica de uma população.


* Uma **estatística amostral** (ou simplesmente **estatística**) é alguma função computada a partir de uma amostra. Uma estatística é uma variável aleatória para a qual cada um de seus valores é resultante de alguma computação realizada sobre uma amostra aleatória retirada de população.

Um parâmetro está para uma população assim como uma estatística está para uma amostra.

Por exemplo, considere a porcentagem de eleitores de uma população que preferem um determinado candidato. Essa porcentagem é um exemplo de parâmetro populacional. Note que é (na maioria dos casos) impraticável perguntar a todos os eleitores da população quais são suas preferências de candidato. Sendo assim, uma amostra de eleitores pode ser consultada e uma estatística (nesse caso, a porcentagem dos eleitores que preferiram cada candidato) pode ser computada. Essa estatística pode então ser usada como um estimativa do parâmetro populacional.

Da mesma forma, em algumas formas de teste de produtos fabricados, em vez de testar destrutivamente todos os produtos, apenas uma amostra de produtos é testada. Esses testes reúnem informações que permitem estimar qual a proporção de produtos fabricados que atende ou às especificações mínimas.

> Repare que enquanto um parâmetro é um valor numérico, uma estatística é uma variável aleatória.

Para entender isso, considere o experimento aleatório de produzir uma amostra aleatória de tamanho $n$ a partir de uma população. Podemos interpretar cada amostra (i.e., cada resultado da realização do experimento aleatório) como um elemento do espaço amostral correspondente a todas as possíveis amostras de tamanho $n$ dessa população. Se por definição cada valor de uma eatatística é uma função dos valores contidos na amostra aleatória correspondente, então faz sentido dizer que uma estatística é uma variável aleatória.

---

Alguns exemplos de parâmetros e suas notações:

* $\mu$: média populacional,
* $\sigma^2$: variância populacional,
* $\sigma$: desvio-padrão populacional,
* $p$: proporção populacional.


Seguem alguns exemplos de estatísticas com suas respectivas notações mais usuais (em todos os exemplos $n$ é o tamanho da amostra):

* **média amostral** (*sample mean*, *empirical mean*):
$$
		\overline{x} = \frac{1}{n}(x_1 + x_2 + \ldots + x_n)
$$
* **variância amostral** (sample variance):
$$
		s^2 = \frac{1}{n-1} \sum_{i}(x_i  - \overline{x})^2
$$

* **desvio padrão amostral** (sample standard deviation):
$$
		s = \sqrt{s^2}
$$

* Considere que $k$ é a quantidade de indivíduos na amostra que possuem uma dada característica de interesse (sendo assim, $n-k$ indivíduos dessa amostra não possuem essas caracterísica). A **proporção amostral** (sample proportion) é uma estatística dada por:

$$
		\widehat{p} = \frac{k}{n}
$$

Repare que os valores de cada uma das estatísticas acima são computados sobre amostras aleatórias de tamanho fixo $n$. De fato, cada uma dessas estatísticas é uma função que mapeia elementos de $\Re^n$ em $\Re$.

---

> 📝 **Pergunta 01.2**
>
> Em uma pesquisa eleitoral, 600 eleitores foram consultados e 312 disseram preferir o candidato A.
>
> **(a)** Calcule a proporção amostral $\widehat{p}$.
>
> **(b)** O valor que você calculou é um **parâmetro** ou uma **estatística**? Justifique.
>
> **(c)** Por que dizemos que uma estatística é uma *variável aleatória*, enquanto um parâmetro é apenas um *valor numérico* (ainda que desconhecido)? Dê uma explicação com suas próprias palavras.

---

## Objetivo da Inferência Estatística

---

> O objetivo da Inferência Estatística é produzir afirmações sobre dada **característica** dos elementos de uma população, com base nos dados contidos em uma ou mais amostras dessa população.

A característica sob estudo pode ser representada por uma variável aleatória, que possui uma determinada distribuição de probabilidades com determinado conjunto de parâmetros. Seguem alguns exemplos:

1. A altura dos indivíduos de uma determinada população é uma característica que pode ser modelada por meio da [distribuição normal](https://en.wikipedia.org/wiki/Normal_distribution) com média $\mu=1.65$ m e variância $\sigma^2 = 0.2$ $m^2$.

2. O tempo de atendimento em um quiosque pode ser modelado por uma [distribuição exponencial](https://en.wikipedia.org/wiki/Exponential_distribution). Se parametrizarmos por **taxa** $\lambda$, então a média é $1/\lambda$ (por exemplo, média 5 minutos implica $\lambda = 1/5$ por minuto).

3. A quantidade de defeitos em cada peça produzida em um processo industrial segue uma [distribuição de Poisson](https://en.wikipedia.org/wiki/Poisson_distribution), com média igual a $\lambda = 0.8$.

Repare que cada um dos exemplos acima presupõe que foi feito um estudo para (1) identificar a distribuição de probabilidades (normal, exponencial, Poisson, etc) mais adequada para o problema em questão e (2) identificar a combinação de parâmetros mais adequada para aquela distribuição.

Quando a função de massa de probabilidade (no caso discreto) ou a função de densidade de probabilidade (no caso contínuo) da variável aleatória é conhecida, o problema de fazer afirmações sobre a população fica substancialmente simplificado. Ocorre que muitas vezes não sabemos nada sobre a variável ou essa informação é parcial. Por exemplo, no caso das alturas dos indivíduos de uma população, podemos presumir que elas sigam uma distribuição normal, mas em geral desconhecemos os parâmetros que a caracterizam (e.g., média e variância).

---

Em geral, pode acontecer de

*	termos uma ideia de qual deve ser a distribuição de probabilidades adequada, mas desconhecermos os valores dos parâmetros dessa distribuição.
*	conhecermos os valores dos parâmetros, mas desconhecermos a distribuição de probabilidades.
*	não conhecermos nem a distribuição de probabilidades nem os respectivos valores dos parâmetros.

Em qualquer caso, o uso de uma amostra pode nos revelar informações sobre o comportamento da variável sob estudo na população.

---

> 📝 **Pergunta 01.3**
>
> Para cada situação abaixo, identifique se o problema é de **estimação de parâmetros** ou de **teste de hipóteses** e justifique em uma frase:
>
> **(a)** Um engenheiro coleta 50 medições do tempo de resposta de um servidor (que segue distribuição exponencial) e calcula $\overline{x} = 120$ ms para estimar o parâmetro $\lambda$.
>
> **(b)** Uma fabricante afirma que seus chips têm taxa de defeitos inferior a 2%. Um laboratório independente testa 200 chips e quer verificar essa alegação.
>
> **(c)** Um pesquisador quer descobrir qual distribuição de probabilidades melhor descreve o número de acessos por minuto a um servidor web.

---

## Problemas alvos da Inferência Estatística

---

As técnicas da Inferência Estatística podem ser divididas em duas grandes famílias:

**Estimação de parâmetros**
> Conjunto de técnicas para **construir uma estimativa** para um parâmetro de uma população por meio de observações de uma amostra.

**Teste de hipóteses**
> Conjunto de técnicas para **verificar alguma alegação** acerca do parâmetro de uma população por meio de observações de um ou mais amostras.

---

## Amostras i.i.d.

Em muitos resultados da Inferência Estatística (por exemplo, LLN e TLC), assume-se que as observações da amostra são **i.i.d.** (*independent and identically distributed*), isto é:

- **independentes**: conhecer o valor de uma observação não altera a distribuição das demais;
- **identicamente distribuídas**: todas as observações seguem a mesma distribuição de probabilidades.

Intuição prática:

- A parte “i.d.” garante que estamos observando o mesmo fenômeno estatístico ao longo da amostra.
- A parte “independente” simplifica o cálculo de variâncias e sustenta resultados assintóticos clássicos.

Observação importante:

- Em amostragem aleatória simples **com reposição**, as hipóteses de independência e de distribuição idêntica são naturais.
- Em amostragem aleatória simples **sem reposição**, há dependência entre sorteios; ainda assim, quando a fração amostral é pequena ($n/N$ pequeno), tratar a amostra como aproximadamente i.i.d. costuma ser uma aproximação útil.

---

> 📝 **Pergunta 01.4**
>
> Considere uma amostra de tamanho $n$ usada para inferir um parâmetro populacional.
>
> **(a)** Explique, com suas palavras, o que significa dizer que as observações são i.i.d.
>
> **(b)** Dê um exemplo de situação em que a hipótese de independência pode falhar na prática.

---

## Planos Amostrais

Dada uma população finita de tamanho $N$, pode-se mostrar que a quantidade de amostras de tamanho $n$ que podem ser formadas a partir dessa população é
$$
\binom{N}{n} = \frac{N!}{n!(N-n)!}
$$
no caso em que a amostragem é **sem reposição** e em que a **ordem dos elementos na amostra não importa**.

Um **plano amostral** é uma forma de produzir amostras a partir de uma população. Existem inúmeros planos amostrais. Alguns planos amostrais são:

* Amostragem aleatória sistemática
* Amostragem aleatória estratificada
* Amostragem aleatória simples

---

> 📝 **Pergunta 01.5**
>
> Uma escola tem $N = 1.200$ alunos e você quer selecionar uma amostra de $n = 60$.
>
> **(a)** Calcule (ou estime usando logaritmos/calculadora) $\log_{10}\binom{1200}{60}$ para ter uma ideia da magnitude do número de amostras possíveis. O que esse número implica sobre a viabilidade de examinar todas as amostras?
>
> **(b)** Por que a **aleatorização** no processo de seleção da amostra é fundamental para que as conclusões da inferência sejam válidas?
>
> **(c)** Se você simplesmente pedisse aos primeiros 60 alunos que chegassem à escola na segunda-feira de manhã para participar do estudo, que tipo de problema isso introduziria?

---

### Amostragem aleatória sistemática

Os itens ou indivíduos da população são ordenados de alguma forma - alfabeticamente ou por meio de algum outro método. Um ponto de partida aleatório é sorteado, e então cada $k$-ésimo membro da população é selecionado para a amostra. A varrecura sobre a lista ordenada é realizada de forma circular.

<p align="center">
  <img src="../figs/systematic_sampling_800.png" />
</p>

---

> 📝 **Pergunta 01.6**
>
> Uma lista com $N = 500$ funcionários está ordenada alfabeticamente. Você quer uma amostra sistemática de tamanho $n = 25$.
>
> **(a)** Qual deve ser o intervalo de seleção $k$?
>
> **(b)** Se o ponto de partida sorteado for o funcionário de número 7, quais são os **três primeiros** funcionários selecionados (informe seus números na lista)?
>
> **(c)** Cite uma situação concreta em que a amostragem sistemática poderia introduzir **viés** nos resultados.

---

### Amostragem aleatória estratificada

A população é inicialmente dividida em subgrupos (estratos) e uma subamostra é selecionada a partir de cada estrato da população. O objetivo é fazer com a amostra resultante contenha proporções similares dos diferentes subgrupos da população.

<p align="center">
  <img src="../figs/stratified_sampling.png" />
</p>

---

> 📝 **Pergunta 01.7**
>
> Uma universidade tem três cursos: Engenharia (400 alunos), Medicina (200 alunos) e Ciência da Computação (100 alunos). Você quer realizar uma **amostragem estratificada proporcional** de tamanho total $n = 70$.
>
> **(a)** Quantos alunos devem ser selecionados de **cada curso**? Mostre o cálculo.
>
> **(b)** Por que a amostragem estratificada pode ser **preferível à AAS simples** quando os estratos têm tamanhos muito diferentes?
>
> **(c)** O que poderia acontecer com as conclusões do estudo se o estrato de Ciência da Computação fosse completamente ignorado na amostragem?

---

### Amostragem aleatória simples (AAS)

Na AAS, cada amostra é escolhida de tal forma que cada elemento da população tem a mesma probabilidade de ser selecionado. Em uma AAS sem reposição de tamanho $n$ a partir de uma população de tamanho $N$, a probabilidade de inclusão de cada elemento é $n/N$.

Uma AAS pode ser recolhida *com reposição* ou *sem reposição*.

* Quando a amostra é recolhida com reposição, cada elemento eventualmente selecionado pode ser selecionado novamente.

* Quando a amostra é recolhida sem reposição, não há independência entre os elementos, fato que tem impacto na fórmula do cálculo das estimativas feito a partir dessa amostra.

Observação importante sobre probabilidades:

- Em um único sorteio, a probabilidade de escolher um elemento específico é $1/N$.
- Em uma amostra final de tamanho $n$, a probabilidade de inclusão desse elemento depende de haver ou não reposição.

**Sem reposição (AAS sem reposição):**

- A população efetiva diminui a cada sorteio, mas a probabilidade final de inclusão é:
$$
P(\text{inclusão}) = \frac{n}{N}.
$$
- Uma forma de ver isso é pelo complemento:
$$
P(\text{não inclusão})=
\frac{N-1}{N}\cdot\frac{N-2}{N-1}\cdots\frac{N-n}{N-n+1}
=\frac{N-n}{N},
$$
logo
$$
P(\text{inclusão})=1-\frac{N-n}{N}=\frac{n}{N}.
$$

**Com reposição:**

- Em cada sorteio, a probabilidade de seleção continua sendo $1/N$.
- Em $n$ sorteios com reposição, a probabilidade de o elemento aparecer pelo menos uma vez é:
$$
P(\text{inclusão ao menos uma vez}) = 1-\left(1-\frac{1}{N}\right)^n.
$$
- Portanto, nesse caso, a probabilidade de inclusão não é $n/N$.

<p align="center">
  <img src="../figs/simple_random_sampling_qp.jpg" />
</p>

---

## Dúvida frequente: AAS com ou sem reposição?

Em estudos estatísticos aplicados com população finita, a escolha mais comum é **AAS sem reposição**.

Por quê?

- Evita selecionar a mesma unidade mais de uma vez sem necessidade.
- Em geral, produz estimativas mais eficientes (menor variabilidade) para o mesmo tamanho amostral.

Quando considerar cada caso:

1. **Coleta em população finita (pessoas, escolas, empresas):** preferir **sem reposição**.
2. **Modelagem teórica e simulações:** **com reposição** pode ser útil por simplificar a análise (sorteios independentes).
3. **Fração amostral pequena** ($n/N \leq 5\%$): a diferença prática entre com e sem reposição costuma ser pequena em muitas fórmulas.
4. **Fração amostral não pequena:** é importante tratar o caso sem reposição explicitamente (incluindo correção para população finita quando necessário).

Resumo prático:

> Para pesquisa aplicada, normalmente usa-se AAS sem reposição.  
> Com reposição é mais comum em contextos teóricos, simulação ou quando repetir unidades faz sentido no desenho amostral.

---

> 📝 **Pergunta 01.8**
>
> Uma urna contém $N = 1.000$ nomes. Você realiza $n = 50$ sorteios.
>
> **(a)** Supondo **sem reposição**, qual é a probabilidade de inclusão de um elemento específico? Mostre o cálculo usando a fórmula do complemento apresentada no texto.
>
> **(b)** Supondo **com reposição**, qual é a probabilidade de um elemento específico ser incluído *ao menos uma vez*? Calcule numericamente e compare com o resultado do item (a).
>
> **(c)** A fração amostral $n/N$ nesse caso é pequena o suficiente (i.e., $\leq 5\%$) para que a diferença entre os dois regimes seja desprezível na prática? Justifique.
>
> **(d)** Em qual dos seguintes contextos faria mais sentido usar AAS **com** reposição: (i) pesquisa de opinião com eleitores, (ii) simulação computacional de um processo estocástico, (iii) controle de qualidade em linha de produção?
