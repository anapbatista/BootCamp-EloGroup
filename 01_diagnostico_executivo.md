# Diagnóstico Executivo
### Vértice Retail

## Queda da Rentabilidade

A rentabilidade da Vértice não está caindo de forma generalizada — a margem de contribuição da empresa é estável ao longo de todo o período analisado. O problema real é que a empresa não consegue medir, hoje, se e onde existe uma oportunidade real de ganho, porque cinco áreas de decisão dependem de dados que a própria operação ainda não captura.

## Pergunta que originou este diagnóstico

Como usar dados e IA para melhorar rentabilidade, eficiência operacional e qualidade de decisão nos próximos 90 dias?

## Árvore de hipóteses

Seis linhas de investigação foram testadas contra os dados disponíveis (vendas, marketing, cadastro de clientes, atendimento e estoque). Cada uma recebeu um veredito sobre até onde os dados permitem ir:

| Hipótese | O que se queria descobrir | Os dados permitem responder? |
|---|---|---|
| **Margem** | O crescimento veio com perda de qualidade de margem (desconto, frete, devolução, mix)? | Sim, integralmente |
| **Marketing** | Algum canal de aquisição traz clientes mais valiosos que outros? | Parcialmente — comparação de qualidade entre canais sim; retorno em reais, não |
| **Operações** | Falhas de estoque estão destruindo valor pós-venda? | Parcialmente — concentração do problema sim; causa raiz e valor exato, não |
| **Atendimento** | O volume de chamados revela oportunidade de automação? | Sim, integralmente |
| **Cliente** | Existem segmentos de cliente com valor e risco muito diferentes? | Sim, integralmente |
| **Gestão e produtividade** | Retrabalho e dados fragmentados prejudicam a velocidade de decisão? | Sim, como evidência indireta — a própria dificuldade de cruzar as bases é a prova |

## O que está por trás do problema, hipótese por hipótese

| Hipótese | O que os dados mostram | Causa identificada | Tamanho da implicação |
|---|---|---|---|
| **Margem — canal Marketplace** | A margem desse canal é 51,5%, contra 55,1% nos demais canais somados — uma diferença real, embora pequena por pedido individual | O custo de frete desse canal consome quase 5% da receita, contra menos de 1% nos demais canais — cinco vezes mais | Cerca de R$ 117 mil por ano de diferença de margem observada; entre R$ 32 mil e R$ 96 mil por ano são potencialmente recuperáveis via renegociação, a depender do quanto for possível capturar |
| **Margem — devolução** | Quase 15% dos pedidos aprovados são devolvidos, e a margem registrada para esses pedidos é praticamente idêntica à dos não devolvidos | O cálculo de margem da empresa não desconta nenhum custo de devolução — reembolso, logística reversa ou perda de produto simplesmente não entram na conta | Mais de R$ 1,3 milhão de margem contábil está exposta nesses pedidos — não é uma perda confirmada, é uma incerteza que precisa ser resolvida |
| **Atendimento** | Um único tipo de chamado — "onde está meu pedido" — responde por 30% de todo o volume de atendimento, com cerca de 68 chamados por semana | Esse tipo de chamado já tem uma solução automatizada testada, que entrega satisfação equivalente ao atendimento humano por uma fração do custo | Entre R$ 23 mil e R$ 41 mil por ano, dependendo do quanto puder ser automatizado com segurança |
| **Operações — estoque** | Quase toda a ruptura de estoque da empresa está concentrada em uma única categoria de produto: Beleza | A categoria de Beleza é a única com validade de prateleira variável — um fator plausível, mas ainda não comprovado como causa | Entre R$ 12 mil e R$ 48 mil de receita potencialmente perdida no período, mais cerca de R$ 58 mil por mês de receita em risco se o estoque crítico virar ruptura |
| **Marketing** | Existe um ranking claro de qual canal traz retorno de melhor qualidade | As duas bases de dados usadas — investimento em marketing e vendas realizadas — não são comparáveis na escala atual, o que impede qualquer conta em reais | Nenhum valor financeiro pode ser atribuído a esta frente hoje |
| **Cliente** | Um grupo de quase 22% da base de clientes está classificado como em risco de abandono, concentrando uma fatia relevante do valor histórico da empresa | A forma como esse grupo é definido usa a mesma métrica que se usaria para calcular o ganho de recuperá-lo — o que tornaria qualquer conta financeira circular | Prioridade estratégica para ação de retenção, sem valor em reais anexado até que exista uma forma de medir recompra real |

## O tamanho das oportunidades, junto

| Frente | Faixa de valor anual | Nível de confiança |
|---|---|---|
| Frete no Marketplace | R$ 32 mil a R$ 96 mil | Cenário — depende de negociação ainda não iniciada |
| Devolução | Exposição de R$ 1,35 milhão | Fato observado, não é perda confirmada |
| Automação de atendimento | R$ 23 mil a R$ 41 mil | Cenário — depende de piloto ainda não realizado |
| Ruptura de estoque em Beleza | R$ 12 mil a R$ 48 mil | Cenário — depende de premissa de duração ainda não medida |
| Marketing | Não mensurável hoje | Bloqueado por incompatibilidade de dado |
| Retenção de clientes em risco | Não mensurável hoje | Bloqueado por circularidade de definição |

Nenhuma dessas frentes está pronta para virar meta de economia sem um passo adicional de validação — e é isso que diferencia este diagnóstico de um levantamento de oportunidades convencional.

## As duas frentes que recomendamos priorizar primeiro

Entre as seis hipóteses, duas reúnem hoje o melhor equilíbrio entre valor, velocidade de teste e confiança nos dados — e são o ponto de partida recomendado para os próximos 90 dias:

**Frente financeira — frete no Marketplace.** É a única frente com um número em reais já defensável. O próximo passo é a negociação de cláusulas de frete e comissão diretamente com a plataforma, com meta de recuperar parte do gab observado no primeiro mês.

**Frente operacional — automação do atendimento sobre status de pedido.** É a frente com o caminho mais rápido de validação. O próximo passo é um piloto monitorado medindo se a automação de fato resolve o chamado sem intervenção humana, mantendo a satisfação do cliente estável.

As demais quatro frentes permanecem no plano de trabalho, mas nenhuma delas abre a conversa com a diretoria: devolução e ruptura de estoque dependem de dado que ainda não existe; marketing e retenção de clientes dependem de uma correção estrutural na forma como o dado é coletado antes de qualquer valor financeiro poder ser calculado.

## Limitações que qualificam todo este diagnóstico

- A base de vendas tem uma concentração de clientes muito acima do que se esperaria de uma operação real — um único cliente responde por mais de 11 mil dos quase 28 mil pedidos analisados. Todo valor financeiro deste diagnóstico deve ser lido como ordem de grandeza, não como número definitivo.
- As diferentes fontes de dados cobrem períodos de tempo diferentes: vendas cobre pouco mais de um ano; atendimento, marketing e estoque cobrem quase três anos; o cadastro de clientes remonta a mais tempo ainda. Por isso, nenhum valor deste diagnóstico combina fontes de janelas de tempo diferentes numa mesma conta.
- Marketing e a base de vendas não reconciliam em nenhuma escala razoável — o investimento registrado é mais de quatro vezes a receita real do mesmo período. Essa incompatibilidade, e não um erro de modelo de atribuição entre canais, é a razão pela qual marketing não recebe um valor financeiro neste documento.
