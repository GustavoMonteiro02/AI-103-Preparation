# Implement information extraction solutions

Peso segundo o manual: **10–15%**.

Fonte: manual v3 em [docs](../../docs/README.md). Excertos de revisão agrupados por domínio; algumas secções são transversais.

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

## Extração estruturada

Fonte: secções 13 e 34.6. OCR converte conteúdo visual em texto; layout preserva estrutura; Content Understanding usa analyzers e schemas e pode produzir estrutura ou Markdown para RAG e agents. Validar os campos antes de os usar.

## Registo pessoal

- [ ] Li e consigo explicar as decisões deste domínio.
- [ ] Resolvi um cenário prático.
- [ ] Registei erros em practice-tests.

Dúvidas e referências: a preencher.

