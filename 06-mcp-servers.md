# MCP Servers — Integrações do Claude Code

MCP (Model Context Protocol) é o protocolo que conecta o Claude a ferramentas externas. Com MCP servers, o Claude pode interagir com GitHub, bancos de dados, sistemas de arquivos e qualquer API — sem precisar de copiar e colar manualmente.

---

## 1. Conceito

```
Claude Code  ←→  MCP Server  ←→  Ferramenta externa
                               (GitHub, Postgres, Slack...)
```

Cada MCP server expõe ferramentas que o Claude pode chamar dentro de uma sessão. O usuário vê e aprova cada chamada, igual às ferramentas nativas.

---

## 2. Escopo de configuração

| Escopo | Onde fica | Quando usar |
|---|---|---|
| `user` | `~/.claude.json` | Servidores pessoais (GitHub, etc.) |
| `project` | `.mcp.json` na raiz do projeto | Servidores específicos do time |
| `local` | `.mcp.json` local (não versionado) | Testes locais |

---

## 3. GitHub MCP (o mais popular)

Permite ao Claude: ler issues, criar PRs, comentar, verificar CI/CD, listar branches, etc.

### Instalação

Requer o [GitHub CLI](https://cli.github.com/) autenticado:

```bash
# Instalar gh CLI (se não tiver)
sudo apt install gh
gh auth login

# Adicionar o MCP server do GitHub
claude mcp add github --scope user -- npx -y @modelcontextprotocol/server-github
```

Configure a variável de ambiente com seu token:

```bash
# No ~/.zshrc ou ~/.zsh_aliases
export GITHUB_PERSONAL_ACCESS_TOKEN="ghp_xxxxxxxxxxxx"
```

O token precisa das permissões: `repo`, `read:org`, `read:user`.

### Uso dentro de uma sessão

```
/mcp              # lista servidores conectados
```

O Claude passa a ter acesso às ferramentas:
- `github_list_issues` — listar issues de um repositório
- `github_create_pull_request` — abrir PR
- `github_get_file_contents` — ler arquivo de outro repo
- `github_search_repositories` — buscar repositórios

---

## 4. Filesystem MCP

Útil quando você quer que o Claude acesse diretórios fora do projeto atual com controle granular:

```bash
claude mcp add filesystem --scope user -- \
  npx -y @modelcontextprotocol/server-filesystem /home/$USER/workspace
```

Substitua o caminho pelo diretório que deseja expor. Você pode adicionar múltiplos caminhos:

```bash
claude mcp add filesystem --scope user -- \
  npx -y @modelcontextprotocol/server-filesystem \
  /home/$USER/workspace \
  /home/$USER/documentos
```

---

## 5. PostgreSQL / Supabase MCP

Para projetos com banco de dados:

```bash
claude mcp add postgres --scope project -- \
  npx -y @modelcontextprotocol/server-postgres \
  "postgresql://user:password@localhost:5432/dbname"
```

O Claude consegue rodar queries, inspecionar schema e ajudar com migrations.

---

## 6. Gerenciar servidores

```bash
# Listar servidores configurados
claude mcp list

# Remover um servidor
claude mcp remove github

# Ver detalhes de um servidor
claude mcp get github
```

---

## 7. Verificar dentro de uma sessão

```
/mcp
```

Mostra os servidores conectados e as ferramentas disponíveis em cada um.

---

## 8. Dicas da comunidade

- Adicione MCP servers no escopo `user` para que fiquem disponíveis em qualquer projeto pessoal
- Para projetos de time, commite o `.mcp.json` no repositório — todos herdam os mesmos servidores
- Não coloque tokens ou credenciais no `.mcp.json` versionado — use variáveis de ambiente
- O GitHub MCP + filesystem MCP cobre 80% dos casos de uso comuns

---

## Próximo passo

Configure a aparência do terminal em [07-claude-statusline.md](07-claude-statusline.md).
