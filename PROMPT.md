# Segundo Cérebro — Prompt Replicável

> Cole este prompt nas instruções globais da sua ferramenta de IA (CLAUDE.md, AGENTS.md, Cursor Rules, etc.)
> Adapte apenas o `CAMINHO_DO_VAULT` para o seu ambiente.
>
> Neste repositório a versão já adaptada (caminho relativo `./segundo-cerebro/`) está em [`AGENTS.md`](AGENTS.md).
> Use este arquivo para levar o mesmo vault a outros projetos ou ferramentas, apontando `CAMINHO_DO_VAULT` para o clone local deste repositório.

---

## Instruções para a IA

````markdown
# Segundo Cérebro — Protocolo Automático

OBRIGATÓRIO em TODAS as sessões, independente do projeto.

Caminho do Segundo Cérebro:
`CAMINHO_DO_VAULT`

## Estrutura de Pastas

O vault tem esta estrutura fixa:

```
Segundo Cérebro/
├── _INDEX.md              ← Índice master (lido sempre antes de qualquer tarefa)
├── _DASHBOARD.md          ← Painel visual (opcional)
├── Templates/             ← Templates de notas
├── Inbox/                 ← Conversas coladas para processar
│   ├── _Indice Inbox.md
│   └── processados/       ← Conversas já processadas
├── Padroes/               ← Padrões de código recorrentes
│   └── _Indice Padroes.md
├── Decisoes/              ← Decisões arquiteturais e trade-offs
│   └── _Indice Decisoes.md
├── Stack/                 ← Tecnologias, libs, configs
│   └── _Indice Stack.md
├── Projetos/              ← Contexto e estado dos projetos
│   └── _Indice Projetos.md
├── Preferencias/          ← Como o usuário gosta de trabalhar
│   └── _Indice Preferencias.md
├── Solucoes/              ← Bugs resolvidos, workarounds
│   └── _Indice Solucoes.md
├── Snippets/              ← Código reutilizável
│   └── _Indice Snippets.md
└── Aprendizados/          ← Lições e insights
    └── _Indice Aprendizados.md
```

## ANTES de qualquer tarefa

1. Leia `_INDEX.md` do Segundo Cérebro
2. Identifique categorias relevantes ao pedido do usuário
3. Leia os `_Indice [Categoria].md` dessas categorias (ex: `Padroes/_Indice Padroes.md`)
4. Se encontrar notas úteis, leia-as e use o contexto
5. Mencione brevemente (1 frase) se encontrou algo relevante

Faça silenciosamente — não narre "vou consultar o segundo cérebro".

## DEPOIS de concluir qualquer tarefa

Registre automaticamente o que foi aprendido. NÃO peça confirmação.

1. Verifique se já existe nota similar — atualize em vez de duplicar
2. Crie/atualize notas com este frontmatter:

   ```yaml
   ---
   titulo: Nome descritivo
   categoria: padrao|decisao|stack|projeto|preferencia|solucao|snippet|aprendizado
   tags: [tag-categoria, tag-especifica]
   projeto: nome-do-projeto
   data_criacao: YYYY-MM-DD
   data_atualizacao: YYYY-MM-DD
   ---
   ```

3. Use `[[links]]` entre notas relacionadas (formato Obsidian wikilink)
4. Atualize o `_Indice [Categoria].md` da categoria e o `_INDEX.md` master
5. Use português brasileiro
6. Nomes de arquivo sem acentos (ex: `PGlite como Postgres Local.md`)

### Categorias

| Pasta          | Tag            | O que registrar                    |
|----------------|----------------|------------------------------------|
| Padroes/       | #padrao        | Padrões de código recorrentes      |
| Decisoes/      | #decisao       | Decisões arquiteturais, trade-offs |
| Stack/         | #stack         | Tecnologias, libs, configs         |
| Projetos/      | #projeto       | Contexto e estado dos projetos     |
| Preferencias/  | #preferencia   | Como o usuário gosta de trabalhar  |
| Solucoes/      | #solucao       | Bugs resolvidos, workarounds       |
| Snippets/      | #snippet       | Código reutilizável                |
| Aprendizados/  | #aprendizado   | Lições e insights                  |

Não narre o processo de registro — faça silenciosamente ao final.

## Inbox — Processamento de Conversas

Ao iniciar uma sessão, verifique se há arquivos novos em `Inbox/` (exceto `_Indice Inbox.md` e a pasta `processados/`).

Para cada arquivo encontrado:
1. Leia o conteúdo
2. Extraia padrões, decisões, soluções, stack, etc.
3. Crie notas nas categorias apropriadas
4. Mova o arquivo para `Inbox/processados/` (renomeie com prefixo da data: `YYYY-MM-DD - nome.md`)
5. Atualize os índices

## Formato do _INDEX.md

O índice master agrupa as notas por seção:

```markdown
# Índice Geral

## Projetos
- [[Nome do Projeto]] — Descrição curta.

## Decisões Arquiteturais
- [[Nome da Decisão]] — Resumo.

## Stack Recorrente
- [[Tecnologia]] — Onde é usada.

## Padrões
- [[Nome do Padrão]] — O que faz.

## Preferências do Usuário
- [[Preferência]] — Resumo.

## Soluções
- [[Nome da Solução]] — Problema que resolve.

## Snippets
- [[Nome do Snippet]] — Onde usar.

## Aprendizados
- [[Nome do Aprendizado]] — Insight.
```

## Formato dos _Indice [Categoria].md

Cada índice de categoria lista as notas da pasta com links:

```markdown
---
titulo: Índice de [Categoria]
categoria: [tipo]
data_atualizacao: YYYY-MM-DD
---

# [Título da Categoria]

Descrição breve. Tag: #[tag]

## Lista

- [[Nota 1]] — Descrição curta.
- [[Nota 2]] — Descrição curta.
```

## Regras Importantes

- NUNCA importe dados sensíveis (senhas, chaves de API, tokens, CPF/CNPJ, dados bancários)
- Sempre verifique duplicatas antes de criar nota nova
- Wikilinks `[[Nome da Nota]]` conectam o grafo de conhecimento
- O sistema funciona por leitura/escrita direta de arquivos .md — não precisa de API nem plugin
````

---

## Como usar em cada ferramenta

| Ferramenta       | Onde colar o prompt                                      |
|------------------|----------------------------------------------------------|
| **Claude Code**  | `~/.claude/CLAUDE.md` (instruções globais)               |
| **OpenAI Codex** | `AGENTS.md` na raiz do repositório                       |
| **Cursor**       | `.cursor/rules` ou `.cursorrules` na raiz do projeto     |
| **Windsurf**     | `.windsurfrules` na raiz do projeto                      |
| **Cline**        | `.clinerules` na raiz do projeto                         |
| **Aider**        | `.aider.conf.yml` → `read:` apontando para o arquivo     |
| **Continue**     | `.continue/config.json` → system prompt customizado      |

## Adaptações necessárias

1. **Trocar `CAMINHO_DO_VAULT`** pelo caminho real no seu sistema
2. **Se for repositório Git (Codex)**: o caminho é relativo à raiz do repo (ex: `./segundo-cerebro/`)
3. **Idioma**: trocar "português brasileiro" se quiser outro idioma
4. **Categorias**: adicionar ou remover conforme sua necessidade
