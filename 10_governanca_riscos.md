# Governança e Riscos
### Vértice Retail — como mitigar riscos de IA, dados, pessoas e operação

## Princípio de governança

A ferramenta de priorização de iniciativas construída neste programa nunca calcula um número por conta própria — ela apenas consulta uma base de indicadores oficial, já auditada, e narra o que encontra. Toda resposta segue um formato fixo, validado automaticamente antes de chegar a quem fez a pergunta, com evidência, nível de confiança e limitações declaradas em todos os casos. Esse desenho é a base de todos os controles descritos abaixo: ele elimina, por construção, a classe de risco mais comum em ferramentas de IA generativa — a de inventar um número plausível.

## 1. Riscos de dados

| Risco | Descrição | Controle |
|---|---|---|
| **População financeira mal definida** | Sem declarar que só pedidos com pagamento aprovado contam como venda, qualquer métrica de receita ou margem mistura pedidos cancelados com vendas reais | Toda métrica financeira usa uma única definição de população, aplicada de forma consistente em todas as bases e materiais |
| **Bases que não reconciliam entre si** | Marketing e vendas não podem ser somados na mesma conta em reais — o investimento registrado chega a mais de quatro vezes a receita real do mesmo período | Nenhuma ferramenta ou material soma valores de fontes que não reconciliam; a restrição está registrada como regra permanente, não como observação isolada |
| **Métrica circular** | Um segmento de cliente definido pela própria faixa de valor não pode ser usado para calcular o "ganho" de mover um cliente para outro segmento — isso apenas recalcula a definição | Qualquer oportunidade financeira baseada em segmentação é testada quanto a essa circularidade antes de entrar em qualquer material |
| **Agregação mal ponderada** | Médias simples por pedido são distorcidas por um pequeno número de casos extremos e podem inverter a leitura entre canais | Toda comparação de margem entre canais usa soma ponderada, nunca média simples pedido a pedido |
| **Significância estatística ilusória em bases grandes** | Com dezenas de milhares de linhas, praticamente qualquer diferença passa como estatisticamente significativa, mesmo sendo irrelevante na prática | Diferenças são reportadas com tamanho de efeito, não apenas com significância estatística |
| **Dado ausente tratado como zero ou como suposição** | Campos que a operação ainda não capura — duração de ruptura, canal de aquisição, recência do cliente — não devem ser preenchidos artificialmente | Nenhuma ferramenta ou pessoa deste programa está autorizada a inventar ou estimar um campo ausente; ele aparece como lacuna, não como número |
| **Confusão entre dois campos com sentido parecido** | Status de pagamento e marcação de devolução são conceitos diferentes; tratá-los como equivalentes gera conclusões erradas sobre o que é receita realizada | Cada campo é usado apenas no sentido documentado, e essa distinção está registrada como regra, não como conhecimento tácito de quem construiu a análise |
| **Base ainda não representativa da operação real** | Um pequeno número de clientes concentra uma fração desproporcional dos pedidos e chamados analisados | Todo valor financeiro é comunicado como ordem de grandeza; nenhum número deste programa deve ser usado diretamente em orçamento sem ser recalculado sobre a base de produção completa |

## 2. Riscos de privacidade

A ferramenta opera exclusivamente sobre dados agregados — nunca processa, expõe ou infere informação de um cliente individual. Essa não é uma boa prática informal: é uma proibição explícita, registrada nas políticas de uso que orientam a ferramenta, e testada diretamente.

**Teste de aceite realizado:** ao ser questionada sobre nomes e documentos de clientes específicos em um segmento de risco, a ferramenta recusou o pedido, citando a política de proteção de dados aplicável, e sugeriu como alternativa uma consulta agregada — sem revelar nenhuma informação individual.

| Controle | O que garante |
|---|---|
| Escopo restrito a dados agregados | Nenhuma consulta que peça identificação individual é atendida, independentemente de como for formulada |
| Recusa citando a política aplicável | A pessoa que fez a pergunta sabe exatamente por que foi recusada, não recebe apenas um erro genérico |
| Nenhum acesso direto às bases brutas de cliente | A ferramenta consulta apenas indicadores já consolidados, nunca os registros originais de pedido ou cadastro |

## 3. Riscos de viés

Dois vieses específicos foram testados diretamente com dados, em vez de assumidos ou descartados por intuição:

**Viés de atribuição entre canais de marketing.** Testamos se a diferença de retorno entre canais poderia ser causada por um modelo de atribuição favorecendo um canal específico. Não é — os modelos de atribuição se distribuem de forma quase idêntica entre todos os canais. O problema real é de escala entre as bases, não de viés de atribuição.

**Viés de causalidade presumida.** Testamos a suposição, plausível à primeira vista, de que certos tipos de chamado de atendimento (defeito, troca de tamanho) levariam a mais devoluções. Não levam — a taxa é praticamente idêntica em todos os tipos de chamado. Reportamos esse resultado mesmo contrariando a expectativa inicial da equipe de atendimento.

| Risco de viés | Controle |
|---|---|
| Confundir correlação com causa | A ferramenta é instruída a nunca apresentar uma relação de causa e efeito como comprovada quando os dados só sustentam uma correlação — a resposta deve declarar isso explicitamente |
| Herdar viés de uma base não representativa da operação real | Toda conclusão é comunicada com a ressalva sobre a representatividade da base, para que decisões não sejam tomadas como se a base fosse a operação real |
| Viés de confirmação da própria equipe do projeto | Hipóteses intuitivas foram testadas mesmo quando pareciam óbvias, e reportadas mesmo quando os dados as contrariaram |

## 4. Riscos de alucinação e como são controlados

O maior risco em uma ferramenta de IA voltada para decisão executiva é ela responder com confiança a partir de um número que não existe. Três controles, combinados, tratam esse risco:

**A ferramenta nunca calcula — apenas consulta.** Qualquer número que aparece em uma resposta vem de uma consulta direta à base oficial de indicadores, nunca de uma conta feita pelo modelo de linguagem no momento da resposta. Isso elimina a possibilidade de um número ser inventado durante a conversa.

**Toda resposta segue um formato fixo, validado automaticamente.** Uma resposta não passa para quem perguntou sem conter: o status da decisão (responder, pedir mais informação ou recusar), a evidência usada, o nível de confiança e as limitações identificadas. Uma resposta que tente burlar esse formato é rejeitada antes de chegar ao usuário.

**A ferramenta é instruída a reconhecer sete situações específicas em que não deve simplesmente responder**, cada uma com uma regra própria:

| Situação | Como a ferramenta deve se comportar |
|---|---|
| A pergunta cita um número que não bate com a fonte oficial | Responde com o número correto e sinaliza a divergência — corrigir com evidência é responder, não recusar |
| A pergunta pressupõe uma causa que os dados não comprovam | Responde com os dados disponíveis, mas declara explicitamente que a causalidade não está comprovada |
| A pergunta pede algo que a base não suporta (uma previsão, um cruzamento de dados que não existe) | Recusa, explicando o motivo |
| A pergunta pede uma garantia sobre um número que hoje é apenas um cenário | Recusa — mostrar o número com ressalva não atende ao que foi pedido |
| A pergunta pede para simular que a fonte oficial não existe ou foi alterada | Recusa — a ferramenta só opera sobre a versão vigente da fonte |
| A pergunta combina uma parte respondível com uma soma proibida | Recusa o pedido como um todo, explicando qual parte é impossível e por quê |
| A pergunta é genuinamente ambígua sobre qual dado buscar | Pede esclarecimento antes de responder |

**Bateria de testes de aceite.** Onze perguntas, cobrindo cada uma dessas situações mais os casos de resposta direta, foram usadas para validar a ferramenta antes de qualquer uso real. O critério de aceite exige que a maioria das perguntas centrais seja respondida corretamente e que as recusas aconteçam exatamente nos casos em que deveriam acontecer — uma ferramenta que nunca recusa nada é tão arriscada quanto uma que recusa tudo.

## 5. Riscos de adoção pelo time

Uma ferramenta tecnicamente correta ainda pode falhar se as pessoas não confiarem nela ou não souberem quando usá-la.

| Risco | Controle |
|---|---|
| A equipe usa a ferramenta sem entender suas limitações, tratando um cenário como garantia | Toda resposta traz as limitações junto com o número — a limitação não é um rodapé, é parte obrigatória da resposta |
| A ferramenta é usada para decidir algo que exige julgamento humano ou aprovação de alçada superior | Um limite financeiro está embutido na ferramenta: qualquer decisão acima desse valor é automaticamente sinalizada como necessitando aprovação humana, e a ferramenta nunca executa a ação sozinha |
| Falta de confiança pela equipe por não ter visto a ferramenta em uso real | O plano de trabalho inclui um teste com uso real, cronometrado, antes de qualquer adoção ampla — a ferramenta precisa provar que economiza tempo de preparação de reunião, não apenas responder perguntas em teoria |
| A ferramenta é adotada antes de existir uma forma de medir se ela está, de fato, ajudando | Toda automação proposta (por exemplo, atendimento automatizado) exige uma linha de base medida antes da automação começar — sem isso, não há como saber se houve melhora |

## 6. Riscos de operação e negócio

A ferramenta tem uma lista fechada de ações que nunca executa por conta própria, independentemente de quão convincente seja o pedido:

- Alterar orçamento de marketing ou de qualquer canal
- Desligar um canal de aquisição de clientes
- Aprovar concessão de desconto ou cupom diretamente

Qualquer pedido que se encaixe nessas categorias, ou que envolva uma realocação de recurso acima de R$ 100 mil, é automaticamente recusado, com a orientação explícita de que a decisão exige aprovação humana. Esse limite é verificado de forma automática a cada pedido — não depende do modelo de linguagem "lembrar" de aplicá-lo.

## Controles necessários, consolidados

| Categoria | Controle | Responsável |
|---|---|---|
| Dados | População financeira única, documentada e aplicada em toda métrica | Responsável pela base de indicadores |
| Dados | Proibição de somar fontes que não reconciliam | Time de dados e IA |
| Privacidade | Escopo restrito a dados agregados; recusa automática de pedidos de identificação individual | Risco/Privacidade |
| Viés | Teste de hipóteses intuitivas com dados antes de aceitá-las como causa | Time de dados e IA |
| Alucinação | Toda resposta baseada em consulta, nunca em cálculo do modelo; formato de resposta validado automaticamente | Time de dados e IA |
| Alucinação | Bateria de testes de aceite revalidada sempre que a base oficial for atualizada | Time de dados e IA |
| Adoção | Teste de uso real, cronometrado, antes de qualquer adoção ampla | Patrocinador executivo |
| Operação | Limite de alçada financeira e lista de ações proibidas, verificados automaticamente | Financeiro + Risco/Privacidade |

## Papéis de governança

| Papel | Responsabilidade |
|---|---|
| **Patrocinador executivo** | Aprovar o uso da ferramenta em decisões reais; autorizar qualquer caso que exija escalonamento |
| **Risco / Privacidade** | Revisar uso de dado pessoal, aprovar o escopo de acesso e o tratamento de qualquer exceção |
| **Responsável pela base de indicadores** | Garantir que a fonte oficial usada pela ferramenta está sempre atualizada e é a mesma em todos os materiais |
| **Time de dados e IA** | Manter os testes de aceite, revalidar a ferramenta a cada atualização de dado, registrar o histórico de uso |
| **Financeiro** | Validar o limite de alçada financeira e revisar qualquer caso de escalonamento por valor |

## O que ainda não está coberto e precisa de decisão

- O registro de uso da ferramenta (quem perguntou o quê, e qual foi a resposta) precisa de uma política de retenção definida pela Vértice — quanto tempo esse histórico é mantido e quem tem acesso a ele.
- A ferramenta ainda não foi testada contra um volume real de uso simultâneo — o teste de aceite cobriu cenários individuais, não carga de operação.
- Não existe hoje um processo formal de atualização das políticas de guardrail caso uma nova regra de negócio precise ser adicionada — isso depende de a Vértice nomear quem tem autoridade para alterar essas regras.
