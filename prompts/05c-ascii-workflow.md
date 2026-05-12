# 🔀 Prompt 5c — ASCII Workflow Process (Layer 4 Human-in-loop)

**Khi dùng**: Day 25 Solution Design Phase B (sau khi pick option Process-first)
**Layer**: 4 — Human-in-the-loop
**Tool recommended**: Claude / ChatGPT / Gemini
**Output save vào**: `worksheet/02-solution-design/artifact/{1-uiux|3-architecture}/demo.md`
**Time budget**: 5-10 phút

---

## Khi nào dùng prompt này

Pick option B — Process-first ở Prompt 4, hoặc primary layer focus là **Layer 4 Human-in-the-loop**.

Solution typical:
- Approval queue
- Escalation flow
- Reviewer SLA workflow
- RACI matrix process

---

## PROMPT (paste sau 00-context.md)

```
# REQUEST — Generate ASCII workflow diagram (chỉ ASCII, KHÔNG Mermaid)

## Background

Tôi đang design solution ở Layer 4 Human-in-the-loop cho failure case:
[Paste case ID + summary từ §6]

Solution involves: approval queue / escalation flow / reviewer SLA.

## Workflow to sketch

- **Trigger**: 
  [Keyword detected / classifier flag / user request escalation]
  
- **Process steps**:
  - [Step 1: Detection]
  - [Step 2: Routing]
  - [Step 3: Review]
  - [Step 4: Decision]
  - [Step 5: Response delivery]
  
- **SLA constraints**: 
  [Review within 4h / Reviewer roles / escalation tree]
  
- **Edge cases**: 
  [What happens if reviewer offline? After-hours?]

## Request

Generate ASCII workflow diagram (KHÔNG Mermaid):

### Constraints
- **Box-drawing chars**: ┌ ┐ └ ┘ │ ─ ┬ ┴ ├ ┤ ┼ → ▶ ▲ ▼
- **Direction**: Top-down (natural cho process flow)
- **Decision points**: ┌─┴─┐ với YES/NO branches
- **Max 8 nodes**: nếu nhiều hơn → tách sub-workflows
- **SLA inline**: ghi thời gian/role trong box ("SLA 4h", "Senior counselor")

### Pattern to follow

1. Entry point (user query / trigger event)
2. Decision node (keyword detect / classifier)
3. Branches (YES path → human / NO path → AI direct)
4. Action nodes (queue, review, escalate, send)
5. Exit point (user receives outcome)

### Output structure example

```
        [User query]
              │
              ▼
    ┌──────────────────┐
    │ Keyword detector │
    │ "scholarship"    │
    │ "deadline"       │
    │ "tuition"        │
    └────────┬─────────┘
             │
       ┌─────┴─────┐
       │           │
   MATCH         NO MATCH
       │           │
       ▼           ▼
┌──────────────┐ ┌──────────────┐
│ 🚦 Reviewer  │ │  AI direct   │
│   Queue      │ │  response    │
│   SLA: 4h    │ │              │
└──────┬───────┘ └──────┬───────┘
       │                │
       ▼                │
┌──────────────┐        │
│ Counselor    │        │
│ ✓ approve    │        │
│ ✏️ edit      │        │
│ ✗ reject     │        │
└──────┬───────┘        │
       │                │
       └────────┬───────┘
                ▼
       [User receives
        approved response]
```

### Iteration

Gen v1 trước. Sau đó tôi sẽ feedback:
- "Add escalation tree cho weekend/after-hours"
- "Show retry logic nếu reviewer không respond trong SLA"
- "Add audit log node"

## Anti-patterns AVOID

❌ Mermaid output (yêu cầu ASCII-only)
✅ Pure box-drawing chars

❌ Quá nhiều branches (>5) — không readable
✅ Max 3 paths chính + edge cases ghi note

❌ SLA generic ("ASAP", "soon")
✅ SLA cụ thể ("4h", "next business day", "30 phút")
```

---

## ✅ Review checklist

- [ ] Top-down flow rõ ràng (entry on top, exit at bottom)
- [ ] Decision diamonds có YES/NO branches
- [ ] SLA inline trong box
- [ ] Max 8 nodes
- [ ] Action nodes có verb rõ (approve/edit/reject)

## 🔄 Iteration patterns

Thường iterate 2-3 lần để workflow chính xác:

```
v1 prompt: basic flow
v2 prompt: add edge case (timeout / after-hours)
v3 prompt: add audit/log node + monitoring touchpoints
```

## 💡 Tip — Sub-workflows

Nếu workflow >8 nodes:
1. Tách thành main flow + sub-flows
2. Main flow: high-level decisions
3. Sub-flow: detail từng path (e.g., "Escalation tree", "After-hours handling")

Save mỗi sub-flow vào file riêng trong `worksheet/02-solution-design/artifact/1-uiux/` (gộp vào 1 file demo).
