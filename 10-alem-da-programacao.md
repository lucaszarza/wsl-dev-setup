# Além da Programação — Claude Code no Dia a Dia

Claude Code não é só para código. É um agente que opera no seu computador — lê arquivos, escreve, executa scripts, abre browser. Isso significa que ele pode ajudar com apresentações, planilhas, documentos, e-mails e qualquer tarefa que envolva arquivos ou automação.

O segredo está em ensinar o contexto certo no `CLAUDE.md` do projeto.

---

## 1. Apresentações (PowerPoint / Google Slides)

O Claude consegue criar e editar arquivos `.pptx` via Python, seguindo sua identidade visual se você fornecer as instruções:

```bash
pip install python-pptx
```

Exemplo de sessão:

```
Crie uma apresentação de 8 slides sobre [tema].
Use a fonte Montserrat, cor primária #1A2E4A, secundária #E8A020.
Salve como apresentacao.pptx
```

O Claude escreve o script Python, executa e entrega o arquivo pronto.

Para revisar visualmente, use o gstack:

```
/design-review
```

Abre o arquivo no browser e avalia hierarquia, espaçamento e consistência visual.

---

## 2. Planilhas Excel

O Claude manipula arquivos `.xlsx` e `.xlsm` via `openpyxl` ou `pandas`:

```bash
pip install openpyxl pandas
```

O que ele consegue fazer:

- Criar abas, fórmulas, gráficos e tabelas dinâmicas
- Formatar células (cores, bordas, fontes)
- Consolidar dados de múltiplas planilhas
- Gerar relatórios a partir de dados brutos
- Corrigir fórmulas quebradas

Exemplo:

```
Leia o arquivo dados.xlsx, calcule a média por categoria
e crie uma aba "Resumo" com um gráfico de barras.
```

> Dica: para arquivos `.xlsm` (com macros VBA), sempre use `keep_vba=True` no `openpyxl` para preservar as macros.

---

## 3. Documentos Word e PDFs

```bash
pip install python-docx reportlab
```

O Claude cria relatórios, contratos, propostas e documentos formatados:

```
Crie um relatório executivo em Word com os dados do arquivo csv.
Fonte: Calibri 11, margens 2,5cm, logo no cabeçalho.
```

Para PDFs diretamente:

```
Converta o relatório.md em PDF com margens de 2,5cm e fonte Georgia.
```

---

## 4. E-mails e comunicação

O Claude rascunha e-mails, respostas, comunicados e propostas com o tom certo — desde que você defina o tom no `CLAUDE.md`:

```
Escreva um e-mail para o cliente sobre o atraso na entrega.
Tom: formal, direto, sem desculpas excessivas.
```

Com o **Gmail MCP** configurado ([06-mcp-servers.md](06-mcp-servers.md)):

```
Resuma os e-mails não lidos de hoje e classifique por urgência.
```

---

## 5. Identidade visual no CLAUDE.md

O ponto que muda tudo: se você registrar sua identidade visual no `CLAUDE.md` do projeto (ou no global), o Claude aplica automaticamente em tudo que cria — sem você precisar repetir cores e fontes toda vez.

Adicione ao `CLAUDE.md` do seu projeto:

```markdown
## Identidade visual

**Fontes**
- Principal: Montserrat (títulos)
- Texto corrido: Open Sans
- Monospace (código): JetBrains Mono

**Cores**
- Primária: #1A2E4A (azul escuro)
- Secundária: #E8A020 (âmbar)
- Fundo claro: #F5F5F5
- Texto: #222222

**Tom de voz**
- Formal, mas acessível
- Sem jargões técnicos desnecessários
- Direto ao ponto

**Logo**
- Arquivo: assets/logo.png
- Versão escura: assets/logo-dark.png
- Não distorcer, não recortar

**Regras de aplicação**
- Apresentações: fundo branco ou azul escuro, nunca os dois misturados
- Documentos: sempre rodapé com logo + nome da empresa
- E-mails: assinatura padronizada conforme assets/assinatura.html
```

A partir daí, qualquer pedido de criação de conteúdo já vem formatado corretamente.

---

## 6. Pesquisa e síntese de informações

Com o **gstack** instalado ([08-gstack.md](08-gstack.md)):

```
/browse https://site.com
```

O Claude acessa a página, extrai o que você precisa e formata o resultado.

Para pesquisas mais profundas:

```
Pesquise os 5 maiores players do mercado de energia solar no Brasil.
Monte uma tabela comparativa com capacidade instalada, modelo de negócio e presença regional.
```

---

## 7. Automações recorrentes

O Claude pode criar scripts que você roda periodicamente:

```
Crie um script Python que:
1. Lê os arquivos .xlsx da pasta /relatorios
2. Consolida na aba "Geral" do arquivo master.xlsx
3. Atualiza os gráficos
4. Salva com a data de hoje no nome
```

Salvo como `consolidar.py`, você roda quando precisar — ou agenda via cron.

---

## Dica final

O Claude é tão útil quanto o contexto que você fornece.

Um `CLAUDE.md` bem escrito — com identidade visual, tom de voz, estrutura de pastas e exemplos do que você quer — elimina 80% das instruções repetidas e faz o agente trabalhar como alguém que já conhece sua empresa.

---

## Próximo passo

Volte ao [README.md](README.md) para revisar a configuração completa.
