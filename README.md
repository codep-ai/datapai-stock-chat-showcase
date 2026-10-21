# datapai-stock-chat-showcase — governed, tool-calling stock chat runtime

The chat runtime behind stock.datap.ai: a FastAPI endpoint that streams Gemini over SSE with
function calling (live price and FX tools), behind a pre-call AI-governance gate. Reference code:
it imports modules that are not included, so it is not runnable standalone.

| Runtime function | File |
|---|---|
| Streaming endpoint, tool-calling loop (`get_stock_price`, `get_fx_rate`), budgets, audit persistence | `agents/stock_chat/endpoint.py` |
| Context assembly (page, ticker, profile, history) | `context_builder.py`, `user_context.py`, `user_profile.py`, `history.py` |
| Retrieval | `rag_retriever.py` |
| Governance gate bridge (sensitivity levels, write-once decision evidence, SSE governance event) | `guardrail_bridge.py` |
| CRM audit trail (secondary, non-fatal) | `twenty_context.py` |

Prices come from a public Yahoo Finance endpoint, so "live" means near-real-time. All credentials are
read from environment variables.
