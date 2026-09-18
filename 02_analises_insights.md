# Análises e Insights
### Vértice Retail — descobertas suportadas por dados

## Como este documento deve ser lido

Cada descoberta abaixo é apresentada com o que os dados mostram, a premissa que sustenta qualquer número calculado a partir deles, e o que essa descoberta significa para a decisão de negócio. Onde os dados não sustentam uma conclusão financeira, isso é dito explicitamente — inclusive quando o resultado contraria a intuição.

## Premissas que valem para toda a análise

- Todo valor financeiro considera apenas pedidos com pagamento efetivamente aprovado — pedidos cancelados ou ainda aguardando confirmação foram excluídos de qualquer cálculo de receita ou margem, porque não representam venda realizada.
- Toda comparação de margem entre canais ou categorias usa a soma dos valores, não a média por pedido — a média simples é distorcida por um pequeno número de pedidos com margem fortemente negativa.
- Nenhum valor combina fontes de dados com janelas de tempo diferentes na mesma conta.
- A base de clientes tem uma concentração incomum de pedidos e chamados em poucos identificadores — por isso, nenhuma análise de comportamento individual de cliente foi construída sobre vendas ou atendimento; apenas sobre os indicadores já consolidados no cadastro de clientes.

## 1. Margem — o canal Marketplace tem uma rentabilidade menor, e a causa é o frete

**O que os dados mostram:** a margem de contribuição do canal Marketplace é 51,5%, contra 55,1% nos demais canais somados — uma diferença de 3,6 pontos percentuais. O efeito é estatisticamente pequeno por pedido individual, mas ganha relevância porque o Marketplace é um dos canais de maior volume da empresa.

**Causa identificada:** decompondo a diferença de margem por componente de custo, o frete explica quase toda ela — o custo de frete consome 4,9% da receita do Marketplace, contra menos de 1% nos demais canais, um gap de quase 4 pontos percentuais.

**Premissa explícita:** o custo de frete está registrado na contabilidade da empresa, mas os dados não informam se ele é um repasse ao cliente, um subsídio da própria empresa ou uma comissão contratual fixa da plataforma. Por isso, o valor calculado é um gap observado, não uma economia garantida.

**Interpretação de negócio:** antes de qualquer negociação, é preciso responder se o volume desse canal é incremental — ou seja, vendas que não existiriam por outro canal — ou se ele apenas substitui vendas que ocorreriam de qualquer forma nos canais próprios. Essa resposta muda completamente a recomendação.

## 2. Margem — a devolução não está sendo descontada no cálculo de rentabilidade

**O que os dados mostram:** quase 15% dos pedidos aprovados estão marcados como devolvidos. A margem contábil desses pedidos é praticamente igual à dos pedidos não devolvidos — o que revela que a fórmula de margem da empresa simplesmente não desconta nada quando um pedido é devolvido.

**Premissa explícita:** os dados confirmam que um pedido foi marcado como devolvido, mas não informam se houve reembolso de fato, estorno, retorno do produto ao estoque, revenda ou custo de logística reversa. Por isso, apresentamos dois números com rótulos diferentes: a exposição observada (o que está registrado) e um cenário de perda bruta sob a hipótese extrema de que toda essa margem foi de fato perdida — nunca como uma perda confirmada.

**Interpretação de negócio:** mais de R$ 1,3 milhão de margem contábil está em uma zona cinzenta contábil. Essa é, hoje, a maior oportunidade financeira identificada em todo o diagnóstico — e também a mais incerta, porque depende inteiramente de uma pergunta ainda não respondida: o que acontece, na prática, com um pedido depois que ele é devolvido?

## 3. Marketing — o ranking entre canais é válido, mas nenhum valor em reais pode ser calculado

**O que os dados mostram:** comparando os canais de marketing por qualidade (não apenas volume), o canal de Influenciadores tem o melhor retorno relativo, a melhor margem e o maior ticket médio entre todos os canais. O canal Marketplace, coerente com o que já foi visto na análise de margem, tem o pior retorno relativo entre todos.

**Premissa explícita e achado negativo:** testamos se essa diferença poderia ser causada por um modelo de atribuição de conversão diferente entre canais, e não é — os modelos de atribuição se distribuem de forma quase idêntica entre todos os canais. O problema real é outro, e mais sério: o investimento em marketing registrado na janela de vendas analisada equivale a mais de quatro vezes a receita real do mesmo período, e a receita atribuída às campanhas chega a quase 19 vezes a receita real. As duas bases foram construídas em escalas que não se comunicam.

**Interpretação de negócio:** o ranking entre canais pode ser usado para orientar prioridade relativa de investimento — por exemplo, priorizar Influenciadores em detrimento de Marketplace. O que não pode ser feito, em nenhuma hipótese, é somar qualquer valor de "receita gerada por marketing" a qualquer outra conta financeira deste diagnóstico.

## 4. Operações — a ruptura de estoque está quase inteiramente concentrada em uma categoria

**O que os dados mostram:** dos casos de ruptura efetiva de produto na empresa, 97% estão na categoria Beleza. Outros 232 produtos dessa mesma categoria estão em estado de estoque crítico — ainda disponíveis, mas em risco iminente de ruptura.

**Causa identificada, com ressalva:** testamos os fatores óbvios que poderiam explicar essa concentração — tempo de reposição, ponto de pedido e número de fornecedores — e nenhum deles difere entre categorias. O único fator que se destaca é que Beleza é a única categoria com validade de prateleira variável. Isso reforça essa hipótese como plausível, mas os dados disponíveis não permitem prová-la como causa definitiva, porque não existe um histórico contínuo de disponibilidade por produto — apenas uma fotografia do momento atual.

**Premissa explícita:** o valor de receita potencial calculado depende de uma suposição sobre por quanto tempo cada produto ficou indisponível — testamos um intervalo de meio mês a dois meses, sem confirmação de qual é o valor real.

**Interpretação de negócio:** ruptura e estoque crítico não são a mesma coisa e não devem ser somados — ruptura já bloqueia venda agora; estoque crítico é um risco de virar ruptura, ainda não uma perda ocorrida. Tratar os dois como uma perda única infla o número e mistura fato com risco futuro.

## 5. Atendimento — um único tema de chamado concentra quase um terço do volume, com solução já testada

**O que os dados mostram:** o tema "onde está meu pedido" responde por 30% de todos os chamados de atendimento — cerca de 68 por semana — e tem uma satisfação do cliente abaixo da média geral. O canal automatizado de atendimento já entrega uma satisfação equivalente à dos canais humanos, a uma fração pequena do custo tabelado.

**Achado negativo relevante:** testamos, cruzando atendimento com vendas de fato, se algum tipo de chamado — como "defeito" ou "troca de tamanho" — leva a mais devoluções do que os demais. Não leva. A taxa de devolução é praticamente idêntica em todos os tipos de chamado, inclusive em elogios. É um resultado que contraria a intuição do time de atendimento, e reportamos exatamente como veio.

**Premissa explícita:** os dados atuais mostram por onde um chamado entrou, não se ele foi de fato resolvido sem intervenção humana — a taxa de resolução é praticamente idêntica entre todos os canais de entrada, o que significa que ainda não existe um sinal real de que a automação está, de fato, contendo o chamado sozinha. Os valores de custo por canal também são tabelados, não o custo real de resolver um chamado a mais.

**Interpretação de negócio:** a oportunidade de economia é real em direção, mas ainda não em tamanho — o valor calculado é ilustrativo até que um piloto meça, de fato, a taxa de resolução sem humano, o índice de recontato e o custo real por chamado.

## 6. Cliente — o valor da base está concentrado, e uma parte relevante está em risco

**O que os dados mostram:** os clientes classificados como mais valiosos representam pouco mais de um quarto da base, mas concentram mais da metade de todo o valor histórico já gerado. No extremo oposto, um quarto da base — clientes inativos ou já perdidos — responde por menos de um décimo desse valor. O grupo classificado como "em risco" representa quase 22% da base de clientes, ainda concentrando uma fatia relevante do valor histórico.

**Achado negativo relevante, incluído a pedido de revisão interna:** antes de transformar a diferença de valor entre o grupo "em risco" e um grupo saudável equivalente numa oportunidade em reais, testamos se essa conta seria circular — e é. A forma como esses grupos são definidos já usa a mesma métrica de valor histórico que se usaria para calcular o ganho de "recuperar" um cliente de um grupo para o outro. Além disso, o valor histórico acumulado de toda a base é mais de oito vezes maior que a receita real do período analisado — as duas métricas estão em janelas de tempo diferentes e não podem ser comparadas diretamente.

**Interpretação de negócio:** o grupo de clientes em risco é uma prioridade estratégica legítima para ação de retenção — mas nenhum valor em reais deve ser anexado a essa ação até que exista uma forma de medir recompra real ao longo do tempo, em vez do valor histórico acumulado.

## Resumo das descobertas por grau de confiança

| Descoberta | Grau de confiança |
|---|---|
| A margem da empresa é estável — não há colapso generalizado de rentabilidade | Alto — observado diretamente nos dados |
| O gap de margem do Marketplace existe e a causa é o frete | Alto — observado e decomposto |
| A devolução não é descontada na margem | Alto — observado diretamente |
| O valor financeiro da devolução é uma perda confirmada | Baixo — depende de dado que não existe hoje |
| O ranking de qualidade entre canais de marketing | Alto — observado, mas apenas como comparação relativa |
| O valor financeiro de marketing | Não disponível — bases não reconciliam |
| A concentração de ruptura em Beleza | Alto — observado diretamente |
| A causa da ruptura ser a validade de prateleira | Médio — hipótese plausível, não comprovada |
| O potencial de automação do atendimento | Médio — direção confirmada, tamanho ainda não |
| Tickets de defeito geram mais devolução | Refutado — os dados não sustentam essa hipótese |
| O grupo de clientes em risco é uma prioridade | Alto — observado diretamente |
| O valor financeiro de recuperar esse grupo | Não disponível — cálculo seria circular |
