# Dados B3 — metodologia aberta

Este repositório publica a **metodologia completa** do [Dados B3](https://dados-b3.onrender.com) — API de dados fundamentalistas de 402 companhias abertas brasileiras (2010–hoje), construída sobre os dados públicos da CVM (licença ODbL) e o COTAHIST da B3.

**A tese do projeto:** número que não se explica não merece confiança. Por isso cada indicador tem a fórmula publicada ANTES do número existir — NOPAT e capital investido abertos conta CVM a conta CVM, escolhas declaradas (goodwill, IFRS 16, alíquota efetiva com travas), e uma bateria de testes de invariantes que roda antes de cada publicação: **se um teste reprova, o dado não vai ao ar.**

## Metodologia

- [ROIC](metodologia/roic.md) — NOPAT / capital investido, passo a passo
- [ROE](metodologia/roe.md)
- [Margens](metodologia/margens.md)
- [Crescimento](metodologia/crescimento.md)
- [Dívida líquida / EBITDA](metodologia/divida_liquida_ebitda.md)
- [Múltiplos ponto-no-tempo](metodologia/multiplos.md) — P/L com o preço do 1º pregão APÓS a publicação real do balanço (sem look-ahead)
- [Dados trimestrais e TTM](metodologia/trimestral.md)
- [Fontes e padronização](metodologia/fontes_e_padronizacao.md) — inclui como normalizamos sinais por identidade contábil e por que reapresentações nunca são corrigidas em silêncio

## Experimente sem cadastro

A WEG (WEGE3) é 100% aberta em todos os endpoints:

```
curl -s "https://dados-b3.onrender.com/empresas/WEGE3/indicadores"
```

- Plano grátis: chave sem cartão, 200 consultas/dia — [criar chave](https://dados-b3.onrender.com/assinar?plano=gratis)
- Conector MCP para agentes de IA: `https://dados-b3.onrender.com/mcp/`
- [Comparativo honesto com as APIs concorrentes](comparativo.md)

*A fonte canônica desta metodologia é o site (ela evolui com o produto e com os invariantes); este repositório é um espelho versionado para leitura, citação e crítica. Encontrou um erro? Abra uma issue — a promessa do projeto é exatamente essa auditabilidade.*
