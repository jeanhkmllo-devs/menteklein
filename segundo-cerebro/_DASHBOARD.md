# Painel

Atalhos do vault. A navegação funciona sem plugins; os blocos `dataview` só renderizam com o plugin Dataview instalado (opcional).

## Navegação

- [[_INDEX]] — Índice geral
- [[_Indice Inbox]] — Conversas a processar
- [[_Indice Projetos]] · [[_Indice Decisoes]] · [[_Indice Stack]] · [[_Indice Padroes]]
- [[_Indice Preferencias]] · [[_Indice Solucoes]] · [[_Indice Snippets]] · [[_Indice Aprendizados]]

## Atualizadas recentemente

```dataview
TABLE categoria, projeto, data_atualizacao
FROM -"Templates" AND -"Inbox"
WHERE categoria AND !startswith(file.name, "_")
SORT data_atualizacao DESC
LIMIT 15
```

## Notas por categoria

```dataview
TABLE WITHOUT ID key AS Categoria, length(rows) AS Notas
FROM -"Templates" AND -"Inbox"
WHERE categoria AND !startswith(file.name, "_")
GROUP BY categoria
```
