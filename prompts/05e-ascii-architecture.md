# 🏗️ Prompt 5e — ASCII Architecture/RAG (Layer 1 Input)

**Khi dùng**: Day 25 Solution Design Phase B (sau khi pick option Tech-first)
**Layer**: 1 — Input / RAG / Data
**Tool recommended**: Claude / ChatGPT / Gemini
**Output save vào**: `worksheet/02-solution-design/artifact/{1-uiux|3-architecture}/demo.md`
**Time budget**: 5-10 phút

---

## Khi nào dùng prompt này

Pick option A — Tech-first ở Prompt 4, hoặc primary layer focus là **Layer 1 Input / RAG / Data**.

Solution typical:
- RAG architecture với fallback
- API integration với official source
- Vector DB + retrieval pipeline
- Hybrid AI + deterministic search

---

## PROMPT (paste sau 00-context.md)

```
# REQUEST — Generate ASCII system architecture (chỉ ASCII, KHÔNG Mermaid)

## Background

Tôi đang design solution ở Layer 1 Input / RAG / Data cho failure case:
[Paste case ID + summary từ §6]

Solution involves: RAG architecture với fallback, API integration với 
official source.

## Architecture to sketch

- **External dependencies**: 
  [admissions API, official policy doc DB]
  
- **Internal components**: 
  [Intent classifier, RAG service, prompt orchestrator]
  
- **Data flow**: 
  [User query → classifier → RAG → official API → response]
  
- **Failure paths**: 
  [API timeout, API null, classifier low confidence]
  
- **Fallback**: 
  [Refuse + escalate when uncertain]

## Request

Generate ASCII architecture (KHÔNG Mermaid):

### Constraints
- **Box-drawing chars**: ┌ ┐ └ ┘ │ ─ ┬ ┴ ├ ┤ ┼ → ▶ ▲ ▼
- **Direction**: Left-to-right HOẶC top-down (pick natural for data flow)
- **Annotate edges** với protocol/method/SLA inline
- **Max 6-8 components** (nếu nhiều hơn → tách sub-architecture)
- **Show external vs internal**: 
  - External boxes dùng `╭ ╮ ╰ ╯` (rounded)
  - Internal dùng `┌ ┐ └ ┘` (sharp)

### Pattern to follow

1. **Entry**: User/Client (top or left)
2. **API/Service layer**: routing, classifier
3. **External services**: APIs, databases (rounded boxes)
4. **Decision/Router**: which path based on response
5. **Output paths**: success / failure / fallback

### Output structure example

```
[USER]
   │ HTTP request
   ▼
┌──────────────┐
│ Intent       │
│ Classifier   │
│ (scholarship?│
│ Y/N + conf)  │
└──────┬───────┘
       │
       ▼
╭──────────────╮      ╭──────────────╮
│ admissions   │◀────│ RAG Service │
│ /api/        │ REST│ (orchestrator)│
│ scholarships │ 200ms ╰──────┬──────╯
╰──────┬───────╯              │
       │                       │
   ┌───┴───┐                  │
   ▼       ▼                  │
┌──────┐ ┌──────┐              │
│ data │ │ null │              │
└───┬──┘ └───┬──┘              │
    │       │                  │
    ▼       ▼                  ▼
┌──────────┐ ┌──────────┐ ┌──────────────┐
│ AI cite  │ │ AI refuse│ │ General LLM  │
│ source + │ │ + escalate│ │ + disclaimer │
│ answer   │ │ counselor│ │ (off-topic)  │
└──────────┘ └──────────┘ └──────────────┘
```

### Iteration

Gen v1 trước. Sau đó tôi sẽ feedback:
- "Add caching layer cho admissions API"
- "Show monitoring/log component"
- "Add retry logic nếu API timeout"

## Anti-patterns AVOID

❌ Mermaid output
✅ Pure box-drawing chars

❌ Components không annotated (không biết protocol/SLA)
✅ Inline annotation: "REST 200ms", "Redis cache 1h", "Postgres"

❌ Too many components mà không phân layer
✅ Group external (rounded) vs internal (sharp), max 8 total
```

---

## ✅ Review checklist

- [ ] External services dùng `╭ ╮ ╰ ╯`, internal `┌ ┐ └ ┘`
- [ ] Edges có annotation (protocol, SLA)
- [ ] Failure paths đầy đủ (timeout, null, error)
- [ ] Fallback rõ ràng (refuse + escalate)
- [ ] Max 8 components

## 🔄 Iteration patterns

Gen 2-3 lần để architecture chính xác:

```
v1: basic flow (3-4 components)
v2: add fallback paths + retry logic
v3: add monitoring + caching + logging
```

## 💡 Tip — Spec follow-up

Sau khi có ASCII architecture, gen tiếp **Component spec**:

```
# COMPONENT SPEC follow-up prompt

Cho architecture vừa gen, write spec mô tả mỗi component:
- Input format
- Processing logic
- Output format
- SLA/latency
- Failure mode

Format: 1 paragraph per component. Max 200 words total.
```

Save vào `worksheet/02-solution-design/artifact/3-architecture/demo.md`.
