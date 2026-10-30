# Implement text analysis solutions

Peso segundo o manual: **10–15%**.

Fonte: manual v3 em [docs](../../docs/README.md). Excertos de revisão agrupados por domínio; algumas secções são transversais.

## Manual — secção 12

Serviço/conceito
Faz
Escolha típica
Azure Language
NER, PII, sentiment, language tasks
Extração/deteção previsível
Generative LLM
Reasoning e texto flexível
Resumo contextual, transformação complexa
Azure Speech
STT/TTS especializado
Reconhecimento/síntese controlados
Voice Live
Conversação voz realtime
Baixa latência, interrupções, turn-taking
Translator
Translation/transliteration
Tradução especializada e consistente
Speech MCP
Expõe speech como tool
Agent chama voz apenas quando precisa

## Manual — secção 28

A
B
Diferença decisiva
Azure Language PII/NER
LLM geral
Language é especializado/previsível; LLM é flexível e contextual.
Translator
LLM translation
Translator é serviço especializado; LLM é útil quando contexto/style/reasoning acrescenta valor.
Speech STT/TTS
Voice Live
Speech clássico para reconhecimento/síntese; Voice Live para conversa realtime bidirecional.
Vision multimodal
Content Understanding
Vision responde/raciocina livremente; CU extrai estrutura/analyzer/schema.
OCR/layout
Content Understanding
OCR/layout são componentes de extração; CU combina extração e entendimento multimodal em output estruturado.
Image understanding
Image generation
Um analisa media existente; o outro cria/edita media.
RAG
Fine-tuning
RAG fornece factos externos/atuais; fine-tuning altera comportamento/padrões, não é base de conhecimento dinâmica.
Session memory
RAG knowledge
Session mantém contexto de interação; RAG recupera conhecimento externo.
Tool calling
Workflow
Tool calling pode ser decidido pelo modelo; workflow impõe sequência/control flow.
Function tool
MCP tool
Função é integração específica; MCP é protocolo padronizado para expor/discover capabilities.

## Registo pessoal

- [ ] Li e consigo explicar as decisões deste domínio.
- [ ] Resolvi um cenário prático.
- [ ] Registei erros em practice-tests.

Dúvidas e referências: a preencher.

