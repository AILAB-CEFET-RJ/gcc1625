# Laboratório: Estimação Intervalar, Precisão e Cobertura

## Organização da atividade

- Formem grupos de 2 a 4 alunos.
- Tempo total: **1h30min**, incluindo preparação e revisão da entrega.
- Entreguem um único notebook Jupyter por grupo, com identificação dos integrantes, código, tabelas, gráficos e respostas breves às perguntas de interpretação.
- Usem Python com `numpy`, `pandas`, `matplotlib` e `scipy.stats`.
- Usem a semente indicada na simulação para que os resultados possam ser reproduzidos.
- Dividam as tarefas de programação, conferência das contas e interpretação, mas discutam as conclusões em conjunto.

## Objetivos

Ao final da atividade, o grupo deve ser capaz de:

- distinguir estimativa pontual, erro padrão, margem de erro e intervalo de confiança;
- construir intervalos para média e proporção e verificar suas condições de aplicabilidade;
- relacionar nível de confiança, precisão e tamanho amostral;
- usar a distribuição t quando o desvio padrão populacional é desconhecido e avaliar a plausibilidade da normalidade em uma amostra pequena;
- interpretar o nível de confiança pela cobertura do procedimento em amostragens repetidas.

## Material de consulta

Usem a [Nota de Aula 03 — Estimação Intervalar](../notas_aula/GCC1625_03_estimacao_intervalar.pdf), especialmente as Seções 1 a 3. Não é necessário estudar os apêndices para realizar o laboratório.

## Roteiro sugerido de tempo

| Etapa | Tempo |
|---|---:|
| Preparação do notebook e leitura do contexto | 5 min |
| Parte 1. Média, confiança e precisão | 20 min |
| Parte 2. Proporção e planejamento amostral | 20 min |
| Parte 3. Amostra pequena e distribuição t | 20 min |
| Parte 4. Simulação de cobertura | 15 min |
| Síntese final e revisão da entrega | 10 min |
| **Total** | **90 min** |

Não é necessário implementar funções de distribuição do zero. Priorizem as contas essenciais e as interpretações; uma ou duas frases por pergunta são suficientes.

---

## Situação-problema

Uma equipe está avaliando uma plataforma de ensino. Ela quer estimar o tempo médio de resposta de uma funcionalidade, a proporção de estudantes satisfeitos e o tempo médio necessário para concluir uma tarefa.

Os estudos abaixo usam dados didáticos e amostras distintas. Admitam amostragem aleatória e observações independentes e identicamente distribuídas dentro de cada estudo. As populações são suficientemente grandes para dispensar a correção para população finita. Na pesquisa de satisfação, cada estudante fornece uma única resposta, classificada como satisfeito ou não satisfeito.

### Preparação em Python

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats
```

Nas Partes 1 a 3, organizem os intervalos em uma tabela:

| Estudo | Parâmetro e unidade | Método | Confiança | Estimativa pontual | Erro padrão | Valor crítico | Margem de erro | Limite inferior | Limite superior |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|

Lembrem-se: a margem de erro é **metade** da largura do intervalo. Usem os valores críticos sem arredondamento nos cálculos e arredondem apenas a apresentação dos resultados.

---

## Parte 1. Média, confiança e precisão

Uma amostra de $n=100$ operações apresentou tempo médio de resposta $\overline{x}=123$ ms. Um estudo prévio independente permite tratar o desvio padrão populacional como conhecido: $\sigma=18$ ms. Admitam que a aproximação normal da distribuição amostral da média é adequada neste estudo.

1. Identifiquem o parâmetro populacional e sua estimativa pontual. Calculem o erro padrão e construam intervalos de confiança para a média com níveis de **90%, 95% e 99%**. Registrem os três intervalos na tabela e interpretem o de 95% no contexto.
2. Comparem os centros, as margens de erro e as larguras dos intervalos. Aumentar o nível de confiança, mantendo os mesmos dados, torna a estimativa mais precisa? O intervalo de 95% descreve onde se encontram 95% dos tempos individuais? Justifiquem.
3. Planejem uma nova coleta com 95% de confiança e margem de erro de **no máximo 3 ms**, mantendo $\sigma=18$ ms. Calculem o tamanho amostral mínimo e confiram a margem de erro resultante. Repitam para **1,5 ms**. Qual é a relação entre reduzir a margem pela metade e o tamanho amostral antes do arredondamento?

### Dicas de Python

Para um nível de confiança $c=1-\alpha$, o valor crítico positivo é:

```python
z_critico = stats.norm.ppf((1 + c) / 2)
```

As fórmulas são:

$$
EP=\frac{\sigma}{\sqrt{n}},\qquad
E=z_{\text{crítico}}\,EP,\qquad
IC=[\overline{x}-E,\ \overline{x}+E].
$$

Para planejar a coleta:

$$
n_{\min}=\left\lceil\left(\frac{z_{\text{crítico}}\sigma}{E_{\text{alvo}}}\right)^2\right\rceil.
$$

- Usem `int(np.ceil(...))` para arredondar o tamanho amostral **para cima**.
- A margem de erro planejada não é uma garantia de que toda estimativa obtida ficará a essa distância da média verdadeira; ela faz parte de um procedimento com nível de confiança definido.

---

## Parte 2. Proporção e planejamento amostral

Em uma pesquisa com $n=240$ estudantes, **180** declararam estar satisfeitos com a plataforma.

4. Identifiquem o parâmetro $p$ e calculem sua estimativa $\widehat{p}$. Verifiquem a condição de pelo menos dez sucessos e dez falhas. Construam o intervalo normal de Wald de **95%** para $p$ e registrem-no na tabela. Apresentem os limites também em porcentagem e a margem de erro em **pontos percentuais**.
5. A equipe deseja realizar outra pesquisa com 95% de confiança e margem de erro de **3 pontos percentuais**. Calculem o tamanho amostral planejado em dois casos: usando $\widehat{p}=180/240$ como estimativa piloto e sem informação prévia, usando $p=0{,}5$. Expliquem por que a segunda escolha é conservadora e por que o planejamento com piloto depende da qualidade dessa estimativa.
6. Outra pesquisa observou apenas **2 estudantes insatisfeitos em 40 entrevistados**. Para estimar a proporção de insatisfeitos, a mesma aproximação de Wald seria adequada? Justifiquem pelas contagens e indiquem uma alternativa citada na nota de aula. Não é necessário calcular outro intervalo.

### Dicas de Python

$$
\widehat{p}=\frac{x}{n},\qquad
EP=\sqrt{\frac{\widehat{p}(1-\widehat{p})}{n}},\qquad
IC=\widehat{p}\pm z_{\text{crítico}}\,EP.
$$

Para o planejamento com uma estimativa piloto $p_{\text{pil}}$:

$$
n_{\min}=\left\lceil
\frac{z_{\text{crítico}}^2\,p_{\text{pil}}(1-p_{\text{pil}})}{E_{\text{alvo}}^2}
\right\rceil.
$$

- Usem `E_alvo = 0.03`, pois 3 pontos percentuais correspondem a 0,03 na escala de proporções.
- Sem piloto, substituam o produto $p(1-p)$ por $1/4$, seu valor máximo.
- A regra das contagens é uma condição prática para a aproximação, não uma garantia de cobertura nominal exata.

---

## Parte 3. Amostra pequena e distribuição t

Doze estudantes realizaram individualmente uma tarefa na plataforma. Os tempos, em minutos, foram:

```python
tempos = np.array([42, 45, 47, 48, 49, 50,
                   51, 52, 53, 54, 56, 59], dtype=float)
```

O desvio padrão populacional é desconhecido. O contexto da tarefa sugere uma população aproximadamente normal, mas a equipe deseja avaliar essa suposição com os dados disponíveis.

7. Façam um **Q-Q plot normal** e comentem se há sinais fortes de assimetria ou valores extremos. Um gráfico aproximadamente linear prova que a população é normal? Expliquem considerando o tamanho amostral.
8. Admitindo que a suposição de normalidade é razoável, calculem $\overline{x}$, o desvio padrão amostral $s$, o erro padrão e os graus de liberdade. Construam o intervalo t de **95%** para a média populacional e registrem-no na tabela. Confiram os limites com `stats.t.interval` e interpretem o resultado.
9. Calculem, apenas para comparação, a margem de erro obtida ao usar o valor crítico z de 95% com o **mesmo** erro padrão $s/\sqrt{n}$. Qual margem é maior? Expliquem por que a distribuição t tem caudas mais pesadas e por que o intervalo mais estreito não é automaticamente preferível.

### Dicas de Python

Para o diagnóstico:

```python
fig, ax = plt.subplots(figsize=(5, 4))
stats.probplot(tempos, dist="norm", plot=ax)
ax.set_title("Q-Q plot dos tempos de conclusão")
plt.tight_layout()
plt.show()
```

Para o intervalo:

$$
gl=n-1,\qquad EP=\frac{s}{\sqrt{n}},\qquad
IC=\overline{x}\pm t_{\text{crítico}}\,EP.
$$

- Usem `tempos.std(ddof=1)` para $s$ e `stats.t.ppf(0.975, df=n-1)` para o valor crítico.
- Para conferir, usem `stats.t.interval(confidence=0.95, df=n-1, loc=tempos.mean(), scale=erro_padrao)`.
- O resultado do procedimento t é exato sob observações i.i.d. normais; com normalidade aproximada, a cobertura também é aproximada.

---

## Parte 4. Simulação de cobertura

Na prática, a média verdadeira é desconhecida. Em uma simulação, podemos conhecê-la e verificar quantos intervalos a contêm.

Considerem uma população normal com $\mu=50$ minutos e $\sigma=6$ minutos. Para cada $n\in\{8,40\}$, gerem $R=5\,000$ amostras e construam intervalos nominais de **95%** por três métodos:

- **z com sigma conhecido:** usa $\sigma/\sqrt{n}$ e o valor crítico normal;
- **t com sigma estimado:** usa $s/\sqrt{n}$ e o valor crítico t;
- **z com sigma estimado:** usa $s/\sqrt{n}$ e o valor crítico normal, permitindo avaliar essa aproximação.

Os métodos devem usar as **mesmas amostras** para cada tamanho $n$. Executem o código guiado abaixo:

```python
rng = np.random.default_rng(20260915)
mu, sigma = 50, 6
R = 5_000
z_critico = stats.norm.ppf(0.975)
linhas = []
intervalos_t = {}

for n in [8, 40]:
    amostras = rng.normal(loc=mu, scale=sigma, size=(R, n))
    medias = amostras.mean(axis=1)
    desvios = amostras.std(axis=1, ddof=1)
    t_critico = stats.t.ppf(0.975, df=n-1)
    margens = {
        "z com sigma conhecido": np.full(R, z_critico * sigma / np.sqrt(n)),
        "t com sigma estimado": t_critico * desvios / np.sqrt(n),
        "z com sigma estimado": z_critico * desvios / np.sqrt(n),
    }
    for metodo, erros in margens.items():
        inferiores = medias - erros
        superiores = medias + erros
        contem_mu = (inferiores <= mu) & (mu <= superiores)
        linhas.append({
            "n": n, "método": metodo,
            "cobertura_empirica": contem_mu.mean(),
            "largura_media": (superiores - inferiores).mean(),
        })
        if metodo == "t com sigma estimado":
            intervalos_t[n] = (inferiores, superiores, contem_mu)

tabela_cobertura = pd.DataFrame(linhas)
tabela_cobertura
```

10. Comparem as coberturas com 95%. Para $n=8$, qual é o efeito de usar z com $s$ em lugar de t com $s$? Como essa diferença se comporta para $n=40$? Comparem também as larguras médias nos dois tamanhos amostrais.
11. Façam um gráfico dos **primeiros 40 intervalos t para $n=8$**, com uma linha vertical em $\mu=50$. Destaquem os intervalos que não contêm $\mu$. Expliquem o que varia de amostra para amostra e o que permanece fixo. É obrigatório que exatamente 38 desses 40 intervalos contenham a média verdadeira? Justifiquem.

### Dicas para o gráfico

- Recuperem os vetores com `inferiores, superiores, contem_mu = intervalos_t[8]`.
- Para cada índice `i` entre 0 e 39, usem `ax.hlines(i, inferiores[i], superiores[i], color=...)`.
- Escolham a cor pela condição `contem_mu[i]`, por exemplo cinza quando contém e vermelho quando não contém.
- Usem `ax.axvline(mu, linestyle="--", color="black")`, indiquem as unidades no eixo horizontal e identifiquem as amostras no eixo vertical.

---

## Síntese final

Em um único parágrafo, corrijam as três afirmações abaixo, usando o que observaram no laboratório:

1. “O intervalo já calculado tem 95% de probabilidade de conter a média verdadeira.”
2. “Para obter mais confiança e mais precisão, basta aumentar o nível de confiança.”
3. “Sempre devemos escolher o intervalo mais estreito, independentemente do método e das suposições.”

Antes de entregar, confiram se o notebook executa do início ao fim e contém as **cinco linhas** da tabela de intervalos das Partes 1 a 3, os quatro tamanhos amostrais planejados (dois para média e dois para proporção), as **seis linhas** da tabela de cobertura, o Q-Q plot, o gráfico dos intervalos e as interpretações solicitadas.
