# Business Case — Vértice
### Diagnóstico de dados e oportunidades de IA para a Vértice Retail

---

## Sumário executivo

Este documento responde a uma pergunta simples que a diretoria da Vértice colocou no início do projeto: **onde está o vazamento de margem, e o que fazer a respeito?**

A resposta que a análise devolveu não foi a que se esperava. A margem de contribuição da empresa está em 54,34%, é estável ao longo dos treze meses analisados e não mostra sinal de colapso em nenhum canal, categoria ou período. Não há, hoje, evidência de um problema de margem do tamanho que o briefing original supunha.

O que a análise encontrou foi outra coisa, e ela se repete cinco vezes ao longo da base: a Vértice não consegue medir, com a granularidade necessária, o que acontece depois de um pedido ser devolvido, quanto cada canal de marketing efetivamente retorna, se um cliente classificado como "em risco" está de fato prestes a churnar, quanto tempo um produto fica fora de estoque, e se um atendimento foi de fato resolvido sem intervenção humana. Em nenhuma dessas cinco frentes existe hoje um número de reais que resista a uma segunda pergunta.

Isso muda a natureza da recomendação. Em vez de propor uma economia, propomos que os primeiros 90 dias do programa sejam usados para construir a capacidade de medir essas cinco frentes — porque, sem isso, qualquer meta de economia construída sobre os números atuais não seria defensável diante do primeiro questionamento sério. A única exceção, a única linha deste documento com um valor em reais que já pode ser discutido com o Financeiro, é o gap de custo de frete do canal Marketplace, tratado em detalhe na Seção 5.

Este é, portanto, um business case que recomenda construir uma capacidade antes de prometer uma economia — e explica, número por número, por que essa é a escolha mais responsável disponível hoje.

---

## 1. Como chegamos a este diagnóstico

A análise partiu de uma base histórica de vendas, atendimento, marketing, estoque e cadastro de clientes, consolidada e cruzada para permitir uma leitura única e comparável entre as áreas. Sempre que um número aparece neste documento, ele vem de uma de três origens, e fazemos questão de deixar isso explícito porque essa é a diferença entre um business case defensável e um que não é:

- **Números observados diretamente na base** — o que de fato aconteceu no período analisado, sem cálculo intermediário.
- **Números derivados** — uma conta feita sobre os números observados, sempre acompanhada da fórmula usada, para que qualquer pessoa possa reproduzi-la.
- **Perguntas em aberto** — pontos em que a base não tem informação suficiente para chegar a um número, e que aparecem aqui como pergunta a ser decidida ou investigada, nunca como um valor estimado às pressas.

Essa disciplina existe por um motivo prático: um número de custo ou de retorno inventado para preencher uma lacuna não sobrevive à primeira pergunta de um CFO. Preferimos mostrar exatamente onde a informação acaba do que mascarar essa lacuna com uma suposição.

---

## 2. O que a base de dados permite e o que ela não permite dizer

Antes de qualquer número, é importante alinhar expectativas sobre a qualidade e a abrangência da base analisada, porque isso condiciona a confiança que se pode depositar em cada cifra deste relatório.

**A base tem uma concentração de clientes e de tickets muito acima do que se esperaria de uma operação real** — poucos identificadores de cliente respondem por uma fração desproporcional dos pedidos e dos atendimentos. Isso é típico de bases de teste ou de amostragem parcial, e o efeito prático é que todo valor financeiro deste documento deve ser lido como **ordem de grandeza para apoiar uma decisão**, não como previsão de caixa. Antes de qualquer número entrar em orçamento, ele precisa ser recalculado sobre a base de produção completa.

**As diferentes fontes de dados cobrem períodos diferentes.** Vendas cobre pouco mais de um ano; atendimento, marketing e estoque se estendem por um horizonte bem mais longo; o cadastro de clientes é ainda mais antigo. Isso significa que, ao longo deste documento, cada valor anualizado se refere à janela de tempo da sua própria fonte — nunca somamos valores vindos de janelas diferentes, porque isso produziria um número tecnicamente incorreto mesmo que pareça mais impactante.

**Marketing e a base de clientes não reconciliam com vendas em nenhuma escala razoável.** O investimento de marketing registrado equivale a mais de quatro vezes a receita real da janela, e o valor de vida do cliente acumulado é mais de oito vezes a receita observada. Isso não é um erro de cálculo nosso — é uma incompatibilidade nas próprias fontes, e por isso essas duas frentes não recebem um valor financeiro neste documento. Tratamos isso como um impedimento a ser resolvido, não como uma lacuna que podemos estimar.

Nenhuma dessas limitações invalida o exercício. Elas explicam por que a recomendação principal deste documento é sobre capacidade de medição, e não sobre uma cifra de economia.

---

## 3. O ponto de partida financeiro

Para que a leitura dos números seja comparável, fixamos um recorte único: consideramos apenas os pedidos com pagamento efetivamente aprovado, dentro da janela de treze meses coberta pela base de vendas. Isso resultou em 24.454 pedidos válidos, de um total de 27.758 registros.

Dois grupos foram deliberadamente excluídos desse recorte, e vale explicar por quê: 2.207 pedidos cancelados, que somavam mais de R$ 800 mil de margem contábil, e 1.097 pedidos ainda aguardando confirmação, somando mais de R$ 400 mil. Um pedido cancelado não é uma venda — mas, até esta revisão, ele estava sendo contado como se fosse, inflando artificialmente todas as métricas de margem da empresa. Corrigir isso já é, em si, um ganho de precisão que muda a leitura de qualquer indicador anterior.

Com esse recorte corrigido, a receita líquida do período é de R$ 16.668.956, e a margem de contribuição é de R$ 9.058.428 — uma margem ponderada de 54,34%, consistente independentemente de testarmos populações ligeiramente diferentes (incluir ou excluir devoluções, por exemplo, move esse número em menos de meio ponto percentual). Isso é o que nos dá confiança de que **não existe hoje um vazamento generalizado de margem** — o problema está em outro lugar.

**O custo de simplesmente não agir também é mensurável, e vale a pena nomeá-lo:**

- A exposição de devolução — mais de R$ 1,3 milhão de margem contábil em cerca de 3.600 pedidos devolvidos — segue sem que ninguém saiba dizer se ela foi de fato reembolsada, revendida ou perdida. Cada mês que passa sem resolver isso é um mês em que essa incerteza permanece.
- O orçamento de marketing continua sendo decidido sem que se possa atribuir retorno a nenhum canal com confiança, mesmo havendo um ranking direcional razoavelmente claro entre eles.
- A reposição de estoque na categoria de Beleza — onde está concentrada praticamente toda a ruptura observada na empresa — continua sendo reativa, com mais de R$ 58 mil de receita mensal exposta a esse risco.

E há um quarto custo, mais difícil de traduzir em reais: enquanto essas lacunas não forem fechadas, a diretoria segue tomando decisões de alocação de recursos com base em um conjunto de indicadores que, em alguns pontos, ainda diverge de si mesmo.

---

## 4. Alternativas consideradas

A análise gerou seis frentes candidatas a receber investimento. Priorizamos essas frentes não pelo tamanho da cifra que aparentam, mas pela maturidade da evidência que as sustenta — e isso é deliberado: uma iniciativa com um número grande, mas construído sobre uma base frágil, é mais perigosa do que uma com número pequeno e sólido.

| Iniciativa | O que já sabemos hoje | O que ainda falta descobrir | Próximo passo recomendado |
|---|---|---|---|
| **Frete no canal Marketplace** | O gap de margem e o custo de frete desse canal, já comparados com os demais canais | Se esse custo é negociável contratualmente, e como ele reage a uma eventual mudança de política de frete | Auditoria contratual e teste controlado, medindo margem por faixa de ticket ou de produto |
| **Atendimento sobre "onde está meu pedido"** | Volume de chamados, custo tabelado por canal de atendimento e nível de serviço | Quais chamados podem de fato ser automatizados sem gerar retrabalho ou reabertura | Piloto com grupo de controle, medindo contenção, qualidade percebida e custo líquido |
| **Ruptura de estoque em Beleza** | Onde a ruptura está concentrada hoje | Por quanto tempo cada produto fica indisponível e quanta demanda se perde nesse período | Instrumentar o acompanhamento contínuo de disponibilidade e testar uma nova regra de reposição em um subconjunto de produtos |
| **Devoluções** | O volume de pedidos devolvidos e a margem contábil associada a eles | O que de fato acontece financeiramente depois da devolução — reembolso, estorno, revenda ou perda | Mapear esse fluxo ponta a ponta e conferir uma amostra de casos reais |
| **Retorno por canal de marketing** | Um ranking direcional entre os canais, coerente com a intuição do negócio | Uma base de investimento real, comparável na mesma janela de tempo | Reconciliar as duas fontes antes de qualquer decisão de alocação |
| **Clientes em risco de churn** | Um grupo de clientes concentrando parcela relevante do valor de vida da base | Uma régua de risco que não dependa da própria definição do segmento que está sendo avaliado | Medir recompra real ao longo do tempo |

Vale destacar um teste que fizemos e que **não confirmou** uma hipótese intuitiva: testamos se chamados relacionados a defeito ou troca de tamanho levavam a mais devoluções do que outros tipos de chamado. Não levavam — a proporção é praticamente a mesma em todas as categorias, inclusive nas de elogio. Achamos importante registrar isso porque descartar uma hipótese com dados vale tanto quanto confirmar uma.

Das seis frentes, apenas a primeira — frete no Marketplace — tem hoje evidência suficiente para sustentar uma cifra financeira defensável. É nela que nos aprofundamos a seguir.

---

## 5. Ganhos e investimento — a oportunidade do frete no Marketplace

### 5.1 O que os dados mostram

Comparando o canal Marketplace com os demais canais de venda somados, dois números chamam atenção: a margem de contribuição do Marketplace é 51,50%, contra 55,11% dos demais canais — uma diferença de 3,61 pontos percentuais. E o custo de frete sobre a receita nesse canal é de 4,90%, contra apenas 0,95% nos demais — uma diferença de 3,95 pontos percentuais.

O fato de o gap de frete ser *maior* que o gap de margem é revelador: significa que o frete, sozinho, já explica toda a diferença de rentabilidade entre o Marketplace e os demais canais, e ainda sobra alguma margem. Ou seja, o Marketplace está sendo parcialmente compensado em outras linhas — o que reforça a hipótese de que o frete é a alavanca certa a puxar, e não apenas uma correlação de fundo.

### 5.2 Traduzindo o gap em reais

Partindo da receita que o canal Marketplace gerou no período analisado, projetamos essa receita para uma base anual — cerca de R$ 3,26 milhões por ano, representando pouco mais de um quinto da receita total da empresa. Sobre essa receita anualizada, o custo de frete do canal representa cerca de R$ 160 mil por ano, e a margem de contribuição que o canal entrega, mesmo com esse custo, chega a R$ 1,68 milhão por ano.

Conferimos esse número por dois caminhos de cálculo independentes — um partindo do gap de frete, outro partindo do gap de margem — e as duas rotas convergem, com uma diferença inferior a 0,1%, atribuível apenas a arredondamento. Essa checagem cruzada é o motivo pelo qual confiamos nesse número o suficiente para trazê-lo à mesa.

### 5.3 A pergunta que precisa vir antes da negociação

Antes de tratar esse gap como um vazamento a ser corrigido, é preciso responder a uma pergunta que os dados, sozinhos, não respondem: **o volume que passa pelo Marketplace é incremental — ou seja, vendas que a Vértice não teria por outro canal — ou ele está apenas canibalizando vendas que ocorreriam de qualquer forma nos canais próprios?**

Essa distinção muda completamente a recomendação. Se o volume for incremental, pagar uma margem menor nesse canal pode ser simplesmente o preço de acessar uma demanda que não existiria de outra forma — e nesse caso, a recomendação correta pode ser não mexer em nada. Se for canibalização, o gap de margem é, de fato, uma perda evitável.

Colocamos essa pergunta em perspectiva com os próprios números: a margem que o canal entrega por ano (R$ 1,68 milhão) é treze vezes maior que o gap de frete que se buscaria recuperar (cerca de R$ 129 mil). Uma renegociação mal calibrada, que reduza o volume do canal, arrisca uma quantia muito maior do que aquela que se está tentando recuperar. Por isso, esta pergunta — e não o valor do gap — deveria abrir a conversa com o CFO.

### 5.4 Como calculamos o benefício, termo a termo

Para manter a disciplina de nunca embutir um custo suposto dentro de um número de retorno, calculamos o benefício líquido dessa iniciativa da seguinte forma: o volume de receita elegível, multiplicado pela fração do gap que se consegue efetivamente capturar, multiplicado pelo valor que se deixa de pagar por unidade de receita — menos o esforço de implementação, menos o custo de manter essa mudança operando, menos qualquer perda que a mudança gere em outra frente (como conversão).

A tabela abaixo mostra, para cada um desses termos, de onde ele vem e quem precisa se responsabilizar por defini-lo:

| Termo do cálculo | O que representa nesta iniciativa | De onde vem | Quem precisa validar ou decidir |
|---|---|---|---|
| Volume elegível | A receita anual do canal Marketplace | Projeção sobre a receita observada na análise | Já calculado; squad de dados confirma se novos dados mudam a base |
| Fração capturável | Quanto do gap de frete se consegue de fato renegociar — usamos três cenários: 25%, 50% e 75% | Cenário de trabalho da squad, não um dado observado | Financeiro e Comercial decidem qual cenário é realista para o contrato em questão |
| Valor evitável por unidade | O gap de 3,95 pontos percentuais de custo de frete sobre a receita | Observado diretamente na análise | Não depende de decisão — é um fato já constatado |
| Custo de implementação | O esforço de auditar o contrato atual e conduzir a renegociação | Ainda não dimensionado | Financeiro e Jurídico precisam estimar em horas de trabalho |
| Custo de operação | O esforço de manter essa nova condição funcionando ao longo do tempo | Ainda não dimensionado | A definir junto com quem assumir a governança dos dados |
| Perdas secundárias | O risco de que uma eventual mudança na política de frete reduza a conversão de vendas | Estimado a partir da própria margem do canal | Deve ser medido no piloto controlado, não suposto |

Para as demais cinco iniciativas do pipeline, os dois primeiros termos desse cálculo — a fração capturável e o valor evitável — ainda não existem com confiança suficiente. É exatamente por isso que nenhuma delas aparece com um valor de benefício líquido neste documento: preferimos deixar a lacuna visível a preenchê-la com uma suposição.

### 5.5 Cenários e o teto que o investimento pode ter

Combinando esses termos, chegamos a três cenários de captura do gap de frete, cada um definindo o valor máximo que faria sentido investir para que a iniciativa se pague já no primeiro ano:

| Cenário | Fração do gap capturada | Benefício anual estimado | Investimento máximo que ainda se paga no ano 1 |
|---|---:|---:|---:|
| Conservador | 25% | R$ 32,1 mil | R$ 32,1 mil |
| Central | 50% | R$ 64,3 mil | R$ 64,3 mil |
| Otimista | 75% | R$ 96,4 mil | R$ 96,4 mil |

A leitura prática disso é: se o esforço interno de auditoria contratual e renegociação — envolvendo Financeiro, Comercial e Jurídico — ficar abaixo de R$ 32 mil, a iniciativa se paga mesmo no cenário mais pessimista de captura, com retorno dentro de doze meses. Se ficar acima disso, ela só se justifica a partir do cenário central — e essa é uma decisão que cabe à diretoria, não à squad de análise.

É importante deixar claro que nenhum desses cenários representa uma economia garantida. O custo de frete registrado na base pode ser um repasse ao cliente final, um subsídio da própria empresa ou uma comissão contratual fixa — e só a auditoria contratual vai revelar qual dessas hipóteses é a verdadeira.

### 5.6 Um risco que o ganho pode não sobreviver

Se a forma escolhida para capturar esse gap for repassar o custo de frete ao cliente final, existe um risco direto de queda na conversão de vendas — e esse risco pode anular o ganho projetado bem antes do que se imagina:

| Cenário de captura | Ganho projetado | Anulado por uma queda de conversão de apenas |
|---|---:|---:|
| 25% | R$ 32,1 mil | 1,9 ponto percentual |
| 50% | R$ 64,3 mil | 3,8 pontos percentuais |
| 75% | R$ 96,4 mil | 5,8 pontos percentuais |

Isso significa que qualquer piloto testado precisa medir margem e conversão ao mesmo tempo. Um piloto que reporte apenas a economia obtida em frete, sem acompanhar o que aconteceu com as vendas, corre o risco de comemorar um ganho que, na prática, já foi mais do que anulado.

### 5.7 Visão consolidada de ganhos e investimento

| | Impacto estimado | Premissas assumidas | Esforço necessário | Retorno esperado |
|---|---|---|---|---|
| **Frete Marketplace** | Entre R$ 32 mil e R$ 96 mil de margem recuperada por ano, a depender do cenário de captura | Nenhuma premissa de custo — apenas o percentual de captura do gap, que é uma escolha de cenário, não um fato assumido | A definir junto com Financeiro e Jurídico (auditoria contratual e renegociação) | Payback dentro do primeiro ano, por construção do próprio cálculo |
| **Devolução, atendimento, estoque, marketing e retenção** | Ainda não mensurável em reais — cada uma depende do próximo experimento indicado na Seção 4 | Dependem inteiramente dos resultados desses experimentos | Custo de instrumentação e de coleta adicional de dados, ainda a dimensionar | Sem retorno calculável até que a lacuna de dados seja fechada |

---

## 6. Recomendação e justificativa

Chegamos a uma recomendação que foge do formato tradicional de um business case, e achamos importante justificar por quê.

As duas entregas centrais propostas para os próximos 90 dias — fechar a lacuna de informação sobre devoluções e concluir a ferramenta de priorização de iniciativas que vem sendo desenvolvida ao longo do projeto — não são iniciativas com retorno financeiro direto. Calcular um ROI para elas seria um erro conceitual: fechar a lacuna de devolução não gera economia por si só, ela apenas revela se existe ou não uma economia a ser capturada ali. A ferramenta de priorização, por sua vez, não substitui horas de reunião de forma mensurável — o valor dela está em impedir que a empresa comprometa metas com base em números que, como mostramos ao longo deste documento, ainda não se sustentam sozinhos.

Já testamos essa ferramenta contra um conjunto de casos reais construídos a partir dos próprios erros que este documento evita — por exemplo, tratar o gap de frete como uma economia garantida, somar iniciativas que ainda não têm valor calculável em um "total" de business case, ou aceitar um número que contradiz a fonte oficial de indicadores. Em quatro desses casos, a ferramenta identificou corretamente o erro e recusou-se a segui-lo — o que nos dá confiança de que ela está cumprindo a função para a qual foi desenhada.

A pergunta que substitui o ROI tradicional, nesse caso, é outra: **quanto custa, por trimestre, uma decisão de alocação de investimento tomada com base em um número errado?** Essa é uma pergunta que cabe à diretoria responder, não à squad — e a resposta a ela é o que vai justificar, ou não, o investimento na capacidade de medir. O que nos cabe entregar é o custo de construir essa capacidade; a comparação com o custo do erro que ela evita é uma decisão de negócio.

Vale registrar que a primeira etapa desse trabalho — o desenho da ferramenta, seus critérios de decisão, as salvaguardas contra os erros mais comuns e a bateria de testes usada para validá-la — já foi entregue e não representa custo adicional a partir daqui.

**Diante disso, recomendamos à diretoria quatro decisões:**

1. **Aprovar a construção da capacidade de medir** as cinco lacunas identificadas — devolução, marketing, retenção, estoque e atendimento — condicionada a que cada uma tenha um responsável e um prazo definidos.
2. **Responder à pergunta sobre incrementalidade do canal Marketplace** e, caso a resposta favoreça agir, autorizar a auditoria contratual e a eventual renegociação, respeitando o teto de investimento apresentado no cenário conservador.
3. **Autorizar a conclusão da ferramenta de priorização de iniciativas**, tratando-a como infraestrutura de governança do programa, e não como um produto isolado.
4. **Nomear um responsável único pela base de indicadores** da empresa, de forma que nenhuma mudança de critério ou de recorte aconteça sem registro e sem nova validação.

Por fim, uma clareza importante: **não estamos pedindo à diretoria que aprove uma meta de economia.** Nenhum número deste documento está, hoje, em condição de virar uma meta formal — e dizer o contrário seria exatamente o tipo de erro que este trabalho foi desenhado para evitar.

---

## 7. Riscos e plano de mitigação

| Risco | O que está em jogo | Como pretendemos mitigar |
|---|---|---|
| O volume do Marketplace é incremental, e mexer nele reduz vendas que não existiriam por outro canal | Arriscar R$ 1,68 milhão de margem anual para tentar recuperar R$ 129 mil | Responder à pergunta de incrementalidade (Seção 5.3) antes de qualquer negociação |
| O custo de frete é uma comissão contratual não negociável | Elimina a única linha deste documento com valor financeiro defensável | Conduzir a auditoria contratual já nos primeiros 30 dias do programa |
| Repassar o custo de frete ao cliente reduz a conversão de vendas | O ganho projetado pode ser integralmente anulado (Seção 5.6) | Rodar um experimento controlado medindo margem e conversão simultaneamente |
| Um número desatualizado ou divergente chega a uma apresentação para a diretoria | Perda de credibilidade do time diante do CFO | Corrigir divergências identificadas antes do fim do primeiro mês; padronizar a checagem em todos os materiais |
| A amostragem de devoluções mostrar que a perda real é próxima de zero | A maior linha do pipeline de oportunidades deixa de existir | Tratado como resultado legítimo — é exatamente para descobrir isso que a apuração está sendo proposta |
| Conclusões tiradas de uma base ainda não totalmente representativa da operação real | Decisão tomada sobre um número que pode não se repetir em produção | Toda cifra deste documento é comunicada como ordem de grandeza, nunca como valor definitivo |
| Uso de dado pessoal na ferramenta de priorização | Exposição a risco de conformidade com a LGPD | Escopo da ferramenta restrito a dados agregados, com bloqueio ativo contra qualquer tentativa de identificação individual |

---

## Considerações finais

Este documento não recomenda uma economia porque, com honestidade, os dados disponíveis hoje não sustentam uma. Recomenda, em vez disso, que se invista nos próximos 90 dias em fechar as lacunas de medição que impedem a Vértice de saber, com confiança, onde estão suas maiores oportunidades reais — e aponta a única frente, o frete do Marketplace, em que já é possível agir com uma base de cálculo defensável.

Ficamos à disposição para detalhar qualquer um dos números aqui apresentados, sua origem e sua fórmula de cálculo, junto às equipes de Financeiro, Comercial ou Dados da Vértice.
