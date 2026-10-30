---
titulo: Menteklein
categoria: projeto
tags: [projeto, segundo-cerebro, obsidian]
projeto: menteklein
data_criacao: 2026-10-10
data_atualizacao: 2026-10-30
---

# Menteklein

Repositório que versiona o Segundo Cérebro: um vault Obsidian em `segundo-cerebro/` mantido por agentes de IA, que leem o índice antes de cada tarefa e registram o que aprenderam depois.

## Estado atual

- Estrutura do vault criada: oito categorias, cada uma com seu `_Indice`, mais `Templates/` e `Inbox/`.
- Protocolo em `AGENTS.md`, importado pelo `CLAUDE.md` do repo e, em cada computador, pelo `~/.claude/CLAUDE.md` (ver `INSTALACAO.md`).
- `PROMPT.md` guarda a versão genérica do prompt, para as instruções globais de outras ferramentas.
- `main` criada como commit vazio e PR aberto com a estrutura inicial; ver [[PR em Repositorio sem Branch Base]].

## Próximos passos

- Tornar o repositório privado no GitHub: hoje ele é público.
- Instalar no computador pessoal e no da empresa seguindo o `INSTALACAO.md`.
- Depois do merge do PR, tornar `main` a branch padrão no GitHub.
- Alimentar o vault: colar conversas em `Inbox/` ou deixar os agentes registrarem ao fim das tarefas.

## Relacionadas

- [[Vault Versionado no Repositorio]]
- [[PR em Repositorio sem Branch Base]]
- [[Ambiente de Trabalho]]
