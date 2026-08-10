# ROE — Retorno sobre o Patrimônio Líquido

**Fórmula:** `ROE = Lucro atribuído aos controladores / PL dos controladores médio`

- **Lucro dos controladores** = conta CVM **3.11.01** da DRE consolidada.
  Quando a companhia não reporta a abertura (sem minoritários), usamos o lucro
  consolidado **3.11** com flag `lucro_total_sem_minoritarios`.
- **PL dos controladores** = **2.03** menos **2.03.09** (participação de não
  controladores). Sem a linha 2.03.09, usamos o PL total — coerente com o
  numerador no caso sem minoritários.
- **Média**: PL no fim do ano anterior e no fim do ano corrente. Primeiro ano
  da série: só o valor final, flag `pl_final_sem_media`.
- **PL médio ≤ 0**: ROE não é publicado (flag `pl_nao_positivo`) — ROE sobre
  patrimônio negativo é número sem sentido econômico.

Fonte, tratamento e limitações: ver `fontes_e_padronizacao.md`.
