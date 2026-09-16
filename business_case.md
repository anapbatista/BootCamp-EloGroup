# Business Case — O Custo de Não Medir
### Vértice Retail · squad de diagnóstico de dados e IA
Fonte de dados congelada: `kpis.json` (hash `1c33bed0384a`, gerado a partir de `vendas_base_financeira`, jan/2023–jan/2024)

Documento irmão: `roadmap_30_60_90.md` · Artefato de processo — entrega obrigatória do case (Seção 9 do briefing).

---

## 0. Regra de leitura

Todo número deste documento pertence a uma de três classes. **Não existe uma quarta.**

| Classe | Definição | Como aparece |
|---|---|---|
| **Oficial** | Vem do `kpis.json` ou de uma célula de saída do notebook | Citado com o campo de origem no Anexo A |
| **Derivado** | Álgebra sobre valores oficiais | Citado com a fórmula, sempre |
| **A decidir** | Custo, esforço ou prazo que o cliente precisa dimensionar | Aparece como **pergunta**, nunca como valor |

**Não há premissas de custo neste business case.** Um número de custo que a squad inventasse não sobreviveria à primeira pergunta do CFO — e a estrutura abaixo não precisa dele: em vez de supor um custo e calcular um retorno, calculamos o **teto de investimento** que o benefício observado sustenta, e devolvemos ao cliente a pergunta de se ele cabe nesse teto.

Cada número oficial carrega os quatro campos da Seção 8.1 do notebook: **recorte**, **fórmula**, **nível de evidência** (`observado` · `cenário` · `hipótese` · `dado insuficiente`) e **decisão que informa**.

---

## 1. A tese

**A Vértice não tem, hoje, um problema de margem demonstrável. Tem um problema de mensuração — e ele é grande o bastante para ser a recomendação principal.**

A margem de contribuição ponderada da empresa é **54,34%** e a margem mensal é estável ao longo dos 13 meses, sem colapso. O diagnóstico não encontrou o vazamento que o briefing sugeria. Encontrou outra coisa, cinco vezes:

| # | O que a empresa não consegue medir | Evidência oficial |
|---|---|---|
| 1 | **O que acontece com um pedido devolvido.** 14,88% dos pedidos aprovados estão marcados como devolvidos, somando **R\$ 1.351.707** de margem contábil no período. A base não tem coluna de reembolso, estorno, custo de logística reversa, retorno ao estoque ou revenda | `devolucao.*` |
| 2 | **Quanto cada canal de aquisição custa e retorna.** O investimento de marketing na janela de vendas equivale a **452% da receita real** e a receita atribuída é **18,9×** a real. As bases não reconciliam em escala nenhuma | `marketing_reconciliacao.*` |
| 3 | **Se um cliente está em risco de verdade.** O `segmento_rfm` é, na prática, uma faixa ordenada de LTV — calcular "gap de LTV entre segmentos" recalcula a definição do segmento. E o LTV acumulado (R\$ 139.092.569) é **8,3×** a receita da janela oficial | `retencao_clientes_em_risco.*` |
| 4 | **Quanto tempo um SKU fica em ruptura.** 96 dos 99 casos de ruptura da empresa estão em Beleza, mas `estoque.csv` é uma fotografia: não há série temporal, duração, demanda não atendida ou backorder | `operacoes_ruptura_beleza.dados_necessarios` |
| 5 | **Se um ticket foi resolvido sem humano.** `canal_entrada` diz por onde o ticket entrou; `status_atendimento` é praticamente idêntico em todos os canais (~65% Resolvido, ~10% Escalado) | `atendimento_automacao_wismo.status` |

E uma sexta, sobre a própria empresa: até a revisão desta AED, todas as métricas financeiras incluíam **2.207 pedidos Cancelados** (R\$ 809.612 de margem contábil) e **1.097 Aguardando** (R\$ 402.397). Pedido cancelado não é venda — e estava dentro da conta de margem.

**A implicação executiva.** A Vértice tem R\$ 1,35 milhão de margem contábil em pedidos que ninguém sabe classificar como perda ou não, e nenhuma das outras quatro frentes pode receber um valor em R\$ hoje. Enquanto isso não muda, qualquer decisão de alocação é tomada no escuro — e nenhuma meta construída sobre esses números é auditável.

**O que recomendamos, então, não é uma economia. É uma capacidade.** Os próximos 90 dias devem entregar a ponte financeira da devolução, a reconciliação de marketing e a instrumentação de estoque. A única iniciativa com valor defensável hoje — frete Marketplace — é o que se faz *enquanto* essa capacidade é construída, não a razão do programa.

---

## 2. Ressalvas que precedem qualquer número

Valem para **todo** valor deste documento. Nenhuma foi contornada com suposição.

| # | Limitação | Evidência | Consequência |
|---|---|---|---|
| **R1** | **A base é sintética.** 346 `customer_id` distintos respondem por 27.758 pedidos — um único cliente concentra 11.282. Em atendimento, 445 clientes para 35.840 tickets, contra 15.000 cadastrados | Notebook, Seção 1 | Toda cifra é **ordem de grandeza para exercício de decisão**, não previsão de caixa. Nenhum número aqui entra em orçamento sem refazer a conta sobre dado de produção |
| **R2** | **As janelas não coincidem.** `vendas.csv` cobre 2023-01-01 a 2024-01-26 (13 meses); `atendimento`, `marketing` e `estoque` vão até dez/2025; `clientes.csv` remonta a jan/2020. Apenas 34,6% dos `order_id` de atendimento existem em vendas | Notebook, Seção 1 | Valores anualizados de frentes diferentes são **run-rates de janelas distintas**. Não são somados neste documento |
| **R3** | **Marketing e clientes não reconciliam com vendas.** 452%, 18,9× e 8,3× | Seções 4 e 7 | `oportunidade_financeira_rs: null` — **trava de projeto, não lacuna a preencher** |

Nenhuma dessas ressalvas invalida o exercício. Elas definem o que ele é: um diagnóstico que prioriza corretamente e dimensiona por ordem de grandeza, com a régua de evidência explícita em cada linha.

---

## 3. Recorte financeiro oficial

| Item | Definição |
|---|---|
| **População** | `vendas_base_financeira = vendas[vendas.status_pagamento == "Aprovado"]` |
| **N** | 24.454 pedidos (de 27.758 registros válidos) |
| **Excluídos** | 2.207 Cancelados (R\$ 809.612 de margem contábil) e 1.097 Aguardando (R\$ 402.397) |
| **Janela** | 2023-01-01 a 2024-01-26 (13 meses) |
| **Unidade** | R\$ correntes |
| **Devolução** | Incluída na receita principal; corte de exposição mostrado à parte, **nunca subtraído automaticamente** |
| **Receita líquida** | R\$ 16.668.956 |
| **Margem de contribuição** | R\$ 9.058.428 (54,34% ponderada) |

**Sensibilidade da população — a direção não muda, o tamanho muda:**

| População | Pedidos | Receita líquida | Margem | Margem % pond. |
|---|---:|---:|---:|---:|
| Todos os registros válidos | 27.758 | R\$ 18.889.334 | R\$ 10.270.437 | 54,37% |
| **Somente Aprovados (oficial)** | **24.454** | **R\$ 16.668.956** | **R\$ 9.058.428** | **54,34%** |
| Aprovados e não devolvidos | 20.815 | R\$ 14.168.520 | R\$ 7.706.720 | 54,39% |

**Nota de versão.** O documento de mentoria cita margem Marketplace de 51,40%, gap de 3,76 p.p., frete de R\$ 138.374 e devolução de R\$ 1.523 mi / R\$ 1.406 mi. São valores da versão **anterior** à declaração da população oficial. Este business case usa os valores recalculados sobre Aprovados, que constam do `kpis.json` atual.

---

## 4. O que custa não fazer nada

O cenário de não intervenção não é neutro. Ele tem três consequências, todas amarradas a números oficiais:

| Consequência | Tamanho |
|---|---|
| **A exposição de devolução permanece não classificada por mais um ciclo.** R\$ 1.351.707 de margem contábil em 3.639 pedidos aprovados e devolvidos — média de R\$ 371 por pedido — sem que ninguém saiba se foi reembolsado, revendido ou perdido | `devolucao.observado_margem_contabil_no_periodo_rs` |
| **Marketing continua sem poder receber orçamento com base em retorno.** O ranking direcional existe (Influenciador ROAS 7,7 e margem 52,3% vs. Marketplace ROAS 3,0), mas nenhum R\$ pode ser atribuído | `marketing_reconciliacao.status` |
| **A reposição de Beleza continua reativa.** 96 SKUs já com venda bloqueada e 232 em estoque crítico, representando **R\$ 58.421/mês** de receita exposta *se* virarem ruptura | `operacoes_ruptura_beleza.*` |

E uma quarta, sem número: a diretoria continua decidindo alocação sobre um catálogo de KPIs que ainda diverge de si mesmo — ver Seção 8.

---

## 5. Âncora 1 — Frete Marketplace

### 5.1 Ficha do número

| Campo | Conteúdo |
|---|---|
| **Recorte** | `vendas_base_financeira`, canal Marketplace vs. demais canais agregados, 13 meses |
| **Fórmula** | `soma(custo_frete) / soma(receita_liquida)` por canal — denominador explícito, não média simples de razão por pedido |
| **Nível de evidência** | **observado** (o gap) → **cenário** (a fração capturável) |
| **Decisão que informa** | Se renegociar frete/comissão com a plataforma |

| Métrica | Marketplace | Demais canais | Gap |
|---|---:|---:|---:|
| Margem de contribuição ponderada | 51,50% | 55,11% | **3,61 p.p.** |
| Custo de frete sobre receita | 4,90% | 0,95% | **3,95 p.p.** |
| Tamanho de efeito (Cohen's d) | — | — | 0,28 (pequeno-médio) |

O gap de frete (3,95 p.p.) é **maior** que o gap de margem (3,61 p.p.): o frete explica integralmente a diferença de margem do canal e ainda sobra. O Marketplace é parcialmente compensado por outras linhas, o que reforça o frete como alavanca e não como correlação incidental.

### 5.2 Valores derivados — com a fórmula à vista

Todos abaixo são álgebra sobre os campos oficiais acima. Nenhum é premissa.

| Valor derivado | Fórmula | Resultado |
|---|---|---:|
| Receita Marketplace (13 meses) | `gap_frete_anual × 13 ÷ (gap_frete_pp × 12)` | R\$ 3.526.291 |
| Receita Marketplace anualizada | `receita_13m ÷ 13 × 12` | R\$ 3.255.038 |
| Participação do canal na receita oficial | `3.526.291 ÷ 16.668.956` | 21,2% |
| Custo de frete anual do canal | `receita_anual × 4,90%` | R\$ 159.497 |
| **Margem de contribuição anual do canal** | `receita_anual × 51,50%` | **R\$ 1.676.345** |
| Margem perdida por 1 p.p. de queda de conversão | `receita_anual × 1% × 51,50%` | R\$ 16.763 |

*Checagem cruzada: refazendo a receita do canal pelo gap de margem (`117.422 × 13 ÷ (0,0361 × 12)`) em vez do gap de frete, chega-se a R\$ 3.252.687 — 0,07% de diferença, atribuível ao arredondamento dos p.p. publicados no `kpis.json`. As duas rotas concordam.*

### 5.3 Contra-hipótese — a pergunta que precede a negociação

**Antes de tratar o gap como vazamento, é preciso testar se ele é um defeito ou um custo de servir.** Um canal de marketplace com margem menor e volume incremental pode ser perfeitamente racional: paga-se comissão e logística da plataforma em troca de demanda que não viria pelos canais próprios.

Os números derivados colocam a questão em proporção:

| | Valor |
|---|---:|
| Margem de contribuição que o canal **entrega** por ano | R\$ 1.676.345 |
| Gap de frete que se busca **recuperar** por ano | R\$ 128.574 |
| **Razão** | **13,0×** |

O gap equivale a **7,7% da contribuição do canal**. Uma intervenção mal calibrada arrisca R\$ 1,68 milhão para perseguir R\$ 128 mil.

**O que os dados não respondem, e precisa ser perguntado ao cliente:** o volume do Marketplace é incremental ou canibaliza os canais próprios? Se for incremental, a margem menor é o preço da demanda adicional e a recomendação correta pode ser *não mexer*. Se for canibalização, o gap é perda real. **`vendas.csv` não tem como distinguir os dois casos** — não há dado de origem de demanda nem de sobreposição de cliente entre canais (e a ressalva R1 torna impossível investigá-la por cliente: 346 IDs para 27.758 pedidos).

> Esta é a pergunta que abre a conversa com o CFO, não o número de R\$ 128 mil. Um gap de margem por canal apresentado sem ela é uma recomendação incompleta.

### 5.4 Cenários de captura e teto de investimento

Condicionados a a) a contra-hipótese acima ser respondida a favor da intervenção e b) o `custo_frete` se revelar contratualmente negociável.

| Cenário | Captura do gap | Benefício bruto/ano | **Teto de investimento para pagar no ano 1** |
|---|---:|---:|---:|
| Conservador | 25% | R\$ 32.144 | R\$ 32.144 |
| Central | 50% | R\$ 64.287 | R\$ 64.287 |
| Otimista | 75% | R\$ 96.431 | R\$ 96.431 |

**Pergunta devolvida ao cliente:** o esforço interno de auditoria contratual e renegociação (Financeiro, Comercial e Jurídico) cabe abaixo de R\$ 32.144 no cenário mais conservador? Se sim, a iniciativa se paga mesmo na hipótese mais pessimista de captura. Se não, ela só existe a partir do cenário central — e isso é uma decisão de alçada, não uma conta da consultoria.

> Nenhum destes cenários é economia garantida. `custo_frete` é um custo **registrado**; a base não informa se é repasse ao cliente, subsídio, comissão contratual ou custo sintético. Esta é a resposta literal ao caso de teste nº 9 do agente.

### 5.5 Guardrail — perdas secundárias

Se a alavanca for **repassar frete ao cliente**, o ganho pode ser devorado pela queda de conversão.

| Cenário de captura | Ganho | Anulado por uma queda de conversão de |
|---|---:|---:|
| 25% | R\$ 32.144 | **1,9 p.p.** |
| 50% | R\$ 64.287 | **3,8 p.p.** |
| 75% | R\$ 96.431 | **5,8 p.p.** |

**Implicação:** o experimento precisa medir **margem E conversão**. Um piloto que reporta apenas economia de frete não sabe se destruiu valor.

*Simplificação declarada: o cálculo não desconta o custo de frete evitado nos pedidos perdidos — é um limite superior da perda, deliberadamente conservador.*

---

## 6. Pipeline priorizado

Ordenado por valor potencial. Nenhuma linha descartada; nenhuma com R\$ defensável hoje.

| Iniciativa | Valor potencial | Confiança | Por que não entra no business case | Experimento | Gate |
|---|---:|---|---|---|---|
| **Devolução** | R\$ 1.247.730/ano (cenário de perda bruta) · R\$ 1.351.707 de margem contábil no período (observado) | hipótese | Margem contábil dos devolvidos (54,1%) é quase igual à dos não devolvidos (54,4%) — a fórmula não desconta devolução. Isso é **exposição**, não perda: sem reembolso, estorno, custo reverso ou destino do produto na base | Apurar estorno real de uma amostra de devoluções | Ponte financeira construída: pedido → devolução concluída → reembolso → custo reverso → destino |
| **Atendimento WISMO** | R\$ 23.022 a R\$ 41.439/ano (automação de 50% a 90%) | hipótese | 10.765 tickets (30,0% do volume, 68/semana). Mas `canal_entrada` mostra onde o ticket **entrou**, não se foi resolvido sem humano. E os R\$ 14,83 do tema vs. R\$ 2,00 do ChatBot são **tabela de custo**, não custo marginal. Como a fração elegível é menor que 100% e o custo marginal não é maior que o tabelado, **esses valores são teto, não estimativa central** | Piloto assistido com elegibilidade por subintenção e grupo de controle | Contenção ≥ 50% sem escalar E CSAT/recontato não pioram |
| **Ruptura Beleza** | R\$ 12.087 a R\$ 48.349 (central R\$ 24.174) | cenário | 96 de 99 rupturas da empresa estão em Beleza (97%), de 1.512 SKUs da categoria. Mas estoque é *snapshot*: a duração é premissa (0,5 a 2 meses). Os 232 SKUs em estoque crítico (R\$ 58.421/mês em risco) são **risco**, nunca somados. A escala de `estoque.csv` e `vendas.csv` não reconcilia — a receita média por SKU saudável (R\$ 251,82/mês) serve para **ranquear**, não para prometer data de ruptura | Instrumentar `dias_sem_estoque` nos 96 SKUs | Duração real medida por ≥ 1 ciclo de reposição |
| **Marketing** | `null` | dado insuficiente | 452% e 18,9×. Ranking direcional é válido (Influenciador ROAS 7,7, margem 52,3%, ticket R\$ 902 > Marketplace ROAS 3,0). O modelo de atribuição foi checado e **não** é a causa — é escala | Pedir base de investimento real por canal, mesma janela | As duas bases reconciliam em escala |
| **Cliente "Em Risco"** | `null` | dado insuficiente | 3.269 clientes (21,8% da base de 15.000), concentrando 12,7% do LTV. Segmento definido pela própria faixa de LTV — "gap de LTV" é **circular** | Régua de retenção medindo recompra real | Taxa de recompra medida sem circularidade com `segmento_rfm` |

**Achado negativo relevante.** Testamos se tickets de "Defeito" e "Troca de Tamanho" levam a mais devolução. **Não levam** — a taxa é praticamente idêntica em todas as categorias (14,5% a 16,4%), inclusive em "Elogio". A conexão intuitiva não existe nesta base, e o agente tem proibição explícita de reintroduzi-la.

---

## 7. O custo do programa — e por que ele não é um ROI

As duas capacidades que os 90 dias entregam — **a ponte financeira da devolução** e o **Agente de Priorização de Iniciativas** — são infraestrutura de decisão, não iniciativas com retorno.

**Calcular ROI sobre elas seria erro de categoria.** A ponte de devolução não gera economia: ela informa se existe economia. O agente não economiza horas de reunião em escala material: ele impede que a empresa comprometa metas sobre números que não se sustentam.

### 7.1 O que o agente entrega, demonstrado por teste

O valor é verificável sem inventar cifra. Quatro dos dez casos do Sprint 1 são quatro erros que a empresa cometeria hoje:

| Caso | O erro que o agente bloqueia |
|---|---|
| nº 9 | Comprometer o gap de frete como economia garantida |
| nº 8 | Somar Marketing + Retenção + Margem num "total do business case" — linhas com `oportunidade_financeira_rs: null` |
| nº 3 | Aceitar um número de slide que contradiz a fonte oficial — exatamente a divergência D1 da Seção 8, viva no notebook hoje |
| nº 5 | Tratar "shelf life causa ruptura" como causa comprovada |

### 7.2 A pergunta que substitui o ROI

**"Quanto custa uma decisão de alocação errada por trimestre?"** Essa pergunta é do CFO, não da consultoria — e a resposta dele define se o programa se paga. A squad entrega o custo de construção; a diretoria compara com o custo do erro que ele evita.

| A decidir com o cliente | Por quê |
|---|---|
| Custo de concluir os Sprints 2 e 3 do agente | A squad pode dimensionar em horas; o valor-hora carregado é do cliente |
| Custo de curadoria contínua do `kpis.json` | Depende de quem for nomeado owner de dados |
| Custo da amostragem de devoluções | Depende do volume que o Financeiro conseguir apurar |
| Custo do esforço de auditoria e renegociação do frete | Comparar com o teto da Seção 5.4 |

**O Sprint 1 é custo afundado** — blueprint, contratos, guardrails, 10 casos de teste e `kpis.json` versionado já estão entregues.

---

## 8. Divergências a corrigir antes do deck

| # | Onde | Diz hoje | `kpis.json` diz | Classificação |
|---|---|---|---|---|
| **D1** | Célula "Diagnóstico executivo por hipótese" | *"custo de frete consome ~8,7% da receita, quase o dobro dos outros canais"* | **4,90% vs. 0,95%** — cinco vezes, não o dobro | **Bloqueante.** É a tabela executiva; alimenta o deck |
| **D2** | Célula "Insight preliminar" (Seção 3) | margem Marketplace ~46,0%, gap ~4,6 p.p., frete 8,7% vs. 2,4–4,8% | 51,50% vs. 55,11%, gap 3,61 p.p. | **Tolerável se rotulado.** É o registro da leitura exploratória por média simples; precisa de rótulo "superada pela ponderada" |
| **D3** | Contradição entre artefatos | Célula 8.1 do notebook indica **automação WISMO** como produto de IA | `blueprint_agente_priorizacao.md` e `sprint1_10_perguntas_teste.md` constroem o **Agente de Priorização** | **Bloqueante.** A mentoria pediu **um** caminho (Etapa 4.2) |

**Proposta da squad para D3, a confirmar antes do deck — não é decisão tomada.** Adotar o Agente de Priorização como caminho único: é o que tem blueprint aprovado, 10 casos de teste versionados e Sprint 1 com nota de aceite, e é um dos três caminhos que a mentoria listou. A automação WISMO não é um agente de decisão — é iniciativa operacional, e permanece no pipeline da Seção 6. **Esta escolha precisa do aceite do time antes de entrar em qualquer slide**, porque contradiz o que o notebook diz hoje.

---

## 9. Riscos

| Risco | Impacto | Mitigação |
|---|---|---|
| O volume do Marketplace é incremental e a intervenção o reduz | Arrisca R\$ 1.676.345/ano de contribuição para perseguir R\$ 128.574 | Responder a contra-hipótese (5.3) **antes** de negociar |
| `custo_frete` é comissão contratual não negociável | Elimina a única linha com R\$ do business case | Auditoria contratual nos primeiros 30 dias |
| Repasse de frete derruba conversão | Ganho anulado a partir de 1,9 p.p. no cenário conservador | Experimento controlado medindo margem **e** conversão |
| D1 e D3 chegam ao deck | O caso de teste nº 3 vira realidade diante do CFO | Correção antes do dia 30; teste automático estendido ao `Dashboard.html` |
| A amostra de devoluções mostra que a perda é próxima de zero | A maior linha do pipeline desaparece | **Resultado legítimo** — é exatamente o que a ponte financeira existe para descobrir |
| Conclusão extrapolada de base sintética | Decisão sobre número que não existe em produção | Ressalva R1 em todo slide com R\$ |
| Uso de dado pessoal no agente | Risco de LGPD | Escopo fechado em agregados; caso de teste nº 6 bloqueia identificação individual |

---

## 10. Decisão solicitada à diretoria

| # | Decisão | Owner | Gate / teto |
|---|---|---|---|
| 1 | **Aprovar a construção da capacidade de medir** — ponte financeira de devolução, reconciliação de marketing e instrumentação de `dias_sem_estoque` | Sponsor executivo | 4 de 4 dependências de dado com owner e prazo |
| 2 | **Responder a contra-hipótese do Marketplace** e, se ela sustentar a intervenção, dar mandato de auditoria e renegociação | Financeiro/Comercial | Esforço abaixo do teto de R\$ 32.144 (cenário conservador) |
| 3 | **Concluir os Sprints 2 e 3 do Agente de Priorização** como infraestrutura de governança do programa | Time de dados/IA | 6/6 casos com o status esperado |
| 4 | **Nomear um owner de dados** para o `kpis.json` | Sponsor executivo | Nenhuma alteração de recorte sem nova versão e hash |

**O que não estamos pedindo:** aprovação de uma meta de economia. Nenhum número deste documento está pronto para virar meta, e dizer o contrário seria o erro que o caso de teste nº 9 existe para impedir.

---

## Anexo A — Rastreabilidade

**Valores oficiais** (`kpis.json`, hash `1c33bed0384a`):

| Número | Campo |
|---|---|
| Margem ponderada Marketplace 51,50% / demais 55,11% / gap 3,61 p.p. / Cohen's d 0,28 | `margem_marketplace.*` |
| Frete 4,90% vs. 0,95% / gap 3,95 p.p. / gap anual R\$ 128.574 | `margem_marketplace.*` |
| Cenários de captura R\$ 32.144 / 64.287 / 96.431 | `margem_marketplace.cenarios_captura_frete_rs` |
| Devolução 14,88% / R\$ 1.351.707 / R\$ 1.247.730 | `devolucao.*` |
| WISMO 30,0% / 68 por semana / 20,5% via ChatBot / R\$ 23.022 a 41.439 | `atendimento_automacao_wismo.*` |
| Ruptura Beleza 6,3% / 15,3% / R\$ 12.087–48.349 / R\$ 58.421 mês | `operacoes_ruptura_beleza.*` |
| Marketing 452% / 18,9× | `marketing_reconciliacao.*` |
| Clientes em risco 3.269 / 21,8% | `retencao_clientes_em_risco.*` |

**Valores de célula do notebook** (não estão no `kpis.json`): população e sensibilidade da Seção 1.1; 2.207 Cancelados e 1.097 Aguardando; 3.639 pedidos devolvidos; margem 54,1% vs. 54,4%; custo por ticket R\$ 14,83 / R\$ 2,00 / R\$ 15,00 / R\$ 45,00; CSAT 3,27 vs. 3,24; 96 de 99 rupturas e 1.512 SKUs de Beleza; R\$ 251,82 por SKU saudável; ROAS 7,7 / 3,0; LTV R\$ 139.092.569 e 8,3×; taxa de devolução por categoria 14,5%–16,4%; cardinalidade de 346 / 445 / 15.000.

**Valores derivados** (fórmula publicada na Seção 5.2): receita Marketplace 13 meses e anualizada; participação de 21,2%; custo de frete anual R\$ 159.497; margem de contribuição anual do canal R\$ 1.676.345; razão 13,0×; margem perdida por p.p. de conversão R\$ 16.763; R\$ 371 por pedido devolvido.

**Premissas de custo:** nenhuma. Ver Seção 0 e Seção 7.2.

**Campos do briefing ausentes nos dados:** `clientes.csv` — `canal_aquisicao`, `recência`; `estoque.csv` — `giro`, `dias_sem_estoque`, `ruptura` (booleana).

---

## Nota de aceite

- [x] Tese declarada e sustentada por seis evidências oficiais
- [x] Cenário de não fazer nada quantificado
- [x] Recorte financeiro declarado (população, janela, unidade, tratamento da devolução)
- [x] Todo número classificado como oficial, derivado ou a decidir — **zero premissas de custo**
- [x] Toda derivação com a fórmula publicada e checagem cruzada por rota alternativa
- [x] Contra-hipótese do canal apresentada antes da recomendação de intervir
- [x] Teto de investimento calculado em vez de custo suposto
- [x] Perdas secundárias quantificadas (guardrail de conversão)
- [x] Limitações da base declaradas antes de qualquer número (R1, R2, R3)
- [x] Divergências entre artefatos registradas; D3 apresentada como proposta, não como decisão
- [ ] D1 corrigido e D2 rotulado no notebook — **pendente, Trilha A do roadmap**
- [ ] D3 confirmada pelo time — **pendente, decisão da squad**

**Critério de aprovação deste documento:** uma pessoa de fora consegue reproduzir qualquer valor a partir do `kpis.json`, dizer de qual das três classes ele é, e explicar por que a recomendação principal não é uma economia.
