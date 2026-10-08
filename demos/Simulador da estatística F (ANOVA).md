## Componente da demo

- **Painel principal:** três grupos de pontos arrastáveis, como na figura da nota. Cada grupo tem uma marca vermelha de média, arrastável para deslocar o grupo inteiro. A linha azul tracejada é a média global.
- **Desvios desenhados:** em laranja, o desvio de cada ponto até a média do seu grupo (o que forma SQ_dentro). Em azul, o desvio da média do grupo até a média global (o que forma SQ_entre). Cada tipo pode ser ligado ou desligado.
- **Slider de dispersão:** contrai ou expande os pontos em torno das médias, sem mexer nelas. Com ele o aluno vê F cair quando a variação dentro dos grupos aumenta, mesmo com as médias fixas.
- **Painel de resultados:**
  - F em destaque, com a decisão e o p-valor.
  - Barras de QM_entre e QM_dentro na mesma escala.
  - Tabela ANOVA completa (SQ, GL, QM e F).
  - Curva F(d₁, d₂) com F_obs, o F crítico para α = 0,05 e a cauda direita sombreada.
- **Presets:** exemplo da nota, F ≈ 1 e F grande. Clique duplo numa linha adiciona um ponto. Clique direito em um ponto o remove, com mínimo de 2 por grupo.

## Roteiro de uso

1. Abra o exemplo da nota e confira os números da tabela ANOVA com o cálculo feito à mão.
2. Arraste uma média até F ≈ 1 e peça ao aluno que preveja o que acontece com as barras.
3. Com o slider, aumente a dispersão sem mexer nas médias. É o caso da Pergunta (a) da nota: médias parecidas e muita variação interna.
4. Reduza a dispersão: F sobe, p cai e a área sombreada some.

## Limitações

- O número de grupos fica fixo em 3, então d₁ = 2 o tempo todo. Só d₂ muda, com o número de pontos.
- O eixo vai de 0 a 10.
- Se todos os pontos de cada grupo coincidirem com a média do grupo (QM_dentro = 0), F aparece como ∞.