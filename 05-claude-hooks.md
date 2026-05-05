# Hooks — Automações no Claude Code

Hooks são scripts que executam automaticamente em resposta a ações do Claude. Permitem adicionar guardrails, notificações, validações e automações sem intervenção manual.

---

## 1. Tipos de hooks

| Hook | Quando executa |
|---|---|
| `PreToolUse` | Antes de o Claude usar uma ferramenta (pode bloquear) |
| `PostToolUse` | Após o Claude usar uma ferramenta |
| `Notification` | Quando o Claude envia uma notificação ao usuário |
| `Stop` | Quando o Claude termina uma resposta |

---

## 2. Estrutura de configuração

Hooks são configurados em `settings.json` (global ou por projeto):

```json
{
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
    ],
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "bash ~/.claude/hooks/notify-edit.sh"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "*",
        "hooks": [
          {
            "type": "command",
            "command": "bash ~/.claude/hooks/session-summary.sh"
          }
        ]
      }
    ]
  }
}
```

O `matcher` aceita nome da ferramenta (`Bash`, `Edit`, `Write`, `Read`) ou padrões com `|` para múltiplos.

---

## 3. Criar o diretório de hooks

```bash
mkdir -p ~/.claude/hooks
```

---

## 4. Hook: bloquear comandos destrutivos

Crie `~/.claude/hooks/check-destructive.sh`:

```bash
#!/bin/bash
# Bloqueia rm -rf em caminhos perigosos e força confirmação

input=$(cat)
command=$(echo "$input" | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('tool_input',{}).get('command',''))" 2>/dev/null)

DANGEROUS_PATTERNS=(
  "rm -rf /"
  "rm -rf ~"
  "rm -rf \$HOME"
  "sudo rm"
  "git push --force"
  "git reset --hard"
  "DROP TABLE"
  "DROP DATABASE"
)

for pattern in "${DANGEROUS_PATTERNS[@]}"; do
  if echo "$command" | grep -qi "$pattern"; then
    echo "BLOCKED: comando potencialmente destrutivo detectado: $pattern" >&2
    echo '{"decision": "block", "reason": "Comando destrutivo requer confirmação manual"}' 
    exit 0
  fi
done

echo '{"decision": "approve"}'
```

```bash
chmod +x ~/.claude/hooks/check-destructive.sh
```

---

## 5. Hook: notificação sonora ao terminar

Útil para tarefas longas — emite um beep quando o Claude termina:

Crie `~/.claude/hooks/session-summary.sh`:

```bash
#!/bin/bash
# Notifica via terminal bell quando Claude termina uma resposta
printf '\a'
```

```bash
chmod +x ~/.claude/hooks/session-summary.sh
```

Configure no `settings.json`:

```json
"Stop": [
  {
    "matcher": "*",
    "hooks": [{"type": "command", "command": "bash ~/.claude/hooks/session-summary.sh"}]
  }
]
```

---

## 6. Hook: auto-lint após edição (Python)

Crie `~/.claude/hooks/lint-python.sh`:

```bash
#!/bin/bash
# Roda ruff em arquivos .py após edição
input=$(cat)
file=$(echo "$input" | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('tool_input',{}).get('file_path',''))" 2>/dev/null)

if [[ "$file" == *.py ]]; then
  if command -v ruff &>/dev/null; then
    ruff check "$file" --fix --silent 2>/dev/null
  fi
fi
echo '{"decision": "approve"}'
```

```bash
chmod +x ~/.claude/hooks/lint-python.sh
```

---

## 7. Verificar hooks configurados

Dentro de uma sessão Claude:

```
/hooks
```

Mostra todos os hooks ativos com matchers e comandos.

---

## 8. Dicas da comunidade

- Hooks devem ser **rápidos** — operações lentas bloqueiam o fluxo do Claude
- Um hook `PreToolUse` que retorna código de saída não-zero **cancela** a operação
- Teste os hooks manualmente antes de ativar: `echo '{"tool_input":{"command":"rm -rf /"}}' | bash ~/.claude/hooks/check-destructive.sh`
- Mantenha os scripts em `~/.claude/hooks/` versionados — faça backup junto com este repositório

---

## Próximo passo

Conecte ferramentas externas via [06-mcp-servers.md](06-mcp-servers.md).
