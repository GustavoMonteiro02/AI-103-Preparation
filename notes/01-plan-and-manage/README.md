# Plan and manage an Azure AI solution

Peso segundo o manual: **25–30%**.

Fonte: manual v3 em [docs](../../docs/README.md). Excertos de revisão agrupados por domínio; algumas secções são transversais.

## Manual — secção 4

Foundry resource: fronteira Azure onde vivem capacidades, identidade, rede, quotas e integrações.
Project: espaço lógico de trabalho para uma solução/equipa, com configurações e ligações aos recursos.
Model catalog: onde descobres modelos disponíveis; model deployment: instância/configuração consumível pela app.
Playgrounds: ambiente de experimentação; não substituem código, testes automatizados nem CI/CD.
Quotas/rate limits: planeia throughput, retries/backoff, concorrência e custos.
CI/CD: configura infraestrutura e deployments de forma repetível; separa dev/test/prod e segredos.
Pergunta típica — Se o requisito é “usar um modelo já disponível, expô-lo à aplicação e controlar quota/capacidade”, pensa em model deployment; se é “organizar ativos, ligações e experiências de uma solução”, pensa em project.

## Manual — secção 5

Escolha
Quando
Trade-off
Exemplo de requisito
LLM
Raciocínio/geração geral
Qualidade vs custo/latência
Assistente complexo, código, análise
SLM
Tarefa mais estreita/baixo custo
Menor capacidade geral
Classificação/extração simples em escala
Multimodal
Texto + imagem/áudio
Tokens/custo e segurança multimodal
Q&A visual, áudio contextual
Foundry Tool
Tarefa especializada
Menos flexível, mais previsível
PII, translation, speech, extraction
Model router
Vários modelos por request
Complexidade e avaliação
Balancear custo/qualidade automaticamente
Evaluation deve responder a duas perguntas: “o modelo/app faz a tarefa?” e “faz de forma segura, grounded e operacionalmente aceitável?”. Métricas relevantes incluem quality, relevance, groundedness, fabrication/hallucination rate, safety, latency, token usage e cost.

## Manual — secção 11

Identity: Entra ID, managed identity, keyless credentials; evitar segredos estáticos.
Authorization: RBAC, least privilege, scopes e separação de leitura/escrita.
Network: private networking/private endpoints quando exigido.
Content safety: filtros, moderation, risk detection e políticas multimodais.
Prompt injection: tratar input e retrieved content como não confiável; limitar tool access e validar ações.
Guardrails: regras de entrada/saída, tool policies, data boundaries, approvals e stop conditions.
Auditing: tracing, provenance, logs, approval records e versioning.
Evaluation: safety evaluators, red teaming e testes adversariais.
Operational controls: quotas, rate limits, budgets, retries, monitoring e incident response.

## Manual — secção 26

Risco
Mitigação típica
Secrets leakage
Managed identity/keyless auth; Key Vault quando segredo é inevitável; nunca hardcode.
Excesso de permissões
RBAC, scopes mínimos, separar read/write e ambientes.
Prompt injection direto
Tratar user input como não confiável; instructions robustas; policy/guardrails.
Indirect prompt injection
Conteúdo recuperado, documentos, webpages e imagens também são input não confiável.
Tool abuse
Allowlist, schema validation, authorization, approval para ações sensíveis, rate limits.
Data exfiltration
Private networking, data boundaries, ACL/security trimming, egress control quando aplicável.
Hallucinated actions
Structured output + deterministic validation antes de executar.
Runaway agents/cost
Budgets, token/tool limits, stop conditions, timeouts, max iterations.
Untraceable decisions
Tracing, provenance, correlation IDs, audit logs e approval records.
Unsafe multimodal content
Content filters/policy, visual safety e deteção de prompt injection em media.

## Manual — secção 27

Camada
Métricas/observações
Modelo/app generativa
Quality, relevance, fabrication/hallucination, safety, latency, token/cost.
RAG retrieval
Recall/relevance, top-k usefulness, index health, freshness, filters/ACL.
Resposta grounded
Groundedness, citation/provenance, answer relevance.
Agent
Task success, tool selection, tool-call accuracy, loops, autonomy violations, safety.
Workflow
Step failures, retries, checkpoint/resume, SLA, human wait time, end-to-end latency.
Speech/voice
Latency, recognition quality, interruption/turn handling, synthesis quality.
Content Understanding
Field accuracy/completeness, schema validity, extraction confidence, downstream errors.
Produção
Drift, safety events, quotas, scaling, rate limits, cost footprint, incidents.

Evaluation offline diz se a solução está pronta; observability online diz se continua saudável em produção.

## Manual — secção 34

Depois de comparar novamente o manual com o blueprint oficial do AI-103, a cobertura geral estava forte, mas havia alguns objetivos oficiais que apareciam apenas na checklist final ou de forma demasiado breve. Esta secção aprofunda esses pontos.
34.1 Reflection, self-critique e avaliações de reasoning
Reflection/self-critique: o sistema pode produzir uma primeira resposta, avaliá-la segundo critérios definidos e tentar melhorar o resultado antes de o devolver.
No exame, pensa nisto como um padrão de otimização/evaluation, não como substituto de grounding, validação ou regras de negócio.
Uma segunda passagem do mesmo modelo não garante verdade. Se o problema é conhecimento privado/atual, continua a ser necessário RAG/grounding.
Avaliações de reasoning devem medir a qualidade do processo e do resultado com critérios observáveis; em produção, evita depender de texto de raciocínio interno como mecanismo de auditoria.
Quando o enunciado pedir uma combinação de raciocínio flexível com regras obrigatórias, pensa em hybrid LLM + rules engine.
34.2 Observability mais granular
Tracing: correlaciona chamadas ao modelo, retrieval, tools, agents e workflow steps numa execução.
Token analytics: acompanha input/output tokens, custo por chamada, por utilizador, por agent e por workflow.
Latency breakdown: mede separadamente retrieval latency, model latency, tool/API latency e tempo total end-to-end.
Safety signals: acompanha content filters, policy violations, blocked tool calls e eventos de guardrails.
Agent error analysis: distingue erro de routing, tool selection, tool arguments, retrieval, grounding e geração final.
Uma solução lenta não implica necessariamente trocar de modelo: primeiro identifica em que camada está a latência.
34.3 Multimodal vision — objetivos específicos do blueprint
Visual Q&A: responder a perguntas com base em evidência contida numa ou mais imagens.
Captions: gerar descrições concisas ou detalhadas; extended descriptions dão mais contexto.
Alt text: produzir descrições adequadas a acessibilidade; o objetivo não é apenas descrever visualmente, mas tornar a informação útil a quem não vê a imagem.
Video analysis: processar e interpretar segmentos de vídeo, e não apenas frames isolados.
Regions/objects/components: identificar elementos ou regiões concretas dentro de imagens ou vídeo.
Não confundir vision-enabled LLM com Content Understanding: o primeiro raciocina de forma flexível; o segundo cria extração estruturada e pipelines previsíveis.
34.4 Responsible AI para conteúdo multimodal
Aplicar filtros para classificar conteúdo visual inseguro ou proibido.
Indirect prompt injection: texto malicioso pode estar incorporado numa imagem/documento e tentar alterar o comportamento do agent; trata conteúdo recuperado como não confiável.
Separar instruções de sistema das instruções encontradas nos dados e restringir tools/ações permitidas.
Visual policy controls podem incluir watermarks, brand rules, deteção de símbolos proibidos e sinalização de conteúdo inadequado.
Em ações de maior risco, acrescenta validação determinística e/ou human approval.
34.5 Speech — pontos que merecem ficar explícitos
Custom Speech: adaptar reconhecimento de fala a vocabulário, domínio ou condições acústicas específicas quando o cenário o exigir.
Audio multimodal reasoning: alguns modelos podem receber áudio como modalidade, permitindo raciocínio sobre o conteúdo sem reduzir mentalmente o problema apenas a STT tradicional.
Speech translation: pode combinar reconhecimento, tradução e, se necessário, síntese na língua de destino.
SpeechRecognizer/Synthesizer são componentes especializados; Voice Live é a opção mental para conversação bidirecional em tempo real, baixa latência, turn-taking e interrupções.
34.6 Information extraction e Content Understanding — detalhe adicional
O pipeline pode ingerir documentos, imagens, áudio e vídeo; a extração não está limitada a PDFs.
Enrichment skills podem transformar texto, imagem e layout antes da indexação/retrieval.
OCR converte conteúdo visual em texto; layout analysis preserva estrutura; field extraction transforma conteúdo em campos úteis.
Content Understanding pode produzir outputs estruturados ou Markdown limpo para downstream reasoning, RAG e agents.
Single-task e pro-mode devem ser reconhecidos como opções de pipeline/configuração no Content Understanding conforme a complexidade do cenário.
A pergunta de exame pode testar a diferença entre extrair campos estruturados e simplesmente perguntar a um LLM multimodal sobre um documento.

## Manual — secção 35

Pontuação mínima de aprovação: 700.
Tempo indicado pela Microsoft para o AI-103: 120 minutos.
O exame é proctored e pode incluir componentes interativos, não apenas perguntas de escolha múltipla.
Usa o Exam Sandbox da Microsoft para conhecer a interface e os tipos de interação antes do exame.
O exame está disponível em várias línguas; confirma a língua escolhida no momento do agendamento.
A Microsoft recomenda agendar com uma conta Microsoft pessoal (MSA) para manter os registos de certificação independentes da entidade empregadora.

## Registo pessoal

- [ ] Li e consigo explicar as decisões deste domínio.
- [ ] Resolvi um cenário prático.
- [ ] Registei erros em practice-tests.

Dúvidas e referências: a preencher.

