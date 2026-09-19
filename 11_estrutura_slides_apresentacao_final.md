# Estrutura da Apresentação Final — 12 slides · ~10 minutos
### Vértice Retail — Diagnóstico, Agente de Priorização e Business Case

> Fontes: `01_diagnostico_executivo.md`, `02_analises_insights.md`, `05_blueprint_agente_priorizacao.md`, `06_sprint_10_perguntas_teste.md`, `08_v2_bussiness_case.md`, `09_v2_roadmap_30_60_90.md`, `10_governanca_riscos.md`.

---

## Slide 1 — Tese executiva
**Título:** "A Vértice não tem um problema de margem — tem um problema de capacidade de medir"

- Margem de contribuição estável em **54,34%** ao longo de 13 meses — sem colapso generalizado de rentabilidade.
- Recomendação central: investir os próximos 90 dias em fechar **5 lacunas de medição** (devolução, marketing, retenção, estoque, atendimento) — não prometer uma economia que os dados ainda não sustentam.
- Única frente com número já defensável hoje: **gap de frete no Marketplace** (R$ 32 mil a R$ 96 mil/ano).
- Pedido à diretoria: aprovar a construção da capacidade de medir + destravar a decisão sobre o Marketplace.

---

## Slide 2 — Pergunta, escopo e recorte
**Título:** O que foi perguntado e sobre qual base respondemos

- Pergunta original: como usar dados e IA para melhorar rentabilidade, eficiência operacional e qualidade de decisão nos próximos 90 dias.
- Recorte financeiro único: pedidos com pagamento **Aprovado**, jan/2023–jan/2024 → 24.454 de 27.758 pedidos (2.207 cancelados e 1.097 pendentes excluídos).
- Limitações que qualificam todo o resto da apresentação: fontes com janelas de tempo diferentes; concentração incomum de pedidos em poucos clientes; marketing e vendas não reconciliam (4x de diferença).

---

## Slide 3 — O que os dados confirmam
**Título:** Três mensagens com evidência

1. **Margem estável** — nenhum canal, categoria ou período mostra colapso de rentabilidade.
2. **Marketplace tem gap de margem (3,61 p.p.) explicado pelo frete** — custo de frete consome 4,9% da receita do canal, contra 0,95% nos demais (gap de 3,95 p.p.).
3. **Atendimento concentrado**: "onde está meu pedido" = 30% dos chamados (~68/semana); automação já testada entrega satisfação equivalente ao humano por uma fração do custo.

---

## Slide 4 — O que os dados não respondem
**Título:** Lacunas e riscos de interpretação

- **Devolução**: 15% dos pedidos, R$ 1,3 milhão de margem contábil exposta — não se sabe se foi reembolsada, revendida ou perdida.
- **Marketing**: ranking direcional entre canais é válido, mas investimento registrado é 4x a receita real da janela — sem valor em R$.
- **Retenção**: 22% da base "em risco", mas calcular o ganho de recuperá-los seria circular (mesma métrica usada para definir o grupo).
- **Achado negativo relevante**: hipótese de que chamados de defeito/troca geram mais devolução foi testada e **refutada**.

---

## Slide 5 — Iniciativa prioritária 1: Frete no Marketplace
**Título:** Valor, mecanismo, piloto e gate

- **Valor**: R$ 32 mil a R$ 96 mil/ano de margem recuperável, a depender do % de captura do gap (25/50/75%).
- **Mecanismo**: frete é a causa quase integral do gap de margem do canal (margem anual do canal: R$ 1,68 milhão — 13x maior que o gap de R$ 129 mil).
- **Piloto**: auditoria contratual + teste controlado medindo margem **e** conversão ao mesmo tempo (uma queda de 1,9 a 5,8 p.p. na conversão anula o ganho).
- **Gate**: responder se o volume do canal é incremental ou canibaliza vendas próprias — antes de qualquer renegociação.

---

## Slide 6 — Iniciativa prioritária 2: Automação de atendimento (WISMO)
**Título:** Valor, mecanismo, piloto e gate

- **Valor**: R$ 23 mil a R$ 41 mil/ano, dependendo do quanto puder ser automatizado com segurança.
- **Mecanismo**: canal automatizado já entrega satisfação equivalente ao atendimento humano, a uma fração do custo tabelado.
- **Piloto**: monitorado, medindo contenção (resolução sem humano), taxa de recontato e custo real por chamado.
- **Gate**: medir a linha de base do atendimento **antes** de automatizar — sem isso não há como comprovar melhora.

---

## Slide 7 — Produto de dados e IA: Agente de Priorização de Iniciativas
**Título:** Usuário, decisão, arquitetura e guardrails

- **Usuário e decisão**: COO/CFO (ou analista que prepara a reunião) decidindo em qual iniciativa investir dado orçamento/esforço limitado no ciclo.
- **Arquitetura**: agente ReAct (LangGraph + LiteLLM); a LLM nunca calcula, só chama funções determinísticas sobre o `kpis.json` (`get_iniciativa`, `comparar_cenarios`, `rankear_iniciativas`, `checar_escopo`).
- **Guardrails**: nunca soma Marketing/Retenção em R$; nunca apresenta cenário como economia garantida; nunca reintroduz causalidade já refutada; recusa dado individual de cliente.
- **Contrato de saída**: toda resposta traz status, evidência, nível de confiança e limitações — validado antes de chegar ao usuário.

---

## Slide 8 — Demo do agente
**Título:** Caso normal, ambíguo e recusa

- **Normal**: *"Tenho R$ 50 mil de esforço este trimestre, onde alocar?"* → `RESPONDER` com ranking e evidência por item.
- **Ambíguo**: *"Quanto vamos economizar com o frete do Marketplace?"* → `PEDIR_ESCLARECIMENTO` (falta escolher o cenário de captura).
- **Recusa**: *"Some marketing + retenção + margem e me dê o total"* → `RECUSAR`, explicando a soma proibida.
- Validado contra bateria de **10 casos de teste**, cobrindo os 7 tipos (suportada, ambígua, número inconsistente, não suportada, causalidade indevida, dado sensível, falha de fonte).

---

## Slide 9 — Business case
**Título:** Cenários, custos, sensibilidade e break-even

- Três cenários de captura do frete: **conservador** (25% → R$ 32,1 mil), **central** (50% → R$ 64,3 mil), **otimista** (75% → R$ 96,4 mil) — cada um define o investimento máximo que ainda se paga no ano 1.
- Sensibilidade: o ganho projetado pode ser anulado por uma queda de conversão de apenas 1,9 a 5,8 p.p. — por isso o piloto mede margem e conversão juntos.
- Não é um ROI tradicional: a pergunta central é **"quanto custa, por trimestre, uma decisão tomada com um número errado?"**
- As outras 5 iniciativas do pipeline seguem sem valor calculável até fechar a lacuna de medição de cada uma.

---

## Slide 10 — Roadmap 30–60–90
**Título:** Entregas, responsáveis, dependências e gates

- **0–30 dias**: recorte oficial validado, contrato de marketplace, matriz de evidências, ferramenta testada nos 10 casos.
- **31–60 dias**: amostra de devolução apurada, ferramenta revalidada, experimento de frete desenhado, linha de base do atendimento.
- **61–90 dias**: resultado real do frete, duração real de ruptura em Beleza, custo real do programa, business case final sem campos "a decidir".
- **Gate final**: valor (custo abaixo do teto sustentado pelo benefício), qualidade (6/6 casos críticos), risco (zero exposição de dado individual).

---

## Slide 11 — Governança e avaliação
**Título:** Qualidade, logs, humano no circuito e métricas

- Princípio: o agente **nunca calcula** — só consulta o `kpis.json` e narra; toda resposta é validada por schema antes de chegar ao usuário.
- Três controles contra alucinação: consulta em vez de cálculo, formato fixo validado automaticamente, reconhecimento de 7 situações de não-resposta direta.
- Privacidade: escopo restrito a dados agregados; recusa automática de identificação individual (testado e aprovado).
- Alçada: ações proibidas (mudar orçamento, desligar canal, aprovar desconto) e qualquer valor acima de R$ 100 mil são sempre escalados a um humano.

---

## Slide 12 — Decisão solicitada
**Título:** O que a diretoria precisa aprovar agora

1. Aprovar a construção da capacidade de medir as 5 lacunas identificadas, cada uma com responsável e prazo.
2. Responder à pergunta de incrementalidade do Marketplace e, se favorável, autorizar auditoria contratual e renegociação dentro do teto conservador.
3. Autorizar a conclusão do agente de priorização como infraestrutura de governança do programa.
4. Nomear um responsável único pela base de indicadores.

> **Não estamos pedindo aprovação de uma meta de economia** — estamos pedindo aprovação para construir a capacidade de saber, com confiança, se ela existe.
