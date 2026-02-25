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
