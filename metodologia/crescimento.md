# Crescimento de receita

- **Crescimento 1 ano** (`cresc_receita_1a`) = Receita do ano / Receita do ano
  anterior − 1. Sem ano anterior na série, o valor fica nulo.
- **CAGR 5 anos** (`cresc_receita_5a_cagr`) = (Receita do ano / Receita de 5
  anos atrás)^(1/5) − 1. Exige as duas pontas positivas; caso contrário, nulo.

Receita = conta CVM **3.01** da DRE consolidada, valores nominais em R$
(sem ajuste de inflação — um CAGR real deflacionado pode ser adicionado como
indicador separado, nunca trocado em silêncio).

Atenção do usuário: crescimento nominal em período de inflação alta superestima
o crescimento real. Essa escolha está declarada aqui de propósito.

Fonte, tratamento e limitações: ver `fontes_e_padronizacao.md`.
