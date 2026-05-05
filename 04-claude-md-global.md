# CLAUDE.md Global — Instruções Pessoais

O arquivo `~/.claude/CLAUDE.md` é o "perfil" do usuário para o Claude Code. Ele é carregado automaticamente em **todas** as sessões, em qualquer projeto, antes do CLAUDE.md do projeto.

Use este arquivo para definir suas preferências pessoais, estilo de trabalho e regras que você quer que o Claude siga sempre — independente do projeto.

---

## 1. Localização

```
~/.claude/CLAUDE.md     ← instruções do usuário (carregado sempre)
./CLAUDE.md             ← instruções do projeto (carregado no diretório)
./.claude/CLAUDE.md     ← alternativa por projeto
```

A hierarquia é: usuário global → projeto → subdiretório. Cada nível herda e pode sobrescrever o anterior.

---

## 2. Template — copie e adapte

Crie `~/.claude/CLAUDE.md` com o conteúdo abaixo e adapte ao seu estilo:

```markdown
# Instruções Pessoais

## Idioma e comunicação
- Responda sempre em português (pt-BR)
- Seja direto e conciso — prefiro respostas curtas a explicações longas
- Não adicione emojis nas respostas a menos que eu peça
- Não escreva comentários óbvios no código — apenas onde o "por quê" não é evidente

## Estilo de código
- Python: siga PEP 8, use type hints, prefira f-strings
- JavaScript/TypeScript: use ES modules, async/await em vez de .then()
- Nomes de variáveis e funções em inglês; comentários em português quando necessário
- Não crie abstrações antes de precisar delas (YAGNI)

## Git
- Mensagens de commit em inglês, no imperativo (ex: "Add feature X", não "Added")
- Nunca use --force-push sem confirmar comigo primeiro
- Sempre prefira criar um novo commit a fazer amend em commits já publicados

## Comportamento geral
- Edite apenas os arquivos necessários para a tarefa — não faça refatorações não solicitadas
- Se uma tarefa parecer muito grande ou arriscada, me avise antes de executar
- Quando tiver dúvida sobre a intenção, pergunte — não assuma
- Ao terminar uma tarefa, informe o que foi feito em 1-2 frases (sem listar cada arquivo)

## Ferramentas
- Prefira ferramentas de leitura (Read, Grep) antes de editar
- Não rode comandos destrutivos sem confirmação explícita

## Identidade visual
- Fonte principal: [ex: Montserrat para títulos, Open Sans para texto]
- Cores primárias: [ex: #1A2E4A (azul), #E8A020 (âmbar)]
- Tom de voz: [ex: formal, direto, sem jargões]
- Logo: assets/logo.png (não distorcer, não recortar)
- Em apresentações e documentos, sempre aplicar estas diretrizes sem precisar pedir

## Registro de trabalho
- Ao início de cada sessão, leia WORKLOG.md e DECISIONS.md se existirem no projeto
- Ao final de cada sessão, atualize WORKLOG.md com: data, o que foi feito, decisões tomadas, pendências e contexto para próxima sessão
- Se uma decisão importante de arquitetura, stack ou estrutura for tomada, registre também em DECISIONS.md com contexto e motivo
```

---

## 3. Boas práticas da comunidade

**O que vale a pena incluir:**

- Idioma preferido para respostas
- Convenções de código do seu dia a dia
- Regras de git que você quer que o Claude siga
- Tom e verbosidade das respostas
- O que o Claude NÃO deve fazer (refatorar sem pedir, commitar sem confirmar, etc.)
- Informações de contexto que você sempre precisa dar (ex: stack preferida, padrões de projeto)

**O que NÃO colocar no global (coloque no CLAUDE.md do projeto):**

- Detalhes específicos de um projeto
- Estrutura de pastas de um repositório
- Comandos de build/test específicos
- Dependências ou versões de uma aplicação

---

## 4. Inspecionar o que o Claude está lendo

Durante uma sessão, use `/context` para ver quais arquivos CLAUDE.md estão carregados e o conteúdo de cada um.

---

## 5. Dica: memória persistente

O Claude Code tem um sistema de memória em `~/.claude/projects/<projeto>/memory/`. Você pode pedir ao Claude para "lembrar" de algo e ele salva em arquivos `.md` nesse diretório.

Para ver o que está salvo:

```bash
ls ~/.claude/projects/
cat ~/.claude/projects/<nome-do-projeto>/memory/MEMORY.md
```

---

## Próximo passo

Configure automações em [05-claude-hooks.md](05-claude-hooks.md).
