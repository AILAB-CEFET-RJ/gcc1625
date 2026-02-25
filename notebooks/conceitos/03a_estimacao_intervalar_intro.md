# 03a Introdução à Estimação Intervalar

---

## Intervalos de Confiança

Suponha que estejamos interessados em estudar um parâmetro populacional $\theta$. Podemos estimar $\theta$ usando informação de uma amostra aleatória simples. Chamamos o único número que representa o valor mais plausível do parâmetro (baseado nos dados amostrais) de uma estimativa pontual de $\theta$. Contudo, sabemos que o valor estimado na maior parte das vezes não será exatamente igual ao valor real. Então, seria interessante encontrar um intervalo de confiança que forneça um intervalo de valores plausíveis para o parâmetro baseado nos dados amostrais. Aqui, estudamos a construção de intervalos de confiança para dois parâmetros populacionais importantes, a média $\mu$ e a proporção $p$. A subárea da Inferência Estatística que lida com esse tipo de problema é conhecida como **Estimação de Intervalos de Confiança**.

---

## Estimativa (pontual)

> Uma **estimativa pontual** de um parâmetro desconhecido $\theta$ é um valor obtido a partir de uma amostra (por meio de uma estatística). Esse é um valor aproximado do parâmetro.

* **Exemplo 1 -** Foi feita uma pesquisa junto a uma amostra de tamanho $n = 500$ de uma comunidade acadêmica acerca da criação de um bandejão. Cada entrevistado deveria dar uma de duas respostas possíveis, SIM (i.e., a favor da criação) ou NÃO (não favorável à criação). Deseja-se estimar a *proporção* de pessoas da comunidade como um todo (i.e., da população) que são favoráveis à criação do bandejão. Se 300 pessoas dizem sim, então uma estimativa pontual para a proporção populacional $p$ é o valor da proporção amostral computado naquela amostra: $\widehat{p} =\frac{300}{500}$ = 60\%.

* **Exemplo 2 -**
Em uma amostra grande de medições independentes da altura de indivíduos do sexo feminino daquela comunidade acadêmica, foram computados os valores $\overline{x} = 161$ cm e $s = 5$ cm. Sendo assim, $\overline{x} = 161$ é uma estimativa pontual do valor (desconhecido) da média de altura na população.

Nos exemplos dados, 60\% e 161 cm são denominados **estimativas pontuais** para os parâmetros populacionais *proporção favorável ao bandejão* e *altura média das mulheres*, respectivamente. **Repare: outras amostras poderiam levar a valores diferentes dessas estimativas pontuais.**

> Em geral, há uma diferença (para mais ou para menos) entre estimativas pontuais computadas conforme os exemplos acima e o valor do parâmetro correspondente. Conhecer apenas o valor da estimativa pontual não permite julgar qual a *magnitude do erro* cometido. **O adequado é construir um procedimento de intervalo que, em repetições amostrais, tenha alta taxa de cobertura do parâmetro.**

---

> 📝 **Pergunta 03a.1**
>
> Uma pesquisa entrevistou 500 pessoas, e 300 responderam "SIM" para um tema de interesse.
>
> **(a)** Calcule a estimativa pontual de $p$.
>
> **(b)** Explique por que esse valor é uma estatística e não o próprio parâmetro populacional.

---

## Intervalo de Confiança

Uma abordagem mais apropriada é construir um *intervalo de confiança* por meio de um procedimento com nível de confiança definido, centrado na estimativa pontual computada. Por exemplo, no caso do parâmetro relativo à altura, uma informação mais útil seria poder afirmar que *a altura média das mulheres da comunidade acadêmica está entre 1,56 m e 1,67 m, com 95% de confiança*.

> Um **intervalo de confiança** (ou **estimativa intervalar**) para um parâmetro populacional $\theta$ corresponde a um par de números obtido por um procedimento amostral com cobertura controlada.

No caso em que o estimador é $\widehat{p}$, temos que o intervalo de confiança para $p$ é da forma:
$$
\left[\widehat{p}-E, \widehat{p}+E\right]
$$
No caso em que o estimador é $\overline{x}$, temos que o intervalo de confiança para $\mu$ é da forma:
$$
\left[\overline{x}-E, \overline{x}+E\right]
$$

O valor $E$, que corresponde à metade do comprimento do intervalo, é denominado **erro amostral** ou **margem de erro**. Em geral, dada uma amostra da população, construir um intervalo de confiança para um dado parâmetro populacional $\theta$ corresponde a determinar $E$.

Um intervalo de confiança está sempre associado a um **nível de confiança** (*confidence level*). O valor do nível de confiança corresponde ao quão confiável é a informação de que o parâmetro populacional de interesse se encontre dentro do intervalo computado. 

> O nível de confiança é a probabilidade de que o procedimento de construção de intervalos de confiança produza um intervalo que contenha o verdadeiro valor do parâmetro populacional.

Em geral, o valor do nível de confiança usado em um estudo estatístico é definido pelo projetista antes de iniciar o estudo.

Como exemplo, considere que o nível de confiança definido para um experimento foi de 95%. Uma possível interpretação desse valor é a seguinte: se fosse possível construir 100 intervalos de confiança para um determinado parâmetro populacional $\theta$ (por meio de 100 amostras diferentes), então aproximadamente 95% desses intervalos conteriam o valor de $\theta$.

---

> 📝 **Pergunta 03a.2**
>
> O texto apresenta intervalos de confiança nas formas $[\widehat{p}-E,\widehat{p}+E]$ e $[\overline{x}-E,\overline{x}+E]$.
>
> **(a)** O que representa o termo $E$?
>
> **(b)** Por que conhecer apenas a estimativa pontual pode ser insuficiente em inferência estatística?

---

> 📝 **Pergunta 03a.3**
>
> Uma turma interpretou "nível de confiança de 95\%" como:
> "há 95\% de probabilidade de o parâmetro estar dentro do intervalo já calculado".
>
> Usando a explicação do texto, reescreva essa interpretação de forma correta.

---

## Estimadores: conceitos fundamentais

### Estimador

Um estimador $\widehat{\theta}$ é uma estatística (função da amostra) cujas realizações fornecem estimativas pontuais para um parâmetro populacional.

Exemplos usuais:

- $\widehat{p}$ (proporção amostral) como estimador de $p$.
- $\overline{x}$ (média amostral) como estimador de $\mu$.

### Precisão de um estimador

A precisão está relacionada à variabilidade das estimativas produzidas pelo estimador ao longo de amostras repetidas.

$$
\operatorname{Var}(\widehat{\theta}) = E[(\widehat{\theta} - E(\widehat{\theta}))^2]
$$

Maior precisão implica menor variância do estimador.

### Viés de um estimador

O viés mede o desvio sistemático entre o valor esperado do estimador e o parâmetro verdadeiro:

$$
\text{Viés}(\widehat{\theta}) = E[\widehat{\theta}] - \theta
$$

Se $E[\widehat{\theta}] = \theta$, o estimador é não-viesado (unbiased).

---

> 📝 **Pergunta 03a.4**
>
> Considere dois estimadores para o mesmo parâmetro:
>
> - estimador A: não-viesado, mas com variância alta;
> - estimador B: viesado, mas com variância baixa.
>
> **(a)** Qual conceito diferencia esses dois casos em termos de erro sistemático?
>
> **(b)** Qual conceito diferencia esses dois casos em termos de dispersão entre amostras?

### Exemplos clássicos

Considere população com média $\mu$ e variância $\sigma^2$.

1. **Média amostral**  
$\overline{x}$ é estimador não-viesado de $\mu$.

2. **Proporção amostral**  
$\widehat{p}$ é estimador não-viesado de $p$.

3. **Variância amostral**  
O estimador com divisor $n$ é viesado para $\sigma^2$.  
A correção de Bessel (divisor $n-1$) produz estimador não-viesado.

### Precisão versus viés e EQM

Um estimador pode combinar diferentes níveis de viés e variância. O compromisso entre esses termos aparece no Erro Quadrático Médio (EQM):

$$
\text{EQM}(\widehat{\theta}) = \text{Viés}(\widehat{\theta})^2 + \text{Var}(\widehat{\theta})
$$

Em geral, preferimos estimadores com baixo viés e baixa variância.

---

> 📝 **Pergunta 03a.5**
>
> O texto apresenta $\text{EQM}(\widehat{\theta}) = \text{Viés}(\widehat{\theta})^2 + \text{Var}(\widehat{\theta})$.
>
> **(a)** Explique, com suas palavras, o que essa decomposição mostra.
>
> **(b)** No caso da variância amostral, por que a correção de Bessel ($n-1$) é citada como importante?
