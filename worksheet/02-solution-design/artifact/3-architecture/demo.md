---
pack: 3 — Architecture Demo
format: ASCII / Mermaid architecture diagram + component spec
build-via: prompts/05e-ascii-architecture.md hoặc 05f-mermaid-architecture.md
---

# 📦 Pack 3 — Architecture Demo

## Diagram

(Paste ASCII / Mermaid output từ prompt 5e/5f)

```
[Paste diagram ở đây — ASCII hoặc Mermaid code block]
```

## Component spec

| Component | Input | Processing | Output | SLA / Notes |
|---|---|---|---|---|
| Intent Classifier | User query | Detect "scholarship + deadline" keywords | Route to RAG (Y) / General LLM (N) | <50ms |
| RAG Service | Classified query | Query /api/scholarships?date=current | Verified data + source URL | <200ms |
| Cache (Redis) | Query hash | Check cache → return if hit | Cached response | 1h TTL |
| Admissions API | RAG call | Lookup official policy | JSON data | REST 200ms, 99% uptime |
| Fallback handler | API null/timeout | Trigger AI refuse + escalation | "Counselor sẽ trả lời 4h" | — |
| Monitoring | All requests | Log query + response + verdict | Audit log + alerts | Daily review |

## Failure paths

- **API timeout (>2s)** → return cached if available, else AI refuse + escalate
- **API null** → AI refuse + escalate counselor (SLA 4h)
- **Cache miss + API down** → AI refuse with explicit "service degraded" message
- **Rate limit hit** → queue + retry với exponential backoff

## Iteration history

- **v1**: Basic RAG flow (3 components: Classifier + RAG + API)
- **v2** (after AI critique): Added cache layer + fallback escalation
- **v3** (after team review): Added monitoring + rate limit + circuit breaker
