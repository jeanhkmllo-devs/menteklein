---
titulo: Vault Versionado no Repositório
categoria: decisao
tags: [decisao, segundo-cerebro, git]
projeto: menteklein
data_criacao: 2026-10-10
data_atualizacao: 2026-10-30
---

# Vault Versionado no Repositório

## Contexto

O protocolo do Segundo Cérebro foi pensado para um vault local, apontado por caminho absoluto nas instruções globais da ferramenta. Aqui ele vive num repositório Git, para que agentes em ambientes efêmeros (nuvem, Codex) também consigam ler e escrever nele.

## Decisão

- Vault em `segundo-cerebro/`, caminho relativo à raiz, sem acento nem espaço: evita escape no shell e diferenças de normalização Unicode entre sistemas (macOS grava nomes em NFD).
- `AGENTS.md` é a fonte única do protocolo; `CLAUDE.md` apenas o importa com `@AGENTS.md`.
- `PROMPT.md` mantém a versão genérica, com `CAMINHO_DO_VAULT`, para quem quiser usar o vault a partir de outros projetos.
- As notas registradas entram no commit da própria tarefa: sem commit, o que o agente aprendeu some quando o ambiente é descartado.
- **Uso em todos os projetos (2026-10-30):** clone sempre em `~/menteklein`, e o `~/.claude/CLAUDE.md` de cada computador importa `@~/menteklein/AGENTS.md`. O protocolo chega a qualquer projeto e se atualiza com um `git pull`, sem cópia colada.
- **Sincronização:** um hook `SessionStart` faz `pull` ao abrir a sessão. Ao fim da tarefa, o agente faz um commit separado só com o vault e dá push. Passo a passo em `INSTALACAO.md`.

## Alternativas consideradas

- Vault na raiz do repositório: o Obsidian exibiria `README.md` e `AGENTS.md` como notas, misturando configuração com conhecimento.
- Protocolo duplicado em `CLAUDE.md` e `AGENTS.md`: as duas cópias divergiriam com o tempo.
- Colar o `PROMPT.md` no `~/.claude/CLAUDE.md` de cada computador: três cópias para manter, e cada máquina com um caminho diferente.
- Confiar só no agente para o `pull`: se ele esquecer, trabalha com notas velhas. O hook garante o `pull`; a instrução no protocolo fica como reserva.

## Consequências

- Ferramentas que não leem `AGENTS.md` (Windsurf, Cline) precisam de um arquivo próprio apontando para ele.
- O histórico do Git passa a ser o histórico das notas.

## Relacionadas

- [[Menteklein]]
- [[Ambiente de Trabalho]]
