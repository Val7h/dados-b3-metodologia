# Dados B3 — metodologia aberta

**Site oficial: https://dadosb3.com** · Metodologia viva: https://dadosb3.com/metodologia ·
Conector MCP: `https://dadosb3.com/mcp/` · [llms.txt](https://dadosb3.com/llms.txt)

> dadosb3.com é o único endereço oficial. O endereço antigo no onrender.com foi aposentado; o que
> ainda aponta para lá está desatualizado.

Este repositório publica a **metodologia** do [Dados B3](https://dadosb3.com) — dados abertos da
bolsa brasileira (B3): fundamentos de todas as companhias com balanço na CVM (2010–hoje), dividendos,
FIIs, ETFs, BDRs e empresas que saíram da bolsa, construídos sobre os dados públicos da CVM (licença
ODbL) e o COTAHIST da B3. A contagem de companhias de hoje está em https://dadosb3.com/saude.

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

Sem chave, **qualquer ticker**, um por vez, em indicadores, múltiplos, contas CVM, dividendos e FIIs
(60 consultas por hora e 150 por dia, por endereço; assistentes de IA, 2.000 por hora e 20.000 por dia):

```
curl -s -H "Accept: application/json" "https://dadosb3.com/empresas/PETR4/indicadores"
```

- Página aberta por companhia, com a linhagem de cada número até a linha do arquivo da CVM:
  https://dadosb3.com/acoes/ITUB4 → https://dadosb3.com/linhagem/ITUB4/2025/roe
- Audite com a sua semente: https://dadosb3.com/auditoria
- Chave grátis, sem cartão, 200 consultas/dia: https://dadosb3.com/chave-gratis · Pro (10.000/dia): https://dadosb3.com/assinar
- Conector MCP para agentes de IA (36 ferramentas, só leitura): `https://dadosb3.com/mcp/` — código em https://github.com/Val7h/dados-b3-mcp
- Cliente Python: `pip install dadosb3`
- [Comparativo com as APIs concorrentes](comparativo.md) (versão viva: https://dadosb3.com/comparativo)

Palavras-chave: B3, bolsa brasileira, ações brasileiras, dividendos, FII, CVM, deslistagem,
metodologia, ROIC, ROE, múltiplos ponto-no-tempo, Brazilian stock market, MCP.

*A fonte canônica desta metodologia é o site, https://dadosb3.com/metodologia (ela evolui com o produto e com os invariantes); este repositório é um espelho versionado de 10/08/2026 para leitura, citação e crítica — números de cobertura nos arquivos de `metodologia/` são daquela data. Encontrou um erro? Abra uma issue — a promessa do projeto é exatamente essa auditabilidade.*
