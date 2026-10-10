# menteklein

Segundo Cérebro versionado em Git: um vault Obsidian que agentes de IA (Claude Code, Codex, Cursor…) consultam antes de cada tarefa e alimentam ao final dela.

## O que tem aqui

| Caminho            | Para quê                                                                 |
|--------------------|--------------------------------------------------------------------------|
| `AGENTS.md`        | Protocolo que os agentes seguem neste repo — fonte única.                |
| `CLAUDE.md`        | Importa `AGENTS.md` para o Claude Code.                                   |
| `PROMPT.md`        | Versão genérica do prompt (com `CAMINHO_DO_VAULT`) para outras ferramentas. |
| `segundo-cerebro/` | O vault: índices, categorias, templates e Inbox.                         |

## Como usar

1. **Trabalhe com um agente neste repositório.** Ele lê `segundo-cerebro/_INDEX.md` antes da tarefa e registra o que aprendeu nas categorias ao terminar, incluindo as notas no commit.
2. **Processe conversas antigas.** Salve a conversa como `.md` em `segundo-cerebro/Inbox/`. Na sessão seguinte o agente extrai as notas e move o arquivo para `Inbox/processados/`.
3. **Navegue no Obsidian.** Abra `segundo-cerebro/` como vault. Para usar os templates, aponte *Configurações → Templates → Local da pasta de templates* para `Templates`. O `_DASHBOARD.md` usa o plugin Dataview, opcional.
4. **Use o vault em outros projetos.** Clone este repo, copie o bloco de `PROMPT.md` para as instruções globais da ferramenta (ex.: `~/.claude/CLAUDE.md`) e troque `CAMINHO_DO_VAULT` pelo caminho de `segundo-cerebro/` no clone. Lembre de commitar e dar push nas notas que forem criadas lá.

## Regras do vault

- Português brasileiro, nomes de arquivo sem acento.
- Atualizar nota existente em vez de duplicar.
- Nada de dados sensíveis: senhas, chaves de API, tokens, CPF/CNPJ, dados bancários.
