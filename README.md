# WSL Dev Setup

Configure o Claude Code do jeito certo — do zero até um time virtual de agentes AI prontos para usar em código, planilhas, apresentações e qualquer tarefa do dia a dia.

---

## Passo 0 — Instale o Claude Code

Se você ainda não tem o Claude Code instalado, faça isso primeiro. São dois comandos:

```bash
# 1. Instale o Node.js via Volta (gerenciador de versões recomendado)
curl https://get.volta.sh | bash

# Feche e reabra o terminal, depois:
volta install node

# 2. Instale o Claude Code
npm install -g @anthropic-ai/claude-code

# 3. Autentique (abre o navegador automaticamente)
claude
```

Você precisa de uma conta em [claude.ai](https://claude.ai). O plano **Pro** ou **Max** é recomendado para uso intenso — o plano gratuito tem limite de mensagens.

> Documentação oficial: [docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code)

---

## Passo 1 — Clone este repositório

```bash
git clone https://github.com/lucaszarza/wsl-dev-setup.git ~/wsl-dev-setup
```

---

## Passo 2 — Deixe o Claude configurar tudo

Com o Claude Code instalado e autenticado, abra uma sessão e cole o prompt abaixo.
O Claude vai ler o repositório e executar cada etapa, pedindo sua confirmação antes de cada bloco principal.

```
Leia o arquivo ~/wsl-dev-setup/SETUP.md e execute o processo de
configuração completo do meu ambiente de desenvolvimento.

Verifique o que já está instalado antes de instalar qualquer coisa.
Me avise o que será feito antes de cada etapa e aguarde minha confirmação.
```

> Se preferir configurar manualmente, siga os guias numerados abaixo na ordem.

---

## O que você vai ter ao final

```
WSL Ubuntu
│
├── Claude Code
│   ├── Instalado e autenticado
│   ├── settings.json global     permissões, modelo, guardrails
│   ├── CLAUDE.md pessoal        instruções, tom e identidade visual
│   ├── Hooks                    segurança, lint e lembrete de worklog
│   ├── MCP Servers              GitHub, filesystem e banco de dados
│   ├── gstack                   23 especialistas em slash commands
│   └── Worklog + Decisions      memória persistente entre sessões
│
├── Terminal
│   ├── Zsh + Oh My Zsh          shell rápido com plugins
│   ├── Spaceship Prompt         prompt limpo com info de git
│   ├── fzf                      busca fuzzy no histórico e arquivos
│   └── zoxide                   navegação inteligente entre pastas
│
└── Além do código
    ├── Apresentações PowerPoint
    ├── Planilhas Excel
    ├── Documentos Word e PDF
    └── Identidade visual configurada
```

---

## Guias — configuração manual

Se preferir executar etapa por etapa:

| # | Guia | O que faz |
|---|---|---|
| 1 | [01-claude-instalacao.md](01-claude-instalacao.md) | Instala o Claude Code, configura aliases e primeiros comandos |
| 2 | [02-terminal-zsh.md](02-terminal-zsh.md) | Zsh · Oh My Zsh · Spaceship · fzf · zoxide |
| 3 | [03-claude-settings.md](03-claude-settings.md) | `~/.claude/settings.json` com permissões e modelo padrão |
| 4 | [04-claude-md-global.md](04-claude-md-global.md) | `~/.claude/CLAUDE.md` — instruções e identidade visual |
| 5 | [05-claude-hooks.md](05-claude-hooks.md) | Hooks de segurança, lint automático e lembrete de worklog |
| 6 | [06-mcp-servers.md](06-mcp-servers.md) | GitHub MCP, filesystem, PostgreSQL |
| 7 | [07-claude-statusline.md](07-claude-statusline.md) | Status line e atalhos de teclado |
| 8 | [08-gstack.md](08-gstack.md) | 23 slash commands — time virtual de agentes |
| 9 | [09-worklog-decisions.md](09-worklog-decisions.md) | Memória persistente entre sessões |
| 10 | [10-alem-da-programacao.md](10-alem-da-programacao.md) | Planilhas, apresentações, documentos e identidade visual |

---

## Templates prontos

Copie para qualquer projeto:

```bash
cp ~/wsl-dev-setup/templates/WORKLOG.md ./WORKLOG.md
cp ~/wsl-dev-setup/templates/DECISIONS.md ./DECISIONS.md
```

---

## Referências

| Recurso | O que é |
|---|---|
| [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Curadoria de skills, hooks e plugins da comunidade |
| [garrytan/gstack](https://github.com/garrytan/gstack) | Time virtual de agentes — ver [08-gstack.md](08-gstack.md) |
| [Documentação Claude Code](https://docs.anthropic.com/claude-code) | Referência oficial |
| [Hooks reference](https://docs.anthropic.com/claude-code/hooks) | Documentação de hooks |
| [MCP reference](https://docs.anthropic.com/claude-code/mcp) | Documentação de MCP |
