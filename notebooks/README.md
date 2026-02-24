# Organizacao dos Materiais

Este diretorio contem notebooks de aulas de Inferencia Estatistica.
A proposta e separar:

- teoria em arquivos Markdown (`.md`)
- pratica em notebooks Jupyter (`.ipynb`)

## Estrutura Recomendada

```text
notebooks/
  conceitos/                 # teoria por tema
    01_conceitos_iniciais.md
    ...
  aulas/                     # notebooks de codigo
    01_conceitos_iniciais.ipynb
    ...
  templates/                 # modelos padrao para novos materiais
    conceito_template.md
    codigo_template.ipynb
  old_stuff/                 # material legado
  INDEX.md                   # mapeamento atual -> novo padrao
```

## Convencoes

- Manter o mesmo slug/base-name para teoria e codigo.
- Sempre incluir link cruzado:
  - no `.md`: link para o notebook correspondente
  - no notebook: celula inicial com link para o `.md`
- Evitar texto conceitual longo nos notebooks; manter foco em execucao e interpretacao dos resultados.

## Migracao Sugerida

1. Criar o `.md` do tema usando `templates/conceito_template.md`.
2. Copiar o notebook atual para `aulas/` sem mudar o conteudo de codigo.
3. Remover explicacoes teoricas extensas do notebook (deixar so o essencial para contexto).
4. Registrar o status de migracao no `INDEX.md`.

## Status

O `INDEX.md` ja foi criado com todos os notebooks atuais no nivel raiz de `notebooks/`.
Nenhum notebook foi movido automaticamente nesta etapa.
