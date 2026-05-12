# 🎨 Prompt 4 — Solution Design Options (3 options sketch)

**Khi dùng**: Day 25 Solution Design Lab Phase A (10:55-11:10)
**Tool recommended**: Claude / ChatGPT / Gemini
**Output save vào**: `worksheet/02-solution-design/1-map-and-format.md` Phần C + `worksheet/02-solution-design/1-map-and-format.md` Phần C
**Time budget**: 15 phút (10' gen 3 options + 5' pick)

---

## Cách dùng

```
Step 1: Paste 00-context.md vào conversation
Step 2: Paste prompt dưới đây + fill [BRACKET] với input từ §3 + §6 + Day A System Map
Step 3: AI gen 3 options khác metaphor (Tech / Process / UX)
Step 4: Group discuss + pick 1 option
Step 5: Save 3-options.md + picked.md
Step 6: Tiếp tục với Prompt 5 (ASCII/Mermaid) cho demo phase
```

---

## PROMPT (paste sau 00-context.md)

```
# REQUEST — Solution Design: 3 Options sketch

## Background

Tôi đã hoàn thành Day 24 Risk Map + Day 25 Diverge + Converge (test set v1 
group). Hôm nay design Solution cho primary failure.

## Failure addressed

Paste exact từ §3 Risk Map + §6 Test Set:

- **Case ID** (từ §6 group test set v1): [T2]
- **Failure mode** (1 of 8): [Hallucination về scholarship/deadline]
- **Trigger**: 
  [User hỏi học bổng/deadline specific mà KB official không có data]
- **Bad behavior**: 
  [AI bịa với tone confident]
- **Expected safe behavior**: 
  [Refuse + cite source + escalate counselor]
- **Harm**: 
  [User lỡ deadline thật, mất cơ hội]

## Failure root cause layer (Day 24 System Map 5 layers)

- **Primary layer**: 
  [Layer 1 Input — thiếu RAG đến official admissions API]
- **Secondary layer**: 
  [Layer 3 UI — không có disclaimer khi không cite source]
- **Layer rationale**: 
  [Failure đến từ thiếu data source ở Input; UI không signal uncertainty]

## Constraints

- **Budget**: [1-2 sprint engineering effort]
- **Existing infra**: 
  [Có Postgres DB, chưa có vector DB / RAG infrastructure]
- **Team**: [2 engineer + 1 designer + 1 PM]
- **Timeline**: [4 tuần đến soft launch]

## Request — Generate 3 Solution OPTIONS

3 options KHÁC METAPHOR (KHÔNG phải "thin/medium/thick border"):

### Option A — Tech-first
**Cách tiếp cận**: Solve problem ở Layer 1-2 (Input + Model)
Examples: RAG + system prompt rules / Fine-tune / Constrained generation

### Option B — Process-first
**Cách tiếp cận**: Solve problem ở Layer 4 (Human-in-the-loop)
Examples: Approval queue / Reviewer SLA / Escalation workflow

### Option C — UX-first
**Cách tiếp cận**: Solve problem ở Layer 3 (UI Response)
Examples: Disclosure UI / Verification button / Uncertainty wording / 
Source citation badge

## Output format per option

```
### Option [A/B/C] — [Metaphor name]

**Approach** (1 paragraph, concrete):
[Mô tả cụ thể solution làm gì, components nào, ai sẽ build]

**Pros** (3 điểm cụ thể):
1. [Pro liên quan đến failure root cause]
2. [Pro liên quan đến cost/effort]
3. [Pro liên quan đến user experience]

**Cons** (3 điểm cụ thể):
1. [Con liên quan đến limitation]
2. [Con liên quan đến side effect mới]
3. [Con liên quan đến cost/maintenance]

**When to pick this option**:
[1 dòng — tình huống nào option này hợp nhất]

**Estimated cost/effort**:
[1-2 sprint? Cần infra mới? Cần hire?]

**Side effects to monitor**:
[Risk mới mà option này tạo ra]
```

## Demo format (sẽ làm sau khi pick option)

Sau khi tôi pick 1 option, demo theo layer (xem Prompt 5a-5f riêng):

- **Layer 1 Input/RAG** → Architecture diagram (Prompt 5e ASCII / 5f Mermaid)
- **Layer 2 Model** → System Prompt snippet + Test plan
- **Layer 3 UI** → UI sketch (Prompt 5a ASCII / 5b Mermaid)
- **Layer 4 Human-in-loop** → Workflow (Prompt 5c ASCII / 5d Mermaid)
- **Layer 5 Monitoring** → Dashboard mockup spec + metric list

## Anti-patterns AVOID

❌ Generic ("add safety measures", "improve evaluation")
✅ Specific ("RAG hits admissions.school.edu/api/scholarships, refuse if null")

❌ Same solution presented 3 ways (thin/medium/thick variants)
✅ 3 metaphors khác nhau (tech / process / UX) — different layer focus

❌ Pros all positive, no honest cons
✅ Honest cons + cost + side effects + maintenance burden

❌ Hypothetical-only ("could potentially help if...")
✅ Implementable với cost + effort + tools cụ thể
```

---

## ✅ Group decision checklist (làm SAU AI gen 3 options)

Group sit together, discuss:

- [ ] Option nào address root cause (Layer chính) trực tiếp nhất?
- [ ] Option nào fit constraints (budget, team, timeline)?
- [ ] Cons của option này có acceptable không?
- [ ] Side effects có manageable không?
- [ ] Cost/effort có realistic cho team chúng ta?

**Pick 1 option** (hoặc combine 2 nếu cần defense-in-depth).

Save vào `worksheet/02-solution-design/1-map-and-format.md` Phần C:

```markdown
# Picked Option

**Option chosen**: [A / B / C / combined]
**Rationale** (3-5 dòng): [Tại sao pick]
**Layer focus**: [Layer 1 / 2 / 3 / 4 / 5]
**Demo format sẽ build**: [ASCII Architecture / Mermaid UI Flow / etc.]
```

→ Sau khi pick, tiếp tục với Prompt 5 phù hợp với layer.

## 💡 Tip — Generate iteratively

Nếu AI gen 3 options quá generic lần đầu, paste tiếp:

```
Critique 3 options vừa gen:
- Option nào quá generic, thiếu detail implementable?
- Option nào duplicate logic của option khác?
- Có solution approach nào MỚI (không trong 3 options) mà tôi nên consider không?

Sau đó gen lại 3 options mới với detail cụ thể hơn.
```
