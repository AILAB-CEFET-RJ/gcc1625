# 03 Estimação Intervalar para Amostras Grandes

Notebook prático (código): `../03_estimacao_intervalar_amostras_grandes.ipynb`

## Escopo

Quando $n > 30$, usamos aproximações assintóticas (TLC) para construir intervalos de confiança (ICs) para:

- média populacional $\mu$;
- proporção populacional $p$.

## IC para a média populacional $\mu$

Com nível de confiança $(1-\alpha)$ e ponto crítico $z_{\alpha/2}$:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}
$$

Se $\sigma$ é desconhecido e $n$ é grande, usa-se $s$:

$$
\overline{x} \pm z_{\alpha/2}\cdot\frac{s}{\sqrt{n}}
$$

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

Regra prática comum: usar essa aproximação quando houver, na amostra, pelo menos 10 sucessos e 10 falhas.

## Confiabilidade vs precisão

- Maior nível de confiança => intervalo mais largo.
- Menor nível de confiança => intervalo mais estreito.

Para tamanho amostral fixo, há trade-off entre confiabilidade e precisão.

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

## Determinação do tamanho da amostra (detalhado)

Nesta seção, o objetivo é planejar o estudo antes da coleta, definindo um tamanho amostral mínimo que garanta:

- nível de confiança $(1-\alpha)$;
- margem de erro máxima $E$.

### Caso 1: parâmetro de interesse é $\mu$

Queremos atender a restrição:

$$
\Pr\left(\left|\overline{x}-\mu\right|\le E\right)\ge 1-\alpha
$$

Com padronização e uso da normal padrão:

$$
Z=\frac{\overline{x}-\mu}{\sigma/\sqrt{n}} \sim \mathcal{N}(0,1)
$$

obtemos:

$$
n=\left\lceil\frac{\sigma^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

Se $\sigma$ for desconhecido, usa-se estimativa de estudo piloto ($s$):

$$
n=\left\lceil\frac{s^2 z_{\alpha/2}^2}{E^2}\right\rceil
$$

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

Essa escolha pode superdimensionar a amostra quando $p$ real é próximo de 0 ou 1.

### Exemplos (planejamento amostral)

1. Exemplo com média:
- piloto com $s^2=16$, $E=0.5$, 95% de confiança ($z_{0.025}=1.96$)
- resultado:
$$
n=\left\lceil\frac{16\cdot(1.96)^2}{(0.5)^2}\right\rceil=245
$$

2. Exemplo com proporção:
- estimativa prévia $p\approx0.60$, $E=0.03$, 95% de confiança
- resultado aproximado:
$$
n=\left\lceil\frac{(1.96)^2(0.6)(0.4)}{(0.03)^2}\right\rceil\approx1024
$$

3. Leitura prática:
- reduzir $E$ aumenta fortemente $n$;
- aumentar o nível de confiança também aumenta $n$;
- em custos altos, amostra piloto tende a melhorar o planejamento.

4. Exemplo (proporção, inferência a partir de IC já publicado):
- foi reportado IC 95% para proporção de obesidade entre 22% e 24%;
- a margem de erro é $E=0.01$ (metade da largura 0.02);
- usando aproximação conservadora para 95%:
$$
n=\left\lceil\frac{(1.96)^2}{4(0.01)^2}\right\rceil
=\left\lceil 9604 \right\rceil
=9604
$$
- interpretação: para garantir erro de 1 p.p. sem estimativa prévia de $p$, o tamanho amostral necessário é da ordem de 9.6 mil indivíduos.

5. Exemplo (média, renda com $\sigma$ conhecido):
- deseja-se erro máximo de R\$ 500, com 95% de confiança e $\sigma=6250$;
$$
n=\left\lceil\frac{(6250)^2(1.96)^2}{(500)^2}\right\rceil
=\left\lceil 600.25 \right\rceil
=601
$$
- se a margem de erro for relaxada para R\$ 1000:
$$
n=\left\lceil\frac{(6250)^2(1.96)^2}{(1000)^2}\right\rceil
=\left\lceil 150.06 \right\rceil
=151
$$
- leitura: dobrar $E$ reduz o tamanho amostral aproximadamente por um fator de 4.
