---
titulo: PR em Repositório sem Branch Base
categoria: solucao
tags: [solucao, git, github]
projeto: menteklein
data_criacao: 2026-10-30
data_atualizacao: 2026-10-30
---

# PR em Repositório sem Branch Base

## Sintoma

O repositório nasceu vazio e o primeiro push foi de uma branch de trabalho. Não existe `main` no remoto, então não há base para abrir o PR — e criar `main` a partir da própria branch deixaria o PR sem diff.

## Causa

O GitHub só compara branches que compartilham histórico, e a branch base precisa existir antes do PR.

## Solução

1. Criar um commit raiz com árvore vazia e publicá-lo como `main`:

   ```bash
   ROOT=$(git commit-tree "$(git hash-object -t tree /dev/null)" -m "Commit inicial")
   git push origin "$ROOT:refs/heads/main"
   ```

2. Na branch de trabalho, juntar as histórias com merge (sem rebase nem force-push):

   ```bash
   git fetch origin main
   git merge --allow-unrelated-histories origin/main
   git push
   ```

3. Abrir o PR da branch para `main`.

`git merge -F -` não lê a mensagem do stdin: grave a mensagem num arquivo antes.

## Como verificar

- `git ls-remote origin` mostra `refs/heads/main`.
- `git diff --stat origin/main HEAD` lista todos os arquivos da branch.
- Depois do merge do PR, vale tornar `main` a branch padrão em *Settings → General*: a branch padrão continua sendo a primeira que recebeu push.

## Relacionadas

- [[Menteklein]]
