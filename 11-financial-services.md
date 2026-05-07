# Financial Services — Skills Financeiros da Anthropic

O marketplace `claude-for-financial-services` disponibiliza 6 agentes especializados e dezenas de slash commands para modelagem financeira, valuation, M&A, auditoria de planilhas e pesquisa de mercado — tudo dentro do Claude Code.

---

## 1. O que é

São plugins oficiais da Anthropic distribuídos via marketplace privado (`anthropics/financial-services` no GitHub). Cada plugin instala um conjunto de slash commands especializados em finanças corporativas:

| Plugin | Foco |
|---|---|
| `financial-analysis` | Core financeiro — DCF, LBO, 3-statement, comps, auditoria |
| `model-builder` | Constrói e mantém modelos Excel do zero |
| `statement-auditor` | Audita consistência em demonstrações financeiras |
| `valuation-reviewer` | Valuation contra comparáveis de mercado |
| `investment-banking` | CIM, one-pager, M&A, deal tracker, pitch decks |
| `market-researcher` | Research de setor, landscape competitivo |

---

## 2. Instalação

### 2.1 Registrar o marketplace

Adicione ao `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "claude-for-financial-services": {
      "source": {
        "source": "github",
        "repo": "anthropics/financial-services"
      }
    }
  }
}
```

### 2.2 Instalar os plugins

Dentro de uma sessão Claude Code:

```
/install-plugin financial-analysis@claude-for-financial-services
/install-plugin model-builder@claude-for-financial-services
/install-plugin statement-auditor@claude-for-financial-services
/install-plugin valuation-reviewer@claude-for-financial-services
/install-plugin investment-banking@claude-for-financial-services
/install-plugin market-researcher@claude-for-financial-services
```

Ou habilite todos de uma vez no `settings.json`:

```json
{
  "enabledPlugins": {
    "financial-analysis@claude-for-financial-services": true,
    "model-builder@claude-for-financial-services": true,
    "statement-auditor@claude-for-financial-services": true,
    "valuation-reviewer@claude-for-financial-services": true,
    "investment-banking@claude-for-financial-services": true,
    "market-researcher@claude-for-financial-services": true
  }
}
```

---

## 3. Skills disponíveis

### financial-analysis (core)

| Comando | O que faz |
|---|---|
| `/financial-analysis:dcf` | Modelo de Fluxo de Caixa Descontado |
| `/financial-analysis:dcf-model` | DCF completo com sensibilidades |
| `/financial-analysis:3-statement-model` | Popula DRE, Balanço e Fluxo de Caixa integrados |
| `/financial-analysis:lbo` | Modelo de alavancagem (Leveraged Buyout) |
| `/financial-analysis:lbo-model` | LBO com estrutura de capital e retornos |
| `/financial-analysis:comps` | Análise de empresas comparáveis |
| `/financial-analysis:comps-analysis` | Comps com múltiplos e spread |
| `/financial-analysis:competitive-analysis` | Landscape competitivo do setor |
| `/financial-analysis:debug-model` | Audita fórmulas e inconsistências no Excel |
| `/financial-analysis:audit-xls` | Auditoria completa de planilha `.xlsx/.xlsm` |
| `/financial-analysis:xlsx-author` | Cria ou edita planilhas Excel estruturadas |
| `/financial-analysis:clean-data-xls` | Limpa e padroniza dados em planilhas |
| `/financial-analysis:pptx-author` | Cria apresentações PowerPoint financeiras |
| `/financial-analysis:ppt-template` | Aplica template visual a uma apresentação |
| `/financial-analysis:ppt-template-creator` | Cria novo template de PPT do zero |
| `/financial-analysis:deck-refresh` | Atualiza dados em deck existente |
| `/financial-analysis:ib-check-deck` | Revisão IB de apresentação antes de enviar |
| `/financial-analysis:skill-creator` | Cria novos skills financeiros customizados |

### model-builder

| Comando | O que faz |
|---|---|
| `/model-builder:dcf-model` | DCF com premissas e outputs estruturados em Excel |
| `/model-builder:lbo-model` | LBO com waterfall de retornos |
| `/model-builder:3-statement-model` | Três demonstrações integradas e balanceadas |
| `/model-builder:comps-analysis` | Trading comps com múltiplos automatizados |
| `/model-builder:xlsx-author` | Cria planilhas Excel seguindo convenções financeiras |
| `/model-builder:audit-xls` | Audita consistência e erros no modelo |

### statement-auditor

| Comando | O que faz |
|---|---|
| `/statement-auditor:audit-xls` | Auditoria de demonstrações financeiras em Excel |
| `/statement-auditor:nav-tieout` | Reconciliação de NAV contra pacote do fundo |
| `/statement-auditor:xlsx-author` | Edita planilhas durante o processo de auditoria |

### valuation-reviewer

| Comando | O que faz |
|---|---|
| `/valuation-reviewer:xlsx-author` | Revisa e ajusta valuation em planilhas Excel |

### investment-banking

| Comando | O que faz |
|---|---|
| `/investment-banking:cim` | Confidential Information Memorandum |
| `/investment-banking:one-pager` | Perfil de empresa ou projeto (1 página) |
| `/investment-banking:teaser` | Teaser anônimo para processo M&A |
| `/investment-banking:pitch-deck` | Deck completo de pitch |
| `/investment-banking:merger-model` | Modelo de M&A — acreção/diluição |
| `/investment-banking:deal-tracker` | Tracker de processo M&A |
| `/investment-banking:process-letter` | Carta de processo para compradores |
| `/investment-banking:buyer-list` | Lista de compradores estratégicos e financeiros |
| `/investment-banking:datapack-builder` | Monta data pack para due diligence |
| `/investment-banking:strip-profile` | Perfil de strip de ativo |

### market-researcher

| Comando | O que faz |
|---|---|
| `/market-researcher:competitive-analysis` | Análise de landscape competitivo |
| `/market-researcher:comps-analysis` | Comparáveis de mercado com dados setoriais |
| `/market-researcher:pptx-author` | Research em formato de apresentação |

---

## 4. Quando usar cada agente

```
Modelagem financeira / Excel         → /model-builder ou /financial-analysis:3-statement-model
Auditoria de fórmulas / erros        → /financial-analysis:debug-model ou /statement-auditor:audit-xls
Valuation / múltiplos                → /valuation-reviewer ou /financial-analysis:comps
M&A / processo de venda              → /investment-banking:cim, :merger-model, :buyer-list
Research de setor                    → /market-researcher:competitive-analysis
Apresentações financeiras            → /financial-analysis:pptx-author ou :deck-refresh
Dados brutos / limpeza               → /financial-analysis:clean-data-xls
```

---

## 5. Verificar instalação

Dentro de uma sessão Claude Code:

```
/plugins   # lista plugins instalados e ativos
```

Se os comandos não aparecerem, confirme que o `settings.json` tem as entradas `enabledPlugins` e `extraKnownMarketplaces` corretamente configuradas.

---

## 6. Dicas de uso

- Os agentes financeiros funcionam melhor com contexto explícito: nome da empresa, setor, moeda e período
- Para `.xlsm` com macros VBA, sempre mencione ao agente que o arquivo deve ser salvo com `keep_vba=True`
- Combine `/financial-analysis:debug-model` com `/model-builder:audit-xls` para auditorias mais completas
- Use `/financial-analysis:deck-refresh` quando só precisar atualizar números em uma apresentação existente, sem refazer o layout

---

## Próximo passo

Seu ambiente está completo. Veja em [10-alem-da-programacao.md](10-alem-da-programacao.md) como usar o Claude Code para além do código.
