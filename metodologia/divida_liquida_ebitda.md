# Dívida líquida / EBITDA

**Fórmulas:**
- `Dívida bruta = 2.01.04 + 2.02.01` (empréstimos e financiamentos, circulante
  e não circulante, incluindo debêntures e — desde 2019/IFRS 16 —
  arrendamentos)
- `Dívida líquida = Dívida bruta − Caixa (1.01.01) − Aplicações financeiras (1.01.02)`
- `EBITDA = EBIT (3.05) + D&A`
- `DL/EBITDA = Dívida líquida / EBITDA`

## De onde vem o D&A (a parte honesta)

Depreciação/amortização **não tem conta fixa** no plano padronizado da CVM.
Extraímos da **DFC método indireto** (bloco 6.01): somamos as linhas cuja
descrição contém "deprecia", "amortiza" ou "exaust", tomando só as linhas mais
profundas (pai e filho nunca contam duas vezes). As contas exatas usadas ficam
gravadas em `fato.origem`, empresa a empresa, ano a ano.

Travas declaradas (cada uma vira flag):
- Empresa sem DFC método indireto no ano → D&A nulo → EBITDA e DL/EBITDA nulos,
  flag `sem_da_na_dfc`. **Não estimamos.**
- EBITDA ≤ 0 → DL/EBITDA não é publicado (flag `ebitda_nao_positivo`).

Limitação declarada: esse "EBITDA" é o contábil reconstituído (EBIT + D&A da
DFC), não o "EBITDA ajustado" dos releases das companhias — que cada empresa
define de um jeito e por isso não é comparável.

Fonte, tratamento e limitações gerais: ver `fontes_e_padronizacao.md`.
