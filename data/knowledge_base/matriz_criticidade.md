# Matriz de Criticidade e Regra de Prioridade — v1.1

> ⚠️ **DOCUMENTO SIMULADO.** Critérios, pesos e prazos foram definidos pelo grupo para fins acadêmicos.
> Não são a política real de nenhuma concessionária.

| Campo | Valor |
|---|---|
| Código do documento | `KB-D04` |
| Versão / data | v1.1 — 2026-11-07 |
| Uso no assistente | Indexado no RAG + **cópia compacta da Parte C no system prompt** (bloco `PRIORIZAÇÃO`). Quando a versão da base for mais recente que a do prompt, prevalece a base e o prompt deve ser atualizado. |

O documento tem duas partes que **não podem ser confundidas**:

- **Criticidade do ativo (A/B/C):** é fixa, cadastrada no catálogo. Diz quanto aquele ativo importa.
- **Prioridade da ordem de serviço (P1 a P4):** é calculada a cada ocorrência, cruzando a criticidade do ativo com a severidade do sintoma.

---

## Parte A — Critérios de criticidade do ativo

| Critério | Peso | Pergunta que responde |
|---|---|---|
| **S** — Segurança | **0,5** | Se o ativo parar ou errar, cresce o risco de acidente (fila da praça chegando à rodovia, cancela baixando sobre veículo)? |
| **R** — Arrecadação | **0,3** | Se o ativo parar ou errar, há perda ou cobrança incorreta de tarifa? |
| **D** — Disponibilidade da faixa | **0,2** | Se o ativo parar, a faixa fecha ou passa a operar em modo manual? |

**Score = 0,5·S + 0,3·R + 0,2·D** → **A** se ≥ 3,5 · **B** se entre 2,5 e 3,49 · **C** se < 2,5

> **Por que segurança pesa mais:** receita perdida é recuperável; acidente na fila da praça não é. A decisão é da Engenharia de Manutenção e está escrita aqui para ser auditável e contestável.

## Parte B — Classes de contexto e criticidade resultante

| Ativo | Contexto | S | R | D | Score | Criticidade |
|---|---|---|---|---|---|---|
| Laço, sensor de eixo ou PLC | Faixa automática (TAG) de alto fluxo (F01, F02) | 3 | 5 | 4 | 3,8 | **A** |
| Laço, sensor de eixo ou PLC | Faixa de veículos pesados, cobrança por eixo (F04) | 3 | 5 | 3 | 3,6 | **A** |
| Laço, sensor de eixo ou PLC | Faixa mista, manual + TAG (F03) | 2 | 4 | 3 | 2,8 | **B** |
| Câmera de classificação | Piloto em modo sombra (não tarifa) | 1 | 1 | 2 | 1,2 | **C** |

## Parte C — Prioridade da ordem de serviço

### C.1 Severidade do sintoma

| Severidade | Definição verificável | Exemplos |
|---|---|---|
| **Alta** | Perda total da função agora, **ou** classificação/tarifação incorreta em curso, **ou** cancela sem abrir | Sensor de eixo sem sinal; PLC travado com a faixa parada; divergência acima de 3% na auditoria; contagem dupla confirmada |
| **Média** | Falha intermitente com recuperação espontânea, **ou** divergência entre 1% e 3%, **ou** degradação sem erro de classificação confirmado | Laço com detecção intermitente após chuva; amplitude do sensor caindo, mas contagem correta; câmera piloto com 2% de divergência |
| **Baixa** | Sem impacto na função agora: achado de preventiva, sujeira leve, alarme sem falha confirmada | Selante com início de fissura; alarme de divergência explicado por manobra de veículo |

### C.2 Tabela de prioridade

| Criticidade \ Severidade | Alta | Média | Baixa |
|---|---|---|---|
| **A** | P1 | P2 | P3 |
| **B** | P2 | P3 | P4 |
| **C** | P3 | P4 | P4 |

### C.3 Regra de risco imediato (sobrepõe a tabela)

Classificar como **P1, qualquer que seja a criticidade**, quando houver risco imediato à segurança. Exemplos:
- fila da praça alcançando o acostamento ou a pista da rodovia por falha de faixa;
- cancela baixando sobre veículos por falha de detecção do laço de saída.

Ao aplicar esta regra, informar também a prioridade que a tabela daria.

### C.4 Desempate (duas ou mais OS com a mesma prioridade)

1. Risco imediato à segurança (C.3) vem primeiro;
2. maior criticidade do ativo;
3. maior severidade;
4. ordem de chegada.

### C.5 Prazos de atendimento (SLA simulado)

| Prioridade | Início do atendimento em campo |
|---|---|
| P1 | até 4 h |
| P2 | até 24 h |
| P3 | até 72 h |
| P4 | próxima janela preventiva (até 15 dias) |

## Parte D — O que NUNCA é critério de prioridade

Praça, km, região, fabricante, nome da equipe, quem abriu o chamado, valor arrecadado pela praça ou o quanto o usuário insiste.
Esses fatores não aparecem na fórmula. Se aparecerem numa justificativa de prioridade, ela está errada.

## Parte E — Auditoria de viés

A cada trimestre, a Engenharia de Manutenção compara a distribuição de prioridades por **tipo de ativo** e por **praça** com a distribuição de criticidade do catálogo. Diferença persistente sem explicação na severidade é tratada como suspeita de viés e revisada.

## Controle de revisão

| Versão | Data | Alteração |
|---|---|---|
| v1.0 | 2026-10-20 | Versão inicial (domínio CFTV/PMV/laço) |
| v1.1 | 2026-11-07 | Domínio de classificação por eixos; exemplos de severidade; regra C.3 exige informar a prioridade da tabela |
