# AI-103 Preparation — Gustavo Monteiro

Repositório de preparação para **Microsoft AI-103 — Developing AI Apps and Agents on Azure**, baseado nos manuais pessoais v3, preparados em outubro de 2026. Reúne leitura, notas por domínio, revisão de erros, roteiros de laboratório e um plano de capstone.

## Materiais principais

- [Manual completo — PDF](docs/AI-103_Manual_Completo_Gustavo_v3.pdf)
- [Manual completo — DOCX](docs/AI-103_Manual_Completo_Gustavo_v3.docx)
- [Proveniência e integridade](docs/README.md)

As notas referenciam secções do manual. Os planos e templates organizam o estudo; não representam código implementado, avaliações executadas ou experiência prática já concluída. Os pesos e regras abaixo refletem o manual, sem validação externa de atualidade nesta preparação.

## Organização

```text
AI-103-Preparation/
├── README.md
├── docs/                 # Manuais originais, proveniência e checksums
│   └── resources/        # Materiais Citizen Developer futuros
├── notes/                # Cinco domínios do manual
├── practice-tests/       # Template de score e revisão de erros
├── code-samples/         # Onze roteiros de laboratório
└── capstone/             # Plano de solução integrada
```

## Domínios de estudo

| Domínio | Peso no manual | Notas |
| --- | --- | --- |
| Plan and manage an Azure AI solution | 25–30% | [Abrir](notes/01-plan-and-manage/) |
| Implement generative AI and agentic solutions | 30–35% | [Abrir](notes/02-generative-ai-and-agents/) |
| Implement computer vision solutions | 10–15% | [Abrir](notes/03-computer-vision/) |
| Implement text analysis solutions | 10–15% | [Abrir](notes/04-text-analysis/) |
| Implement information extraction solutions | 10–15% | [Abrir](notes/05-information-extraction/) |

## Como estudar

1. Ler o manual e rever as [notas por domínio](notes/).
2. Explicar as escolhas e trade-offs sem consultar o material.
3. Implementar os [laboratórios](code-samples/) e registar versões, resultados, erros e custos.
4. Fazer simulados com o [template](practice-tests/TEMPLATE.md), rever erros e voltar aos tópicos fracos.
5. Consolidar tudo no [capstone](capstone/).

A prioridade sugerida pelo manual (secção 36) é planeamento/gestão e GenAI/agents, seguidos de Vision, Text/Speech e Information Extraction. A secção 35 reporta 120 minutos e pontuação de aprovação de 700; percentagens de simulados não equivalem à escala oficial.

## Série Microsoft Learn — 26 episódios estudados

O estado de estudo vem do pedido de Gustavo, não de uma verificação de conclusão. Os títulos seguem a secção 3 do manual. A série tem 26 episódios segundo o manual, que confirma apenas 25 títulos; o título oficial do episódio 26 fica pendente.

[Série oficial](https://aka.ms/AI-103onYouTube)

| Episódio | Título segundo o manual | Estado |
| --- | --- | --- |
| 1 | Plan and prepare to develop AI solutions on Azure | Estudado (indicação do pedido) |
| 2 | Select, deploy, and evaluate Microsoft Foundry models | Estudado (indicação do pedido) |
| 3 | Develop a generative AI chat app with Microsoft Foundry | Estudado (indicação do pedido) |
| 4 | Develop generative AI apps that use tools | Estudado (indicação do pedido) |
| 5 | Optimize generative AI model performance with Microsoft Foundry | Estudado (indicação do pedido) |
| 6 | Implement a responsible generative AI solution in Microsoft Foundry | Estudado (indicação do pedido) |
| 7 | Develop AI agents with Microsoft Foundry and Visual Studio Code | Estudado (indicação do pedido) |
| 8 | Integrate custom tools into your agent | Estudado (indicação do pedido) |
| 9 | Integrate MCP tools with Azure AI agents | Estudado (indicação do pedido) |
| 10 | Build knowledge-enhanced AI agents with Foundry IQ | Estudado (indicação do pedido) |
| 11 | Integrate your agent with Microsoft 365 | Estudado (indicação do pedido) |
| 12 | Build agent-driven workflows using Microsoft Foundry | Estudado (indicação do pedido) |
| 13 | Develop an AI agent with the Microsoft Agent Framework | Estudado (indicação do pedido) |
| 14 | Orchestrate a multi-agent solution using the Microsoft Agent Framework | Estudado (indicação do pedido) |
| 15 | Analyze text with Azure Language in Foundry Tools | Estudado (indicação do pedido) |
| 16 | Develop a text analysis agent with the Azure Language MCP server | Estudado (indicação do pedido) |
| 17 | Develop a speech-capable generative AI application | Estudado (indicação do pedido) |
| 18 | Create speech-enabled apps with Microsoft Foundry | Estudado (indicação do pedido) |
| 19 | Develop a speech agent with the Azure Speech MCP server | Estudado (indicação do pedido) |
| 20 | Develop an Azure Speech Voice Live agent in Microsoft Foundry | Estudado (indicação do pedido) |
| 21 | Translate text and speech with Microsoft Foundry Tools | Estudado (indicação do pedido) |
| 22 | Develop a vision-enabled generative AI application | Estudado (indicação do pedido) |
| 23 | Generate images and video | Estudado (indicação do pedido) |
| 24 | Analyze images with Content Understanding | Estudado (indicação do pedido) |
| 25 | Analyze documents with Content Understanding | Estudado (indicação do pedido) |
| 26 | Título oficial não confirmado no manual; capítulo de integração final | Estudado (indicação do pedido) |

## Dois vídeos de revisão

| Vídeo | Referência | Limitação |
| --- | --- | --- |
| John Savill — AI-103 Develop AI Apps and Agents on Azure Study Cram | [YouTube](https://www.youtube.com/watch?v=WK2BvjOYTCQ) | Síntese transversal na secção 14 do manual |
| Segundo overview fornecido por Gustavo | [YouTube](https://youtu.be/nUIPbpVjOc4?is=X75dbjR7RI-Uqksl) | Título, transcript e conteúdo exclusivo não confirmados no manual; secção 15 |

## Recursos Citizen Developer

Os slides e exemplos serão fornecidos mais tarde. Guardar slides em [docs/resources](docs/resources/) e código nas pastas relevantes de [code-samples](code-samples/), preservando origem e versões. Ainda não estão incluídos.

## Referências presentes no manual

- [Study Guide AI-103](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103) — o manual refere competências de 16 de abril de 2026.
- [Curso AI-103T00](https://learn.microsoft.com/en-us/training/courses/ai-103t00)
- [Página do exame](https://learn.microsoft.com/credentials/certifications/exams/ai-103/)

## Privacidade e manutenção

Destino pretendido: `GustavoMonteiro02/AI-103-Preparation`, privado. A preparação local não verifica nem altera a visibilidade remota. Confirmar acesso e visibilidade privada antes de enviar os manuais. Não publicar credenciais, dados empresariais ou resultados sensíveis; configurar segredos fora do código.

Atualizar notas com referência à secção e versão do manual. Acrescentar novas fontes apenas quando recebidas/verificadas; não preencher lacunas com títulos, código ou resultados presumidos.

