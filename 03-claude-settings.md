# Configuração Global — settings.json

O arquivo `~/.claude/settings.json` controla o comportamento global do Claude Code: permissões, modelo padrão, aparência e automações.

---

## 1. Localização

```bash
~/.claude/settings.json          # configuração do usuário (global)
.claude/settings.json            # configuração do projeto (por repositório)
.claude/settings.local.json      # configuração local do projeto (não versionar)
```

As configurações de projeto sobrescrevem as globais. Use o arquivo do usuário para preferências pessoais e o do projeto para regras específicas do time.

---

## 2. Template recomendado

Crie ou substitua `~/.claude/settings.json`:

```json
{
  "model": "claude-opus-4-5",
  "theme": "dark",
  "cleanupPeriodDays": 30,
  "autoUpdaterStatus": "enabled",

  "permissions": {
    "allow": [
      "Bash(git:*)",
      "Bash(npm:*)",
      "Bash(python3:*)",
      "Bash(uv:*)",
      "Bash(ls:*)",
      "Bash(cat:*)",
      "Bash(grep:*)",
      "Bash(find:*)",
      "Bash(mkdir:*)",
      "Bash(cp:*)",
      "Bash(mv:*)",
      "Bash(touch:*)",
      "Read(*)",
      "Edit(*)",
      "Write(*)"
    ],
    "deny": [
      "Bash(rm -rf /*)",
      "Bash(sudo rm:*)",
      "Bash(git push --force:*)"
    ]
  },

  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "bash ~/.claude/hooks/check-destructive.sh"
          }
        ]
      }
    ]
  }
}
```

---

## 3. Explicação dos campos

| Campo | Descrição |
|---|---|
| `model` | Modelo padrão. Opções: `claude-opus-4-5`, `claude-sonnet-4-5`, `claude-haiku-4-5` |
| `theme` | Tema da interface: `dark`, `light`, `auto` |
| `cleanupPeriodDays` | Dias para manter conversas salvas (0 = nunca apagar) |
| `autoUpdaterStatus` | `enabled` atualiza automaticamente, `disabled` desabilita |
| `permissions.allow` | Comandos/ferramentas que nunca pedem aprovação |
| `permissions.deny` | Comandos sempre bloqueados, independente de aprovação |
| `hooks` | Automações — ver [05-claude-hooks.md](05-claude-hooks.md) |

---

## 4. Permissões por padrão inteligente

Em vez de aprovar tudo manualmente, a comunidade recomenda liberar ferramentas **read-only** e operações git comuns, e bloquear apenas operações destrutivas:

```json
"permissions": {
  "allow": [
    "Bash(git status:*)",
    "Bash(git diff:*)",
    "Bash(git log:*)",
    "Bash(git add:*)",
    "Bash(git commit:*)",
    "Read(*)"
  ],
  "deny": [
    "Bash(rm -rf:*)",
    "Bash(git push --force:*)",
    "Bash(git reset --hard:*)"
  ]
}
```

> Use `/fewer-permission-prompts` dentro de uma sessão Claude para gerar automaticamente uma lista de permissões baseada no que você aprovou nas últimas sessões.

---

## 5. Configuração por projeto

Dentro de qualquer repositório, crie `.claude/settings.json` para regras específicas:

```json
{
  "permissions": {
    "allow": [
      "Bash(pytest:*)",
      "Bash(make:*)"
    ]
  }
}
```

Este arquivo deve ser versionado junto com o projeto para que toda a equipe herde as mesmas regras.

---

## 6. Verificar configuração ativa

```bash
claude /config    # abre menu interativo de configuração
```

---

## Próximo passo

Defina suas instruções pessoais em [04-claude-md-global.md](04-claude-md-global.md).
