# Perguntas da Banca — Preparação (5 minutos)
### Vértice Retail — perguntas prováveis fora do escopo direto dos 12 slides

Organizado por tema. Cada resposta é um ponto de partida curto — na hora, respondam em 20-30s e ofereçam aprofundar depois se a banca quiser.

---

## 1. Dados, premissas e cálculos

**"Por que excluir os pedidos cancelados e pendentes do cálculo de margem?"**
> Um pedido cancelado não é uma venda — mas estava sendo contado como se fosse, o que inflava artificialmente a margem em todas as leituras anteriores. Excluí-los (2.207 cancelados + 1.097 pendentes) já foi, em si, uma correção de precisão, não uma escolha arbitrária.

**"Por que usar soma ponderada em vez de média simples por pedido para comparar margem entre canais?"**
> A média simples é distorcida por um pequeno número de pedidos com margem fortemente negativa. A soma ponderada reflete o peso real de cada canal na receita total e é a métrica que não se inverte quando um outlier entra ou sai da base.

**"Como vocês confirmaram que o número do gap de frete (R$ 129 mil) está certo?"**
> Calculamos por dois caminhos independentes — partindo do gap de frete e partindo do gap de margem — e as duas rotas convergem com diferença inferior a 0,1%, atribuível a arredondamento. Essa checagem cruzada é o motivo da confiança no número.

**"A base tem um único cliente respondendo por 11 mil de 28 mil pedidos — isso não invalida tudo?"**
> Não invalida, mas condiciona a leitura: tratamos todo valor financeiro como ordem de grandeza para apoiar uma decisão, não como número definitivo. Antes de qualquer valor virar meta de orçamento, ele precisa ser recalculado sobre a base de produção completa, sem essa concentração.

**"Por que não estimar um valor de devolução, mesmo sabendo que existe risco de R$ 1,3 milhão?"**
> Porque não temos a informação central: o que acontece de fato depois da devolução (reembolso, estorno, revenda, perda). Qualquer número aqui seria uma suposição vestida de dado — preferimos mostrar a exposição contábil e apontar o próximo passo (mapear o fluxo ponta a ponta) do que inventar uma taxa de perda.

**"Por que não simplesmente assumir que toda devolução vira perda, para ter um número conservador?"**
> Isso não seria conservador, seria arbitrário no sentido oposto — infla o número tanto quanto assumir zero perda o subestima. As duas pontas do intervalo existem nos dados internos como cenário, mas não colocamos isso como manchete do documento porque nenhuma das duas foi observada, só a exposição contábil.

**"Por que marketing não recebe um valor em reais, já que existe um ranking entre canais?"**
> Porque o ranking é direcional (qual canal é relativamente melhor) e não depende da escala das bases — mas qualquer valor em reais dependeria de comparar investimento com receita, e essas duas bases não reconciliam (investimento é 4x a receita real da mesma janela). Testamos inclusive se isso viria de viés de atribuição entre canais — não vem, os modelos se distribuem quase igual entre eles. O problema é de escala das fontes, não de método.

**"De onde veio o intervalo de meio mês a dois meses para a duração da ruptura em Beleza?"**
> É um cenário de trabalho da squad, não um dado observado — a base só tem uma fotografia do estoque no momento atual, não um histórico contínuo de disponibilidade por produto. Por isso o valor de receita potencial (R$ 12 mil a R$ 48 mil) é apresentado como faixa, e o próximo passo do roadmap é instrumentar esse acompanhamento continuamente.

**"Por que calcular o ganho de recuperar um cliente 'em risco' seria circular?"**
> Porque o próprio segmento "em risco" é definido usando a mesma métrica de valor histórico que se usaria para calcular quanto se ganharia ao "recuperar" esse cliente para outro segmento — na prática, a conta apenas recalcularia a definição do grupo, não mediria um ganho real. Por isso propomos medir recompra real ao longo do tempo, em vez do valor histórico acumulado.

---

## 2. O agente de priorização (arquitetura e limites técnicos)

**"Por que a LLM nunca calcula — qual seria o risco se calculasse?"**
> Um modelo de linguagem pode produzir um número plausível, mas incorreto, com a mesma confiança de um número certo — é o principal vetor de alucinação em ferramentas de IA para decisão executiva. Ao restringir a LLM a decidir *qual função chamar* e narrar a saída literal dela, eliminamos essa classe de erro por construção, não por instrução de prompt (que pode falhar).

**"O que acontece se o `kpis.json` for atualizado — o agente precisa ser re-treinado?"**
> Não — o agente não é treinado sobre os dados, ele consulta o arquivo em tempo de execução. Atualizar o `kpis.json` é suficiente, mas isso dispara a exigência de revalidar a bateria de testes de aceite antes de qualquer uso real com a nova versão (é um dos controles de governança).

**"Como o agente decide entre responder, pedir esclarecimento ou recusar?"**
> Segue um fluxo determinístico: primeiro checa escopo, depois identifica se período/recorte/cenário necessários estão claros na pergunta, só então chama a função. Se a pergunta exige causalidade, previsão ou soma não suportada, o passo 4 do fluxo força recusa antes mesmo de tentar montar uma resposta.

**"O que acontece se a pergunta for completamente fora do domínio, tipo 'qual a capital da França'?"**
> `checar_escopo` retorna fora do escopo e o agente recusa, sem tentar responder com conhecimento geral do modelo — o agente é intencionalmente restrito às 5 iniciativas diagnosticadas.

**"Quantos dos casos de teste o agente está passando hoje?"**
> *(Confirmem o número mais atual antes da apresentação — na última rodada registrada o agente estava abaixo do critério de aceite de 6/8 a 8/10. Se ainda for esse o caso, a resposta honesta é: "Estamos em [X]/10 na última rodada; o critério de aceite é [Y]; os casos que ainda falham são [tipo], e a próxima iteração ataca exatamente isso." Uma banca de bootcamp valoriza mais transparência sobre o que ainda não funciona do que uma alegação de 10/10 não verificável.)*

**"Qual modelo de linguagem está por trás do LiteLLM, e por que essa escolha?"**
> *(Preencham com o modelo efetivamente configurado no notebook — LiteLLM é uma camada de abstração, não um modelo; a banca pode querer saber o provider real usado nos testes.)*

**"O agente mantém contexto entre perguntas, ou cada pergunta é isolada?"**
> *(Verifiquem no notebook se há memória de conversa entre chamadas ou se cada pergunta reinicia o estado — isso muda a resposta sobre perguntas de acompanhamento tipo "e se eu mudar o peso do critério X?".)*

**"Quanto custa, em tokens ou em R$, cada execução do agente?"**
> Esse dado está previsto no campo `latencia_ms` / `tokens_usados` do log de observabilidade (Seção 9 do blueprint), mas o cálculo de custo real por execução só é entregue formalmente na Etapa 61-90 do roadmap, junto ao relatório de avaliação da ferramenta. Se ainda não rodaram esse número, digam isso diretamente.

**"Como o agente evita alucinar um argumento de função (ex.: inventar o nome de uma iniciativa que não existe)?"**
> *(Se houver validação de schema/enum nos argumentos das function calls, mencionem — isso é uma defesa adicional que vale citar se implementada.)*

---

## 3. Business case e ROI

**"Por que não comparar o custo do programa inteiro com o valor total do pipeline de oportunidades?"**
> Porque quatro das seis iniciativas ainda não têm valor calculável — somar um número real (frete) com faixas não confirmadas de outras frentes produziria um total artificialmente maior e violaria a mesma disciplina que aplicamos ao proibir a soma de marketing/retenção. Preferimos mostrar o payback isolado do frete e tratar o resto como custo de descobrir se existe valor.

**"Como chegaram ao teto de alçada de R$ 100 mil para escalonamento humano?"**
> *(Se esse número veio de uma política real da Vértice ou foi um valor de referência definido pela squad para a demonstração, expliquem a origem — a banca pode perguntar se é um número real do cliente ou um placeholder do exercício.)*

**"O argumento de que a margem do canal (R$ 1,68 milhão) é 13x o gap (R$ 129 mil) não é só para desencorajar a ação?"**
> Não é uma recomendação de não agir — é uma recomendação de sequenciar: primeiro responder a pergunta de incrementalidade, só depois negociar. O ponto é dimensionar o risco de uma renegociação mal calibrada antes de comprometer volume que talvez seja incremental.

---

## 4. Governança, privacidade e riscos

**"Como garantem que um dado 'agregado' não permite reidentificar um cliente, especialmente com a concentração que vocês mesmos apontaram?"**
> O escopo da ferramenta bloqueia qualquer consulta que peça identificação individual, independentemente de como for formulada — não é uma boa prática informal, é uma regra testada (Seção 2 da governança). Mas é uma pergunta justa: com poucos clientes concentrando muito volume, um agregado muito granular (ex.: "o cliente que fez 40% dos pedidos") poderia reidentificar por exclusão — vale reconhecer isso como um risco residual a monitorar, não fingir que está 100% resolvido.

**"Quem revisa os logs de execução do agente, e com que frequência?"**
> Está definido como responsabilidade do time de dados e IA revalidar a bateria de testes a cada atualização da fonte, mas a política de retenção do histórico de uso (quanto tempo guardar, quem acessa) é explicitamente listada no documento de governança como **decisão ainda pendente da Vértice** — é honesto dizer isso se perguntados.

**"O que acontece se o agente recusar algo que deveria ter respondido (falso positivo)?"**
> Isso conta contra o critério de aceite da bateria de testes — uma ferramenta que recusa demais é tratada como tão arriscada quanto uma que nunca recusa. Não há hoje um mecanismo automático de "apelação" da recusa; isso ficaria para uma iteração futura.

---

## 5. Perguntas de limite (a banca testando se vocês sabem dizer "não sabemos")

- "Vocês testaram isso com volume real de uso simultâneo?" → **Não** — o teste de aceite cobriu cenários individuais, não carga de operação (está listado como pendência aberta no documento de governança).
- "Existe um processo formal para alguém adicionar uma nova regra de guardrail no futuro?" → **Ainda não** — depende de a Vértice nomear quem tem autoridade para alterar essas regras (também listado como pendência aberta).
- "Esse business case já foi validado com o CFO real da Vértice?" → Sejam honestos sobre o estágio do projeto (exercício de bootcamp / diagnóstico simulado) se a banca perguntar isso diretamente.

---

## Como usar isso nos 5 minutos
- Não tentem decorar respostas longas — cada bullet acima já está no tamanho de uma resposta falada.
- Se a pergunta cair fora de tudo isso, é mais seguro dizer "não temos esse número validado ainda, mas o próximo passo do roadmap para isso é [X]" do que inventar uma resposta na hora — é literalmente o princípio que vocês estão defendendo no agente.
- Três pontos marcados com *(preencham)* dependem de detalhes do notebook/configuração do agente que só vocês têm — revisem antes da apresentação.
