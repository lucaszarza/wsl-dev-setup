# gstack — Time Virtual de Agentes AI

O [gstack](https://github.com/garrytan/gstack) é a configuração de Claude Code de Garry Tan, presidente e CEO do Y Combinator. São 23 slash commands que transformam o Claude Code de um assistente em um time virtual completo: CEO, designer, eng manager, QA, security officer e release engineer.

> "I don't think I've typed like a line of code probably since December."
> — Andrej Karpathy, cofundador da OpenAI, março de 2026

---

## Por que vale a pena

Sem o gstack, o Claude responde ao que você pede. Com o gstack, cada comando assume um papel especializado com um framework de perguntas próprio:

- O `/plan-ceo-review` não aprova sua ideia — ele **desafia a premissa**
- O `/qa` não lê o código — ele **abre um browser de verdade e clica nas coisas**
- O `/review` não sugere melhorias — ele **bloqueia bugs de produção antes do merge**
- O `/ship` não commita — ele roda os testes, revisa o diff, abre o PR e monitora o CI

O resultado: um ciclo completo de ideação → planejamento → implementação → review → QA → deploy, tudo dentro do Claude Code.

---

## Pré-requisitos

Além do Claude Code instalado ([02-claude-instalacao.md](02-claude-instalacao.md)):

```bash
# Bun (runtime necessário para o setup do gstack)
curl -fsSL https://bun.sh/install | bash
```

Reinicie o terminal e verifique:

```bash
bun --version   # deve retornar 1.0+
```

---

## Instalação — 30 segundos

Dentro de uma sessão Claude Code, cole este prompt e pressione Enter:

```
Install gstack: run git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup
then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack
for all web browsing, never use mcp__claude-in-chrome__* tools directly, and lists
the available skills.
```

O Claude executa o clone, roda o setup e atualiza o `CLAUDE.md` automaticamente.

### Verificar instalação

```bash
ls ~/.claude/skills/gstack/    # deve listar os arquivos do gstack
```

Dentro de uma sessão Claude:

```
/office-hours
```

Se abrir o fluxo de perguntas sobre seu produto, está funcionando.

---

## Os 23 comandos — por papel

### Planejamento e produto
| Comando | O que faz |
|---|---|
| `/office-hours` | 6 perguntas que expõem o problema real antes de você escrever uma linha de código |
| `/plan-ceo-review` | Desafia a premissa do que você está construindo, propõe o produto de 10 estrelas |
| `/plan-eng-review` | Trava arquitetura, diagramas ASCII de fluxo, matriz de testes, casos de falha |
| `/plan-design-review` | Review de design com olhar de designer — hierarquia, espaçamento, "AI slop" |
| `/plan-devex-review` | Audita a experiência do desenvolvedor: onboarding, DX, ergonomia de API |
| `/autoplan` | Roda CEO + Eng + Design + DX review em sequência e gera o plano completo |

### Design e frontend
| Comando | O que faz |
|---|---|
| `/design-consultation` | Pesquisa o mercado, propõe uma direção visual completa |
| `/design-shotgun` | Gera múltiplas variantes de design lado a lado para comparar |
| `/design-html` | Produz HTML/CSS de qualidade final, com Pretext-native |
| `/design-review` | Abre o browser e avalia o produto com olhar de designer |

### Código e review
| Comando | O que faz |
|---|---|
| `/review` | Review pré-merge: SQL safety, trust boundaries, segredos expostos, bugs de produção |
| `/investigate` | Debug sistemático em 4 fases: investigar, analisar, hipótese, validar |
| `/health` | Dashboard de qualidade: type checker, linter, testes, cobertura |
| `/codex` | Wraps o Codex CLI para review independente via outro modelo |
| `/cso` | Chief Security Officer: auditoria OWASP + STRIDE, secrets archaeology |

### QA e browser
| Comando | O que faz |
|---|---|
| `/qa` | Testa o app em um browser real, encontra e **corrige** os bugs |
| `/qa-only` | Testa e reporta — sem corrigir (para auditorias) |
| `/browse` | Browser headless para navegação e testes manuais |
| `/connect-chrome` | Lança um Chromium com sidebar de IA integrado |
| `/benchmark` | Detecta regressões de performance com baselines |
| `/canary` | Monitoramento pós-deploy: console errors, performance |

### Ship e deploy
| Comando | O que faz |
|---|---|
| `/ship` | Detecta branch base, roda testes, revisa diff, bump de versão, abre PR |
| `/land-and-deploy` | Merge, aguarda CI, verifica saúde em produção |
| `/document-release` | Atualiza docs após o deploy cruzando com o diff |
| `/retro` | Retrospectiva semanal: commits, padrões, qualidade de código |

### Segurança e guardrails
| Comando | O que faz |
|---|---|
| `/careful` | Alertas antes de `rm -rf`, DROP TABLE, force-push |
| `/guard` | Modo segurança total: careful + edições restritas ao diretório atual |
| `/freeze` | Restringe edições a um diretório específico pela sessão |
| `/unfreeze` | Remove a restrição do `/freeze` |

### Setup e manutenção
| Comando | O que faz |
|---|---|
| `/setup-deploy` | Detecta plataforma (Fly.io, Render, Vercel) e configura deploy |
| `/setup-browser-cookies` | Importa cookies do Chromium real para o browser headless |
| `/setup-gbrain` | Configura gbrain para busca semântica no código |
| `/gstack-upgrade` | Atualiza o gstack para a versão mais recente |
| `/learn` | Gerencia aprendizados do projeto: revisar, buscar, exportar |

---

## Fluxo típico de uma feature nova

```bash
# 1. Validar a ideia antes de implementar
/office-hours

# 2. Travar o plano técnico
/plan-eng-review

# 3. Implementar (Claude Code normal)

# 4. Review antes do merge
/review

# 5. QA no staging
/qa https://staging.seuapp.com

# 6. Ship
/ship
```

---

## Modo time (repositórios compartilhados)

Para que toda a equipe herde o gstack automaticamente ao abrir uma sessão Claude:

```bash
(cd ~/.claude/skills/gstack && ./setup --team) && \
~/.claude/skills/gstack/bin/gstack-team-init required && \
git add .claude/ CLAUDE.md && \
git commit -m "require gstack for AI-assisted work"
```

Troque `required` por `optional` se preferir sugerir sem bloquear.

---

## Atualizar

```bash
/gstack-upgrade
```

Ou manualmente:

```bash
cd ~/.claude/skills/gstack && git pull
```

---

## Referência

- Repositório oficial: [github.com/garrytan/gstack](https://github.com/garrytan/gstack)
- Autor: [Garry Tan](https://x.com/garrytan), CEO do Y Combinator
- Licença: MIT
