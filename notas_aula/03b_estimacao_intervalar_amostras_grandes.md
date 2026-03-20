# 03b Estimação Intervalar para Amostras Grandes

## Escopo

Com amostras i.i.d. suficientemente grandes, usamos aproximações assintóticas (TLC) para construir intervalos de confiança (ICs) para:

- média populacional $\mu$;
- proporção populacional $p$.

**Sobre o critério "amostra grande":** para a média, a regra prática $n > 30$ costuma funcionar bem quando a distribuição subjacente é aproximadamente simétrica e sem caudas muito pesadas. Em distribuições muito assimétricas ou de cauda pesada (ex.: log-normal, Pareto), a aproximação normal pode exigir $n$ consideravelmente maior — não existe um limiar universal. Para a proporção, além de $n$ grande, é importante verificar se há quantidade suficiente de sucessos e falhas na amostra (ver seção específica abaixo).

## IC para a média populacional $\mu$

Com nível de confiança $(1-\alpha)$ e ponto crítico $z_{\alpha/2}$:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}
$$

Se $\sigma$ é desconhecido e $n$ é grande, usa-se $s$:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{s}{\sqrt{n}}
$$

---

> 📝 **Pergunta 03b.1**
>
> No caso de IC para $\mu$ com amostra grande:
>
> **(a)** Qual fórmula é usada quando $\sigma$ é conhecido?
>
> **(b)** O que muda na fórmula quando $\sigma$ é desconhecido?

### Procedimento prático

1. calcular $\overline{x}$;
2. calcular erro-padrão ($\sigma/\sqrt{n}$ ou $s/\sqrt{n}$);
3. obter $z_{\alpha/2}$ na normal padrão;
4. calcular os limites do IC.

## IC para a proporção populacional $p$

Para amostras grandes, usando $\widehat{p}$:

$$
\widehat{p} \pm z_{\alpha/2}\sqrt{\frac{\widehat{p}(1-\widehat{p})}{n}}
$$

**Condição de aplicabilidade:** a heurística mais comum requer pelo menos 10 sucessos e 10 falhas na amostra (i.e., $n\widehat{p} \ge 10$ e $n(1-\widehat{p}) \ge 10$). Essa condição garante que a distribuição binomial subjacente seja razoavelmente simétrica e bem aproximada pela normal. Alguns textos adotam o limiar mais conservador de 15 em cada categoria; outros aceitam 5. O limiar de 10 é amplamente usado e representa um equilíbrio razoável entre exigência e praticidade.

---

> 📝 **Pergunta 03b.2**
>
> Para cada situação abaixo, verifique se a condição de aplicabilidade do IC para proporção é satisfeita. Justifique calculando o número de sucessos e falhas na amostra.
>
> **(a)** $n = 80$, $\widehat{p} = 0{,}08$
>
> **(b)** $n = 200$, $\widehat{p} = 0{,}15$
>
> **(c)** $n = 50$, $\widehat{p} = 0{,}50$

## Confiabilidade vs precisão

- Maior nível de confiança ⟹ intervalo mais largo.
- Menor nível de confiança ⟹ intervalo mais estreito.

Para tamanho amostral fixo, há trade-off entre confiabilidade e precisão.

---

> 📝 **Pergunta 03b.3**
>
> Mantendo $n$ fixo, o que acontece com a largura do intervalo quando:
>
> **(a)** aumentamos o nível de confiança?
>
> **(b)** reduzimos o nível de confiança?

## Tamanho da amostra

### Para estimar $\mu$ com erro máximo $E$

$$
n = \left\lceil\frac{\sigma^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

Na prática, se $\sigma$ é desconhecido, usar estimativa de estudo piloto ($s$).

### Para estimar $p$ com erro máximo $E$

$$
n = \left\lceil\frac{z_{\alpha/2}^2 p(1-p)}{E^2}\right\rceil
$$

Se $p$ é desconhecido e não há piloto, aproximação conservadora:

$$
n = \left\lceil\frac{z_{\alpha/2}^2}{4E^2}\right\rceil
$$

---

> 📝 **Pergunta 03b.4**
>
> Calcule $p(1-p)$ para os valores $p = 0{,}50$, $p = 0{,}30$ e $p = 0{,}10$. Com base nos resultados:
>
> **(a)** Para qual valor de $p$ o produto é maior?
>
> **(b)** O que isso implica sobre o tamanho amostral calculado com a fórmula conservadora $p(1-p) = 1/4$ quando o $p$ real é próximo de 0 ou 1?

## Determinação do tamanho da amostra (detalhado)

Nesta seção, o objetivo é planejar o estudo antes da coleta, definindo um tamanho amostral mínimo que garanta:

- nível de confiança $(1-\alpha)$;
- margem de erro máxima $E$.

### Caso 1: parâmetro de interesse é $\mu$

Para planejar o tamanho amostral necessário para estimar $\mu$ com margem de erro máxima $E$ e nível de confiança $(1-\alpha)$, usa-se:

$$
n=\left\lceil\frac{\sigma^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

Se $\sigma$ for desconhecido, substituímos por uma estimativa obtida em estudo piloto ($s$):

$$
n=\left\lceil\frac{s^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

A derivação dessa expressão é apresentada no apêndice ao final da seção.

### Caso 2: parâmetro de interesse é $p$

Usando a aproximação normal para a proporção amostral:

$$
\widehat{p}\sim\mathcal{N}\left(p,\frac{p(1-p)}{n}\right)
$$

o tamanho amostral pode ser calculado por:

$$
n=\left\lceil\frac{z_{\alpha/2}^2\,p(1-p)}{E^2}\right\rceil
$$

Se houver amostra piloto, substitui-se $p$ por $\widehat{p}_{\text{pil}}$:

$$
n=\left\lceil\frac{z_{\alpha/2}^2\,\widehat{p}_{\text{pil}}(1-\widehat{p}_{\text{pil}})}{E^2}\right\rceil
$$

Sem piloto, usa-se aproximação conservadora $p(1-p)\le 1/4$:

$$
n=\left\lceil\frac{z_{\alpha/2}^2}{4E^2}\right\rceil
$$

Essa escolha maximiza $p(1-p)$ — o produto é máximo em $p=0{,}5$ e decresce à medida que $p$ se afasta desse valor. Por isso, quando o $p$ real está próximo de 0 ou 1, a fórmula conservadora superdimensiona a amostra.

### Exemplos (planejamento amostral)

**1. Exemplo com média:**
- piloto com $s^2=16$, $E=0{,}5$, 95% de confiança ($z_{0{,}025}=1{,}96$)
- resultado:
$$
n=\left\lceil\frac{16\cdot(1{,}96)^2}{(0{,}5)^2}\right\rceil=245
$$

**2. Exemplo com proporção:**
- estimativa prévia $p\approx0{,}60$, $E=0{,}03$, 95% de confiança
- resultado:
$$
n=\left\lceil\frac{(1{,}96)^2(0{,}6)(0{,}4)}{(0{,}03)^2}\right\rceil\approx1024
$$

**3. Leitura prática:**
- reduzir $E$ aumenta fortemente $n$;
- aumentar o nível de confiança também aumenta $n$;
- em custos altos, amostra piloto tende a melhorar o planejamento.

**4. Exemplo (proporção, inferência a partir de IC já publicado):**
- foi reportado IC 95% para proporção de obesidade entre 22% e 24%;
- a margem de erro é $E=0{,}01$ (metade da largura 0,02);

Abordagem conservadora (sem estimativa prévia de $p$):
$$
n=\left\lceil\frac{(1{,}96)^2}{4(0{,}01)^2}\right\rceil
=\left\lceil 9604 \right\rceil
=9604
$$

Abordagem com $\widehat{p}=0{,}23$ (usando a estimativa disponível no IC publicado):
$$
n=\left\lceil\frac{(1{,}96)^2(0{,}23)(0{,}77)}{(0{,}01)^2}\right\rceil
=\left\lceil 6828{,}7 \right\rceil
=6829
$$

**Comparação:** usar a estimativa $\widehat{p}=0{,}23$ reduz o tamanho amostral necessário de 9.604 para 6.829 — uma economia de cerca de 29%. Isso ilustra concretamente como a abordagem conservadora superdimensiona a amostra quando $p$ está longe de 0,5.

**5. Exemplo (média, renda com $\sigma$ conhecido):**
- deseja-se erro máximo de R\$500, com 95% de confiança e $\sigma=6250$:
$$
n=\left\lceil\frac{(6250)^2(1{,}96)^2}{(500)^2}\right\rceil
=\left\lceil 600{,}25 \right\rceil
=601
$$
- se a margem de erro for relaxada para R\$1000:
$$
n=\left\lceil\frac{(6250)^2(1{,}96)^2}{(1000)^2}\right\rceil
=\left\lceil 150{,}06 \right\rceil
=151
$$
- **leitura:** dobrar $E$ reduz o tamanho amostral aproximadamente por um fator de 4 (de 601 para 151).

---

> 📝 **Pergunta 03b.5**
>
> No caso de tamanho amostral para estimar $\mu$, use a expressão
> $$
> n=\left\lceil\frac{\sigma^2 z_{\alpha/2}^2}{E^2}\right\rceil
> $$
> para justificar, em uma frase, por que dobrar a margem de erro $E$ reduz aproximadamente o tamanho amostral por um fator 4.

## Exercícios de fixação

### Situações-problema com média populacional

**1. Tempo de atendimento em uma clínica**

Uma clínica deseja estimar o tempo médio de atendimento de seus pacientes. Uma amostra aleatória de $n=64$ atendimentos produziu média amostral $\overline{x}=38$ minutos. Suponha que o desvio-padrão populacional seja conhecido e igual a $\sigma=12$ minutos.

- construa um IC de 95% para o tempo médio de atendimento;
- interprete o intervalo no contexto do problema;
- diga qual seria o efeito de aumentar o nível de confiança para 99%.

**Solução**

Para 95% de confiança, temos $\alpha=0{,}05$ e, portanto, precisamos do valor crítico $z_{\alpha/2}=z_{0{,}025}$.

Em Python, esse valor pode ser obtido com a função `ppf` da normal padrão:

```python
from scipy.stats import norm
norm.ppf(0.975)
```

A sigla `ppf` significa *percent point function* e corresponde à função inversa da CDF. Aqui usamos `0.975` porque:

- a área central desejada é 0,95;
- sobra 0,05 nas duas caudas;
- cada cauda fica com 0,025;
- então o ponto crítico à direita deixa 0,975 de área acumulada à esquerda.

Assim, obtemos aproximadamente:

$$
z_{0{,}025}\approx1{,}96
$$

O erro-padrão é:

$$
\frac{\sigma}{\sqrt{n}}=\frac{12}{\sqrt{64}}=\frac{12}{8}=1{,}5
$$

A margem de erro é:

$$
E=1{,}96\cdot1{,}5=2{,}94
$$

Logo, o intervalo de confiança é:

$$
38\pm2{,}94
$$

ou seja,

$$
(35{,}06,\ 40{,}94)
$$

**Interpretação:** com 95% de confiança, o procedimento produz um intervalo que sugere que o tempo médio de atendimento está entre aproximadamente 35,1 e 40,9 minutos.

Se o nível de confiança aumentar para 99%, o valor crítico aumenta, a margem de erro fica maior e o intervalo se torna mais largo.

**2. Peso médio de embalagens**

Uma indústria quer verificar o peso médio de um produto embalado automaticamente. Foi coletada uma amostra grande com $n=100$ embalagens, obtendo-se $\overline{x}=502$ g e desvio-padrão amostral $s=8$ g.

- construa um IC de 95% para o peso médio populacional;
- explique por que, nesse caso, é aceitável usar $s$ no lugar de $\sigma$;
- avalie se o intervalo é compatível com a meta nominal de 500 g.

**3. Salário médio de estagiários**

Uma universidade deseja estimar a bolsa média mensal recebida por seus estagiários. Uma amostra de $n=49$ alunos apresentou média $\overline{x}=R\$ 1.420$ e desvio-padrão populacional conhecido $\sigma=210$.

- construa um IC de 90% para a bolsa média;
- compare conceitualmente esse intervalo com o que seria obtido para 95% de confiança;
- diga qual dos dois é mais estreito e por quê.

### Situações-problema com proporção populacional

**4. Aprovação de uma política institucional**

Uma instituição entrevistou $n=200$ alunos sobre uma nova política acadêmica. Desses, 136 declararam ser favoráveis à proposta.

- calcule $\widehat{p}$;
- verifique se a condição de aplicabilidade da aproximação normal é satisfeita;
- construa um IC de 95% para a proporção populacional de alunos favoráveis;
- interprete o resultado em linguagem não técnica.

**Solução**

A proporção amostral é:

$$
\widehat{p}=\frac{136}{200}=0{,}68
$$

Para verificar a aplicabilidade da aproximação normal:

$$
n\widehat{p}=200\cdot0{,}68=136
$$

$$
n(1-\widehat{p})=200\cdot0{,}32=64
$$

Como há pelo menos 10 sucessos e 10 falhas, a aproximação normal é adequada.

Para 95% de confiança, temos $\alpha=0{,}05$ e precisamos do valor crítico $z_{0{,}025}$.

Em Python, esse valor pode ser obtido com:

```python
from scipy.stats import norm
norm.ppf(0.975)
```

Assim, usamos aproximadamente:

$$
z_{0{,}025}\approx1{,}96
$$

O erro-padrão é:

$$
\sqrt{\frac{\widehat{p}(1-\widehat{p})}{n}}
=
\sqrt{\frac{(0{,}68)(0{,}32)}{200}}
=
\sqrt{0{,}001088}
\approx0{,}033
$$

A margem de erro é:

$$
E=1{,}96\cdot0{,}033\approx0{,}065
$$

Logo, o intervalo de confiança é:

$$
0{,}68\pm0{,}065
$$

ou seja,

$$
(0{,}615,\ 0{,}745)
$$

Em porcentagem, isso corresponde aproximadamente a:

$$
(61{,}5\%,\ 74{,}5\%)
$$

**Interpretação:** com 95% de confiança, o procedimento indica que a proporção de alunos favoráveis à proposta está entre cerca de 61,5% e 74,5%.

**5. Uso de bicicleta para ir ao campus**

Em uma pesquisa com $n=120$ estudantes, 18 afirmaram ir ao campus de bicicleta com frequência.

- calcule a proporção amostral;
- verifique se a condição de pelo menos 10 sucessos e 10 falhas é satisfeita;
- construa um IC de 90% para a proporção populacional;
- explique se seria adequado usar o mesmo procedimento com $n=30$ mantendo a mesma proporção amostral.

**6. Intenção de voto em uma chapa estudantil**

Uma chapa deseja estimar sua proporção de apoio entre os alunos. Em uma amostra de $n=500$ estudantes, 260 declararam intenção de voto nessa chapa.

- construa um IC de 95% para a proporção populacional de apoio;
- calcule a margem de erro desse intervalo;
- explique como a margem de erro mudaria se a amostra tivesse tamanho $n=1000$, mantendo a mesma proporção amostral.

### Questões de comparação e interpretação

**7. Comparando dois intervalos para a média**

Duas equipes calcularam ICs para a mesma variável:

- equipe A: $\overline{x} \pm 1{,}96\cdot\frac{10}{\sqrt{100}}$
- equipe B: $\overline{x} \pm 2{,}58\cdot\frac{10}{\sqrt{100}}$

Responda:

- qual equipe usou maior nível de confiança;
- qual intervalo é mais largo;
- por que isso acontece.

**Gabarito resumido**

A equipe B usou maior nível de confiança, porque utilizou um valor crítico maior:

- equipe A: $1{,}96$, típico de 95% de confiança;
- equipe B: $2{,}58$, típico de 99% de confiança.

Como o erro-padrão é o mesmo nos dois casos,

$$
\frac{10}{\sqrt{100}}=1,
$$

as margens de erro são:

- equipe A: $1{,}96\cdot1=1{,}96$;
- equipe B: $2{,}58\cdot1=2{,}58$.

Portanto, o intervalo da equipe B é mais largo.

**Interpretação:** quanto maior o nível de confiança, maior é o valor crítico usado, maior é a margem de erro e mais largo fica o intervalo.

**8. Comparando dois intervalos para proporção**

Considere duas pesquisas sobre o mesmo tema:

- pesquisa A: $n=100$, $\widehat{p}=0{,}50$
- pesquisa B: $n=400$, $\widehat{p}=0{,}50$

Sem calcular todos os extremos, responda:

- qual pesquisa tende a produzir menor erro-padrão;
- qual intervalo de confiança tende a ser mais estreito;
- qual é o papel do tamanho amostral nessa comparação.

**9. Leitura crítica de um intervalo publicado**

Um relatório afirma que a proporção de estudantes com acesso diário ao restaurante universitário é de 62%, com IC 95% entre 58% e 66%.

- identifique a estimativa pontual;
- identifique a margem de erro;
- explique o significado prático desse intervalo;
- diga se a frase "há 95% de probabilidade de o verdadeiro valor estar entre 58% e 66%" está conceitualmente correta.

### Desafio de planejamento

**10. Planejamento de pesquisa**

Uma equipe quer estimar a proporção de alunos que pretendem fazer intercâmbio, com margem de erro máxima de 4 pontos percentuais e 95% de confiança.

- calcule o tamanho amostral conservador;
- explique por que a escolha conservadora usa $p(1-p)=1/4$;
- diga o que aconteceria com o tamanho amostral se houvesse estudo piloto indicando $p\approx0{,}20$.

## Apêndice: derivação do IC para a média em amostras grandes

Queremos construir um intervalo de confiança para a média populacional $\mu$ a partir da média amostral $\overline{X}$.

### Passo 1: distribuição da média amostral

Se $X_1,\dots,X_n$ são i.i.d., com média $\mu$ e variância $\sigma^2$, então, para $n$ grande, o Teorema Central do Limite implica:

$$
\overline{X}\approx \mathcal{N}\left(\mu,\frac{\sigma^2}{n}\right)
$$

Isto é, a média amostral tem:

- média igual a $\mu$;
- desvio-padrão igual a $\sigma/\sqrt{n}$.

### Passo 2: padronização

Subtraindo a média e dividindo pelo desvio-padrão, obtemos a variável padronizada:

$$
Z=\frac{\overline{X}-\mu}{\sigma/\sqrt{n}}
\approx \mathcal{N}(0,1)
$$

### Passo 3: região central da normal padrão

Para um nível de confiança $(1-\alpha)$, escolhemos o valor crítico $z_{\alpha/2}$ tal que:

$$
\Pr\left(-z_{\alpha/2}\le Z\le z_{\alpha/2}\right)=1-\alpha
$$

Substituindo $Z$ pela expressão padronizada:

$$
\Pr\left(
-z_{\alpha/2}\le
\frac{\overline{X}-\mu}{\sigma/\sqrt{n}}
\le z_{\alpha/2}
\right)=1-\alpha
$$

### Passo 4: isolamento de $\mu$

Multiplicando todos os termos por $\sigma/\sqrt{n}$:

$$
\Pr\left(
-z_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\le
\overline{X}-\mu
\le
z_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\right)=1-\alpha
$$

Agora, isolando $\mu$:

$$
\Pr\left(
\overline{X}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\le
\mu
\le
\overline{X}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\right)=1-\alpha
$$

Portanto, o intervalo de confiança de nível $(1-\alpha)$ para $\mu$ é:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}
$$

### Interpretação da fórmula

Essa expressão pode ser lida como:

$$
\text{estimativa pontual} \pm \text{margem de erro}
$$

em que:

- a estimativa pontual é $\overline{x}$;
- a margem de erro é $z_{\alpha/2}\cdot \sigma/\sqrt{n}$.

### Resumo

1. a média amostral $\overline{X}$ oscila de amostra para amostra;
2. para $n$ grande, essa oscilação é aproximadamente normal;
3. usamos a parte central da normal padrão para capturar uma fração $(1-\alpha)$ dos resultados;
4. ao desfazer a padronização, obtemos um intervalo plausível para $\mu$.

### Observação importante

Quando $\sigma$ é desconhecido, em amostras grandes substituímos $\sigma$ por $s$, obtendo:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{s}{\sqrt{n}}
$$

## Apêndice: derivação do IC para a proporção em amostras grandes

Queremos construir um intervalo de confiança para a proporção populacional $p$ a partir da proporção amostral $\widehat{P}$.

### Passo 1: distribuição da proporção amostral

Se cada observação pode ser vista como uma variável Bernoulli com parâmetro $p$, então a soma dos sucessos na amostra tem distribuição binomial. Logo, a proporção amostral

$$
\widehat{P}=\frac{X}{n}
$$

tem:

- média igual a $p$;
- variância igual a $\dfrac{p(1-p)}{n}$.

Para $n$ grande, a aproximação normal fornece:

$$
\widehat{P}\approx \mathcal{N}\left(p,\frac{p(1-p)}{n}\right)
$$

### Passo 2: padronização

Padronizando a proporção amostral, obtemos:

$$
Z=\frac{\widehat{P}-p}{\sqrt{p(1-p)/n}}
\approx \mathcal{N}(0,1)
$$

### Passo 3: região central da normal padrão

Para um nível de confiança $(1-\alpha)$, tomamos o valor crítico $z_{\alpha/2}$ tal que:

$$
\Pr\left(-z_{\alpha/2}\le Z\le z_{\alpha/2}\right)=1-\alpha
$$

Substituindo $Z$:

$$
\Pr\left(
-z_{\alpha/2}\le
\frac{\widehat{P}-p}{\sqrt{p(1-p)/n}}
\le z_{\alpha/2}
\right)=1-\alpha
$$

### Passo 4: isolamento de $p$

Se tratássemos a variância como totalmente conhecida, a expressão acima sugeriria um intervalo do tipo:

$$
p \approx \widehat{p} \pm z_{\alpha/2}\sqrt{\frac{p(1-p)}{n}}
$$

Mas há um problema: o erro-padrão depende do próprio parâmetro desconhecido $p$.

### Passo 5: substituição prática

Na prática, para amostras grandes, substituímos $p$ por sua estimativa amostral $\widehat{p}$ dentro do erro-padrão. Assim, obtemos o intervalo de confiança aproximado:

$$
\widehat{p} \pm z_{\alpha/2}\sqrt{\frac{\widehat{p}(1-\widehat{p})}{n}}
$$

Essa substituição é justificada pelo fato de que, em amostras grandes, $\widehat{p}$ tende a ficar próximo de $p$.

### Interpretação da fórmula

Novamente, a estrutura é:

$$
\text{estimativa pontual} \pm \text{margem de erro}
$$

em que:

- a estimativa pontual é $\widehat{p}$;
- a margem de erro é $z_{\alpha/2}\sqrt{\widehat{p}(1-\widehat{p})/n}$.

### Resumo

1. a proporção amostral $\widehat{P}$ varia de amostra para amostra;
2. para amostras grandes, essa variação é aproximadamente normal;
3. usamos a normal padrão para obter uma região central com probabilidade $(1-\alpha)$;
4. como o erro-padrão depende de $p$, substituímos $p$ por $\widehat{p}$ na fórmula final.

### Observação importante

Esse intervalo é uma aproximação assintótica. Por isso, é importante verificar se há quantidade suficiente de sucessos e falhas na amostra, de modo que a aproximação normal seja razoável.

## Apêndice: derivação da fórmula de tamanho amostral com estudo piloto

Queremos determinar um tamanho amostral mínimo $n$ para estimar a média populacional $\mu$ com:

- nível de confiança $(1-\alpha)$;
- margem de erro máxima $E$.

No caso em que $\sigma$ é desconhecido, usamos uma estimativa preliminar obtida em estudo piloto, denotada por $s$.

### Passo 1: começar pela margem de erro do IC

Para amostras grandes, o intervalo de confiança para $\mu$ é dado aproximadamente por:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}
$$

A margem de erro desse intervalo é:

$$
E=z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}
$$

### Passo 2: impor o erro máximo desejado

No planejamento amostral, escolhemos previamente um valor máximo aceitável para a margem de erro. Então, queremos que:

$$
z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}\le E
$$

Para obter o menor $n$ que satisfaça essa exigência, resolvemos a igualdade:

$$
z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}=E
$$

### Passo 3: isolar $n$

Multiplicando ambos os lados por $\sqrt{n}$:

$$
z_{\alpha/2}\sigma = E\sqrt{n}
$$

Dividindo por $E$:

$$
\sqrt{n}=\frac{z_{\alpha/2}\sigma}{E}
$$

Elevando ao quadrado:

$$
n=\frac{\sigma^2 z_{\alpha/2}^2}{E^2}
$$

### Passo 4: substituir $\sigma$ por $s$

Quando $\sigma$ é desconhecido, não podemos usar diretamente a expressão anterior. Nesse caso, usamos o desvio-padrão obtido em uma amostra piloto como aproximação:

$$
\sigma \approx s
$$

Substituindo na fórmula:

$$
n\approx\frac{s^2 z_{\alpha/2}^2}{E^2}
$$

Como o tamanho da amostra deve ser inteiro e precisamos garantir que o erro máximo não seja ultrapassado, arredondamos para cima:

$$
n=\left\lceil\frac{s^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

### Interpretação da fórmula

Essa expressão mostra que:

- aumentar o nível de confiança aumenta $z_{\alpha/2}$ e, portanto, aumenta $n$;
- aumentar a variabilidade estimada pelo piloto ($s$) aumenta $n$;
- reduzir a margem de erro $E$ aumenta fortemente o tamanho amostral, pois $E$ aparece ao quadrado no denominador.

### Resumo

1. começamos pela fórmula da margem de erro do IC da média;
2. definimos qual erro máximo queremos tolerar;
3. isolamos $n$ na expressão;
4. como $\sigma$ é desconhecido, usamos $s$ de um estudo piloto para planejar a amostra.
