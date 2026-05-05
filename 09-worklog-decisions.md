# Worklog e Decisions — Memória Persistente de Projeto

O Claude não lembra nada entre sessões. Sem um registro, cada vez que você reabre um projeto precisa re-explicar o que estava fazendo, quais caminhos já foram tentados e quais decisões já foram tomadas.

Dois arquivos resolvem isso:

| Arquivo | Propósito | Frequência |
|---|---|---|
| `WORKLOG.md` | Registro cronológico de sessões, o que foi feito e pendências | Atualizado ao final de cada sessão |
| `DECISIONS.md` | Decisões importantes e o *porquê* de cada uma | Atualizado quando uma decisão arquitetural é tomada |

O `WORKLOG.md` é a memória de curto prazo — o que aconteceu ontem. O `DECISIONS.md` é a memória permanente — por que o projeto está estruturado assim.

---

## 1. Configurar nos projetos

Na raiz de cada projeto, crie os dois arquivos:

```bash
cp ~/.claude/templates/WORKLOG.md ./WORKLOG.md
cp ~/.claude/templates/DECISIONS.md ./DECISIONS.md
git add WORKLOG.md DECISIONS.md
git commit -m "Add project worklog and decisions log"
```

---

## 2. Instruir o Claude a manter os arquivos

Adicione ao `CLAUDE.md` do projeto (ou ao global em `~/.claude/CLAUDE.md`):

```markdown
## Registro de trabalho
- Ao final de cada sessão, atualize WORKLOG.md: data, o que foi feito, decisões tomadas, pendências
- Se uma decisão importante de arquitetura, stack ou estrutura for tomada, registre também em DECISIONS.md com o contexto e o motivo
- Consulte WORKLOG.md e DECISIONS.md no início de cada sessão para retomar o contexto
```

Com isso, o Claude atualiza os arquivos automaticamente — você não precisa pedir.

---

## 3. Template WORKLOG.md

Salve em `~/.claude/templates/WORKLOG.md`:

```markdown
# Worklog

Registro cronológico de sessões de trabalho.

---

<!-- MODELO DE ENTRADA — copie para cada sessão

## YYYY-MM-DD

### O que foi feito
-

### Decisões tomadas
-

### Pendências
-

### Contexto para próxima sessão
> O que o Claude precisa saber para continuar de onde parou

-->
```

---

## 4. Template DECISIONS.md

Salve em `~/.claude/templates/DECISIONS.md`:

```markdown
# Decisions Log

Registro de decisões importantes e o motivo de cada uma.
Consulte antes de propor mudanças estruturais.

---

<!-- MODELO DE ENTRADA — copie para cada decisão

## [Título da decisão] — YYYY-MM-DD

**Decisão:** o que foi decidido

**Contexto:** qual problema estava sendo resolvido

**Alternativas consideradas:**
- Opção A — por que foi descartada
- Opção B — por que foi descartada

**Motivo da escolha:**

**Consequências:** o que essa decisão implica no futuro

-->
```

---

## 5. Hook: lembrete automático ao encerrar sessão

O hook `Stop` exibe um lembrete no terminal quando o Claude encerra uma resposta, caso o `WORKLOG.md` ainda não tenha sido atualizado na sessão.

Crie `~/.claude/hooks/remind-worklog.sh`:

```bash
#!/bin/bash
# Verifica se WORKLOG.md existe e lembra de atualizá-lo

WORKLOG="WORKLOG.md"
TODAY=$(date +%Y-%m-%d)

if [ ! -f "$WORKLOG" ]; then
  exit 0
fi

# Se a data de hoje não está no worklog, exibe lembrete
if ! grep -q "$TODAY" "$WORKLOG" 2>/dev/null; then
  echo ""
  echo "─────────────────────────────────────────"
  echo " Lembrete: atualize o WORKLOG.md com o"
  echo " resumo desta sessão antes de encerrar."
  echo "─────────────────────────────────────────"
fi
```

```bash
chmod +x ~/.claude/hooks/remind-worklog.sh
```

Adicione ao `~/.claude/settings.json`:

```json
"Stop": [
  {
    "matcher": "*",
    "hooks": [
      {
        "type": "command",
        "command": "bash ~/.claude/hooks/remind-worklog.sh"
      }
    ]
  }
]
```

---

## 6. Retomando contexto numa nova sessão

Ao abrir uma sessão em um projeto que tem worklog:

```
Leia o WORKLOG.md e o DECISIONS.md e me dê um resumo do estado atual do projeto.
```

O Claude lê os dois arquivos e apresenta: o que foi feito, o que está pendente e quais decisões condicionam o trabalho atual.

---

## 7. Complemento: memória nativa do Claude Code

O Claude Code tem um sistema de memória interno em:

```
~/.claude/projects/<nome-do-projeto>/memory/
```

Ele é usado automaticamente pelo Claude para armazenar fatos sobre o projeto entre sessões. O `WORKLOG.md` e o `DECISIONS.md` são complementares — são legíveis por humanos, versionados no git e portáteis entre máquinas.

Use os dois em conjunto: a memória nativa para contexto semântico, os arquivos para registro auditável.

---

## Próximo passo

Com o worklog configurado, volte ao [README.md](README.md) — a configuração está completa.
