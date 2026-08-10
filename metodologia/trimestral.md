# Dados trimestrais (ITR)

## O que a ITR realmente reporta

Cada arquivo trimestral da CVM (ITR) reporta itens de fluxo (DRE, DFC) em
**duas versões**:

- **Acumulado desde 1º de janeiro** (ex.: no arquivo do 2º trimestre, a receita
  cobre 01/01 a 30/06)
- **Trimestre isolado** (ex.: no mesmo arquivo, 01/04 a 30/06)

Este banco guarda só o **isolado** — é o bloco comparável entre trimestres e
recombinável (soma os 3 → acumulado de 9 meses; últimos 4 → TTM). Para o 1º
trimestre as duas versões coincidem, então nada se perde.

**Classificação**: pela duração do período (fim menos início), não pelo mês —
isolado tem 80 a 100 dias. Empresa com ano fiscal fora do calendário (fim em
mês diferente de março/junho/setembro) é descartada nesta camada, não
adivinhada.

## O 4º trimestre não existe na ITR

A CVM não pede ITR do 4º trimestre — ele fica implícito no fechamento anual
(DFP), que é auditado. Quem quiser o Q4 isolado precisa subtrair: `Q4 = Anual
(DFP) − (Q1 + Q2 + Q3 isolados)`. Este banco não pré-calcula isso no MVP; fica
disponível para quem consumir os dados brutos.

## Balanço (BPA/BPP)

Não tem a ambiguidade acima — é foto de um instante (31/03, 30/06 ou 30/09),
um valor só por trimestre, tratado igual ao anual.

## TTM (últimos 12 meses)

O lucro TTM usado nos múltiplos trimestrais sai por identidade — sem precisar
do Q4 isolado e sem estimativa: `TTM no Qk = anual(ano−1) − Q1..Qk(ano−1) +
Q1..Qk(ano)`. Faltou um pedaço, o TTM é nulo com flag. Ver
`multiplos.md`.

## Limitações declaradas

- Indicadores operacionais (ROIC, ROE, margens) **não são recalculados** na
  granularidade trimestral neste MVP — exigiriam média de capital trimestral,
  decisão de design deliberadamente deixada para depois. O TTM implementado
  cobre o lucro (para P/L); receita TTM e demais itens seguem o mesmo caminho
  quando entrarem.
- A DFC da ITR vem só acumulada — não há D&A trimestral isolado e portanto
  não há EBITDA trimestral (medição e consequências em `multiplos.md`).
- Mesma cobertura de empresas do banco anual (402, não-financeiras).
