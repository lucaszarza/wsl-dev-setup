# SETUP — Orquestrador de Configuração

> **Este arquivo é escrito para o Claude Code executar.**
> Se você é humano e chegou aqui por engano, veja o [README.md](README.md).

---

## Missão

Você é o responsável por configurar o ambiente de desenvolvimento completo deste usuário.
Siga as etapas abaixo na ordem. Para cada uma:

1. **Verifique** o que já está instalado ou configurado
2. **Informe** o que será feito em uma frase
3. **Aguarde** confirmação antes de executar
4. **Execute** e confirme o resultado antes de avançar

Se algo falhar, investigue a causa antes de continuar. Não pule etapas.

---

## Etapa 1 — Terminal (Zsh + Oh My Zsh + fzf + zoxide)

**Guia:** [02-terminal-zsh.md](02-terminal-zsh.md)

Antes de executar, verifique:
```bash
echo $SHELL          # já usa zsh?
fzf --version        # fzf instalado?
zoxide --version     # zoxide instalado?
```

Se tudo estiver instalado e configurado, informe o usuário e pule para a Etapa 2.

Se não estiver, siga o guia e execute cada bloco de instalação, confirmando com o usuário antes.

Ao final, verifique:
```bash
echo $ZSH_THEME      # deve retornar "spaceship"
fzf --version
zoxide --version
```

---

## Etapa 2 — Configuração global do Claude Code (settings.json)

**Guia:** [03-claude-settings.md](03-claude-settings.md)

Antes de executar, verifique:
```bash
cat ~/.claude/settings.json 2>/dev/null || echo "não existe"
```

Se já existir um `settings.json`, mostre o conteúdo atual ao usuário e pergunte se deseja sobrescrever ou mesclar com o template.

Execute a configuração seguindo o guia. Ao final, confirme que o arquivo foi salvo corretamente.

---

## Etapa 3 — Instruções pessoais (CLAUDE.md global)

**Guia:** [04-claude-md-global.md](04-claude-md-global.md)

Antes de executar, verifique:
```bash
cat ~/.claude/CLAUDE.md 2>/dev/null || echo "não existe"
```

Mostre o template do guia ao usuário e peça que ele preencha:
- Fontes e cores da identidade visual
- Tom de voz preferido
- Regras de git
- Qualquer preferência pessoal adicional

Salve o arquivo com as informações fornecidas.

---

## Etapa 4 — Hooks

**Guia:** [05-claude-hooks.md](05-claude-hooks.md)

Crie o diretório e os scripts:
```bash
mkdir -p ~/.claude/hooks
```

Instale os três hooks do guia:
- `check-destructive.sh` — bloqueia comandos perigosos
- `session-summary.sh` — notificação sonora ao terminar
- `remind-worklog.sh` — lembrete de worklog

Após criar cada script, execute `chmod +x` e confirme que o arquivo foi criado.

Adicione as referências dos hooks ao `~/.claude/settings.json`.

---

## Etapa 5 — MCP Servers

**Guia:** [06-mcp-servers.md](06-mcp-servers.md)

Verifique o que está disponível:
```bash
claude mcp list 2>/dev/null || echo "nenhum configurado"
gh auth status 2>/dev/null || echo "gh CLI não autenticado"
```

Pergunte ao usuário quais MCP servers deseja instalar:
- [ ] GitHub MCP (requer `gh` autenticado)
- [ ] Filesystem MCP
- [ ] PostgreSQL/Supabase MCP

Instale apenas os que o usuário confirmar.

---

## Etapa 6 — Status line

**Guia:** [07-claude-statusline.md](07-claude-statusline.md)

Aplique as configurações de status line e keybindings conforme o guia.
Pergunte ao usuário se quer adicionar a integração com o Spaceship Prompt.

---

## Etapa 7 — gstack

**Guia:** [08-gstack.md](08-gstack.md)

Verifique:
```bash
ls ~/.claude/skills/gstack 2>/dev/null || echo "não instalado"
bun --version 2>/dev/null || echo "bun não instalado"
```

Se o Bun não estiver instalado, instale primeiro:
```bash
curl -fsSL https://bun.sh/install | bash
```

Execute a instalação do gstack conforme o guia.
Ao final, peça ao usuário para testar com `/office-hours` dentro de uma sessão Claude.

---

## Etapa 8 — Templates de Worklog e Decisions

**Guia:** [09-worklog-decisions.md](09-worklog-decisions.md)

Crie o diretório de templates:
```bash
mkdir -p ~/.claude/templates
```

Copie os templates do repositório:
```bash
cp templates/WORKLOG.md ~/.claude/templates/WORKLOG.md
cp templates/DECISIONS.md ~/.claude/templates/DECISIONS.md
```

Confirme com o usuário se quer aplicar os templates no projeto atual:
```bash
cp ~/.claude/templates/WORKLOG.md ./WORKLOG.md
cp ~/.claude/templates/DECISIONS.md ./DECISIONS.md
```

---

## Conclusão

Ao terminar todas as etapas, apresente um resumo de:

- O que foi instalado e configurado com sucesso
- O que foi pulado (já existia)
- O que falhou ou ficou pendente
- Próximos passos sugeridos (ex: preencher identidade visual no CLAUDE.md, autenticar GitHub MCP)

Sugira que o usuário leia [10-alem-da-programacao.md](10-alem-da-programacao.md) para ver como usar o Claude Code além de programação.
