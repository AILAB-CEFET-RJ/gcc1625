# 03 Regra 68-95-99,7 (Regra Empírica)

Notebook prático (código): `../03_regra_ouro.ipynb`

## Ideia central

Para variáveis com distribuição normal, uma grande fração dos valores fica concentrada em torno da média.

A regra empírica afirma que, aproximadamente:

- 68% dos dados estão no intervalo $[\mu-\sigma,\mu+\sigma]$;
- 95% dos dados estão no intervalo $[\mu-2\sigma,\mu+2\sigma]$;
- 99,7% dos dados estão no intervalo $[\mu-3\sigma,\mu+3\sigma]$.

## Interpretação

- Quanto mais distante da média (em unidades de desvio padrão), menor a probabilidade de observar valores.
- A regra é específica para distribuições aproximadamente normais.
- Em aplicações práticas, ela é útil para análise de dispersão, detecção inicial de outliers e interpretação rápida de variabilidade.

## Ligação com padronização

Se $X\sim\mathcal{N}(\mu,\sigma^2)$, a variável padronizada

$$
Z=\frac{X-\mu}{\sigma}
$$

segue normal padrão $\mathcal{N}(0,1)$. Assim, os percentuais acima são áreas sob a curva normal padrão entre $-1$ e $1$, $-2$ e $2$, e $-3$ e $3$.
