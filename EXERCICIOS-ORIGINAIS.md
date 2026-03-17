# Exercícios Originais

Este arquivo consolida os exercícios que existiam nos notebooks de estimação intervalar antes da divisão do material em arquivos `.ipynb` e `.md`.

Referência histórica usada: commit `4c8dd65`.

## 03 Introdução à Estimação Intervalar

Arquivo original:

- `notebooks/03_estimacao_intervalar_intro.ipynb`

Bloco identificado no notebook:

- `## Exercícios sugeridos`

Exercícios:

1. Troque o nível de confiança de 95% para 90% e 99% e compare a largura dos intervalos.
2. Repita os experimentos com diferentes tamanhos amostrais (`n = 20, 50, 200, 1000`) e descreva o impacto na margem de erro.
3. Substitua a população normal por uma distribuição assimétrica (por exemplo, lognormal) e observe o comportamento da cobertura.
4. No experimento de cobertura, aumente o número de repetições e compare a estabilidade da estimativa de cobertura.
5. Faça uma simulação com variância populacional maior e analise como isso afeta os intervalos de confiança.

## 03 Estimação Intervalar para Amostras Grandes

Arquivo original:

- `notebooks/03_estimacao_intervalar_amostras_grandes.ipynb`

Bloco identificado no notebook:

- `### Exercício sugerido`

Exercício:

1. Altere `E` e o nível de confiança e observe a sensibilidade do tamanho amostral. Em especial, compare o efeito de reduzir `E` pela metade.

## 03 Estimação Intervalar para Amostras Pequenas

Arquivo original:

- `notebooks/03_estimacao_intervalar_amostras_pequenas.ipynb`

Bloco identificado no notebook:

- `## Parte B: exemplos rápidos com distribuição t`

Exercícios práticos correspondentes às células do notebook:

1. Encontre os percentis 2,5% e 97,5% da distribuição `t` com 5 graus de liberdade.
2. Calcule `P(T > 1.833)` para `T ~ t_9`.
3. Encontre o valor de `t_12` que delimita à direita uma área de 0,025.
4. Encontre o valor de `t_14` cuja cauda inferior tem área 0,01.

## Resumo

- Introdução: 5 exercícios.
- Amostras grandes: 1 exercício.
- Amostras pequenas: 4 exercícios práticos.
