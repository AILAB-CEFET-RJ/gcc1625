# Laboratório: Testes de Hipóteses, Erros e Poder

## Organização da atividade

- Formem grupos de 2 a 4 alunos.
- Tempo total: **1h30min**, incluindo preparação e revisão da entrega.
- Entreguem um único notebook Jupyter por grupo, com identificação dos integrantes, código, uma tabela de resultados dos testes, a tabela da simulação e respostas breves às perguntas de interpretação.
- Usem Python com `numpy`, `pandas` e `scipy.stats`.
- Adotem $\alpha=0{,}05$ nos testes das Partes 1 a 3. Na Parte 4, comparem os níveis indicados no roteiro.
- Definam as hipóteses e a direção de cada teste **antes de calcular os resultados**.
- Dividam as tarefas de programação, conferência das contas e interpretação, mas discutam as conclusões em conjunto.

## Objetivos

Ao final da atividade, o grupo deve ser capaz de:

- formular hipóteses sobre médias populacionais e escolher a direção do teste;
- distinguir o teste z dos testes t para uma amostra, amostras pareadas e amostras independentes;
- calcular e interpretar estatística de teste, p-valor e decisão;
- distinguir significância estatística de relevância prática;
- estimar por simulação a taxa de erro tipo I e o poder, relacionando-os ao tamanho amostral, à variabilidade e ao nível de significância.

## Material de consulta

Usem a [Nota de Aula 04 — Testes de Hipóteses](../notas_aula/GCC1625_04_testes_de_hipoteses.pdf), especialmente as Seções 1 a 4.

## Roteiro sugerido de tempo

| Etapa | Tempo |
|---|---:|
| Preparação do notebook e leitura do contexto | 5 min |
| Parte 1. Hipóteses e teste z | 15 min |
| Parte 2. Teste t para uma amostra | 20 min |
| Parte 3. Amostras pareadas e independentes | 25 min |
| Parte 4. Simulação de erros e poder | 15 min |
| Síntese final e revisão da entrega | 10 min |
| **Total** | **90 min** |

Não é necessário programar os testes do zero nem calcular os graus de liberdade de Welch à mão. Priorizem as justificativas e as interpretações; uma ou duas frases por pergunta são suficientes.

---

## Situação-problema

Uma equipe está avaliando o tempo de resposta de uma API. A referência de desempenho é **120 ms**. Tempos menores representam respostas mais rápidas.

Os dados deste laboratório são didáticos e representam estudos distintos. Para as Partes 1 a 3, admitam que as observações foram obtidas por amostragem aleatória, que as condições de carga foram controladas e que as populações de tempos são aproximadamente normais. Admitam independência entre as unidades amostradas; na comparação pareada, essa independência vale **entre os pares**, mas não entre as duas medidas do mesmo par. Na Parte 3, admitam também que as diferenças pareadas são aproximadamente normais.

Essas condições são premissas do exercício. Em uma aplicação real, seria necessário investigar, por exemplo, assimetria, valores extremos e dependência temporal entre requisições.

### Preparação em Python

```python
import numpy as np
import pandas as pd
from scipy import stats

alpha = 0.05
```

Ao longo das Partes 1 a 3, preencham uma tabela com uma linha por teste:

| Estudo | Teste e direção | Estatística | Graus de liberdade, se houver | p-valor | Decisão a 5% | Efeito estimado (ms) |
|---|---|---:|---:|---:|---|---:|

Registrem as hipóteses e a conclusão contextualizada em células de texto próximas ao código. Comparem o p-valor sem arredondamento com $\alpha$; arredondem apenas sua apresentação.

---

## Parte 1. Hipóteses e teste z

Uma auditoria deseja investigar se o tempo médio de resposta **excede 120 ms**. Um estudo prévio, independente da amostra atual, permite tratar o desvio padrão populacional como conhecido: $\sigma=12$ ms. A nova amostra tem $n=64$ requisições e média $\overline{x}=123$ ms.

1. Definam o parâmetro de interesse, escrevam $H_0$ e $H_a$ e identifiquem a direção do teste. Expliquem por que cabe um teste z. Para a hipótese nula unilateral, incluam a desigualdade; o cálculo será feito no valor de fronteira $\mu_0=120$.
2. Calculem o erro padrão, a estatística z e o p-valor. Confiram a decisão também pela região crítica e escrevam uma conclusão sobre a suspeita da auditoria.
3. Interpretem o p-valor como uma probabilidade calculada sob a média de referência. Expliquem por que ele não é a probabilidade de $H_0$ ser verdadeira. Descrevam o que seriam os erros tipo I e tipo II neste contexto.

### Dicas de Python

$$
z=\frac{\overline{x}-\mu_0}{\sigma/\sqrt{n}}.
$$

- Para a cauda direita, usem `stats.norm.sf(z)`; `sf` calcula a probabilidade acima do valor informado.
- O valor crítico é `stats.norm.ppf(1 - alpha)`.
- O efeito estimado neste estudo é $\overline{x}-120$, em ms.

---

## Parte 2. Teste t para uma amostra

Em outro estudo, o desvio padrão populacional é **desconhecido**. A equipe deseja verificar se o tempo médio é **diferente de 120 ms**, em qualquer direção. Foram observados os seguintes tempos:

```python
tempos = np.array([108, 115, 119, 120, 121, 122,
                   123, 125, 126, 128, 130, 139], dtype=float)
```

4. Formulem as hipóteses e justifiquem o uso do teste t para uma amostra. Calculem $n$, $\overline{x}$, o desvio padrão amostral $s$, o erro padrão, a estatística t e os graus de liberdade. Obtenham o p-valor bilateral pela distribuição t e confiram com `stats.ttest_1samp(tempos, popmean=120)`.
5. Concluam a 5% e calculem um intervalo de confiança bilateral de 95% para $\mu$. O valor 120 pertence ao intervalo? Expliquem a relação entre essa resposta e a decisão do teste bilateral.
6. Um colega afirma: “Se o teste não rejeitar $H_0$, estará demonstrado que a média é exatamente 120 ms”. Corrijam a afirmação. Seria adequado trocar para um teste unilateral depois de observar a média? Justifiquem.

### Dicas de Python

$$
t=\frac{\overline{x}-120}{s/\sqrt{n}},
\qquad gl=n-1.
$$

- Usem `tempos.std(ddof=1)` para o desvio padrão amostral.
- O p-valor bilateral é `2 * stats.t.sf(abs(t_observado), df=gl)`.
- Para o intervalo, calculem `t_critico = stats.t.ppf(0.975, df=gl)` e os limites $\overline{x}\pm t_{\text{crítico}}\,s/\sqrt{n}$.
- O efeito estimado é $\overline{x}-120$, em ms.

---

## Parte 3. Amostras pareadas e independentes

### Estudo A: as mesmas unidades antes e depois

Uma otimização foi avaliada em dez cenários de carga. Cada cenário foi executado uma vez com a versão anterior e uma vez com a versão otimizada, em ordem aleatória. As duas medidas de cada posição dos vetores correspondem ao **mesmo cenário**.

```python
antes = np.array([88, 110, 95, 140, 105, 125, 100, 155, 118, 132], dtype=float)
depois = np.array([85, 111, 91, 138, 105, 120, 99, 152, 120, 128], dtype=float)
```

O interesse, definido antes das medições, é investigar se a otimização **reduz** o tempo médio. A equipe considera uma redução de pelo menos **5 ms** relevante para justificar seu custo de implantação.

7. Definam $d_i=\text{antes}_i-\text{depois}_i$, formulem as hipóteses sobre $\mu_d$ e justifiquem o pareamento. Calculem $\overline{d}$, $s_d$, $t=\overline{d}/(s_d/\sqrt{n})$ e $gl=n-1$. Obtenham o p-valor unilateral e confiram com um teste t pareado.
8. Concluam a 5% e comparem a redução média estimada com o limiar de 5 ms. Um resultado significativo para uma redução maior que zero, por si só, demonstra uma redução populacional de pelo menos 5 ms? Expliquem.

### Estudo B: unidades diferentes em cada grupo

Dois provedores foram avaliados com conjuntos distintos e independentes de requisições. Não há correspondência entre as requisições dos grupos A e B. Deseja-se investigar uma diferença de médias **em qualquer direção**. As estatísticas amostrais são:

| Provedor | Tamanho amostral | Média (ms) | Desvio padrão amostral (ms) |
|---|---:|---:|---:|
| A | 20 | 120 | 8 |
| B | 25 | 115 | 15 |

9. Formulem as hipóteses e apliquem o teste de Welch. Calculem a estatística t pela fórmula abaixo e usem a função indicada para o p-valor bilateral. Concluam a 5%. Expliquem por que este estudo não é pareado e qual suposição adicional seria necessária para usar o teste com `equal_var=True`.

### Dicas de Python

- No Estudo A, `d = antes - depois`, `d.mean()` e `d.std(ddof=1)` fornecem os resumos das diferenças.
- `stats.ttest_rel(antes, depois)` retorna, por padrão, o teste bilateral para diferenças `antes - depois`. Para a alternativa $\mu_d>0$, calculem o p-valor com `stats.t.sf(t_observado, df=n-1)`. Não dividam um p-valor bilateral por dois sem conferir o sinal da estatística.
- Para Welch:

$$
t=\frac{\overline{x}_A-\overline{x}_B}
{\sqrt{s_A^2/n_A+s_B^2/n_B}}.
$$

- Como o Estudo B fornece apenas resumos, usem:

```python
resultado_welch = stats.ttest_ind_from_stats(
    mean1=120, std1=8, nobs1=20,
    mean2=115, std2=15, nobs2=25,
    equal_var=False,
)
```

- Para registrar os graus de liberdade de Welch, usem $v_A=s_A^2/n_A$, $v_B=s_B^2/n_B$ e $\nu=(v_A+v_B)^2/[v_A^2/(n_A-1)+v_B^2/(n_B-1)]$.
- Registrem $\overline{d}$ como efeito estimado do Estudo A e $\overline{x}_A-\overline{x}_B$ como efeito estimado do Estudo B.

---

## Parte 4. Simulação de erros e poder

Retomem a pergunta da auditoria: $H_0:\mu\leq120$ versus $H_a:\mu>120$. Agora a média populacional é conhecida **por quem simula**, permitindo verificar se a decisão do teste está correta.

Simulem populações normais em dois casos: $\mu=120$ ms (fronteira de $H_0$) e $\mu=123$ ms (aumento real de 3 ms). Em cada configuração abaixo, o desvio padrão populacional $\sigma$ é conhecido pelo teste z.

| Configuração | $n$ | $\sigma$ (ms) | $\alpha$ |
|---|---:|---:|---:|
| Referência | 20 | 12 | 0,05 |
| Amostra maior | 80 | 12 | 0,05 |
| Variabilidade maior | 20 | 24 | 0,05 |
| Significância menor | 20 | 12 | 0,01 |

Executem o código a seguir. Cada linha da matriz `amostras` é um estudo completo; a taxa de rejeição deve ser calculada sobre os **5.000 estudos**, e não sobre as observações individuais.

```python
rng = np.random.default_rng(20260915)
R = 5_000
configuracoes = [
    ("Referência", 20, 12, 0.05),
    ("Amostra maior", 80, 12, 0.05),
    ("Variabilidade maior", 20, 24, 0.05),
    ("Significância menor", 20, 12, 0.01),
]

linhas = []
for nome, n, sigma, nivel in configuracoes:
    for mu_real in [120, 123]:
        amostras = rng.normal(loc=mu_real, scale=sigma, size=(R, n))
        medias = amostras.mean(axis=1)
        z = (medias - 120) / (sigma / np.sqrt(n))
        p_valores = stats.norm.sf(z)
        taxa_rejeicao = np.mean(p_valores <= nivel)
        linhas.append({
            "configuração": nome, "n": n, "sigma": sigma,
            "alpha": nivel, "mu_real": mu_real,
            "taxa_rejeicao": taxa_rejeicao,
        })

tabela_simulacao = pd.DataFrame(linhas)
tabela_simulacao
```

10. Quando $\mu=120$, o que a taxa de rejeição estima? Comparem cada taxa com seu $\alpha$ e expliquem por que não precisam ser numericamente iguais em uma simulação finita.
11. Quando $\mu=123$, identifiquem o poder e estimem $\beta$ em cada configuração. Comparem cada mudança com a referência, mantendo os demais fatores fixos. Expliquem os efeitos de aumentar $n$, aumentar $\sigma$ e reduzir $\alpha$. O aumento do efeito real, de 3 para 6 ms, tenderia a aumentar ou diminuir o poder?
12. Por que um único estudo com p-valor acima de 0,05 não basta para concluir que não houve aumento? Diferenciem o p-valor de um estudo da estimativa de poder obtida com muitas repetições.

---

## Síntese final

Em um único parágrafo, expliquem a um colega como escolher entre z, t para uma amostra, t pareado e Welch. Incluam por que “não rejeitar $H_0$” não significa demonstrá-la e por que a decisão de implantar uma otimização deve considerar o tamanho do efeito, além do p-valor.

Antes de entregar, confiram se o notebook executa do início ao fim e contém as quatro linhas da tabela de testes, as oito linhas da tabela de simulação e as conclusões contextualizadas.
