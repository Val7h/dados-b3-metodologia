# APIs de dados fundamentalistas da B3 — comparativo honesto

*Verificado em 10/08/2026, com fontes públicas. Este comparativo é mantido
pelo próprio Dados B3 — leia com esse desconto e confira os links.*

Quem precisa de dados de empresas da bolsa brasileira via API tem hoje
algumas opções reais. Cada uma tem pontos fortes genuínos; a escolha depende
do que você valoriza.

| | Dados B3 | brapi | bolsai | Fintz | Economatica |
|---|---|---|---|---|---|
| Preço de entrada | R$ 0 (200/dia) · Pro R$ 49,90/mês | R$ 99,99/mês | ~R$ 43/mês (trimestral) | R$ 12.500/mês (único público) | sob consulta (institucional) |
| Histórico de fundamentos | 16 anos (2010–) | desde 2009 (plano Pro) | 11–15 anos | desde 2010 | desde 1986 |
| Metodologia pública | **Sim — cada fórmula, conta a conta** | Não | Parcial (blog) | Não | Dentro do sistema, para assinantes |
| Testes de qualidade publicados | **Sim — bateria de invariantes; se reprova, não publica** | Não | Auto-benchmark em blog | Não | Não |
| Múltiplos ponto-no-tempo (sem look-ahead) | **Sim — preço do 1º pregão após a publicação real** | Não | Não | Base própria p/ backtest (enterprise) | Não anunciado |
| Histórico de reapresentações | **Sim — 5.209 registradas** | Não | Não | Não | Não |
| Degustação sem cadastro | WEGE3 completa | 4 tickers | Playground | Chave de teste limitada | Não |
| Conector de IA (MCP) | Sim | Sim | Não | Não | Sim |

## Onde cada um é melhor que nós — honestamente

- **brapi**: cotações em tempo quase-real, criptomoedas, moedas e volume de
  comunidade. Se você precisa de preço intradiário, use a brapi — nós só
  temos fim-de-dia (COTAHIST), por decisão jurídica e de escopo.
- **bolsai**: mais barata no plano pago e cobre mais tickers com preços desde
  1986.
- **Economatica**: profundidade institucional incomparável (desde 1986, telas
  de análise prontas, suporte dedicado). Se sua gestora paga R$ 2 mil+/mês,
  é outra categoria de produto.
- **Fintz**: infraestrutura enterprise com SLA e base específica para
  backtest institucional.

## Onde nós somos os únicos

1. **Metodologia 100% pública** — a fórmula de cada indicador (ROIC = NOPAT /
   capital investido, com cada conta CVM identificada) está publicada ANTES
   do número: [metodologia](/metodologia).
2. **Testes de invariantes** — dezenas de verificações automáticas (balanço
   fecha, DRE fecha, identidade do imposto, cobertura de preços) rodam antes
   de cada publicação. Se uma reprova, a atualização não vai ao ar.
3. **Múltiplos ponto-no-tempo** — P/L calculado com o preço que você PODERIA
   ter pago (1º pregão após a publicação do balanço), não com o preço de
   31/12 casado com um balanço que só saiu em março. Para backtest, isso é a
   diferença entre resultado real e ilusão.
4. **Reapresentações nunca corrigidas em silêncio** — quando a empresa
   republica um balanço, as duas versões ficam registradas.

## Fontes

Preços e características verificados em 10/08/2026: [brapi
pricing](https://brapi.dev/pricing) · [bolsai](https://usebolsai.com/) ·
[Fintz](https://fintz.com.br/) · [Economatica](https://www.economatica.com/)
· nossos: [preço](/#preco), [metodologia](/metodologia),
[degustação](/empresas/WEGE3/indicadores). Encontrou algo desatualizado?
Fale conosco pelo [portal](/portal).
