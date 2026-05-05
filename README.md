# WSL Dev Setup

Guia completo para configurar um ambiente de desenvolvimento no WSL com terminal otimizado e Claude Code — pronto para replicar em qualquer máquina nova.

## O que este repositório cobre

| Arquivo | Tema |
|---|---|
| [GUIA.md](GUIA.md) | Índice central — visão geral e ordem recomendada |
| [01-terminal-zsh.md](01-terminal-zsh.md) | Zsh · Oh My Zsh · fzf · zoxide |
| [02-claude-instalacao.md](02-claude-instalacao.md) | Instalação e autenticação do Claude Code |
| [03-claude-settings.md](03-claude-settings.md) | Configuração global `~/.claude/settings.json` |
| [04-claude-md-global.md](04-claude-md-global.md) | Instruções pessoais `~/.claude/CLAUDE.md` |
| [05-claude-hooks.md](05-claude-hooks.md) | Automações com hooks |
| [06-mcp-servers.md](06-mcp-servers.md) | MCP Servers (GitHub, filesystem, etc.) |
| [07-claude-statusline.md](07-claude-statusline.md) | Status line customizada no terminal |

## Pré-requisitos

- WSL2 com Ubuntu 22.04+
- Windows Terminal
- Node.js 18+ (recomendado via [Volta](https://volta.sh))

## Início rápido

Para uma máquina zerada, siga os guias na ordem numerada:

```bash
# 1. Configure o terminal
# → siga 01-terminal-zsh.md

# 2. Instale e configure o Claude Code
# → siga 02-claude-instalacao.md até 07-claude-statusline.md
```

Consulte o [GUIA.md](GUIA.md) para uma visão geral antes de começar.

---

> Mantido por [Lucas Zarza](mailto:lucas@paratyenergia.com.br)
