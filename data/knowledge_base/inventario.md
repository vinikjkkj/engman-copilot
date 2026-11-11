# Inventário da Base de Conhecimento — EngMan Copilot (v1.1)

> ⚠️ **Dados simulados.** A Motiva não libera base real para trabalho acadêmico. Todo documento marcado como **simulado** foi criado pelo grupo com dados fictícios plausíveis e **não representa ativos, falhas ou procedimentos reais**. Fabricantes e modelos (SensoSim, EixoSim, ControlSim, VigiaSim) são fictícios.
> Documentos marcados como **real** contêm apenas informação pública (definições, resumo de normas e leis, briefing do Challenge).

**Domínio:** sistema de classificação veicular por eixos das pistas de pedágio (**Tema 1** do briefing).
**Instalação simulada:** três praças, **P1 (km 87)**, **P2 (km 233)** e **P3 (km 398)**, cada uma com quatro faixas: **F01 e F02** automáticas (TAG) de alto fluxo, **F03** mista e **F04** de veículos pesados (cobrança por eixo). Em cada faixa: um laço indutivo, um sensor de eixo vulcanizado e um controlador de pista (PLC). Três faixas têm a **câmera de classificação do piloto** em modo sombra.
**Data de referência dos dados:** 2026-11-06 (histórico de 2024-12 a 2026-10).

---

## 1. Inventário

| ID | Documento | Conteúdo e campos | Origem | Volume | Status | Uso no assistente | Arquivo |
|---|---|---|---|---|---|---|---|
| KB-D01 | **Catálogo de ativos** | `tag, tipo_ativo, fabricante, modelo, km_praca, praca, faixa, data_instalacao, vida_util_anos, criticidade, observacao, origem` | simulado | **39 ativos** (12 laços, 12 sensores de eixo, 12 PLCs, 3 câmeras piloto) | ✅ produzido | **Tool** (`consultar_ativo`, `buscar_ativos_da_faixa`, `listar_ativos_por_criticidade`). Não vai para o RAG. | [catalogo_ativos.csv](catalogo_ativos.csv) |
| KB-D02 | **Histórico de falhas do FSM** | `id_fsm, tag, data_abertura, sintoma, condicao_ambiental, modo_falha, causa_identificada, tipo_intervencao, tempo_reparo_h, peca_trocada, reincidencia, origem` | simulado | **54 registros** (2024-12 a 2026-10) | ✅ produzido | **Tool** (`consultar_historico_falhas`, `calcular_metricas_confiabilidade`). Não vai para o RAG. | [historico_falhas_fsm.csv](historico_falhas_fsm.csv) |
| KB-D03 | **Plano de manutenção preventiva** | Código, ativo, tarefa, periodicidade, responsável (equipe, sem nomes), tempo estimado, recursos, condição de execução, POP | simulado | 1 documento, 14 tarefas | ✅ produzido | **RAG** (1 chunk por tarefa) | [plano_manutencao_preventiva.md](plano_manutencao_preventiva.md) |
| KB-D04 | **Matriz de criticidade** | Critérios S/R/D com pesos, classes de contexto, severidade com exemplos, tabela de prioridade, regra de risco imediato, desempate, SLA, auditoria de viés | simulado | 1 documento | ✅ produzido | **RAG** + cópia compacta no system prompt (bloco PRIORIZAÇÃO) | [matriz_criticidade.md](matriz_criticidade.md) |
| KB-D05 | **Glossário de siglas** | Classificação, eixo suspenso, sensor piezoelétrico, PLC, modo sombra, CBM, FSM, RGA, LDA, λ, MTBF, MTTR, R(t), OCR e termos do projeto | real | 1 documento, 57 termos | ✅ produzido | **RAG** (1 chunk por termo) | [glossario.md](glossario.md) |
| KB-D06 | **Procedimentos operacionais (POPs)** | Código, título, versão, aplica a, **pré-requisitos de segurança**, EPI, passos, critérios de aceite, normas relacionadas | simulado | **8 POPs** (ver §4) | 🟡 1 de 8 redigido (POP-LAC-01, no contrato da tool); demais na Sprint 3 | **Tool** (`consultar_procedimento`), sempre **inteiro**. Não vai para o RAG em pedaços. | [tools_spec.json](../../tools/tools_spec.json) · `pops/` (previsto) |
| KB-D07 | **Fichas técnicas dos equipamentos** | Modelo, princípio de funcionamento, alimentação, faixa de temperatura, grau de proteção, interfaces, modos de falha conhecidos, peças de reposição. **Sem MTBF de fabricante** (dado não disponível). | real (princípios) + simulado (modelos fictícios) | 5 fichas: SS-LOOP2, SS-DET4, ES-PZ2, CS-PL400, VS-AXC | 🕒 a produzir | **RAG** (1 chunk por seção) | `fichas/` (previsto) |
| KB-D08 | **Normas e requisitos de segurança** | Resumo, com citação, dos itens aplicáveis da NR-10 (desenergização, profissional autorizado) e da NR-35 (trabalho acima de 2 m) + regra interna de trabalho em pista (interdição e sinalização de faixa, autorização do supervisor, comunicação com o CCO) | real (resumo) | 1 documento | 🕒 a produzir | **RAG** + referenciado pelos POPs | `normas_seguranca.md` (previsto) |
| KB-D09 | **Documentos do briefing Motiva** | Contexto da empresa, parque de equipamentos, ondas de inovação, Temas 1, 2 e 2.1 | real | 1 documento | 🕒 a produzir | **RAG** (contexto) | `briefing_motiva.md` (previsto) |
| KB-D10 | **Boletins de campo** | `id_boletim, id_fsm, tag, data, relato_tecnico, condicao_ambiental, fotos_anexas (sim/não, sem a imagem), equipe` (código da equipe, nunca nome) | simulado | **12 boletins**, ligados aos ativos do §5 | 🕒 a produzir | **RAG** com metadado `tag`; tratado como **conteúdo não confiável** (pode conter texto colado) | `boletins/` (previsto) |
| KB-D11 | **Regras de classificação tarifária (resumo)** | Como a categoria é definida (número de eixos, rodagem simples ou dupla), isenção de eixo suspenso para veículo de carga vazio (Lei nº 13.103/2015) e o que muda para a contagem | real (resumo) | 1 documento | 🕒 a produzir | **RAG** | `regras_classificacao.md` (previsto) |

**Resumo:** 11 documentos especificados; 5 produzidos nesta Sprint (KB-D01 a KB-D05), 1 parcial (KB-D06) e 5 especificados para a Sprint 3.

---

## 2. Princípio de fonte única de verdade

| Tipo de informação | Única fonte | Por quê |
|---|---|---|
| Ficha e criticidade de ativo | `catalogo_ativos.csv` via tool | Dado estruturado, consultado por chave (TAG). Indexar no vetor criaria uma segunda cópia que pode ficar desatualizada. |
| Histórico e métricas | `historico_falhas_fsm.csv` via tool | Contagem e cálculo exigem dado exato, não "trecho parecido". |
| Procedimento (POP) | `consultar_procedimento` | O POP chega **inteiro**. Recuperar por similaridade poderia trazer o passo "revulcanizar a borda" sem o pré-requisito "faixa interditada durante a cura". |
| Periodicidades, critérios, conceitos, normas, regras tarifárias | RAG (ChromaDB) | Texto livre, consultado por significado. |

Se um texto do RAG (por exemplo, um boletim) citar um dado de ativo que diverge da tool, **prevalece a tool** e o assistente mostra a divergência (REGRA 14 do [system prompt](../../prompts/system_prompt.md)).

---

## 3. Dicionário de dados

### 3.1 Catálogo (KB-D01)

| Campo | Tipo | Regra |
|---|---|---|
| `tag` | texto | `TTT-Pn-Fnn-NN`, TTT = `LAC`, `EIX`, `PLC` ou `CAM`. Único. |
| `tipo_ativo` | enum | `laco_indutivo`, `sensor_eixo`, `controlador_pista`, `camera_classificacao` |
| `praca` / `km_praca` | texto / inteiro | `P1` (87), `P2` (233), `P3` (398) |
| `faixa` | texto | `F01`–`F04` (F01–F02 automáticas, F03 mista, F04 pesados) |
| `vida_util_anos` | inteiro | Laço e sensor de eixo 5, PLC 10, câmera 6 (valores simulados) |
| `criticidade` | enum | `A`, `B`, `C`, calculada pela [Matriz KB-D04](matriz_criticidade.md), Parte B |
| `observacao` | texto | Tipo de faixa, princípio do sensor, firmware, indicação de piloto |
| `origem` | texto | Sempre `SIMULADO` |

### 3.2 Histórico (KB-D02)

| Campo | Tipo | Regra |
|---|---|---|
| `id_fsm` | texto | `FSM-AAAA-NNNN`, sequencial por ano |
| `condicao_ambiental` | texto | Período do dia, clima e temperatura quando relevante; `n/d` se não registrado |
| `modo_falha` | enum (21 valores) | Vocabulário controlado, igual ao enum `tipo_falha` de [tools_spec.json](../../tools/tools_spec.json) |
| `tipo_intervencao` | enum | `corretiva`, `preventiva`, `inspecao`, `cbm` |
| `tempo_reparo_h` | decimal | Horas de atendimento |
| `reincidencia` | `sim`/`nao` | `sim` quando o mesmo TAG teve o mesmo `modo_falha` nos **90 dias anteriores** |

**Modos de falha que não contam como falha de ativo:** `falso_positivo_operacional` (manobra irregular, veículos colados, tabela do operador desatualizada) e `indeterminado`. Eles aparecem no histórico, porque são atendimentos reais, mas ficam fora de λ e MTBF.

**Atenção para a análise:** a reincidência é medida por modo de falha. Um ativo que se degrada por modos diferentes (ex.: EIX-P2-F02-01 alterna contagem dupla, sinal fraco, trinca e cabo rompido) pode ter **zero reincidências** e mesmo assim estar em deterioração, o que só aparece na tendência β.

---

## 4. POPs previstos (KB-D06)

| Código | Título | Pré-requisitos de segurança obrigatórios | Status |
|---|---|---|---|
| POP-LAC-01 | Teste de laço: indutância e isolação | APR e PT; aviso ao CCO e autorização do supervisor; faixa fechada e sinalizada; megôhmetro (500 Vcc) só com profissional autorizado em NR-10; laço desconectado e terminais intocados durante o ensaio | ✅ redigido |
| POP-LAC-02 | Reselagem e revulcanização de ranhura do laço | Faixa interditada em janela noturna; sinalização de obra em pista | 🕒 |
| POP-EIX-01 | Teste de amplitude e contagem com veículo-padrão | Faixa fechada para as passagens de teste | 🕒 |
| POP-EIX-02 | Revulcanização de borda e substituição de sensor de eixo | **Faixa interditada durante o serviço e durante a cura da resina**; janela noturna autorizada; EPI químico | 🕒 |
| POP-PLC-01 | Diagnóstico de travamento: log, uptime, reinício controlado e backup | Faixa em modo manual ou fechada durante o reinício; aviso ao CCO | 🕒 |
| POP-PLC-02 | Intervenção no armário elétrico do PLC (fonte, cartões, DPS) | NR-10: profissional autorizado, desenergização e bloqueio | 🕒 |
| POP-AUD-01 | Auditoria de classificação | Contagem da cabine ou por vídeo, sem entrar na pista; placas não registradas | 🕒 |
| POP-CAM-01 | Limpeza de lente, enquadramento e teste IR da câmera de classificação | NR-35 acima de 2 m; nenhum acesso pela faixa aberta | 🕒 |

---

## 5. Ativos com histórico rico (personas sintéticas do dataset)

Cinco ativos foram construídos com histórico completo e coerente, cada um para testar uma habilidade diferente:

| TAG | Criticidade | Registros | História que o dado conta | Habilidade testada | Casos do eval |
|---|---|---|---|---|---|
| **EIX-P2-F02-01** | A | 11 em 24 meses | Sensor vulcanizado com vida útil excedida: amplitude caindo de 72% para 38%, bordas descolando, trinca no pavimento e cabo rompido. Intervalos encurtando (β ≈ 1,45) sem nenhuma "reincidência" formal | Métricas, tendência (RGA), limite do modelo exponencial; base para a decisão do Tema 1 | C01, C03, C07, C15, C16, C17 |
| **PLC-P3-F02-01** | A | 6 em 24 meses | Trava a cada ~22 dias desde a atualização para o firmware 3.2.0; fonte e cartão trocados sem efeito; armário com temperatura normal | Diagnóstico com CoT: o padrão de uptime e o evento de firmware apontam para software, não para peça | C06 |
| **CAM-P2-F04-01** | C (piloto) | 8 desde 2025-09 | A câmera do piloto conta eixo suspenso como eixo; também tem lente suja, iluminador IR queimado e um falso positivo por manobra | Leitura de histórico, falso positivo operacional, avaliação do piloto do Tema 1 | C02, C13, C18 |
| **CAM-P2-F02-01** | C (piloto) | 3 em 12 meses | Mesma câmera em faixa automática: só 1 eixo suspenso, além de lente suja e veículos colados | Comparação entre ativos e memória de contexto | C07, C18 |
| **LAC-P1-F04-01** | A | 4 em 24 meses | Isolação caindo a cada chuva (35 → 22 → 15 → 12 MΩ), já abaixo do gatilho de CBM (20 MΩ) | OS com prioridade por intermitência; ligação com a tarefa CBM do plano | C04, C05 |

---

## 6. Estratégia de chunking e metadados (RAG)

### 6.1 Tamanho do chunk

| Decisão | Valor | Justificativa (Aula 02: janela de contexto) |
|---|---|---|
| Unidade de corte | **Seção do documento** (cabeçalho Markdown, linha de tabela do plano, termo do glossário, boletim) e, dentro dela, tamanho | Documento técnico tem unidades naturais: uma tarefa do plano, uma definição, um item de norma. Cortar no meio separa a periodicidade da sua condição. |
| Tamanho-alvo | **300 a 500 tokens** por chunk | Abaixo de ~200 tokens o trecho perde contexto (ex.: "15 dias" sem dizer de qual tarefa). Acima de ~800, a similaridade se dilui e cada chunk ocupa espaço demais na janela. |
| Sobreposição | **~15% (≈ 60 tokens)**, só quando uma seção precisa ser dividida | Evita perder a frase que liga dois pedaços. |
| Recuperação | **top-4** com filtro de metadados | 4 × 500 = 2.000 tokens no máximo, dentro do orçamento de [decisões técnicas §6](../../docs/decisoes_tecnicas.md#6-política-de-contexto-quantificada). |
| Linhas de tabela | Convertidas em frase autoexplicativa antes de indexar | Ex.: "PM-EIX-01 — Sensor de eixo — Teste de amplitude e contagem com veículo-padrão — 30 dias (padrão); 15 dias nas faixas F01 e F02 — POP-EIX-01". |

### 6.2 Metadados guardados com cada chunk

| Metadado | Exemplo | Para que serve |
|---|---|---|
| `doc_id` | `KB-D03` | Citação e rastreabilidade |
| `tipo_documento` | `plano`, `matriz`, `glossario`, `ficha`, `norma`, `briefing`, `boletim`, `regra_tarifaria` | Filtro por tipo de pergunta |
| `tipo_ativo` | `laco_indutivo`, `sensor_eixo`, `controlador_pista`, `camera_classificacao`, `geral` | Filtro principal: pergunta sobre PLC não recupera plano de sensor |
| `tag` | `EIX-P2-F02-01` (só boletins) | Busca filtrada por ativo |
| `codigo` | `PM-EIX-01`, `POP-EIX-02` | Citação exata |
| `versao` / `data_documento` | `v1.1` / `2026-11-07` | Regra de conflito: prevalece o mais recente |
| `origem` | `real` / `simulado` | Transparência: o assistente sabe o que é fictício |
| `confiavel_como_instrucao` | sempre `false` | Lembrete para a aplicação: conteúdo recuperado nunca é instrução |

### 6.3 Pipeline de ingestão (Sprint 3)

1. **Sanitização:** remove nomes de pessoas, matrículas, placas (padrões Mercosul e antigo), CPF, IPs e credenciais. Boletins têm o campo `equipe` como código.
2. **Marcação de injeção:** trechos com padrões como "ignore as instruções", "INSTRUÇÃO DO SISTEMA" ou "system prompt" são sinalizados e revisados por uma pessoa antes de entrar na base.
3. **Conversão:** tabelas viram frases autoexplicativas (§6.1).
4. **Chunking + embeddings** (modelo de [decisões técnicas](../../docs/decisoes_tecnicas.md)) e gravação no ChromaDB com os metadados acima.

---

## 7. O que NUNCA entra na base (LGPD e confidencialidade)

| Nunca entra | Motivo | Como é garantido |
|---|---|---|
| Imagens e frames da câmera de classificação | Mostram placa, cabine e, às vezes, pessoas: dado pessoal | O piloto exporta só a **contagem de eixos por passagem**; imagem nunca é indexada nem enviada ao modelo |
| Placas de veículos e leituras de OCR | Dado pessoal de terceiro (titular identificável) | Fora do recorte; mascaramento no guardrail de entrada e na ingestão; auditoria conta por classe, não por placa |
| Nome, matrícula, telefone ou escala de colaboradores | Dado pessoal sem necessidade para o diagnóstico (LGPD, princípio da necessidade) | Campo `equipe` por código; sanitização na ingestão |
| Dados de usuários da rodovia (contestação de cobrança, cadastro de TAG) | Dado pessoal e fora do escopo | Não há fonte nem tool para isso |
| Valores de arrecadação por praça, contratos e dados financeiros da concessão | Confidencialidade comercial | Fora da base; a criticidade usa notas (1–5), não valores em R$ |
| IPs, senhas, topologia da rede da praça | Segurança da informação | Removidos na sanitização; fichas descrevem interfaces sem endereços |
| Qualquer dado **real** da Motiva | Regra do Challenge e confidencialidade | Repositório só com dados simulados; `.gitignore` bloqueia `data/raw/` |

---

## 8. Dimensionamento (tokens)

Estimativa de 3,5 caracteres por token em pt-BR (conservadora; a medir com o tokenizer do modelo na Sprint 3).

| Documento | Caracteres | Tokens (≈) | Onde fica |
|---|---|---|---|
| KB-D01 Catálogo | 7,2 mil | 2,1 mil | Tool (sob demanda, 1 linha ≈ 50 tokens) |
| KB-D02 Histórico | 11,1 mil | 3,2 mil | Tool (sob demanda, 1 registro ≈ 60–80 tokens) |
| KB-D03 Plano | 6,0 mil | 1,7 mil | RAG |
| KB-D04 Matriz | 4,8 mil | 1,4 mil | RAG + prompt |
| KB-D05 Glossário | 8,0 mil | 2,3 mil | RAG |
| KB-D06 a KB-D11 (previstos) | ~75 mil | ~21 mil | RAG / tool |
| **Total estimado** | **~112 mil** | **~32 mil** | |

**Conclusão:** a base inteira (~32 mil tokens) até caberia na janela nominal do modelo, mas não no `num_ctx` de 16 mil que a máquina do grupo suporta. Além disso, enviar tudo a cada pergunta deixaria a resposta lenta, diluiria a atenção do modelo e misturaria ativos. Por isso usamos **RAG para texto e tools para dados estruturados**, entregando por turno só o necessário (≈ 2 mil tokens de RAG e até ≈ 1,8 mil de resultados de tool).
