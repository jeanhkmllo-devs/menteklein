# Segundo Cérebro — Protocolo Automático

OBRIGATÓRIO em TODAS as sessões que carregam este arquivo, em qualquer projeto.

## Onde fica

O vault é a pasta `segundo-cerebro/` do repositório **menteklein**:

- Sessão dentro do próprio menteklein: `./segundo-cerebro/`
- Sessão em qualquer outro projeto: `~/menteklein/segundo-cerebro/` (clone padrão, ver `INSTALACAO.md`)

## Estrutura de Pastas

```
segundo-cerebro/
├── _INDEX.md              ← Índice master (lido sempre antes de qualquer tarefa)
├── _DASHBOARD.md          ← Painel visual (opcional)
├── Templates/             ← Templates de notas
├── Inbox/                 ← Conversas coladas para processar
│   ├── _Indice Inbox.md
│   └── processados/       ← Conversas já processadas
├── Padroes/               ← Padrões de código recorrentes
├── Decisoes/              ← Decisões arquiteturais e trade-offs
├── Stack/                 ← Tecnologias, libs, configs
├── Projetos/              ← Contexto e estado dos projetos
├── Preferencias/          ← Como o usuário gosta de trabalhar
├── Solucoes/              ← Bugs resolvidos, workarounds
├── Snippets/              ← Código reutilizável
└── Aprendizados/          ← Lições e insights
```

Cada pasta de categoria tem seu `_Indice [Categoria].md` (ex: `Padroes/_Indice Padroes.md`).

## ANTES de qualquer tarefa

1. Atualize o vault com `git -C ~/menteklein pull --rebase --autostash` (dentro do menteklein: `git pull --rebase --autostash`). Se falhar, siga com a cópia local e avise em 1 frase
2. Leia `_INDEX.md` do Segundo Cérebro
3. Identifique categorias relevantes ao pedido do usuário
4. Leia os `_Indice [Categoria].md` dessas categorias
5. Se encontrar notas úteis, leia-as e use o contexto
6. Mencione brevemente (1 frase) se encontrou algo relevante

Faça silenciosamente — não narre "vou consultar o segundo cérebro".

## DEPOIS de concluir qualquer tarefa

Registre automaticamente o que foi aprendido. NÃO peça confirmação.

1. Verifique se já existe nota similar — atualize em vez de duplicar
2. Crie/atualize notas com este frontmatter (modelos em `Templates/`):

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
4. Atualize o `_Indice [Categoria].md` da categoria e o `_INDEX.md` master, no formato que eles já têm
5. Use português brasileiro
6. Nomes de arquivo sem acentos (ex: `PGlite como Postgres Local.md`)
7. Sincronize (seção abaixo)

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

## Sincronização

O mesmo vault é usado em mais de um computador. Sem push, o outro computador não vê as notas novas.

- **Sessão dentro do menteklein:** as mudanças em `segundo-cerebro/` entram no commit da própria tarefa.
- **Sessão em outro projeto:** commit separado, só com o vault, seguido de push:

  ```bash
  git -C ~/menteklein add segundo-cerebro
  git -C ~/menteklein commit -m "Segundo Cérebro: <resumo curto>"
  git -C ~/menteklein push
  ```

  Se o push for recusado, rode `git -C ~/menteklein pull --rebase` e tente de novo.
- Nunca misture: arquivos do vault não entram no commit do outro projeto, e arquivos do projeto não entram no vault.

## Inbox — Processamento de Conversas

Ao iniciar uma sessão, verifique se há arquivos novos em `Inbox/` (exceto `_Indice Inbox.md` e a pasta `processados/`).

Para cada arquivo encontrado:
1. Leia o conteúdo
2. Extraia padrões, decisões, soluções, stack, etc.
3. Crie notas nas categorias apropriadas
4. Mova o arquivo para `Inbox/processados/` com `git mv` (renomeie com prefixo da data: `YYYY-MM-DD - nome.md`)
5. Atualize os índices (inclusive a lista de processados em `_Indice Inbox.md`)

## Regras Importantes

- NUNCA importe dados sensíveis (senhas, chaves de API, tokens, CPF/CNPJ, dados bancários)
- Trabalho da empresa: registre só o aprendizado genérico — sem código proprietário, nomes de clientes, dados internos ou detalhes que identifiquem a empresa
- Sempre verifique duplicatas antes de criar nota nova
- Wikilinks `[[Nome da Nota]]` conectam o grafo de conhecimento
- O sistema funciona por leitura/escrita direta de arquivos .md — não precisa de API nem plugin
