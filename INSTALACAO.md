# Instalação nos seus computadores

Faça isto **uma vez em cada computador** (o pessoal e o da empresa). Depois, toda sessão do Claude Code, em qualquer projeto, lê e alimenta o mesmo vault, e os dois computadores ficam em dia pelo GitHub.

```
Computador pessoal  ⇄  GitHub (menteklein)  ⇄  Computador da empresa

pull quando a sessão abre · commit + push quando a tarefa termina
```

## Antes de começar

1. **Deixe o repositório privado.** Hoje ele é público: tudo que o agente registrar (preferências, projetos, decisões) fica visível para qualquer pessoa. No GitHub: *menteklein → Settings → General → Danger Zone → Change visibility → Private*.
2. **No computador da empresa**, confira se a política da empresa permite usar uma conta pessoal do GitHub e guardar anotações de trabalho fora dela. O protocolo já manda registrar o trabalho da empresa só de forma genérica, mas a decisão de usar ali é sua.
3. Tenha o `git` instalado e permissão de push no repositório (`gh auth login` ou uma chave SSH).

## Instalar

Abra o Claude Code em qualquer pasta do computador e cole:

````text
Instale o Segundo Cérebro neste computador. Siga os passos e me mostre o resultado de cada um:

1. Se ~/menteklein não existir, clone https://github.com/jeanhkmllo-devs/menteklein.git nesse caminho. Se existir, rode git -C ~/menteklein pull.
2. Mostre o resultado de git -C ~/menteklein config user.email e pergunte se é o e-mail que eu quero nos commits do vault. Se não for, configure o que eu disser só nesse repositório.
3. No fim de ~/.claude/CLAUDE.md (crie se não existir, sem apagar nada do que já tem), adicione este bloco, se ele ainda não estiver lá:

   # Segundo Cérebro
   Vault pessoal em `~/menteklein/segundo-cerebro/`. Siga o protocolo abaixo em todas as sessões, em qualquer projeto.

   @~/menteklein/AGENTS.md

4. Em ~/.claude/settings.json (crie se não existir; mescle com o que já tem, sem remover nada), garanta:
   - permissions.additionalDirectories com o caminho absoluto de ~/menteklein
   - em permissions.allow: "Edit(~/menteklein/segundo-cerebro/**)", "Bash(git -C ~/menteklein pull *)", "Bash(git -C ~/menteklein add *)", "Bash(git -C ~/menteklein commit *)", "Bash(git -C ~/menteklein push *)"
   - um hook SessionStart, sem matcher, do tipo command, com timeout 20 e este comando:
     GIT_TERMINAL_PROMPT=0 git -C ~/menteklein pull --rebase --autostash -q >/dev/null 2>&1 || true
   Valide o JSON depois de salvar.
5. Rode git -C ~/menteklein push --dry-run e me diga se o push funciona.
````

## O que a instalação muda

| Onde                      | O que muda                                             | Para quê                                                                 |
|---------------------------|--------------------------------------------------------|--------------------------------------------------------------------------|
| `~/menteklein`            | Clone do repositório                                   | É o vault, sempre no mesmo caminho nos dois computadores.                |
| `~/.claude/CLAUDE.md`     | Bloco com `@~/menteklein/AGENTS.md`                    | Carrega o protocolo em todo projeto, sempre na versão mais nova do repo. |
| `~/.claude/settings.json` | `additionalDirectories` e regras em `permissions.allow` | Ler e editar o vault e rodar git nele sem pedir confirmação toda hora.   |
| `~/.claude/settings.json` | Hook `SessionStart`                                    | Puxar as notas do outro computador sempre que uma sessão abre.           |

Ao terminar uma tarefa, o próprio agente faz o commit e o push das notas (seção *Sincronização* do `AGENTS.md`).

### Instalação manual

Se preferir editar à mão, este é o trecho do `~/.claude/settings.json` (troque o caminho em `additionalDirectories` pelo absoluto da sua máquina e mescle com o que já existe):

```json
{
  "permissions": {
    "additionalDirectories": ["/Users/voce/menteklein"],
    "allow": [
      "Edit(~/menteklein/segundo-cerebro/**)",
      "Bash(git -C ~/menteklein pull *)",
      "Bash(git -C ~/menteklein add *)",
      "Bash(git -C ~/menteklein commit *)",
      "Bash(git -C ~/menteklein push *)"
    ]
  },
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "GIT_TERMINAL_PROMPT=0 git -C ~/menteklein pull --rebase --autostash -q >/dev/null 2>&1 || true",
            "timeout": 20
          }
        ]
      }
    ]
  }
}
```

## Como saber que está funcionando

1. **Leitura:** abra o Claude Code em qualquer projeto e pergunte *"o que o Segundo Cérebro sabe sobre mim?"*. Ele deve citar notas do vault.
2. **Escrita:** termine uma tarefa qualquer e rode `git -C ~/menteklein log -1`. Deve aparecer um commit `Segundo Cérebro: …`.
3. **Sincronia:** abra uma sessão no outro computador e peça para ver essa nota. O hook já terá puxado a nota.

## Desfazer

Apague o bloco *Segundo Cérebro* do `~/.claude/CLAUDE.md` e as entradas acima do `~/.claude/settings.json`. O clone em `~/menteklein` pode ficar ou ser apagado.
