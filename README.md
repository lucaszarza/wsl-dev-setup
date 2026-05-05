# WSL Dev Setup

Guia completo para configurar o Claude Code do jeito certo — no WSL ou em qualquer terminal Linux.

Cobre desde a instalação inicial até um time virtual de agentes AI prontos para usar em código, planilhas, apresentações e qualquer tarefa do dia a dia.

---

## O que é o Claude Code?

Claude Code é o CLI oficial da Anthropic que traz o Claude diretamente para o seu terminal. Em vez de abrir o chat no navegador, você trabalha dentro dos seus projetos — o Claude lê seus arquivos, edita código, roda comandos e executa tarefas complexas de forma autônoma.

Não é um autocomplete. É um agente que opera no seu computador.

**Para começar, você precisa de:**
- Uma conta em [claude.ai](https://claude.ai) (plano Pro ou Max recomendado para uso intenso)
- WSL2 com Ubuntu 22.04+ (Windows) ou terminal Linux/macOS

**Instalação em 1 minuto:**
```bash
npm install -g @anthropic-ai/claude-code
claude   # abre o fluxo de autenticação
```

> Para o guia completo de instalação com Node.js, aliases e primeiros comandos, veja [02-claude-instalacao.md](02-claude-instalacao.md).
> Para a documentação oficial, acesse [docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code).

---

## O que você vai ter ao final

```
WSL Ubuntu
│
├── Terminal
│   ├── Zsh + Oh My Zsh          shell rápido com plugins
│   ├── Spaceship Prompt         prompt limpo com info de git
│   ├── fzf                      busca fuzzy no histórico e arquivos
│   └── zoxide                   navegação inteligente entre pastas
│
└── Claude Code
    ├── Instalação e aliases     CLI configurado e pronto
    ├── settings.json global     permissões, modelo, guardrails
    ├── CLAUDE.md pessoal        instruções, tom e identidade visual
    ├── Hooks                    automações de segurança e lint
    ├── MCP Servers              GitHub, filesystem e banco de dados
    ├── Status line              informações visuais no terminal
    ├── gstack                   23 especialistas em slash commands
    ├── Worklog + Decisions      memória persistente entre sessões
    └── Além do código           planilhas, apresentações, documentos
```

---

## Ordem de instalação

Siga os guias numerados. Cada um leva de 5 a 15 minutos.

### 1. Terminal — [01-terminal-zsh.md](01-terminal-zsh.md)
Instala e configura o Zsh com Oh My Zsh, o tema Spaceship, fzf e zoxide. Se você já tem o terminal configurado, pule para o passo 2.

### 2. Claude Code — [02-claude-instalacao.md](02-claude-instalacao.md)
Instala o CLI, faz autenticação, configura aliases e mostra os comandos essenciais para o dia a dia.

### 3. Configuração global — [03-claude-settings.md](03-claude-settings.md)
Cria o `~/.claude/settings.json` com permissões inteligentes, modelo padrão e bloqueios para comandos destrutivos. Feito uma vez, vale para sempre.

### 4. Instruções pessoais — [04-claude-md-global.md](04-claude-md-global.md)
O `~/.claude/CLAUDE.md` é o "perfil" do usuário: define idioma, estilo de código, identidade visual da sua empresa e tom das respostas. É a configuração mais impactante — o Claude passa a trabalhar como alguém que já conhece você.

### 5. Hooks — [05-claude-hooks.md](05-claude-hooks.md)
Scripts que rodam automaticamente antes/depois de ações do Claude. Inclui hook de segurança para comandos destrutivos, lint automático e lembrete de worklog.

### 6. MCP Servers — [06-mcp-servers.md](06-mcp-servers.md)
Conecta o Claude ao GitHub (issues, PRs, CI), filesystem e bancos de dados. O GitHub MCP muda completamente o fluxo de trabalho.

### 7. Status line — [07-claude-statusline.md](07-claude-statusline.md)
Customiza a linha de status e atalhos de teclado dentro das sessões Claude.

### 8. gstack — [08-gstack.md](08-gstack.md)
23 slash commands de Garry Tan (CEO do Y Combinator) que adicionam papéis especializados ao Claude: CEO, designer, eng manager, QA, security officer e release engineer.

### 9. Worklog e Decisions — [09-worklog-decisions.md](09-worklog-decisions.md)
O Claude não lembra nada entre sessões. Dois arquivos resolvem isso: `WORKLOG.md` (registro cronológico) e `DECISIONS.md` (decisões importantes e o porquê). Inclui templates prontos e hook de lembrete.

### 10. Além do código — [10-alem-da-programacao.md](10-alem-da-programacao.md)
Claude Code não é só para programadores. Este guia mostra como usar o agente para criar apresentações, manipular planilhas Excel, gerar documentos Word, automatizar relatórios e manter identidade visual consistente em tudo que produz.

---

## Pré-requisitos

- WSL2 com Ubuntu 22.04+ (ou Linux/macOS)
- Windows Terminal
- Conexão com internet
- Conta em [claude.ai](https://claude.ai)

---

## Templates prontos

A pasta [`templates/`](templates/) contém arquivos prontos para copiar em qualquer projeto:

| Arquivo | Uso |
|---|---|
| [`templates/WORKLOG.md`](templates/WORKLOG.md) | Registro de sessões de trabalho |
| [`templates/DECISIONS.md`](templates/DECISIONS.md) | Log de decisões do projeto |

---

## Referências da comunidade

| Recurso | O que é |
|---|---|
| [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Curadoria de skills, hooks, plugins e ferramentas |
| [garrytan/gstack](https://github.com/garrytan/gstack) | Time virtual de agentes — ver [08-gstack.md](08-gstack.md) |
| [Documentação Claude Code](https://docs.anthropic.com/claude-code) | Referência oficial |
| [Hooks reference](https://docs.anthropic.com/claude-code/hooks) | Documentação de hooks |
| [MCP reference](https://docs.anthropic.com/claude-code/mcp) | Documentação de MCP |
