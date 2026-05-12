# 🎯 Prompt 3 — Convergent Analysis (Filter pool of cases)

**Khi dùng**: Day 25 Converge Step 2-3 (10:10-10:30)
**Tool recommended**: Claude / ChatGPT (cần upload file support)
**Output save vào**: `worksheet/01-test-set-review/2-converge.md` Phần B + `worksheet/01-test-set-review/2-converge.md` Phần C
**Time budget**: 20 phút (10' dedup + 10' scoring)

---

## Cách dùng

```
Step 1: Group pool 30-45 cases (từ all members) vào group-pool.md
Step 2: Upload group-pool.md lên Claude/ChatGPT
Step 3: Paste 00-context.md vào conversation
Step 4: Paste prompt dưới đây
Step 5: Save dedup output → worksheet/01-test-set-review/2-converge.md Phần B
Step 6: Save scoring output → worksheet/01-test-set-review/2-converge.md Phần C
Step 7: Coverage check + swap → worksheet/01-test-set-review/3-FINAL-test-set-eval-plan.md
```

---

## PROMPT (paste sau 00-context.md + upload group-pool.md)

```
# REQUEST — Convergent Analysis: Filter test set pool

## Input

Tôi vừa upload file group-pool.md gồm 30-45 test cases (group pool sau 
Diverge phase Day 25). File format columns:
- ID
- Author (thành viên group nào contribute)
- Prompt (exact text)
- Failure mode (1 of 8)
- Expected safe behavior
- Severity (Low/Med/High)
- Lens applied (1/2/3/5)

Pool đến từ 2-3 thành viên group (mỗi người 15 cases).

## Background

Group tôi đang ở Converge phase, cần filter từ 30-45 cases xuống 10-15 
final cases cho test set v1 (deliverable Day 25). 

Group dynamics (từ CONTEXT ở trên):
- Same-track: tất cả thành viên cùng track
- Same primary failure mode (vì group form theo primary failure cuối Day 24)
- Diverse perspectives: thành viên có background khác nhau

## Phase A — Dedup Analysis

### Step 1: Group cases by failure mode

Phân loại 30-45 cases vào 8 failure modes:
- Hallucination
- Bias / fairness
- Privacy / data leak
- Sycophancy
- Over-reliance
- Harmful advice
- Policy violation / escalation failure
- Misuse / jailbreak

Output: cluster count + sample case ID mỗi mode.

### Step 2: Within each mode, identify duplicates

Pattern:
- **Duplicate strong**: cùng failure pattern + similar wording + cùng 
  severity → DROP one
- **Duplicate weak**: tương tự nhưng có angle khác → KEEP both với note
- **Unique**: no equivalent → MUST KEEP

Output: deduped list với deduplication notes (cases dropped + why).

## Phase B — Risk Matrix Scoring

Cho mỗi case còn lại sau dedup, score 2 dimensions 1-5:

### Impact — Nguy hại nếu AI fail

- **1**: Inconvenience nhỏ (mất 5 phút thời gian, dễ recover)
- **2**: Annoying, user mất 30+ phút sửa
- **3**: Mất tiền/thời gian đáng kể (vài triệu, vài ngày), recoverable
- **4**: Serious harm — lỡ deadline quan trọng, sai quyết định lớn
- **5**: Legal/safety/irreversible — kiện tụng, học sai trường, sức khỏe

### Urgency — Tốc độ harm xảy ra sau khi AI fail

- **1**: Days/weeks — user check chéo có thể catch trước khi act
- **2**: Day or two — user có thời gian gather thêm info
- **3**: Hours — user act sau khi gather chút info
- **4**: Within hour — user act gần như ngay
- **5**: Minutes/immediate — user act NGAY theo AI không verify

### Risk Score = Impact × Urgency (range 1-25)

## Phase C — Decision Rule

- 🟢 **Score ≥ 15**: MUST INCLUDE (high priority — critical)
- 🟡 **Score 6-14**: MAYBE (decide based on coverage gap, see Phase D)
- 🔴 **Score 1-5**: DROP (low priority)

## Phase D — Coverage Check

Top 10-15 final cases phải cover ≥4/5 categories:
- **Normal** (đúng phạm vi, lịch sự, đủ info)
- **Edge** (ambiguous, partial info, dialect)
- **Pressure-trap** (user cố push bot làm việc không nên)
- **Escalation** (sensitive case cần chuyển human)
- **Out-of-scope** (bot phải refuse + redirect)

Nếu top 15 thiếu category nào → swap 1 case score thấp lấy 1 case fill gap.

## Output format

### Section 1 — Dedup report

```
Cluster breakdown:
- Hallucination: [count] cases (IDs: ...)
- Bias: [count]
- ...

Duplicates dropped: [count]
- ID [X] dropped vì duplicate với ID [Y] (similar prompt + same expected)
- ...

Deduped pool: [count] cases remaining.
```

### Section 2 — Risk scoring table

| Rank | ID | Author | Prompt summary | Failure mode | Impact (1-5) | Urgency (1-5) | Risk Score | Decision (🟢🟡🔴) | Category | Notes |
|---|---|---|---|---|---|---|---|---|---|---|

Sort descending by Risk Score.

### Section 3 — Coverage check

```
Top 15 cases distribution:
- Normal: X cases
- Edge: X cases
- Pressure-trap: X cases
- Escalation: X cases
- Out-of-scope: X cases

Missing category? [YES/NO]
Recommended swap (if missing): [specific case IDs to swap]
```

### Section 4 — Final 10-15 cases

List final cases với justification:
- 5-7 MUST INCLUDE (🟢 high score)
- 3-5 MAYBE included (🟡 fill coverage)
- 2-3 BONUS (optional, kept if time)

## Anti-patterns AVOID

❌ Score "feel" without justification
✅ Score với Impact reason + Urgency reason cụ thể

❌ Drop case mà không note WHY
✅ Mỗi DROP có deduplication note

❌ Skip coverage check, chỉ top-N by score
✅ Coverage check explicit, swap nếu cần
```

---

## ✅ Group review checklist (làm SAU AI output)

Sau khi AI gen output, group sit together review:

- [ ] Score Impact + Urgency của mỗi case có agree không? Nếu disagree → discuss
- [ ] Cases dropped có thật sự duplicate không? Hay angle khác đáng KEEP?
- [ ] Top 10-15 có cover ≥4/5 category không?
- [ ] Mỗi case High severity có justification consequence cụ thể?
- [ ] Final test set có 1-2 cases liên quan đến real-world incident từ Deep Research?

→ Group đồng thuận → commit `worksheet/01-test-set-review/3-FINAL-test-set-eval-plan.md`

## 🛠️ Tool tips

- **Claude (claude.ai)**: support file upload trực tiếp, tốt cho table analysis
- **ChatGPT (chat.openai.com)**: support file upload (Plus/Team plan)
- **Gemini**: support file upload (Advanced plan)

Nếu không có file upload, paste content `group-pool.md` trực tiếp vào prompt.
