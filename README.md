# AI Research Assistant Agent (Agentic AI)

**Stack:** Python, LangChain-style orchestration, MCP-style tool protocol, RAG, LLM APIs (Anthropic/OpenAI)

An autonomous multi-agent system that plans, retrieves, and synthesizes information from
multiple sources to answer complex user queries without manual intervention.

## Components
- **Planner** — decomposes a complex query into sub-tasks
- **RAG retriever** — vector-embedding based retrieval grounding responses in real documents,
  reducing hallucination
- **MCP-style tool registry** — tools are registered with a name, description, and callable,
  mirroring how the Model Context Protocol exposes tools to an agent at runtime
  (`search_documents`, `calculator`, `get_current_date`)
- **Pluggable LLM client** — calls a real Anthropic or OpenAI model if an API key is present
  in the environment, otherwise falls back to a deterministic local planner so the pipeline
  always runs
- **Memory** — full trace of every plan + tool call + result kept per session

## Run it
```bash
pip install -r requirements.txt

# optional — enables real LLM-driven planning instead of the local fallback
export ANTHROPIC_API_KEY=sk-...
# or
export OPENAI_API_KEY=sk-...

jupyter notebook ai_research_assistant.ipynb
```

## Example
```
Query: What is the refund policy and what is 15% of 200?

Agent reasoning (tool calls made automatically):
  [search_documents] task: 'What is the refund policy' -> [...]
  [calculator] task: 'what is 15% of 200' -> 30.0

Synthesized answer:
- Refund Policy: Customers can request a full refund within 30 days of purchase...
- Calculation result: 30.0
```
