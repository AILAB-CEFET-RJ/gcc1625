# Trabalho Prático em Grupo: Testes de Hipóteses e ANOVA

## Organização da atividade

- Formem grupos de 3 a 4 alunos.
- Tempo total sugerido: 1h50min.
- A atividade deve ser resolvida com justificativas, contas essenciais e interpretação dos resultados.
- Sempre que possível, apresentem também a solução em Python usando `scipy.stats`.
- Adotem nível de significância `\(\alpha = 0{,}05\)`.

## Objetivos

Ao final da atividade, o grupo deve ser capaz de:

- formular corretamente `H0` e `Ha`;
- escolher o teste adequado para cada situação;
- calcular e interpretar estatística de teste e p-valor;
- distinguir testes t para uma amostra, pareado e duas amostras independentes;
- aplicar ANOVA de uma via e interpretar a necessidade de um teste post-hoc.

## Entrega

Entreguem um único arquivo por grupo contendo:

- identificação dos integrantes;
- respostas dos itens;
- contas principais;
- interpretação contextualizada dos resultados;
- código Python usado, se houver.

## Roteiro sugerido de tempo

- Parte 1: 20 min
- Parte 2: 35 min
- Parte 3: 45 min
- Fechamento e revisão: 10 min

---

## Parte 1. Escolha do teste e formulação das hipóteses

Para cada situação abaixo:

1. identifique qual teste seria mais adequado;
2. escreva `H0` e `Ha`;
3. diga se o teste é unicaudal à esquerda, unicaudal à direita ou bicaudal;
4. justifique brevemente sua escolha.

### Item 1

Uma empresa afirma que o tempo médio de resposta de seu sistema é de **no máximo 120 ms**. Um analista suspeita que, após uma atualização, o tempo médio tenha aumentado.

### Item 2

Um professor quer verificar se um curso de reforço alterou o desempenho dos mesmos 12 alunos. Cada aluno realizou uma prova antes e outra depois do curso.

### Item 3

Uma pesquisadora deseja comparar a média de horas de sono de estudantes distribuídos em **três** grupos, conforme o nível de uso de redes sociais: baixo, médio e alto.

### Item 4

Uma fábrica informa que o peso médio de suas embalagens é **500 g**. Um fiscal quer verificar se o peso médio está diferente desse valor, para mais ou para menos.

---

## Parte 2. Teste t pareado

Um professor aplicou um minicurso de programação e deseja verificar se houve melhora nas notas dos alunos. As notas dos mesmos 10 estudantes, antes e depois do minicurso, estão na tabela a seguir.

| Aluno | Antes | Depois |
|---|---:|---:|
| 1 | 58 | 62 |
| 2 | 60 | 63 |
| 3 | 55 | 61 |
| 4 | 62 | 66 |
| 5 | 64 | 67 |
| 6 | 59 | 60 |
| 7 | 61 | 65 |
| 8 | 57 | 60 |
| 9 | 63 | 66 |
| 10 | 56 | 59 |

Considere que o interesse é verificar se, em média, o minicurso **aumentou** as notas.

### Item 5

Explique por que o teste t **pareado** é mais adequado do que o teste t para duas amostras independentes.

### Item 6

Defina as diferenças `di` de modo consistente com a hipótese de melhora e calcule:

- as diferenças individuais;
- a média das diferenças `d̄`;
- o desvio padrão amostral das diferenças `sd`.

### Item 7

Calcule a estatística de teste t e os graus de liberdade.

### Item 8

Com base no p-valor, conclua o teste ao nível de 5%. Escreva a conclusão no contexto do problema.

### Item 9

Implemente o teste em Python usando `scipy.stats.ttest_rel`. Se necessário, ajuste o p-valor bilateral para o caso unicaudal.

### Item 10

Suponha que o grupo tenha obtido um resultado **não significativo**. Isso permitiria concluir que o minicurso “não funciona”? Explique.

---

## Parte 3. ANOVA de uma via

Uma professora quer investigar se três métodos de estudo produzem desempenhos médios diferentes em uma avaliação. Foram observadas as seguintes notas:

- Método A: `68, 72, 70, 65, 74`
- Método B: `75, 78, 80, 77, 76`
- Método C: `69, 71, 68, 70, 72`

### Item 11

Identifique:

- a variável independente e seus níveis;
- a variável dependente;
- as hipóteses `H0` e `Ha` da ANOVA.

### Item 12

Calcule:

- a média de cada grupo;
- a média global.

### Item 13

Calcule manualmente:

- a variabilidade entre grupos;
- a variabilidade dentro dos grupos;
- a estatística `F`;
- os graus de liberdade do numerador e do denominador.

### Item 14

Com base no valor de `F`, no p-valor e em `\(\alpha = 0{,}05\)`, conclua o teste. A conclusão da ANOVA permite afirmar que **todos** os métodos diferem entre si? Explique.

### Item 15

Implemente a ANOVA em Python usando `scipy.stats.f_oneway`.

### Item 16

Se a ANOVA for significativa, compare os pares de médias:

- Método A vs. Método B
- Método A vs. Método C
- Método B vs. Método C

Não é necessário aplicar formalmente o teste de Tukey à mão. Basta discutir, com base nas médias observadas, quais comparações parecem mais plausíveis de apresentar diferença.

### Item 17

Explique por que, após uma ANOVA significativa, não é adequado simplesmente fazer vários testes t sem qualquer cuidado adicional.

---

## Desafio final

### Item 18

Responda em poucas linhas:

- Qual é a principal diferença entre “não rejeitar `H0`” e “aceitar `H0`”?
- Por que um p-valor pequeno não mede o tamanho do efeito?
- Em que situação prática a ANOVA é preferível a vários testes t?

---

