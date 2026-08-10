# Múltiplos (P/L, P/VP, EV/EBITDA)

## O princípio que separa este banco da maioria das ferramentas de varejo

O preço usado para calcular um múltiplo **nunca é o preço de fechamento do
exercício** (31/12 do ano). É o preço do **primeiro pregão a partir da data em
que a demonstração daquele ano ficou publicamente disponível** — o campo
`DT_RECEB` da própria capa do documento na CVM.

Por quê: uma DFP de exercício encerrado em 31/12 costuma ser publicada só em
fevereiro ou março do ano seguinte. Usar o preço de 31/12 junto com o lucro
daquele balanço é comparar uma cotação que o mercado tinha naquele dia com uma
informação que o mercado **ainda não tinha** — vazamento de informação futura.
Caso real medido neste banco: a DFP de 2025 da WEG (`cd_cvm` 5410, exercício
encerrado 31/12/2025) só foi recebida pela CVM em **25/02/2026**; o múltiplo de
2025 usa o preço de fechamento de 25/02/2026, não de 31/12/2025.

## Fórmulas

- **Ações em circulação** = total emitido (`QT_ACAO_TOTAL_CAP_INTEGR`) menos
  ações em tesouraria (`QT_ACAO_TOTAL_TESOURO`), da própria composição de
  capital que acompanha a DFP — nunca de fonte externa.
- **Market cap** = preço ponto-no-tempo × ações em circulação.
- **P/L** = Market cap / Lucro atribuído aos controladores (cai para o lucro
  consolidado com flag `lucro_total_sem_minoritarios` quando a companhia não
  reporta a abertura).
- **P/VP** = Market cap / (PL total − participação de não controladores).
- **EV/EBITDA** = (Market cap + Dívida líquida) / EBITDA — herda as mesmas
  travas do EBITDA (ver `divida_liquida_ebitda.md`): sem D&A na DFC, o
  múltiplo não é publicado.

## Escolha do ticker

Uma empresa pode ter mais de uma classe de ação negociada (ON e PN). O ticker
"principal" usado para preço e múltiplos vem do cadastro oficial da CVM (FCA —
Formulário Cadastral, dataset `valor_mobiliario`), nunca de busca por nome:
prioriza-se a classe Ordinária, ainda em negociação (sem data de fim), entre as
listadas em Bolsa. Empresas sem classe elegível (ex.: só debêntures listadas,
ou delistadas) ficam sem múltiplo — não é estimado.

## Travas declaradas (cada uma vira flag)

- Sem `DT_RECEB` ou sem pregão a partir dali: múltiplo não calculado, flag
  `sem_data_publicacao` / `sem_preco_apos_publicacao`.
- Sem ações em circulação: `sem_acoes_em_circulacao`.
- Lucro ≤ 0: P/L é publicado mesmo assim (número real, não escondido), com
  flag `pl_negativo` — P/L negativo não é comparável ao P/L de uma empresa
  lucrativa, mas é informação, não erro.
- PL dos controladores ≤ 0: P/VP não é publicado (`pl_nao_positivo`) — dividir
  por patrimônio negativo não tem leitura econômica direta.
- `|P/L| > 200` ou `|P/VP| > 50`: publicado com flag `pl_extremo` /
  `pvp_extremo` — em 402 empresas isso é quase sempre lucro ou patrimônio
  minúsculo (empresa em recuperação, distressed pós-crise), não erro de conta.

## Fonte e licitude

Preço: COTAHIST (B3), série histórica fim-de-dia — distribuição livre
confirmada na política comercial da B3 (itens 7.9/7.10), sem custo e sem
contrato. Ticker: FCA da CVM (ODbL). Nenhuma fonte de cotação em tempo real é
usada ou redistribuída.

## Múltiplos trimestrais (P/L TTM e P/VP)

Mesma disciplina ponto-no-tempo, ancorada no `DT_RECEB` da **ITR** de cada
trimestre:

- **Lucro TTM** (últimos 12 meses) por identidade, sem estimar o 4º trimestre:
  `TTM no Qk = anual(ano−1) − [Q1..Qk de (ano−1)] + [Q1..Qk de (ano)]`.
  Se qualquer pedaço falta (anual anterior ou um trimestre), o TTM fica NULO
  com flag (`ttm_sem_anual_anterior` / `ttm_sem_trimestre_...`) — nunca
  interpolado.
- **P/L TTM** = Market cap na data do preço / Lucro TTM.
- **P/VP** = Market cap / PL dos controladores **do balanço do próprio
  trimestre** (o balanço trimestral é foto, não fluxo).
- **Ações em circulação**: snapshot mais recente da `composicao_capital`
  (DFP **e** ITR) **até a data do preço** — nunca snapshot futuro, e nunca a
  quantidade do ano anterior quando existe a do trimestre: desdobramento no
  meio do ano quebraria o market cap em silêncio. Snapshot mais velho que 200
  dias em relação ao preço ganha flag `acoes_defasadas`.
- **EV/EBITDA trimestral NÃO existe** neste banco, de propósito: a DFC da ITR
  vem só acumulada (medido no universo inteiro: D&A trimestral isolado existe
  em ~4.200 empresa-anos no Q1, mas só ~35 no Q2 e ~16 no Q3 — o Q1 existe
  porque isolado e acumulado coincidem). Sem D&A isolado não há EBITDA
  trimestral sem estimativa, e este banco não estima. EV/EBITDA fica anual.

## Limitações declaradas

- 402 empresas do universo, ~304 com ticker resolvido (as demais não têm
  classe elegível em Bolsa no cadastro mais recente da CVM — delistadas, só
  dívida, ou nunca negociaram ação).
- O lucro TTM mistura lucro dos controladores com consolidado quando algum
  período só reporta o total — a flag `lucro_total_sem_minoritarios` acompanha
  o número quando isso acontece.
