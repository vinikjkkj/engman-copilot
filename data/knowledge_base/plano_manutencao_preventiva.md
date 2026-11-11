# Plano de Manutenção Preventiva — Classificação por Eixos — v1.1

> ⚠️ **DOCUMENTO SIMULADO.** Conteúdo fictício, criado pelo grupo para fins acadêmicos (Challenge FIAP × Motiva).
> Não representa o plano real de nenhuma concessionária. Periodicidades e limites técnicos são **plausíveis, não oficiais**.

| Campo | Valor |
|---|---|
| Código do documento | `KB-D03` |
| Versão / data | v1.1 — 2026-11-07 |
| Ativos cobertos | Laços indutivos, sensores de eixo vulcanizados, controladores de pista (PLC) e câmeras de classificação (piloto) das pistas de pedágio |
| Uso no assistente | Indexado no RAG (1 chunk por tarefa) — metadados `tipo_documento=plano`, `tipo_ativo`, `codigo` |

## Regras gerais

1. Toda tarefa **dentro da pista** só começa com a **faixa fechada e sinalizada**, autorização do supervisor da praça e aviso ao CCO. Não existe trabalho em pista "entre um veículo e outro".
2. Tarefa com **abertura de armário elétrico** ou **medição com megôhmetro** só é executada por profissional autorizado conforme **NR-10**, seguindo o POP indicado.
3. Câmeras de classificação instaladas em pórtico ou poste acima de 2 m exigem profissional autorizado em **NR-35**.
4. Quando a periodicidade tiver condição especial (tipo de faixa ou resultado de auditoria), prevalece **a condição mais restritiva**.
5. Tarefas marcadas como **CBM** (manutenção baseada em condição) são disparadas pela medição indicada, não pelo calendário.

## Laços indutivos

| Código | Tarefa | Periodicidade | Responsável | Tempo estimado | Recursos | Condição de execução | POP |
|---|---|---|---|---|---|---|---|
| PM-LAC-01 | Teste de indutância/frequência e de resposta do detector | **30 dias** | Equipe de sistemas de pedágio | 0,3 h por faixa | Detector com diagnóstico, notebook de serviço | Pela cabine, sem entrar na pista | POP-LAC-01 |
| PM-LAC-02 | Medição de isolação do laço (megôhmetro 500 Vcc) | **90 dias** | Eletricista autorizado (NR-10) | 0,5 h por faixa | Megôhmetro | Faixa fechada e sinalizada; laço desconectado do detector | POP-LAC-01 |
| PM-LAC-03 | Inspeção visual do pavimento e do selante da ranhura | **90 dias** | Equipe de sistemas de pedágio | 0,5 h por faixa | — | Faixa fechada e sinalizada | POP-LAC-02 |
| PM-LAC-04 | Reselagem ou revulcanização do laço (**CBM**) | **Por condição:** isolação abaixo de 20 MΩ, **ou** trinca transversal sobre a ranhura, **ou** divergência de classificação acima de 3% na auditoria | Equipe de sistemas de pedágio + pavimentação | 6 a 8 h por faixa | Selante, cortadora de piso | Faixa interditada, janela noturna | POP-LAC-02 |

## Sensores de eixo vulcanizados

| Código | Tarefa | Periodicidade | Responsável | Tempo estimado | Recursos | Condição de execução | POP |
|---|---|---|---|---|---|---|---|
| PM-EIX-01 | Teste de amplitude do sinal e contagem com veículo-padrão de eixos conhecidos | **30 dias** (padrão); **15 dias** nas faixas automáticas de alto fluxo (**F01 e F02**) | Equipe de sistemas de pedágio | 0,5 h por faixa | Veículo-padrão, notebook de serviço | Faixa fechada para as passagens de teste | POP-EIX-01 |
| PM-EIX-02 | Inspeção visual das bordas vulcanizadas e do pavimento ao redor do sensor | **60 dias** | Equipe de sistemas de pedágio | 0,5 h por faixa | — | Faixa fechada e sinalizada | POP-EIX-02 |
| PM-EIX-03 | Revulcanização de borda ou substituição do sensor (**CBM**) | **Por condição:** amplitude abaixo de 60% do valor de comissionamento, **ou** borda descolada, **ou** divergência acima de 3% na auditoria | Equipe de sistemas de pedágio + pavimentação | 6 a 10 h por faixa | Resina de vulcanização, cortadora de piso, sensor reserva | Faixa interditada, janela noturna, cura da resina antes de liberar | POP-EIX-02 |

## Controladores de pista (PLC)

| Código | Tarefa | Periodicidade | Responsável | Tempo estimado | Recursos | Condição de execução | POP |
|---|---|---|---|---|---|---|---|
| PM-PLC-01 | Verificação de logs, uptime e alarmes do PLC | **30 dias** | Engenharia de Manutenção | 0,3 h por faixa | Notebook de serviço | Remoto ou pela cabine | POP-PLC-01 |
| PM-PLC-02 | Backup da configuração e conferência da tabela de categorias | **A cada alteração** de tabela ou firmware **+ 180 dias** | Engenharia de Manutenção | 0,5 h por faixa | Notebook de serviço | Fora do horário de pico | POP-PLC-01 |
| PM-PLC-03 | Inspeção do armário elétrico: temperatura, ventilação, fonte, cartões e DPS | **180 dias** | Eletricista autorizado (NR-10) | 1,0 h por faixa | Termômetro infravermelho, multímetro | NR-10 | POP-PLC-02 |

## Auditoria de classificação

| Código | Tarefa | Periodicidade | Responsável | Tempo estimado | Recursos | Condição de execução | POP |
|---|---|---|---|---|---|---|---|
| PM-AUD-01 | Auditoria de classificação: sistema × contagem manual ou por vídeo (mínimo de 200 veículos por faixa) | **90 dias** (padrão); **30 dias** em faixas com divergência acima de 1% na última auditoria | Engenharia de Manutenção + Operação da praça | 2,0 h por faixa | Vídeo da pista **usado só para contagem por classe — placas não são registradas** | Sem interdição | POP-AUD-01 |

## Câmeras de classificação (piloto do Tema 1, modo sombra)

| Código | Tarefa | Periodicidade | Responsável | Tempo estimado | Recursos | Condição de execução | POP |
|---|---|---|---|---|---|---|---|
| PM-CAM-01 | Limpeza de lente e conferência de enquadramento | **30 dias** | Equipe de campo ITS | 0,5 h | Kit de limpeza óptica | NR-35 se acima de 2 m | POP-CAM-01 |
| PM-CAM-02 | Relatório piloto × sensor de solo (divergências por tipo de veículo) | **30 dias** | Engenharia de Manutenção | 2,0 h | Relatório do edge computing | Remoto | — |
| PM-CAM-03 | Teste noturno do iluminador IR | **90 dias** | Equipe de campo ITS + CCO | 0,5 h | Comunicação com o CCO | Noturno | POP-CAM-01 |

## Controle de revisão

| Versão | Data | Alteração |
|---|---|---|
| v1.0 | 2026-10-20 | Versão inicial (domínio CFTV/PMV/laço) |
| v1.1 | 2026-11-07 | Domínio alterado para o sistema de classificação por eixos das pistas de pedágio |
