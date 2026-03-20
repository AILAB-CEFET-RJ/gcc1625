# 02d Regra 68-95-99,7 (Regra Empírica)

## Ideia central

Para variáveis com distribuição normal, uma grande fração dos valores fica concentrada em torno da média.

Para a normal padrão, as áreas são aproximadamente:

- 68,27% dos dados estão no intervalo $[\mu-\sigma,\mu+\sigma]$;
- 95,45% dos dados estão no intervalo $[\mu-2\sigma,\mu+2\sigma]$;
- 99,73% dos dados estão no intervalo $[\mu-3\sigma,\mu+3\sigma]$.

Na prática, esses valores costumam ser arredondados para 68%-95%-99,7%, dando origem à chamada regra empírica.

## Interpretação

- Quanto mais distante da média (em unidades de desvio padrão), menor a probabilidade de observar valores.
- Em distribuições exatamente normais, os percentuais acima são uma boa aproximação numérica das áreas exatas.
- Em dados apenas aproximadamente normais, a regra funciona como guia rápido (não como garantia exata).
- Em aplicações práticas, ela é útil para análise de dispersão, detecção inicial de outliers e interpretação rápida de variabilidade.

## Ligação com padronização

Se $X\sim\mathcal{N}(\mu,\sigma^2)$, a variável padronizada

$$
Z=\frac{X-\mu}{\sigma}
$$

segue normal padrão $\mathcal{N}(0,1)$. Assim, os percentuais acima são áreas sob a curva normal padrão entre $-1$ e $1$, $-2$ e $2$, e $-3$ e $3$.

Para uma observação específica $x$, o valor
$$
z=\frac{x-\mu}{\sigma}
$$
é chamado de **escore-z**: ele indica quantos desvios-padrão $x$ está acima ($z>0$) ou abaixo ($z<0$) da média.

Essa leitura também é útil para interpretar escores-z: por exemplo, $|z|>2$ indica observações relativamente incomuns sob normalidade, e $|z|>3$ indica observações raras.

---

> 📝 **Pergunta 02d.1**
>
> A regra 68-95-99,7 é apresentada com percentuais arredondados.
>
> **(a)** Quais são os valores aproximados mais precisos listados no texto para os intervalos de $1\sigma$, $2\sigma$ e $3\sigma$?
>
> **(b)** Em uma frase, explique por que ainda usamos os valores arredondados na prática.

---

> 📝 **Pergunta 02d.2**
>
> Com base no texto, interprete os valores de escore-z abaixo:
>
> **(a)** $z=1{,}2$  
> **(b)** $z=2{,}4$  
> **(c)** $z=3{,}1$
>
> Para cada caso, classifique qualitativamente a observação como "comum", "incomum" ou "rara", justificando com a regra empírica.
