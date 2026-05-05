# Guia Central — WSL Dev Setup

Índice completo de configuração do ambiente de desenvolvimento. Leia este arquivo primeiro para entender o que cada etapa faz e em que ordem executar.

---

## Visão geral

```
WSL Ubuntu
├── Terminal
│   ├── Zsh + Oh My Zsh (shell principal)
│   ├── Spaceship (tema do prompt)
│   ├── fzf (fuzzy finder)
│   └── zoxide (navegação inteligente)
│
└── Claude Code
    ├── Instalação e autenticação
    ├── settings.json (permissões, modelo, aparência)
    ├── CLAUDE.md global (instruções pessoais)
    ├── Hooks (automações pré/pós ferramentas)
    ├── MCP Servers (GitHub, filesystem)
    └── Status line (informações visuais no terminal)
```

---

## Ordem recomendada de configuração

### Etapa 1 — Terminal
**[01-terminal-zsh.md](01-terminal-zsh.md)**

Configure o shell antes de qualquer coisa. O Zsh com Oh My Zsh, fzf e zoxide vai melhorar drasticamente a produtividade no terminal — e é a base para tudo que vem depois.

Tempo estimado: ~15 minutos

---

### Etapa 2 — Instalar Claude Code
**[02-claude-instalacao.md](02-claude-instalacao.md)**

Instale o CLI, faça autenticação e aprenda os comandos essenciais. Inclui aliases de produtividade e verificação da instalação.

Tempo estimado: ~5 minutos

---

### Etapa 3 — Configuração global
**[03-claude-settings.md](03-claude-settings.md)**

O arquivo `~/.claude/settings.json` controla permissões, modelo padrão, tema e comportamentos globais. Configurar isso uma vez evita aprovações repetidas em cada projeto.

Tempo estimado: ~5 minutos

---

### Etapa 4 — Instruções pessoais (CLAUDE.md global)
**[04-claude-md-global.md](04-claude-md-global.md)**

O `~/.claude/CLAUDE.md` é o "perfil" do usuário para o Claude — define idioma, estilo de código, preferências de resposta e regras que valem em qualquer projeto. É a configuração mais impactante para personalizar o comportamento do Claude.

Tempo estimado: ~10 minutos (para adaptar o template ao seu estilo)

---

### Etapa 5 — Hooks
**[05-claude-hooks.md](05-claude-hooks.md)**

Hooks são scripts que executam automaticamente antes ou depois de ações do Claude (editar arquivo, rodar comando, etc.). Use para segurança, notificações e automações.

Tempo estimado: ~15 minutos

---

### Etapa 6 — MCP Servers
**[06-mcp-servers.md](06-mcp-servers.md)**

MCP (Model Context Protocol) conecta o Claude a ferramentas externas. O GitHub MCP é o mais popular — permite ao Claude ler issues, criar PRs e interagir com repositórios diretamente.

Tempo estimado: ~10 minutos

---

### Etapa 7 — Status line
**[07-claude-statusline.md](07-claude-statusline.md)**

Customize a linha de status exibida dentro das sessões do Claude Code com informações úteis como branch, custo da sessão e modelo em uso.

Tempo estimado: ~5 minutos

---

## Referências da comunidade

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) — curadoria de skills, hooks e plugins
- [Documentação oficial Claude Code](https://docs.anthropic.com/claude-code)
- [Hooks reference](https://docs.anthropic.com/claude-code/hooks)
- [MCP reference](https://docs.anthropic.com/claude-code/mcp)
