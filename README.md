# 📓 Caderno Temático NotebookLM — Automação com Inteligência Artificial

> Estudo estruturado sobre **agentes de IA, automação de workflows (n8n), RAG e ferramentas de codificação agêntica**, construído com o [NotebookLM](https://notebooklm.google.com) a partir de fontes abertas em vídeo do canal *Nate Herk | AI Automation*.

---

## 1. Contexto e Objetivos

**Assunto escolhido:** Automação com Inteligência Artificial — como projetar, construir e colocar em produção agentes de IA e workflows automatizados usando ferramentas low-code (n8n) e agentes de codificação (Claude Code, Codex, Antigravity).

**Por que esse tema?** A automação com IA é uma das habilidades mais demandadas do mercado atual, mas o conteúdo disponível é disperso, cheio de hype e muda toda semana. O objetivo deste caderno é transformar dezenas de horas de vídeo em um material de consulta confiável e estruturado.

**Objetivos de estudo:**

1. Entender a arquitetura de um agente de IA (cérebro/LLM, memória, ferramentas e system prompt) e quando usar agentes vs. workflows determinísticos;
2. Dominar os blocos fundamentais do n8n (triggers, ações, transformação de dados, lógica e memória);
3. Compreender o pipeline completo de RAG (chunking → embeddings → vector database → retrieval → reranking);
4. Comparar as principais ferramentas de codificação agêntica do mercado (Claude Code, OpenAI Codex, Google Antigravity);
5. Aprender boas práticas para levar automações de IA à produção (segurança, logs, QA, gestão de contexto).

---

## 2. Curadoria de Fontes

Fontes abertas (vídeos gratuitos no YouTube) selecionadas e carregadas no NotebookLM:

| # | Fonte | Tema | Link |
|---|-------|------|------|
| 1 | Everything I Learned About AI Agents in 2024 in 19 Minutes | Fundamentos de agentes de IA | [YouTube](https://www.youtube.com/watch?v=pYelCIqkm5Y) |
| 2 | n8n Masterclass: Build AI Agents & Automate Workflows (Beginner to Pro) | Workflows e agentes no n8n | [YouTube](https://www.youtube.com/watch?v=ZHH3sr234zY) |
| 3 | Build & Sell n8n AI Agents (8+ Hour Course, No Code) | Curso completo de agentes no n8n | [YouTube](https://www.youtube.com/watch?v=Ey18PDiaAYI) |
| 4 | From Zero to RAG Agent: Full Beginner's Course (no code) | RAG e bases de conhecimento | [YouTube](https://www.youtube.com/watch?v=cCD303XsUjI) |
| 5 | 100 Hours Testing Claude Code vs Antigravity (honest results) | Ferramentas de codificação agêntica | [YouTube](https://www.youtube.com/watch?v=99VHENEKA9o) |

> O notebook completo contém 265 fontes do mesmo canal; as 5 acima foram as mais citadas pelo NotebookLM nas respostas e formam o núcleo do estudo.

---

## 3. Engenharia de Prompts e "Cicatrizes" 🩹

### Perguntas estratégicas elaboradas

**Prompt 1 — Comparação de ferramentas**

> "Quais as diferenças entre Claude Code, Codex e Anti-gravity?"

*Resultado:* resposta organizada em 4 eixos (UX, modelos/capacidade técnica, pontos fortes e maturidade/preço), com citações diretas das fontes. Destaques: Claude Code como "planejador criativo" (CLI, contexto de 1M tokens, 80,9% no SWE-bench Verified), Antigravity como "designer visual rápido" (IDE standalone, Gemini, 76,2% no SWE-bench) e Codex como "executor eficiente" (respostas 2–5x mais concisas, git worktrees nativos, QA automatizado).

**Prompt 2 — Resumo estruturado**

> "Com base nas fontes deste notebook, crie um RESUMO ESTRUTURADO dos principais temas de automação com IA, organizado por tópicos: (1) O que são agentes de IA e como funcionam; (2) Construção de workflows de automação com n8n; (3) RAG e bases de conhecimento; (4) Ferramentas de codificação agêntica (Claude Code, Codex); (5) Boas práticas para colocar agentes em produção. Seja objetivo e cite as fontes."

*Resultado:* resumo completo dos 5 tópicos com referências às fontes (ver seção 4.1).

**Prompt 3 — Glossário**

> "Crie um GLOSSÁRIO com os 15 conceitos técnicos mais importantes abordados nas fontes (ex: Agente de IA, RAG, embeddings, vector database, chunking, MCP, human in the loop, system prompt, trigger, webhook, context window, workflow determinístico). Formato: termo em negrito seguido de definição curta de 1-2 frases."

*Resultado:* glossário padronizado com 15 termos (ver seção 4.2).

### Variações testadas e o que aprendi (troubleshooting)

- **Prompt genérico vs. estruturado:** perguntas abertas do tipo "me explique automação com IA" retornavam respostas rasas misturando assuntos — com 265 fontes no notebook, a IA tenta cobrir tudo. **Correção:** numerar explicitamente os tópicos desejados no prompt ("(1)... (2)... (3)...") forçou a organização e melhorou drasticamente a resposta.
- **Formato de saída:** sem especificar formato, o glossário vinha em prosa corrida. **Correção:** definir o formato no prompt ("termo em negrito + definição de 1-2 frases") padronizou a saída e facilitou a cópia para este README.
- **Erros de transcrição das fontes em vídeo:** como as fontes são vídeos, a transcrição automática introduz erros nos termos técnicos — o NotebookLM respondeu "claw.md" quando o correto é `CLAUDE.md` e "agents.mmd" em vez de `AGENTS.md`. **Lição:** sempre validar nomes técnicos citados pela IA contra a documentação oficial antes de usar.
- **Sugestões de desvio:** ao final de cada resposta o NotebookLM sugere transformar o conteúdo em podcast/quiz/gráfico — útil, mas desvia do objetivo se aceito sem critério. Manter o foco no roteiro de perguntas planejado.
- **Pedir citações explicitamente** ("cite as fontes") fez cada afirmação vir ancorada em um vídeo específico, o que permitiu montar a curadoria de fontes da seção 2 com base em evidência real de uso.

---

## 4. Miniguia de Estudo (Entrega Final)

### 4.1 Resumos estruturados

#### 🤖 Agentes de IA

Agentes de IA operam de forma autônoma, gerenciando processos complexos de múltiplas etapas sem entrada constante do usuário. Sua arquitetura tem 4 componentes: o **agente central (cérebro)**, que raciocina via LLM; a **memória** (curto e longo prazo), que retém contexto; as **ferramentas** (APIs e scripts externos — os "braços e pernas" do agente); e o **system prompt**, que funciona como a descrição de cargo do agente. Por decidirem livremente quais ferramentas chamar e em que ordem, agentes são **não-determinísticos** (imprevisíveis) — o oposto de workflows lineares.

#### 🔧 Workflows de automação com n8n

O n8n é uma plataforma visual low-code/no-code que conecta APIs por meio de "nós". Há duas abordagens: **workflows de IA** (lineares, determinísticos, previsíveis) e **agentes autônomos** (nó *AI Agent*, que combina LLM + memória + ferramentas). Os blocos de um fluxo: nós de **Gatilho** (e-mail, Slack, formulário, agendamento), de **Ação** (Google Drive, mensagens), de **Transformação de Dados** (*Set/Edit Fields*, *Aggregate*, *Merge*), de **Lógica** (*Switch*, *Wait*) e de **Memória** (*Window Buffer Memory*). Para escalar, tarefas repetitivas devem virar **subworkflows modulares** reutilizáveis via *Call n8n Workflow Tool*.

#### 📚 RAG e bases de conhecimento

RAG (Retrieval-Augmented Generation) permite que o agente busque dinamicamente dados externos ao seu treinamento. Pipeline: documentos → **chunking** (fragmentação via text splitter) → **embeddings** (vetorização semântica) → armazenamento em **vector database** (Pinecone, Supabase). Na consulta, a pergunta é vetorizada, os vetores mais próximos são recuperados por similaridade semântica e entregues ao LLM. Otimizações: **metadados** (rastreabilidade) e **reranker** (reclassifica os fragmentos e entrega só os mais relevantes). ⚠️ Vector DBs **não** servem para dados tabulares (use SQL) nem para documentos pequenos que cabem inteiros no contexto (*full context method*).

#### 💻 Ferramentas de codificação agêntica

**Claude Code** (Anthropic): CLI integrada ao terminal, contexto de 1M tokens, modos de planejamento profundo (*Ultra Plan*/*Ultra Think*), diretrizes globais via `CLAUDE.md`, forte em raciocínio abstrato e brainstorming — 80,9% no SWE-bench Verified. **Codex** (OpenAI): "máquina de entrega" multiplataforma (terminal, desktop, web), contexto de 256–400k tokens, git worktrees nativos, QA automatizado e geração de imagens para mockups; execução pragmática com respostas 2–5x mais concisas. **Antigravity** (Google): IDE standalone com Gemini, ótima em front-ends do zero, mas em preview e sujeita a *guideline drift* em projetos longos.

#### 🚀 Boas práticas de produção

1. **Priorize workflows determinísticos** — só use agentes quando a tarefa exigir decisões livres;
2. **Prompting reativo** — comece o system prompt vazio, adicione uma ferramenta por vez, teste e ajuste (prompts longos escritos "de uma vez" dificultam o debug);
3. **Gerencie a janela de contexto** — arquivos de diretrizes com menos de 150–200 linhas, `/compact` e `/clear` para evitar *context rot*, subagentes para tarefas de leitura pesada;
4. **Separe ambientes** — manutenção só em ambiente de teste, com backups e QA com dezenas de cenários antes do lançamento;
5. **Logs detalhados** — registre inputs, outputs, ferramentas chamadas e erros de cada execução;
6. **Segurança** — chaves de API em variáveis de ambiente (`.env`) e autenticação em webhooks de entrada.

### 4.2 Glossário

| Termo | Definição |
|-------|-----------|
| **Agente de IA** | Sistema autônomo baseado em LLM que formula estratégias, toma decisões e executa ações de forma proativa. Decide de forma não-determinística quais ferramentas chamar e em qual ordem. |
| **RAG (Retrieval-Augmented Generation)** | Técnica que permite ao modelo buscar dinamicamente dados externos no momento da consulta, respondendo com base em fatos atualizados em vez de "adivinhar". |
| **Embeddings** | Representações numéricas que capturam o significado semântico de um texto, permitindo buscas por proximidade de significado. |
| **Vector Database** | Banco que armazena dados não estruturados como vetores num espaço multidimensional, permitindo busca por similaridade semântica (ex.: Pinecone, Supabase). |
| **Chunking** | Fragmentação de documentos extensos em blocos menores antes da vetorização, necessária pelos limites e custos das janelas de contexto. |
| **MCP (Model Context Protocol)** | Protocolo aberto que atua como camada de tradução universal entre agentes de IA e ferramentas externas, simplificando a descoberta e uso de APIs. |
| **Human in the Loop** | Padrão em que a automação pausa e aguarda revisão/aprovação humana antes de concluir uma ação crítica — essencial para confiabilidade em produção. |
| **System Prompt** | Conjunto fixo de instruções que define papel, persona e regras do agente; não muda entre interações, ao contrário das mensagens do usuário. |
| **Trigger (Gatilho)** | Evento que inicia a execução de uma automação: agendamento, mensagem recebida, novo dado inserido etc. |
| **Webhook** | Gatilho que recebe dados de aplicações externas via uma URL pública, integrando plataformas como o n8n a canais de terceiros. |
| **Context Window** | Memória operacional do modelo — o limite total de tokens que ele processa de uma vez. Quando enche, o desempenho degrada (*context rot*). |
| **Workflow Determinístico** | Fluxo previsível que segue uma sequência fixa de etapas; não toma decisões independentes e garante consistência total. |
| **Token** | Menor unidade de texto que o modelo processa (~3-4 caracteres); base de cobrança tanto na entrada quanto na saída. |
| **Reranker** | Otimização de RAG que reavalia e pontua os vetores recuperados, entregando ao agente apenas os fragmentos mais relevantes. |
| **Subagente** | Agente especializado e isolado ao qual o orquestrador delega subtarefas; usar modelos mais simples em subagentes reduz consumo de tokens. |

### 4.3 Prompts reutilizáveis para revisão

```text
1. REVISÃO GERAL
"Com base nas fontes, crie um resumo estruturado de [TÓPICO], organizado
em tópicos numerados, citando as fontes de cada afirmação."

2. QUIZ DE AUTOAVALIAÇÃO
"Gere 10 perguntas de múltipla escolha sobre [TÓPICO], com gabarito
comentado ao final, baseadas exclusivamente nas fontes."

3. COMPARAÇÃO TÉCNICA
"Compare [FERRAMENTA A] e [FERRAMENTA B] em uma tabela com os eixos:
interface, modelos, pontos fortes, limitações e preço. Cite as fontes."

4. EXPLICAÇÃO EM NÍVEIS
"Explique [CONCEITO] em 3 níveis: (1) para um leigo, (2) para um
iniciante técnico, (3) para um profissional. Use analogias no nível 1."

5. CHECKLIST DE PRODUÇÃO
"Crie um checklist prático de boas práticas para colocar [TIPO DE
AUTOMAÇÃO] em produção, com base nas recomendações das fontes."

6. GLOSSÁRIO INCREMENTAL
"Liste os termos técnicos mencionados nas fontes sobre [TÓPICO] que ainda
NÃO estão no meu glossário atual: [colar glossário]. Defina cada um em
1-2 frases."
```

---

## 🛠️ Ferramentas utilizadas

- **NotebookLM** (Google) — upload das fontes, perguntas estratégicas e síntese com citações
- **YouTube** — fontes abertas em vídeo (canal *Nate Herk | AI Automation*)

## 📄 Licença

Material de estudo pessoal. Os vídeos referenciados pertencem aos seus respectivos autores.
