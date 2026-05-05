# Status Line — Customização Visual do Claude Code

O Claude Code exibe uma linha de status no terminal durante as sessões. Ela pode ser customizada para mostrar informações úteis como modelo em uso, custo da sessão, branch atual e mais.

---

## 1. O que é a status line

É a linha de informação exibida no rodapé do terminal durante uma sessão interativa do Claude. Por padrão mostra o modelo e o contexto usado.

---

## 2. Configuração via settings.json

Adicione ao `~/.claude/settings.json`:

```json
{
  "statusBar": {
    "enabled": true,
    "components": ["model", "cost", "context", "git"]
  }
}
```

---

## 3. Script de status customizado

A comunidade compartilha scripts shell que enriquecem o prompt do Zsh com informações da sessão Claude. Adicione ao `~/.zshrc`:

```zsh
# Exibe modelo Claude e custo estimado no lado direito do prompt
claude_status() {
  if [[ -n "$CLAUDE_MODEL" ]]; then
    echo "%F{cyan}[${CLAUDE_MODEL}]%f"
  fi
}

RPROMPT='$(claude_status)'
```

---

## 4. Integração com Spaceship Prompt

Se você usa o Spaceship (configurado em [01-terminal-zsh.md](01-terminal-zsh.md)), adicione uma seção customizada ao `.zshrc`:

```zsh
# Seção customizada do Spaceship para Claude
SPACESHIP_CLAUDE_SHOW=true
SPACESHIP_CLAUDE_PREFIX=" "
SPACESHIP_CLAUDE_SUFFIX=""
SPACESHIP_CLAUDE_COLOR="cyan"

spaceship_claude() {
  [[ $SPACESHIP_CLAUDE_SHOW == false ]] && return
  
  # Verifica se há uma sessão Claude ativa pelo processo
  local claude_pid=$(pgrep -f "claude" 2>/dev/null | head -1)
  [[ -z "$claude_pid" ]] && return
  
  spaceship::section \
    --color "$SPACESHIP_CLAUDE_COLOR" \
    --prefix "$SPACESHIP_CLAUDE_PREFIX" \
    --suffix "$SPACESHIP_CLAUDE_SUFFIX" \
    "⚙ claude"
}

# Adicionar à ordem do prompt
SPACESHIP_PROMPT_ORDER=(
  time
  user
  dir
  git
  claude      # ← adicionar aqui
  line_sep
  char
)
```

---

## 5. Variáveis de ambiente úteis durante sessões

O Claude Code expõe algumas variáveis que você pode usar em scripts:

```bash
# Dentro de hooks ou scripts chamados pelo Claude
echo $CLAUDE_SESSION_ID     # ID da sessão atual
echo $CLAUDE_MODEL          # modelo em uso
```

---

## 6. Atalhos de teclado dentro de sessões

| Atalho | Ação |
|---|---|
| `Ctrl+C` | Interrompe a ação atual do Claude |
| `Ctrl+L` | Limpa a tela |
| `↑` / `↓` | Navega no histórico de prompts da sessão |
| `Shift+Tab` | Alterna entre modo auto e manual de aprovações |
| `Esc` | Cancela a edição atual |

Para customizar atalhos, edite `~/.claude/keybindings.json`:

```json
[
  {
    "key": "ctrl+shift+c",
    "command": "clear"
  },
  {
    "key": "ctrl+shift+r",
    "command": "resume"
  }
]
```

---

## 7. Configuração de tema

O tema afeta cores e contraste da interface. Configure no `settings.json`:

```json
{
  "theme": "dark"
}
```

Opções: `dark`, `light`, `auto` (segue o tema do terminal).

Para alternar dentro de uma sessão:

```
/config
```

Selecione `Theme` no menu interativo.

---

## Configuração completa

Com este guia você concluiu a configuração completa. Consulte o [GUIA.md](GUIA.md) para revisar qualquer etapa ou o [README.md](README.md) para uma visão geral do repositório.
