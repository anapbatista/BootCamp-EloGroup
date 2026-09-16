# Roadmap 30 / 60 / 90 dias
### Vértice Retail · squad de diagnóstico de dados e IA
Fonte de dados congelada: `kpis.json` (hash `1c33bed0384a`, gerado a partir de `vendas_base_financeira`, jan/2023–jan/2024)

Documento irmão: `business_case.md` · Artefato de processo — entrega obrigatória do case (Seção 9 do briefing).

---

## 1. Princípio do plano

O business case conclui que a Vértice não tem um problema de margem demonstrável, e sim de mensuração. **O roadmap, portanto, entrega capacidade de medir — não uma lista de economias.**

Duas regras estruturam o plano:

**Regra 1 — duas trilhas, dois donos.** Metade do trabalho é da consultoria (corrigir artefatos, construir o agente) e metade é do cliente (auditar contrato, apurar devoluções, instrumentar estoque). Misturar as duas numa só tabela esconde que o programa trava se o cliente não se mover. Elas estão separadas e têm governança diferente.

**Regra 2 — gate, não prazo.** Cada horizonte só avança se o anterior provar algo. Prazo cumprido sem o gate correspondente não conta como progresso.

| Horizonte | Objetivo | Pergunta que responde | Gate |
|---|---|---|---|
| **0–30** | Fechar o fundamento e destravar o dado | *Os números são confiáveis e o cliente vai liberar o que falta?* | Zero divergência de KPI; 4 de 4 dependências com owner e prazo |
| **31–60** | Construir a capacidade de medir | *A devolução tem tamanho? O agente responde e recusa?* | Amostra de devolução apurada; agente com log auditável |
| **61–90** | Medir, decidir e apresentar | *O que vira investimento e o que morre?* | Escala apenas se valor, qualidade e risco atenderem aos critérios |

---

## 2. Ponto de partida — o que já está feito

O Sprint 1 tem nota de aceite em `sprint1_10_perguntas_teste.md`. O roadmap não repete o que existe.

| Item | Artefato | Status |
|---|---|---|
| Decisão escolhida e congelada | `blueprint_agente_priorizacao.md` §1 | Concluído |
| Recorte financeiro congelado | Aprovados, jan/23–jan/24 | Concluído |
| `kpis.json` versionado com hash de conteúdo | `1c33bed0384a` | Concluído |
| Manifesto de fontes · lista faz/não faz · contratos de entrada e saída | blueprint §2, §3, §5, §6 | Concluído |
| 10 casos de teste cobrindo os 7 tipos | `sprint1_10_perguntas_teste.md` | Concluído |
| Teste automático tabela × JSON | notebook §8.3 | Concluído (4 valores) |
| Guardrails e observabilidade | blueprint §8 e §9 | Especificados, não implementados |
| Funções determinísticas | blueprint §4 | Especificadas, não implementadas |
| `politicas_vertice.md` | blueprint §3 | Pendente — declarado "a criar" no próprio blueprint |
| Agente executável | — | Pendente |
| Dashboard | `Dashboard.html` | Existe; não verificado contra o `kpis.json` |

---

## 3. Governança das duas trilhas

| | **Trilha A — Consultoria** | **Trilha B — Cliente** |
|---|---|---|
| **Quem executa** | A squad | Times da Vértice |
| **O que entrega** | Artefatos corrigidos, agente, análises, deck | Dado que não existe hoje e decisões de alçada |
| **Ritmo** | Semanal, controlado pela squad | Quinzenal, controlado pelo Sponsor |
| **Se atrasar** | A squad reprioriza | **O programa trava** — escalar em 5 dias |

**Owners nomeados:**

| Papel | Responsabilidade | Trilha |
|---|---|---|
| Sponsor executivo (COO) | Aprovar gates, destravar dado, arbitrar alçada | B |
| Owner de dados | Curar o `kpis.json`, definir fonte, recorte e acesso | A e B |
| Finanças (Controller) | Auditoria contratual, ponte de devolução, validar teto | B |
| Comercial | Negociação com a plataforma de marketplace | B |
| Supply Chain | Instrumentar `dias_sem_estoque` em Beleza | B |
| Operações/CX | Baseline de contenção e piloto WISMO | B |
| Marketing | Base de investimento real por canal | B |
| Time de dados/IA (squad) | Funções, agente, testes, observabilidade | A |
| Risco/privacidade | PII, acesso, retenção, uso aceitável | A e B |

---

## 4. Horizonte 0–30 dias — Fechar o fundamento

**Objetivo:** eliminar as divergências que impedem o agente de nascer confiável e destravar o dado que o programa inteiro depende.

### Trilha A — Consultoria

| # | Entrega | Critério de aceite |
|---|---|---|
| A1 | **Corrigir D1** — a célula "Diagnóstico executivo" diz *"~8,7% da receita"*; o `kpis.json` diz **4,90% vs. 0,95%**. Derivar o texto da variável calculada | Nenhum literal numérico em célula de markdown da Seção 8 |
| A2 | **Rotular D2** — marcar a célula "Insight preliminar" da Seção 3 como leitura exploratória superada pela média ponderada | Rótulo na própria célula; nenhum número dela reaparece em tabela executiva |
| A3 | **Levar D3 ao time** — decidir formalmente entre o Agente de Priorização (repositório) e a automação WISMO (célula 8.1). A proposta da squad está na Seção 8 do business case; **a decisão não é da consultoria** | Um único caminho declarado em todos os artefatos |
| A4 | **Estender o teste automático (§8.3)** ao `Dashboard.html` e ao deck — hoje cobre 4 valores | Pipeline falha se qualquer artefato divergir do `kpis.json` |
| A5 | **Implementar as funções determinísticas** do blueprint §4 | 4 de 4 testadas isoladamente; nenhum cálculo na LLM |
| A6 | **Criar `politicas_vertice.md`** — guardrails de negócio pendentes no próprio blueprint | Versionado e referenciado pelo agente |
| A7 | **Matriz de evidências do pitch** — cada número com classe (oficial / derivado / a decidir), recorte, fórmula e decisão que informa | Nenhum número no deck sem os quatro campos |

### Trilha B — Cliente

| # | Entrega | Owner | Prazo | Bloqueia |
|---|---|---|---|---|
| B1 | **Contrato vigente com a plataforma de marketplace** — cláusulas de frete e comissão | Finanças + Jurídico | Dia 20 | A Âncora 1 inteira |
| B2 | **Responder a contra-hipótese do Marketplace** — o volume do canal é incremental ou canibaliza os canais próprios? | Comercial | Dia 20 | Se for incremental, a recomendação pode ser não intervir |
| B3 | **Amostra de devoluções** com estorno, custo reverso e destino do produto | Finanças | Dia 45 | A maior linha do pipeline |
| B4 | **Série de `dias_sem_estoque`** por SKU de Beleza | Supply Chain | Dia 45 | Tirar o cenário de ruptura da premissa de duração |
| B5 | **Base de investimento real de marketing** na janela de `vendas.csv` | Marketing | Dia 30 | Qualquer R\$ atribuído a canal |
| B6 | **Nomear o owner de dados** do `kpis.json` | Sponsor | Dia 10 | Governança de toda alteração de recorte |

**KPIs do horizonte**

| Indicador | Meta |
|---|---:|
| Divergências de KPI entre artefatos | 0 |
| Campos do `kpis.json` com R\$ cobertos pelo teste automático | 100% |
| Funções determinísticas implementadas | 4 de 4 |
| Dependências da Trilha B com owner e prazo confirmados | 6 de 6 |

**Gate de passagem**

- [ ] Nenhum KPI diverge entre notebook, `kpis.json`, `Dashboard.html` e deck
- [ ] D1 corrigido, D2 rotulado, D3 decidido pelo time
- [ ] `politicas_vertice.md` criado e funções determinísticas prontas
- [ ] Contrato do marketplace em mãos e contra-hipótese respondida

> **Se o gate falhar na Trilha A:** não construir o agente. Um agente sobre KPI divergente responde com confiança a partir de número errado — exatamente o que o caso de teste nº 3 existe para pegar.
>
> **Se o gate falhar na Trilha B:** o programa não tem Âncora 1. Reposicionar o pitch inteiro sobre a construção da capacidade de medir, que independe do contrato.

---

## 5. Horizonte 31–60 dias — Construir a capacidade de medir

**Objetivo:** dar tamanho à devolução e colocar o agente de pé.

### Trilha A — Consultoria

| # | Entrega | Depende de | Critério de aceite |
|---|---|---|---|
| A8 | **Agente MVP** — fluxo do blueprint §7: checar escopo → identificar período/recorte/KPI → chamar função determinística → montar resposta estruturada → validar → registrar | A5, A6 | Demo responde 6–8 perguntas e recusa 2–4 corretamente |
| A9 | **Validação automática de saída** — todo `RESPONDER` com ao menos 1 evidência contendo `periodo` e `recorte`; nenhuma soma proibida | A8 | Resposta que falha é rebaixada para `PEDIR_ESCLARECIMENTO`, nunca entregue |
| A10 | **Observabilidade (blueprint §9)** — timestamp, pergunta, `kpis_version_hash`, funções chamadas, status, latência, validação | A8 | Toda execução auditável |
| A11 | **Rodada 1 dos 10 casos de teste** | A8, A9 | Status obtido vs. esperado registrado por caso |
| A12 | **Reprocessar o `kpis.json`** com o resultado da amostra de devolução | B3 | Nova versão com novo hash; `dados_necessarios` atualizado |
| A13 | **Deck versão 1** (12 slides, roteiro da Etapa 11) | A12 | Tese da Seção 1 do business case no slide 1; ressalvas R1/R2/R3 presentes |

### Trilha B — Cliente

| # | Entrega | Owner | Critério de aceite |
|---|---|---|---|
| B7 | **Apurar a amostra de devoluções**: pedido → devolução concluída → reembolso/estorno → custo reverso → destino (recuperado / revendido / perda total) | Finanças | Percentual de perda real estimado com intervalo |
| B8 | **Desenhar o experimento de frete** — fração de SKUs, instrumentação de margem **e** conversão, guardrail de conversão | Finanças + Comercial | Proposta apresentada à plataforma |
| B9 | **Iniciar a coleta de `dias_sem_estoque`** nos 96 SKUs de Beleza em ruptura | Supply Chain | Data de início e fim registrada por ruptura |
| B10 | **Baseline de contenção WISMO** — medir hoje, antes de qualquer automação: resolução sem humano, recontato em 24/48h, escalonamento, CSAT, tempo até resolução | Operações/CX | Baseline documentado. **Sem baseline não há efeito incremental — só um número antes e depois sem significado** |

**KPIs do horizonte**

| Indicador | Meta |
|---|---:|
| Casos de teste com status esperado (rodada 1) | ≥ 8 de 10 |
| Respostas `RESPONDER` passando a validação de schema | 100% |
| Execuções com `kpis_version_hash` registrado | 100% |
| Devoluções da amostra com destino do produto identificado | ≥ 80% |

**Gate de passagem**

- [ ] Agente responde 6–8 e recusa 2–4, com log auditável
- [ ] Nenhuma resposta expondo número fora do `kpis.json`
- [ ] Amostra de devolução apurada — a exposição de R\$ 1.351.707 tem intervalo real ou foi refutada
- [ ] Proposta de frete apresentada, se B1 e B2 sustentarem a intervenção

> **Se o gate falhar:** manter o agente em demonstração interna, não diante da diretoria. E não levar nenhum número de devolução ao pitch.

---

## 6. Horizonte 61–90 dias — Medir, decidir e apresentar

**Objetivo:** substituir premissa por medição e pedir uma decisão.

### Trilha A — Consultoria

| # | Entrega | Depende de | Critério de aceite |
|---|---|---|---|
| A14 | **Rodada final dos 10 casos de teste**, com relatório antes/depois dos ajustes | A11 | **6/6 dos casos críticos** com status esperado (critério do Sprint 1) |
| A15 | **Relatório de avaliação do agente** — precisão, utilidade, taxa de recusa correta, segurança, latência e **custo real por execução** | A14 | Custo medido, entregue ao cliente para comparar com o custo do erro evitado |
| A16 | **Teste de utilidade com usuário real** — o COO usa o agente para preparar uma reunião de alocação de verdade, e as horas são cronometradas | A14 | Esforço de preparação **medido**, não suposto |
| A17 | **Business case v2** — devolução reclassificada, ruptura com duração real, custo do programa preenchido pelo cliente | A15, B11, B12, B13 | Nenhum campo "a decidir" em aberto |
| A18 | **Governança e riscos** — PII, acesso, retenção de log, humano no circuito, política de recusa, resposta a alucinação | A10, A6 | Aprovado por Jurídico/Compliance |
| A19 | **Backlog priorizado dos demais módulos** (copiloto de gestão, relatório executivo, automação WISMO) — como backlog, **não** como promessa | A17 | Cada módulo com a decisão que habilita e o pré-requisito de dado |
| A20 | **Apresentação final + demonstração de 5 minutos** — caso normal (nº 10), ambíguo (nº 2) e recusa (nº 9) | A17, A18 | Ensaiado; pedido de decisão explícito no último slide |

### Trilha B — Cliente

| # | Entrega | Owner | Critério de aceite |
|---|---|---|---|
| B11 | **Resultado do frete** — repasse obtido e efeito medido em margem **e** conversão | Finanças + Comercial | Efeito nas duas dimensões, nunca só custo |
| B12 | **Duração real de ruptura em Beleza**, medida por ≥ 1 ciclo de reposição | Supply Chain | Cenário substituído por número medido ou descartado |
| B13 | **Dimensionar o custo do programa** — construção do agente, curadoria do `kpis.json`, amostragem e esforço de renegociação | Sponsor + Controller | Comparado ao teto de R\$ 32.144 a R\$ 96.431 da Seção 5.4 do business case |

**KPIs do horizonte**

| Indicador | Meta |
|---|---:|
| Casos de teste com status esperado | 6/6 críticos |
| Respostas expondo número fora do `kpis.json` | 0 |
| Queda de conversão no Marketplace, se houver repasse | ≤ 1,5 p.p. |
| Campos "a decidir" do business case preenchidos com valor medido | 4 de 4 |

**Gate de decisão de escala** — as três condições, simultaneamente:

| Dimensão | Critério |
|---|---|
| **Valor** | Custo do programa **medido** abaixo do teto que o benefício observado sustenta |
| **Qualidade** | 6/6 casos com status esperado; nenhuma soma proibida em nenhuma execução |
| **Risco** | Zero exposição de dado individual; `politicas_vertice.md` aplicado em 100% das execuções |

**Quatro saídas possíveis, todas legítimas:**

| Resultado | Decisão |
|---|---|
| **Continuar** | Agente na rotina da reunião de alocação; abrir o próximo módulo do backlog |
| **Ajustar** | Uso assistido, escopo estreitado, mais um ciclo de 45 dias |
| **Interromper** | Desligar o agente e realocar o esforço para a frente que se mostrou maior |
| **Reposicionar** | Se a amostra mostrar que a perda de devolução é próxima de zero e o frete não for negociável, o programa vira exclusivamente construção de capacidade de medir — e isso continua sendo a recomendação certa |

---

## 7. Riscos do plano

| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Trilha B não se move | Alta | Trava 60 e 90 dias | Pedido formal no dia 1 com owner nomeado; escalada ao Sponsor em 5 dias |
| Contra-hipótese mostra que o Marketplace é incremental | Média | A Âncora 1 deixa de existir | **Resultado legítimo** — evita destruir R\$ 1.676.345/ano de contribuição para perseguir R\$ 128.574 |
| `custo_frete` é comissão contratual não negociável | Média | Idem | Auditoria antecipada para o dia 20 |
| Amostra mostra perda de devolução próxima de zero | Média | A maior linha do pipeline desaparece | É o propósito da ponte financeira — descobrir, não confirmar |
| Agente reprova em um caso de recusa | Média | Não passa no gate do Sprint 3 | Estreitar escopo e reforçar guardrail, nunca relaxar o critério |
| Volume de entregas excede a capacidade da squad | Média | Entrega parcial em 90 dias | Trilha A tem 20 entregas em 3 horizontes; repriorizar dentro do horizonte, nunca cortar gate |
| KPI diverge após alguma edição | Baixa | Perda de credibilidade | Teste automático estendido (A4) + `kpis_version_hash` em cada execução |
| Conclusão extrapolada de base sintética | Média | Decisão sobre número inexistente em produção | Ressalva R1 do business case em todo slide com R\$ |

---

## 8. Visão de uma página

```
DIA 0 ─────────── DIA 30 ──────────── DIA 60 ──────────── DIA 90
   │                 │                    │                   │
   │  FECHAR O       │  CONSTRUIR A       │  MEDIR, DECIDIR   │
   │  FUNDAMENTO     │  CAPACIDADE        │  E APRESENTAR     │
   │                 │                    │                   │
 A ├─ D1/D2/D3       ├─ Agente MVP        ├─ 6/6 casos        │
   ├─ Teste auto.    ├─ Observabilidade   ├─ Custo real       │
   ├─ Funções det.   ├─ 10 casos rodada 1 ├─ Business case v2 │
   ├─ politicas.md   ├─ kpis.json v2      ├─ Governança       │
   ├─ Matriz evid.   ├─ Deck v1           ├─ Apresentação     │
   │                 │                    │                   │
 B ├─ Contrato mkt   ├─ Amostra devolução ├─ Resultado frete  │
   ├─ Contra-hipótese├─ Experimento frete ├─ Duração ruptura  │
   ├─ Owner de dados ├─ Coleta estoque    ├─ Custo do programa│
   ├─ Pedido de dado ├─ Baseline WISMO    │                   │
   ▼                 ▼                    ▼                   ▼
 GATE: zero        GATE: devolução      GATE: custo         DECISÃO:
 divergência;      com intervalo;       medido < teto;      continuar /
 contrato em mãos  agente auditável     6/6 casos           ajustar /
                                                            interromper /
                                                            reposicionar
```

---

## Nota de aceite

- [x] Trilhas separadas por dono, com governança e consequência de atraso distintas
- [x] Cada horizonte com objetivo, entregas, dependências, KPIs e gate verificável
- [x] Dependências do cliente isoladas, com data-limite e o que cada uma bloqueia
- [x] O que já está concluído (Sprint 1) reconhecido e não repetido
- [x] Toda premissa "a decidir" do business case com entrega explícita que a substitui por medição (A15, A16, B13)
- [x] D3 tratada como decisão do time (A3), não como escolha da consultoria
- [x] Quatro saídas no gate final, incluindo interromper e reposicionar
- [x] Nenhum prazo apresentado como progresso sem o gate correspondente

**Critério de aprovação deste documento:** uma pessoa de fora consegue dizer, para qualquer entrega, quem é o dono, de que trilha ela é, do que depende, e o que precisa ser verdade para o programa avançar — sem perguntar a ninguém.
