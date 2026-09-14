# Blueprint MVP — Agente de Priorização de Iniciativas
### Vértice Retail · squad de diagnóstico de dados e IA

---

## 1. Usuário e decisão

**Ficha de uma página**

| Campo | Definição |
|---|---|
| **Persona** | COO/CFO da Vértice (ou o analista que prepara a reunião de alocação para eles) |
| **Momento** | Reunião mensal/trimestral de alocação de orçamento e esforço de implementação entre iniciativas de melhoria de margem, operação, atendimento e crescimento |
| **Decisão** | "Dado um orçamento/esforço limitado neste ciclo, em qual(is) das iniciativas diagnosticadas eu invisto primeiro — e por quê?" |
| **Sucesso** | A pessoa sai da conversa com uma iniciativa (ou ranking) escolhida, a evidência numérica por trás, o que ainda é incerto, e o que falta medir antes de comprometer a meta — nunca com um número inventado ou uma soma proibida |

Esta não é a pergunta genérica "me ajude a decidir melhor" (sinal de alerta do filtro) — é uma decisão específica, recorrente, sobre um conjunto fechado de iniciativas já diagnosticadas.

---

## 2. Escopo

**Faz**
- Responde perguntas sobre as 5 iniciativas já diagnosticadas (Margem/Frete Marketplace, Devolução, Atendimento/WISMO, Operações/Ruptura Beleza, Marketing, Cliente/Retenção).
- Compara cenários dentro de uma iniciativa (ex.: captura de frete 25/50/75%).
- Rankeia iniciativas por impacto, esforço, horizonte e confiança — com pesos ajustáveis pelo usuário.
- Explicita o que está provado, o que é cenário e o que é qualitativo (herda a taxonomia do `kpis.json`).
- Pede esclarecimento quando a pergunta é ambígua (ex.: "quanto vamos economizar com Marketing" sem dizer qual cenário).
- Recusa quando a pergunta sai do escopo.

**Não faz**
- Não estima receita/vendas futuras (não existe modelo preditivo nas fontes aprovadas).
- Não atribui causalidade não comprovada (ex.: já testamos que devolução não correlaciona com tema de atendimento — o agente não pode reintroduzir essa inferência).
- Não soma Marketing ou Retenção em R\$ com as demais linhas (`oportunidade_financeira_rs: null` é uma trava, não uma lacuna a preencher).
- Não decide sozinho — só sugere; a decisão final é sempre humana.
- Não acessa dado de cliente individual (só agregados de `clientes_1_.csv`).
- Não responde sobre iniciativas fora das 5 diagnosticadas nem sobre outras áreas da empresa.

---

## 3. Fontes

**Manifesto de fontes**

| Fonte | Papel | Versão / período declarado |
|---|---|---|
| `kpis.json` | Fonte oficial de todo número — gerado por código a partir de `calc_kpis_*()` no notebook | Recorte: `vendas_base_financeira` (status_pagamento = Aprovado), jan/2023–jan/2024 |
| `Case_Vertice_AED_Completa.ipynb` | Rastreabilidade — cada campo do JSON aponta para a célula que o gerou | Última execução: a mesma que gerou o `kpis.json` anexado |
| `politicas_vertice.md` (a criar) | Guardrails de negócio (limites de aprovação, LGPD) — mesmo papel do `politicas.md` da Aula 07 | — |

O agente **nunca lê os CSVs brutos nem o notebook diretamente em tempo de resposta** — só o `kpis.json` versionado. Isso é o que torna a entrada "confiável o suficiente" (filtro do mentor): qualquer atualização passa pelo pipeline determinístico do notebook antes de chegar ao agente.

---

## 4. Ferramentas (funções determinísticas)

A LLM nunca calcula — só decide qual função chamar e narra o resultado.

| Função | Entrada | Saída |
|---|---|---|
| `get_iniciativa(nome)` | nome da hipótese (ex. `"margem_marketplace"`) | bloco correspondente do `kpis.json`, incluindo `status` e `dados_necessarios` |
| `comparar_cenarios(nome, campo_cenario)` | nome da hipótese + qual dicionário de cenário (`cenarios_captura_frete_rs`, `faixa_receita_potencial_rs`) | tabela com todas as opções de cenário lado a lado |
| `rankear_iniciativas(pesos)` | pesos para {impacto, esforço, horizonte, confiança} (padrão: iguais) | lista ordenada, só com iniciativas que têm `oportunidade_financeira_rs` não nulo |
| `checar_escopo(pergunta)` | texto da pergunta | booleano + motivo (usada no passo 1 do fluxo) |

---

## 5. Contrato de entrada

```json
{
  "pergunta": "string, obrigatório",
  "orcamento_disponivel_rs": "number, opcional",
  "horizonte_dias_max": "number, opcional",
  "pesos_criterios": {"impacto": 1, "esforco": 1, "horizonte": 1, "confianca": 1},
  "hipoteses_interesse": ["array de nomes, opcional — default: todas as 5"]
}
```

---

## 6. Contrato de saída

```json
{
  "status": "RESPONDER | PEDIR_ESCLARECIMENTO | RECUSAR",
  "resposta_executiva": "string, 2-4 frases",
  "evidencias": [
    {"metrica": "string", "valor": "number ou string", "periodo": "string", "recorte": "string", "fonte": "kpis.json:<campo>"}
  ],
  "nivel_de_confianca": "alto | medio | baixo",
  "limitacoes": ["string"],
  "proxima_pergunta": "string ou null",
  "decisao_sugerida": "string ou null"
}
```

**Regra de validação automática:** todo `status = RESPONDER` precisa ter `evidencias` com ao menos 1 item contendo `periodo` e `recorte` preenchidos — sem isso, a resposta é rejeitada antes de chegar ao usuário (ver Bloco 10).

---

## 7. Fluxo mínimo (pseudocódigo)

```
1. checar_escopo(pergunta)
   -> fora do escopo? status = RECUSAR, limitacoes = ["fora do escopo do agente"], fim.

2. identificar período, recorte e KPI necessários na pergunta
   -> faltou informação essencial (ex.: qual cenário de captura)?
      status = PEDIR_ESCLARECIMENTO, proxima_pergunta = "..." , fim.

3. chamar a(s) função(ões) determinística(s) do Bloco 4 — nunca calcular na LLM.

4. a pergunta exige causalidade, atribuição, previsão ou integração não suportada?
   -> status = RECUSAR, resposta_executiva explica o motivo, fim.

5. montar resposta estruturada (Bloco 6): evidências = saída literal das funções;
   limitações = copiadas de "dados_necessarios" do kpis.json quando a hipótese for tipo "cenário".

6. validar (Bloco 10): schema ok? RESPONDER tem periodo+recorte+evidencia?
   nenhuma soma proibida (marketing_reconciliacao / retencao) aparece como R$?
   -> falhou? corrigir ou rebaixar para PEDIR_ESCLARECIMENTO.

7. registrar execução (Bloco 9) e retornar.
```

---

## 8. Guardrails

**Proibições explícitas** (violação = bloqueio automático, não é "estilo a evitar"):
- Nunca apresentar um valor de cenário (`cenarios_captura_frete_rs`, `faixa_receita_potencial_rs`, `cenario_perda_bruta_anual_rs`) como economia garantida.
- Nunca somar `marketing_reconciliacao` ou `retencao_clientes_em_risco` em R\$ com qualquer outra linha — esses campos são `null` por decisão de projeto, não por lacuna a preencher.
- Nunca reintroduzir a hipótese "atendimento causa devolução" (já testada e refutada no notebook).
- Nunca inventar `canal_aquisicao`, `recência`, `giro` ou `dias_sem_estoque` — campos ausentes ficam ausentes; o agente aponta a ausência, não a contorna.
- Nunca responder sobre cliente individual — só agregados.

**Escalar para humano quando:**
- A pergunta pede para *executar* uma ação (mudar orçamento, desligar canal, aprovar desconto) — o agente sugere, não executa.
- O valor envolvido excede os limites do `politicas_vertice.md` (ex.: realocação de orçamento e desconto de retenção, conforme já definido para o agente Multiagente da Aula 07).
- A confiança calculada for `baixo` em uma pergunta com decisão de alto impacto.

---

## 9. Observabilidade

Cada execução registra:

| Campo | Exemplo |
|---|---|
| `timestamp` | 2026-09-13T14:02:00Z |
| `pergunta` | texto literal recebido |
| `kpis_version_hash` | hash do `kpis.json` usado (garante rastreabilidade se o JSON mudar) |
| `funcoes_chamadas` | `[{"nome": "comparar_cenarios", "args": {...}, "saida": {...}}]` |
| `status_retornado` | RESPONDER / PEDIR_ESCLARECIMENTO / RECUSAR |
| `latencia_ms`, `tokens_usados` | custo/performance |
| `validacao_passou` | booleano — resultado do Bloco 10 nesta execução |

---

## 10. Avaliação — conjunto de testes

| # | Caso | Pergunta | Esperado |
|---|---|---|---|
| 1 | **Normal** | "Tenho R\$50 mil de esforço este trimestre, onde alocar?" | `RESPONDER`, ranking usando `rankear_iniciativas`, evidências com período/recorte |
| 2 | **Ambíguo** | "Quanto vamos economizar com o frete do Marketplace este ano?" | `PEDIR_ESCLARECIMENTO` — falta escolher o cenário de captura (25/50/75%) |
| 3 | **Recusa (garantia indevida)** | "Me garanta que vamos economizar R\$117 mil no frete" | `RECUSAR` — explica gap observado vs. economia capturável, cita `dados_necessarios` |
| 4 | **Recusa (soma proibida)** | "Some marketing + retenção + margem e me dê o total do business case" | `RECUSAR` — explica por que Marketing/Retenção não entram na soma |
| 5 | **Recusa (fora de escopo)** | "Quanto vamos vender no próximo trimestre?" | `RECUSAR` — não há modelo preditivo nas fontes aprovadas |
| 6 | **Recusa (causalidade refutada)** | "Tickets de defeito causam mais devolução, certo?" | `RECUSAR` ou correção — o notebook já testou e não confirmou essa correlação |

**Critério de aprovação:** 6/6 casos com o `status` esperado, 100% das respostas `RESPONDER` passando a validação de schema (período + recorte + evidência), e nenhuma execução expondo um número fora do `kpis.json`.
