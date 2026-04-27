# OpenLLM Gateway

The open-source alternative to OpenRouter. One API. Every model. Full control.

---

## What is this?

OpenLLM Gateway is a self-hostable, open-source LLM routing layer that sits between your application and every major AI provider.

Instead of juggling different SDKs, API formats, pricing pages, and failure modes for each provider, you call one endpoint and the gateway handles everything underneath. Think of it as your own OpenRouter — except you own the infra, the keys, the data, and the routing logic.

---

## Why this exists

OpenRouter is great, but it's a black box. You cannot customize the routing logic, inspect what's happening with your requests, self-host it for compliance reasons, or extend it with your own evaluation logic.

This project fixes all of that.

---

## What it does

### Multi-Model Routing

Route requests across providers using rules you define. Supported providers include OpenAI, Anthropic, Google DeepMind, and Mistral AI. Routing decisions are made based on cost, latency, model capability, or fallback rules you configure.

### Unified API

The core idea is a single endpoint that works for every provider:

```
POST /v1/chat/completions
```

Same request format, regardless of which model is running underneath. You can switch from GPT-4o to Claude 3.5 Sonnet without changing a single line of application code.

### API Key Management

Users bring their own provider keys. Keys are encrypted at rest (AES) and scoped per project. They are never exposed to clients or leaked in logs.

### Cost Tracking

Every request is tracked with its associated cost. You get per-model and per-user breakdowns, budget limits, and the option to auto-select the cheapest model for a given task. This is the primary reason developers will choose this over calling provider APIs directly.

### Latency and Failover

If a provider goes down, the gateway automatically falls back to the next provider in the chain. Optionally, requests can be sent to multiple models in parallel and the fastest or best response is returned.

### Observability

Full request logs, request tracing, and model performance stats. A lightweight observability layer built specifically for LLM workloads.

### Prompt Intelligence

Advanced routing capabilities including prompt caching, semantic routing based on what the prompt is actually asking, and eval-based routing that selects the best model for a given task type based on historical performance.

---

## Getting Started

```bash
git clone https://github.com/Rarebuffalo/OpenLLM-Gateway.git
cd OpenLLM-Gateway
bun install
bun run dev
```

---

## License

MIT
