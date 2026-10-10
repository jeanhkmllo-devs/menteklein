---
titulo: Vault Versionado no Repositório
categoria: decisao
tags: [decisao, segundo-cerebro, git]
projeto: menteklein
data_criacao: 2026-10-10
data_atualizacao: 2026-10-10
---

# Vault Versionado no Repositório

## Contexto

O protocolo do Segundo Cérebro foi pensado para um vault local, apontado por caminho absoluto nas instruções globais da ferramenta. Aqui ele vive num repositório Git, para que agentes em ambientes efêmeros (nuvem, Codex) também consigam ler e escrever nele.

## Decisão

- Vault em `segundo-cerebro/`, caminho relativo à raiz, sem acento nem espaço: evita escape no shell e diferenças de normalização Unicode entre sistemas (macOS grava nomes em NFD).
- `AGENTS.md` é a fonte única do protocolo; `CLAUDE.md` apenas o importa com `@AGENTS.md`.
- `PROMPT.md` mantém a versão genérica, com `CAMINHO_DO_VAULT`, para quem quiser usar o vault a partir de outros projetos.
- As notas registradas entram no commit da própria tarefa: sem commit, o que o agente aprendeu some quando o ambiente é descartado.

## Alternativas consideradas

- Vault na raiz do repositório: o Obsidian exibiria `README.md` e `AGENTS.md` como notas, misturando configuração com conhecimento.
- Protocolo duplicado em `CLAUDE.md` e `AGENTS.md`: as duas cópias divergiriam com o tempo.

## Consequências

- Ferramentas que não leem `AGENTS.md` (Windsurf, Cline) precisam de um arquivo próprio apontando para ele.
- O histórico do Git passa a ser o histórico das notas.

## Relacionadas

- [[Menteklein]]
