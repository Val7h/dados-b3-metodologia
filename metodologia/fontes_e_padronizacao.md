# Fontes e padronização

## Fonte primária

Portal de dados abertos da CVM — DFP (demonstrações financeiras padronizadas,
anuais) de companhias abertas, 2010 em diante, CSV.
`https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/DFP/DADOS/`

Licença **ODbL** (uso comercial e redistribuição de derivados permitidos, com
atribuição à CVM). Cotações, quando usadas para múltiplos, virão exclusivamente
de dados fim-de-dia/históricos da B3 (COTAHIST), cuja distribuição a política
comercial da B3 (itens 7.9/7.10) declara livre.

## Como os dados são tratados

1. **Cru preservado.** Cada linha da CVM é gravada como veio (escala já em R$:
   arquivos em "MIL" são multiplicados por 1000). Regra de padronização nova
   nunca exige rebaixar o histórico.
2. **Consolidado primeiro.** Usamos as demonstrações consolidadas; se a empresa
   não consolida em um ano, caímos para as individuais e a escolha fica gravada
   (`fato.agreg`).
3. **Só o exercício ÚLTIMO alimenta os indicadores.** O comparativo PENÚLTIMO
   (o mesmo exercício reportado um ano depois) serve de contraprova: divergência
   acima de 0,5% é **reapresentação** e fica registrada na tabela
   `reapresentacao` — visível, nunca corrigida em silêncio.
4. **Versões.** A CVM publica reapresentações com VERSAO crescente; vale sempre
   a maior.
5. **Sinais normalizados por identidade contábil, nunca por chute.** A
   convenção de sinal de custo e IR varia entre companhias nos arquivos da CVM
   (caso real: Vale 2022 reporta custo positivo). O sinal publicado é o único
   que fecha a identidade — custo: `receita + custo = resultado bruto`; IR:
   `LAIR + IR = resultado das operações continuadas`. Crédito fiscal legítimo
   fecha a identidade sem troca e é preservado. Toda troca fica gravada em
   `fato.origem` (`sinal_normalizado_pela_identidade`); se nenhum sinal fecha,
   o valor fica como veio e o invariante da DRE acusa.
6. **Itens sem conta fixa** (ex.: D&A) são extraídos por regra declarada (busca
   textual na DFC método indireto, bloco 6.01) e a origem exata fica gravada em
   `fato.origem`. Quando a regra não encontra o item, o valor fica NULO com
   flag — nunca estimado.

## Limitações declaradas

- **IFRS 16 (2019)**: quebra estrutural em dívida e EBIT; comparações
  2018→2019 carregam esse efeito.
- **Quebras societárias** documentadas em `dados_b3/empresas.py` (ex.: Ambev
  S.A. só existe como registro desde 2013).
- **Financeiras fora do MVP**: plano de contas próprio.
- DFP é anual; a camada trimestral (ITR) será adicionada com a mesma
  metodologia.
