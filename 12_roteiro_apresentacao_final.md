# Roteiro da Apresentação Final — ~10 minutos
### Vértice Retail · corresponde a `11_estrutura_slides_apresentacao_final.md`

Tempos são sugestões — ajustem no ensaio. Somam ~9h50 a 10min, deixando margem para transição entre quem fala.

---

### Slide 1 — Tese executiva (~45s)
"A pergunta que abriu este projeto foi: onde está o vazamento de margem da Vértice, e o que fazer a respeito? A resposta que os dados devolveram não foi a que se esperava. A margem de contribuição da empresa está em 54,34%, estável ao longo de treze meses — não existe hoje um colapso de rentabilidade generalizado. O que encontramos foi outra coisa: cinco frentes onde a Vértice não consegue medir, hoje, se existe ou não uma oportunidade real. Por isso, a recomendação que vamos apresentar não é uma meta de economia — é um plano para construir, nos próximos 90 dias, a capacidade de medir essas frentes. A exceção é o frete do Marketplace, e vamos mostrar por quê."

---

### Slide 2 — Pergunta, escopo e recorte (~35s)
"Para chegar até aqui, fixamos um recorte único: só pedidos com pagamento efetivamente aprovado, entre janeiro de 2023 e janeiro de 2024 — 24.454 pedidos válidos. Excluímos pedidos cancelados e pendentes, que estavam inflando as métricas de margem antes desta análise. E é importante alinhar três limitações que valem para tudo que vem a seguir: as fontes cobrem janelas de tempo diferentes, há concentração incomum de pedidos em poucos clientes, e marketing não reconcilia com vendas."

---

### Slide 3 — O que os dados confirmam (~60s)
"Três descobertas sustentam o restante da apresentação. Primeiro: a margem é estável — não há sinal de colapso em nenhum canal ou categoria. Segundo: o Marketplace tem uma margem 3,6 pontos percentuais menor que os demais canais, e a causa quase inteira disso é o frete, que consome cinco vezes mais receita nesse canal do que nos outros. Terceiro: no atendimento, um único tipo de chamado — 'onde está meu pedido' — responde por 30% do volume, e já existe uma automação testada que resolve isso com a mesma satisfação do atendimento humano, por uma fração do custo."

---

### Slide 4 — O que os dados não respondem (~45s)
"Mas é igualmente importante mostrar onde os dados param. Mais de R$ 1,3 milhão de margem contábil está em pedidos devolvidos, e não sabemos se esse valor foi reembolsado, revendido ou perdido de verdade. O ranking entre canais de marketing é válido, mas o investimento registrado não bate com a receita real — por isso, nenhum valor em reais pode ser atribuído a marketing hoje. E o grupo de clientes 'em risco', que é 22% da base, não pode virar uma conta financeira sem cairmos numa circularidade. Testamos até uma hipótese intuitiva do time de atendimento — e os dados a refutaram."

---

### Slide 5 — Iniciativa prioritária 1: Frete no Marketplace (~65s)
"A primeira iniciativa que recomendamos priorizar é o frete do Marketplace — porque é a única com um número já defensável hoje: entre R$ 32 mil e R$ 96 mil de margem recuperável por ano, dependendo de quanto do gap conseguirmos negociar. Mas antes de qualquer negociação, existe uma pergunta que precisa vir primeiro: esse canal traz vendas incrementais, ou está apenas substituindo vendas que já aconteceriam nos canais próprios? Essa pergunta importa porque a margem anual que o canal já entrega — R$ 1,68 milhão — é treze vezes maior que o gap que estamos tentando recuperar. Por isso, o piloto recomendado é uma auditoria contratual seguida de um teste controlado, medindo margem e conversão ao mesmo tempo."

---

### Slide 6 — Iniciativa prioritária 2: Automação de atendimento (~50s)
"A segunda frente é a automação do atendimento sobre status de pedido — é a que tem o caminho mais rápido de validação. O ganho estimado é entre R$ 23 mil e R$ 41 mil por ano, e o canal automatizado já demonstrou entregar a mesma satisfação do atendimento humano. Mas, antes de expandir isso, propomos medir a linha de base atual do atendimento — sem esse ponto de partida, não temos como provar, depois, que a automação de fato melhorou alguma coisa."

---

### Slide 7 — Produto de dados e IA: Agente de Priorização (~55s)
"Para sustentar essas decisões — e as próximas — ao longo do programa, desenvolvemos um agente de priorização de iniciativas. Ele foi desenhado para o COO ou CFO da Vértice, no momento da reunião de alocação de orçamento: dado um esforço limitado, em qual iniciativa investir primeiro. A arquitetura usa LangGraph e LiteLLM, mas o ponto central é este: o modelo de linguagem nunca calcula um número — ele só decide qual função determinística chamar sobre a base oficial de indicadores, e depois narra o resultado. Os guardrails impedem, por construção, somar marketing ou retenção em reais, apresentar um cenário como garantia, ou responder sobre um cliente individual."

---

### Slide 8 — Demo do agente (~55s)
"Vamos ver três exemplos rápidos de como isso funciona na prática. [Demonstrar ou narrar] Quando perguntamos 'tenho R$ 50 mil de esforço este trimestre, onde alocar', o agente responde com um ranking e a evidência de cada item. Quando a pergunta é ambígua — 'quanto vamos economizar com o frete' sem especificar o cenário — ele pede esclarecimento em vez de inventar um número. E quando pedimos para somar marketing, retenção e margem num total só, ele recusa e explica por que essa soma é proibida. Isso foi validado contra dez casos de teste, cobrindo os sete tipos de situação que o agente precisa reconhecer."

---

### Slide 9 — Business case (~65s)
"Em termos financeiros, o frete do Marketplace tem três cenários: conservador, capturando 25% do gap, com ganho de R$ 32,1 mil; central, com R$ 64,3 mil; e otimista, com R$ 96,4 mil. Cada um desses valores é também o teto de investimento que ainda se paga no primeiro ano. Um ponto de atenção: se a forma de captura reduzir a conversão de vendas em apenas 1,9 a 5,8 pontos percentuais, o ganho é anulado — por isso o piloto precisa medir as duas coisas juntas. E vale reforçar: isso não é um business case tradicional de ROI. A pergunta que estamos trazendo à diretoria é outra — quanto custa, por trimestre, uma decisão de alocação tomada com base num número que não se sustenta?"

---

### Slide 10 — Roadmap 30-60-90 (~50s)
"O plano de trabalho está dividido em três horizontes. Nos primeiros 30 dias, fechamos o recorte oficial, obtemos o contrato do Marketplace e testamos a ferramenta nos dez casos. De 31 a 60 dias, apuramos a amostra real de devolução e desenhamos o experimento de frete. De 61 a 90, medimos o resultado real do frete e da ruptura, e fechamos um business case final sem nenhum campo 'a decidir'. Cada horizonte só avança se o gate correspondente for cumprido — valor, qualidade e risco."

---

### Slide 11 — Governança e avaliação (~40s)
"Todo esse desenho é sustentado por um princípio simples: a ferramenta nunca calcula, apenas consulta uma base auditada e narra o resultado, e toda resposta passa por uma validação automática antes de chegar a quem perguntou. Ela opera só sobre dados agregados, recusa qualquer tentativa de identificar um cliente individual, e qualquer decisão acima de R$ 100 mil, ou que exija executar uma ação, é sempre escalada para um humano."

---

### Slide 12 — Decisão solicitada (~35s)
"Por fim, o que pedimos à diretoria hoje são quatro decisões: aprovar a construção da capacidade de medir as cinco lacunas, cada uma com responsável e prazo; responder à pergunta de incrementalidade do Marketplace e autorizar a auditoria dentro do teto conservador; autorizar a conclusão do agente de priorização como parte da governança do programa; e nomear um responsável único pela base de indicadores. Para deixar claro: não estamos pedindo para aprovar uma meta de economia. Estamos pedindo para construir a capacidade de saber, com confiança, se ela existe."

---

## Notas de apresentação
- Pratiquem a transição do Slide 4 para o 5: é o ponto onde a apresentação vira de "diagnóstico" para "recomendação" — vale uma pausa curta.
- No Slide 8 (demo), se houver tempo real de tela, reduzam o texto falado e deixem a tela carregar; se for só narrado, mantenham os três exemplos curtos.
- Guardem 30 a 60 segundos de folga para perguntas ao final, mesmo dentro de uma janela fixa de 10 minutos.
