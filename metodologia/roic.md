# ROIC — Retorno sobre o Capital Investido

**Fórmula:** `ROIC = NOPAT / Capital Investido Médio`

Nenhuma etapa é caixa-preta. Cada número intermediário (NOPAT, capital
investido, alíquota efetiva) fica gravado com a conta CVM de origem e pode ser
reconstruído por qualquer pessoa a partir dos arquivos públicos da CVM.

## Passo 1 — NOPAT

`NOPAT = EBIT × (1 − alíquota efetiva)`

- **EBIT** = conta CVM **3.05** da DRE consolidada ("Resultado Antes do
  Resultado Financeiro e dos Tributos"). Não recalculamos EBIT "ajustado":
  usamos o que a companhia reportou no plano de contas padronizado.
- **Alíquota efetiva** = `−(conta 3.08) / (conta 3.07)` — IR/CSLL sobre o lucro
  antes dos tributos. O sinal negativo existe porque a despesa de IR vem
  negativa na DRE.
- **Travas declaradas** (cada uma gera flag visível no dado):
  - LAIR ≤ 0 (prejuízo antes do imposto): alíquota efetiva perde o sentido;
    usamos a **marginal de 34%** com flag `aliq_fallback_34`.
  - Alíquota efetiva negativa (crédito fiscal): travada em **0%**, flag
    `aliq_travada_0`.
  - Alíquota efetiva acima de **45%**: travada no teto, flag `aliq_travada_45`.

## Passo 2 — Capital Investido

`Capital Investido = Dívida Bruta + Patrimônio Líquido Total − Caixa − Aplicações Financeiras`

- **Dívida bruta** = **2.01.04** (empréstimos e financiamentos circulantes) +
  **2.02.01** (não circulantes). Inclui debêntures e, a partir de 2019,
  arrendamentos (IFRS 16) — ver limitações.
- **PL total** = **2.03**, incluindo participação de não controladores (o EBIT
  também é de todo o grupo consolidado — numerador e denominador coerentes).
- **Caixa** = **1.01.01**; **Aplicações financeiras** = **1.01.02**.
- **Média**: usamos a média entre o capital no fim do ano anterior e no fim do
  ano corrente. No primeiro ano da série não há ano anterior: usamos só o valor
  final, com flag `capital_final_sem_media`.
- Capital investido ≤ 0: o ROIC **não é publicado** (flag
  `capital_investido_nao_positivo`) — dividir por capital negativo produz
  número sem sentido econômico.
- |ROIC| > 200%: publicado, mas com flag `roic_extremo` — quase sempre
  holding com capital investido minúsculo ou empresa em recuperação judicial.
  O número é real (não é erro de conta); o denominador é que é pequeno demais
  para o índice significar "retorno operacional" no sentido usual.

## Escolhas de metodologia (e por quê)

1. **Goodwill permanece no capital investido.** Medimos o retorno sobre o
   capital que os acionistas de fato empregaram, incluindo o que foi pago em
   aquisições. Um "ROIC ex-goodwill" pode ser adicionado no futuro como
   indicador separado — nunca trocado em silêncio.
2. **Não excluímos "caixa operacional mínimo".** Toda exclusão dessas é
   arbitrária; preferimos a fórmula reprodutível.
3. **IFRS 16 (2019)**: a conta 2.01.04/2.02.01 passou a incluir arrendamentos,
   e o EBIT também mudou de composição. Comparações que cruzam 2018→2019 têm
   uma quebra estrutural conhecida — está documentado aqui em vez de escondido.
4. **Financeiras (bancos, seguradoras) estão fora.** O conceito de capital
   investido não se aplica a balanço bancário; nessas, só ROE fará sentido.

## Fonte e verificação

- Dados: DFP consolidada, portal de dados abertos da CVM (licença ODbL).
- Todo número passa pela bateria de invariantes (`pytest testes/`) antes de ser
  publicado: balanço fecha, DRE fecha, escala plausível, série sem furo
  silencioso, reapresentações registradas, valores extremos flagados.
