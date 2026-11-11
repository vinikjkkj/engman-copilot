# Glossário de Siglas e Termos — v1.1

> **Origem: real.** Definições de domínio público em manutenção, confiabilidade e pedágio, redigidas pelo grupo.
> Termos específicos deste projeto (TAG, modo de falha, P1–P4) estão marcados com **[projeto]**.

| Campo | Valor |
|---|---|
| Código do documento | `KB-D05` |
| Uso no assistente | Indexado no RAG — **1 chunk por termo** (metadado `tipo_documento=glossario`) |

## Pista de pedágio e classificação

| Termo | Significado |
|---|---|
| **Classificação veicular** | Definição da categoria tarifária do veículo, em geral pelo número de eixos e pelo tipo de rodagem (simples ou dupla). |
| **Categoria tarifária** | Faixa de tarifa do pedágio associada a um tipo de veículo (ex.: 2 eixos com rodagem simples, 3 eixos, 6 eixos). |
| **Eixo suspenso** | Eixo de caminhão que fica levantado, sem tocar o solo, quando o veículo circula vazio. Pela Lei nº 13.103/2015, veículos de carga vazios ficam isentos de pedágio sobre os eixos que mantiverem suspensos, por isso a contagem correta importa. |
| **Rodagem dupla** | Eixo com dois pneus de cada lado; muda a categoria tarifária. |
| **Laço indutivo** | Espira de fio embutida numa ranhura do pavimento. A passagem de massa metálica altera a indutância e o detector gera um pulso; usado para detectar presença e separar um veículo do outro. |
| **Sensor de eixo vulcanizado** | Sensor (em geral piezoelétrico) embutido no pavimento e fixado com resina. Gera um pulso a cada eixo que passa por cima; é o "sensor de solo vulcanizado" citado no briefing. Depende muito da qualidade do pavimento. |
| **Piezoelétrico** | Material que gera tensão elétrica quando é pressionado; base dos sensores de eixo. |
| **Amplitude de sinal** | Intensidade do pulso gerado pelo sensor de eixo. Cai com o desgaste e o descolamento; abaixo de um limiar, eixos deixam de ser contados. |
| **Contagem dupla** | Um eixo registrado duas vezes (por exemplo, por borda solta que vibra), gerando cobrança a maior. |
| **PLC / CLP** | Controlador Lógico Programável — o controlador de pista recebe os pulsos de laço e sensor de eixo, aplica a tabela de categorias e envia a passagem ao sistema de arrecadação. |
| **Watchdog** | Mecanismo que reinicia o controlador automaticamente se ele parar de responder. |
| **Uptime** | Tempo que o equipamento está ligado desde o último reinício. |
| **Câmera de classificação** | Câmera lateral com processamento local (edge computing) que conta eixos por imagem; neste projeto é um **piloto em modo sombra** do Tema 1. |
| **Modo sombra** **[projeto]** | O equipamento novo funciona em paralelo e seus resultados são só comparados com o sistema oficial; **não** é usado para tarifar. |
| **Edge computing** | Processamento feito no próprio equipamento de campo, sem enviar a imagem para um servidor central. |
| **Auditoria de classificação** | Comparação entre a categoria registrada pelo sistema e uma contagem manual ou por vídeo, por amostra de veículos. |
| **Veículo-padrão** | Veículo de serviço com número de eixos conhecido, usado para testar a contagem. |
| **AVI** | *Automatic Vehicle Identification* — leitura automática de TAG veicular nas faixas automáticas. *(Fora do recorte desta versão.)* |
| **Free flow** | Cobrança sem cabine, por pórticos com antenas e câmeras OCR. *(Fora do recorte desta versão.)* |
| **OCR** | *Optical Character Recognition* — leitura automática de placas por imagem. Gera **dado pessoal** (ver LGPD). |
| **CCO** | Centro de Controle Operacional — monitora a rodovia 24 h, recebe alarmes e despacha equipes. |
| **DPS** | Dispositivo de Proteção contra Surtos — protege o equipamento contra descargas atmosféricas. |

## Manutenção

| Termo | Significado |
|---|---|
| **Corretiva** | Intervenção após a falha, para restabelecer a função. |
| **Preventiva** | Intervenção por calendário, antes da falha (ex.: teste de amplitude a cada 30 dias). |
| **Inspeção** | Verificação do estado do ativo sem necessariamente intervir. |
| **CBM** | *Condition-Based Maintenance* — manutenção baseada em condição: a intervenção é disparada por uma medição (isolação, amplitude, divergência), não pelo calendário. |
| **RCM** | *Reliability-Centered Maintenance* — Manutenção Centrada em Confiabilidade: método para escolher a estratégia de manutenção de cada modo de falha. |
| **WCM** | *World Class Manufacturing/Maintenance* — programa de excelência operacional com foco em eliminar perdas. |
| **FSM** | *Field Service Management* — sistema que registra as ordens de serviço e os atendimentos de campo. Fonte do histórico de falhas. |
| **OS** | Ordem de Serviço — registro formal de uma intervenção a executar. |
| **POP** | Procedimento Operacional Padrão — passo a passo oficial de uma tarefa, com pré-requisitos de segurança. |
| **APR** | Análise Preliminar de Risco — avaliação dos riscos da tarefa antes de executá-la. |
| **PT** | Permissão de Trabalho — autorização formal para executar uma tarefa de risco. |
| **EPI** | Equipamento de Proteção Individual. |
| **Revulcanização** | Refazer a fixação do sensor de eixo com resina, total ou parcialmente. |
| **Retrofit** | Modernização ou substituição de um ativo por tecnologia mais nova (ex.: trocar sensor de solo por câmera). |
| **TAG** **[projeto]** | Identificador único do ativo: `TTT-Pn-Fnn-NN`, em que TTT = `LAC` (laço), `EIX` (sensor de eixo), `PLC` (controlador) ou `CAM` (câmera); Pn = praça; Fnn = faixa; NN = sequencial. |
| **Modo de falha** **[projeto]** | Categoria padronizada da causa no histórico (ex.: `sinal_fraco_sensor`, `plc_travamento`). `falso_positivo_operacional` e `indeterminado` **não** contam como falha de ativo. |
| **Reincidência** **[projeto]** | Mesma combinação TAG + modo de falha registrada nos 90 dias anteriores. |
| **P1–P4** **[projeto]** | Prioridade da OS, calculada pela Matriz de Criticidade (KB-D04). |

## Confiabilidade

| Termo | Significado |
|---|---|
| **λ (lambda)** | Taxa de falhas: número de falhas ÷ tempo de operação (ex.: falhas por hora). |
| **MTBF** | *Mean Time Between Failures* — tempo médio entre falhas = tempo de operação ÷ número de falhas = 1/λ. |
| **MTTR** | *Mean Time To Repair* — tempo médio de reparo. |
| **R(t)** | Confiabilidade: probabilidade de o ativo operar sem falhar até o tempo *t*. No modelo exponencial, R(t) = e^(−λt). |
| **Modelo exponencial** | Supõe **taxa de falhas constante** (sem desgaste nem melhoria). Simples, mas otimista quando o ativo está se deteriorando. |
| **RGA** | *Reliability Growth Analysis* — análise da tendência da taxa de falhas ao longo do tempo. |
| **Crow-AMSAA (β)** | Modelo de RGA. **β > 1**: falhas ficando mais frequentes (deterioração); **β ≈ 1**: taxa estável; **β < 1**: melhoria. |
| **LDA** | *Life Data Analysis* — análise de dados de vida (ex.: distribuição de Weibull) para estimar vida útil e desgaste. |
| **Weibull** | Distribuição usada em LDA; o parâmetro de forma indica mortalidade infantil (< 1), falhas aleatórias (≈ 1) ou desgaste (> 1). |

## Normas e privacidade

| Termo | Significado |
|---|---|
| **NR-10** | Norma Regulamentadora de segurança em instalações e serviços em eletricidade. |
| **NR-35** | Norma Regulamentadora de trabalho em altura (acima de 2 m do nível inferior, com risco de queda). |
| **ART** | Anotação de Responsabilidade Técnica — registro que vincula um profissional habilitado a um serviço ou laudo. O assistente **não** emite. |
| **LGPD** | Lei Geral de Proteção de Dados Pessoais (Lei nº 13.709/2018). |

## IA (para leitores do repositório)

| Termo | Significado |
|---|---|
| **LLM** | *Large Language Model* — modelo de linguagem que gera as respostas do assistente. |
| **RAG** | *Retrieval-Augmented Generation* — recuperar trechos da base e colocá-los no contexto antes de o modelo responder. |
| **Tool** | Função que o modelo pode pedir para executar (ex.: consultar o histórico) e cujo resultado volta ao contexto. |
| **Chunk** | Trecho de documento indexado no banco vetorial. |
