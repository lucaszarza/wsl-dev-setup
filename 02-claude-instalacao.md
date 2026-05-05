# Instalação do Claude Code

Guia de instalação, autenticação e primeiros passos com o Claude Code no WSL.

---

## 1. Pré-requisito: Node.js via Volta

O Claude Code requer Node.js 18+. A forma recomendada no WSL é via Volta (gerenciador de versões):

```bash
curl https://get.volta.sh | bash
```

Recarregue o shell e instale o Node:

```bash
volta install node
node --version   # deve retornar v22.x ou superior
```

---

## 2. Instalar o Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Verifique a instalação:

```bash
claude --version
```

---

## 3. Autenticação

```bash
claude
```

Na primeira execução, o Claude abre o fluxo de autenticação no navegador. Faça login com sua conta Anthropic (claude.ai).

Após autenticar, o token fica salvo em `~/.claude/.credentials.json` — não é necessário repetir em cada sessão.

---

## 4. Atualização

O Claude Code se atualiza automaticamente, mas para forçar:

```bash
npm update -g @anthropic-ai/claude-code
```

---

## 5. Aliases essenciais

Adicione ao `~/.zsh_aliases`:

```zsh
# Claude Code
alias cl="claude"
alias clc="claude --continue"   # retoma a última conversa
alias clp="claude --print"      # modo não-interativo (útil em scripts)
alias clr="claude --resume"     # lista conversas para retomar
```

---

## 6. Modos de uso

```bash
# Iniciar nova sessão interativa
claude

# Continuar última sessão
claude --continue

# Pergunta rápida sem abrir sessão
claude -p "explica o que faz este arquivo" < main.py

# Processar saída de outro comando
git diff | claude -p "resume as mudanças em português"
```

---

## 7. Comandos slash úteis dentro de uma sessão

| Comando | O que faz |
|---|---|
| `/help` | Lista todos os comandos disponíveis |
| `/clear` | Limpa o contexto da conversa atual |
| `/compact` | Comprime o histórico para economizar tokens |
| `/cost` | Mostra o custo estimado da sessão |
| `/model` | Troca o modelo (Opus, Sonnet, Haiku) |
| `/config` | Abre o menu de configurações |
| `/hooks` | Lista os hooks configurados |
| `/mcp` | Lista os MCP servers conectados |

---

## 8. Verificação final

```bash
claude --version          # versão instalada
claude -p "olá"           # teste rápido de autenticação
ls ~/.claude/             # deve conter: settings.json, .credentials.json
```

---

## Próximo passo

Configure o comportamento global em [03-claude-settings.md](03-claude-settings.md).
