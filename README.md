# WSL Dev Setup

Guia completo para montar um ambiente de desenvolvimento no WSL do zero — terminal otimizado, Claude Code configurado e um time virtual de agentes AI prontos para usar.

Toda configuração está separada por tema, numerada na ordem certa, e pode ser replicada em qualquer máquina nova em menos de uma hora.

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
    ├── CLAUDE.md pessoal        instruções que valem em todo projeto
    ├── Hooks                    automações de segurança e lint
    ├── MCP Servers              GitHub, filesystem e banco de dados
    ├── Status line              informações visuais no terminal
    └── gstack                   23 especialistas em slash commands
```

---

## Ordem de instalação

Siga os guias numerados. Cada um leva de 5 a 15 minutos.

### 1. Terminal — [01-terminal-zsh.md](01-terminal-zsh.md)
Instala e configura o Zsh com Oh My Zsh, o tema Spaceship, fzf e zoxide. É a base para tudo que vem depois. Se você já tem o terminal configurado, pule para o passo 2.

### 2. Claude Code — [02-claude-instalacao.md](02-claude-instalacao.md)
Instala o CLI via npm, faz autenticação, configura aliases e mostra os comandos essenciais para o dia a dia.

### 3. Configuração global — [03-claude-settings.md](03-claude-settings.md)
Cria o `~/.claude/settings.json` com permissões inteligentes, modelo padrão e bloqueios para comandos destrutivos. Feito uma vez, vale para sempre.

### 4. Instruções pessoais — [04-claude-md-global.md](04-claude-md-global.md)
O `~/.claude/CLAUDE.md` é o "perfil" do usuário: define idioma, estilo de código, regras de git e tom das respostas. É a configuração mais impactante para personalizar o Claude.

### 5. Hooks — [05-claude-hooks.md](05-claude-hooks.md)
Scripts que rodam automaticamente antes/depois de ações do Claude. Inclui hook de segurança para comandos destrutivos, lint automático e notificação ao terminar tarefas longas.

### 6. MCP Servers — [06-mcp-servers.md](06-mcp-servers.md)
Conecta o Claude ao GitHub (issues, PRs, CI), filesystem e bancos de dados via Model Context Protocol. O GitHub MCP é o mais usado e muda completamente o fluxo de trabalho.

### 7. Status line — [07-claude-statusline.md](07-claude-statusline.md)
Customiza a linha de status e atalhos de teclado dentro das sessões Claude. Integração com o Spaceship Prompt.

### 8. gstack — [08-gstack.md](08-gstack.md)
O passo que transforma o Claude Code de um assistente em um time. 23 slash commands criados por Garry Tan (CEO do Y Combinator) que adicionam papéis especializados: CEO, designer, eng manager, QA, security officer e release engineer.

---

## Pré-requisitos

- WSL2 com Ubuntu 22.04+
- Windows Terminal
- Conexão com internet
- Conta em [claude.ai](https://claude.ai) (plano Pro ou Max recomendado)

---

## Referências da comunidade

| Recurso | O que é |
|---|---|
| [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Curadoria de skills, hooks, plugins e ferramentas |
| [garrytan/gstack](https://github.com/garrytan/gstack) | Time virtual de agentes — ver [08-gstack.md](08-gstack.md) |
| [Documentação Claude Code](https://docs.anthropic.com/claude-code) | Referência oficial |
| [Hooks reference](https://docs.anthropic.com/claude-code/hooks) | Documentação de hooks |
| [MCP reference](https://docs.anthropic.com/claude-code/mcp) | Documentação de MCP |
