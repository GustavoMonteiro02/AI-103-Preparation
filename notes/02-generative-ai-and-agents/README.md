# Implement generative AI and agentic solutions

Peso segundo o manual: **30–35%**.

Fonte: manual v3 em [docs](../../docs/README.md). Excertos de revisão agrupados por domínio; algumas secções são transversais.

## Manual — secção 6

Chat Completions: padrão clássico baseado em mensagens system/user/assistant.
Responses API: interface moderna para respostas com tools, multimodalidade e fluxos agentic; pode simplificar novas aplicações.
Foundry SDK: abstrações Azure/Foundry para projeto, agents, deployments e integrações.
Microsoft Agent Framework: camada acima da inferência/provider para agents, sessions, tools e orchestration.
Conversations/session state: contexto persistente não é o mesmo que knowledge/RAG.
Hierarquia mental — Agent Framework → provider/inference API (Responses ou Chat Completions, dependendo do client) → model. O framework abstrai detalhes; não tens de chamar manualmente todas as APIs subjacentes em cada cenário.

## Manual — secção 7

1.  Ingest: recolher documentos/media.
2.  Extract/enrich: OCR, layout, Content Understanding ou skills.
3.  Chunk: dividir preservando contexto e metadata.
4.  Embed: converter chunks em vetores quando usas vector search.
5.  Index: armazenar campos, metadata e vectors no Azure AI Search.
6.  Retrieve: keyword, vector, semantic ou hybrid search.
7.  Ground: fornecer evidência recuperada ao modelo/agent.
8.  Generate: produzir resposta com base na evidência.
9.  Evaluate: relevance, groundedness, citation/provenance e search health.
Search
Força
Quando usar
Keyword
Termos exatos
IDs, nomes, palavras-chave
Vector
Semântica
Perguntas semelhantes em significado
Semantic
Re-ranking/entendimento semântico
Melhorar relevância de resultados textuais
Hybrid
Combina lexical + vector
Default robusto em muitos RAGs empresariais
Memory vs Knowledge — Memory lembra contexto da interação/utilizador. Knowledge fornece factos/documentos externos para grounding. Não são sinónimos.

## Manual — secção 8

Agent: entidade com role/goal/instructions, model, tools, knowledge e state/session.
Tool: capability que o agent pode pedir; a execução é feita por código/serviço, não “magicamente” pelo LLM.
MCP: contrato padronizado para expor tools/resources/context; não é um LLM nem um workflow.
Prompt agent: mais declarativo/gerido; hosted/custom agent: mais controlo de runtime/orchestration.
Agent Framework: framework de código para criar agents, sessions e workflows multi-step/multi-agent.

## Manual — secção 9

Um dos padrões mais importantes para o AI-103 é misturar raciocínio probabilístico com software determinístico. Exemplo:
Pipeline — Evento/HTTP → código determinístico (validar/preparar) → Agent A → API externa → validação/regras → Agent B → HITL/aprovação → persistência/SharePoint.

Usa código para regras exatas, validações, ficheiros, cálculos, API calls e compliance obrigatório.
Usa LLM/agent para interpretação, classificação semântica, reasoning e decisões com ambiguidade.
Usa workflow quando a ordem deve ser explícita e auditável.
Usa HITL quando uma ação precisa de aprovação ou input humano.
Usa checkpoint/persisted state quando o processo pode parar e retomar mais tarde.

## Manual — secção 10

Padrão
Ideia
Usa quando
Sequential
A → B → C
Etapas especializadas dependentes
Concurrent
A, B, C em paralelo
Tarefas independentes/latência
Handoff
Um agent transfere controlo
Especialistas por domínio
Group Chat
Agents dialogam num contexto comum
Debate/consenso controlado
Manager/Magentic
Coordenador escolhe especialistas
Problemas complexos e dinâmicos
Regra de ouro — Começa com uma chamada simples; sobe para agent; sobe para workflow/multi-agent apenas quando existe uma necessidade real de tools, estado, especialização ou controlo.

## Manual — secção 23

RAG é um pipeline, não apenas “ligar documentos ao chat”. Em perguntas de exame, identifica em que fase está o problema: ingestão, enriquecimento, indexação, retrieval, grounding ou evaluation.
Ingestão: recolher conteúdo de Blob, SharePoint, bases de dados, APIs, documentos e media.
Extração/enrichment: OCR, layout, Content Understanding e skills podem transformar conteúdo bruto antes da indexação.
Chunking: dividir conteúdo em unidades recuperáveis. Chunks demasiado pequenos perdem contexto; demasiado grandes reduzem precisão e aumentam tokens.
Metadata: guarda source, document ID, timestamp, ACL, section/title e outros filtros úteis. Metadata é crítica para security trimming e filters.
Embeddings: representação vetorial usada para semelhança semântica. Não substitui o conteúdo original nem a metadata.
Index: define campos pesquisáveis, filtráveis, ordenáveis e vetoriais conforme o cenário.
Retrieval keyword: excelente quando termos exatos importam.
Vector search: encontra semelhança semântica mesmo com vocabulário diferente.
Hybrid search: combina lexical + vector; frequentemente é uma base forte para RAG empresarial.
Semantic ranking: pode reordenar resultados com compreensão semântica para melhorar relevance.
Grounding: os resultados recuperados são contexto/evidência; o prompt deve instruir o modelo a responder com base neles.
Citações/provenance: quando o cenário pede auditabilidade, preserva origem e referências dos chunks.
Evaluation: mede retrieval relevance e groundedness separadamente. Uma resposta má pode vir de retrieval má mesmo que o modelo seja bom.
Diagnóstico rápido: “não encontrou o documento certo” = retrieval/index problem. “Encontrou a evidência certa mas inventou” = generation/grounding/prompt/safety problem.

## Manual — secção 24

Conceito
Responsabilidade
Não confundir com
Modelo
Gerar/raciocinar sobre input
Agent completo
Agent
Modelo + instructions + tools + knowledge + state/policy
Workflow determinístico
Tool/function
Capacidade externa que pode ser solicitada
O LLM executar a ação diretamente
MCP server
Expor tools/resources através de protocolo padronizado
Modelo, agent ou workflow
Session/conversation
Estado/contexto de interação
Knowledge base/RAG
Knowledge
Dados externos usados para grounding
Memória de conversa
Workflow
Orquestração explícita de passos/eventos
Tool calling dinâmico
Checkpoint
Snapshot para retomar/replay de workflow
Uma nova conversa
HITL
Pedido/approval externo e retoma
Outro agent “humano”

Tool calling — ciclo lógico
O modelo recebe instructions, contexto e descrição das tools.
O modelo decide que precisa de uma tool e produz argumentos estruturados.
A aplicação valida os argumentos e a autorização.
O código/serviço executa a tool.
O resultado da tool volta ao modelo/agent ou ao workflow.
O modelo continua o reasoning ou produz resposta final.
Ponto de exame: o modelo não “executa a API”. Ele pede a chamada; a aplicação/tool runtime executa-a.

## Manual — secção 25

O Microsoft Agent Framework deve ser visto como uma camada de programação para agents, sessions, tools e workflows. Não é um modelo e não elimina o provider de inferência.
Quando
Padrão
Um agent e algumas tools chegam
Agent simples + session/state
A ordem tem de ser garantida
Workflow explícito com executors/steps
Passos independentes podem correr juntos
Concurrent/parallel orchestration
Um especialista transfere controlo
Handoff
Vários agents colaboram numa conversa
Group chat
Um coordenador escolhe especialistas
Manager/Magentic-like orchestration
Processo longo precisa parar/retomar
Checkpoint + persisted state
Precisa de aprovação/input externo
Request/HITL + resume

Pseudocódigo mental — workflow híbrido
input_file = download_from_sharepoint()validated = validate_and_reduce(input_file)order = await agent_a.run(validated)output_file = apply_order_deterministically(input_file, order)assert validate_output(output_file)api_result = call_business_api(output_file)summary = await agent_b.run(api_result)approval = await request_human_approval(summary)if approval:    upload_to_sharepoint(output_file)
Este padrão é exatamente o que o exame quer que saibas arquitetar: reasoning onde existe ambiguidade; código onde existe uma regra exata.

## Registo pessoal

- [ ] Li e consigo explicar as decisões deste domínio.
- [ ] Resolvi um cenário prático.
- [ ] Registei erros em practice-tests.

Dúvidas e referências: a preencher.

