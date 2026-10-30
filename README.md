# menteklein

Segundo Cérebro versionado em Git: um vault Obsidian que agentes de IA (Claude Code, Codex, Cursor…) consultam antes de cada tarefa e alimentam ao final dela.

## O que tem aqui

| Caminho            | Para quê                                                                 |
|--------------------|--------------------------------------------------------------------------|
| `AGENTS.md`        | Protocolo que os agentes seguem, em qualquer projeto — fonte única.      |
| `CLAUDE.md`        | Importa `AGENTS.md` para o Claude Code dentro deste repo.                 |
| `INSTALACAO.md`    | Como ligar o vault ao Claude Code de cada computador.                     |
| `PROMPT.md`        | Versão genérica do prompt (com `CAMINHO_DO_VAULT`) para outras ferramentas. |
| `segundo-cerebro/` | O vault: índices, categorias, templates e Inbox.                         |

## Como usar

1. **Instale em cada computador** seguindo o [`INSTALACAO.md`](INSTALACAO.md). A partir daí, em qualquer projeto, o agente atualiza o vault, lê o `_INDEX.md` antes da tarefa e, ao terminar, registra o que aprendeu e faz o push.
2. **Processe conversas antigas.** Salve a conversa como `.md` em `segundo-cerebro/Inbox/`. Na sessão seguinte o agente extrai as notas e move o arquivo para `Inbox/processados/`.
3. **Navegue no Obsidian.** Abra `~/menteklein/segundo-cerebro/` como vault. Para usar os templates, aponte *Configurações → Templates → Local da pasta de templates* para `Templates`. O `_DASHBOARD.md` usa o plugin Dataview, opcional.
4. **Outras ferramentas** (Cursor, Windsurf, Cline…): cole o bloco de `PROMPT.md` nas instruções delas, trocando `CAMINHO_DO_VAULT` por `~/menteklein/segundo-cerebro/`.

## Regras do vault

- Português brasileiro, nomes de arquivo sem acento.
- Atualizar nota existente em vez de duplicar.
- Nada de dados sensíveis: senhas, chaves de API, tokens, CPF/CNPJ, dados bancários.
