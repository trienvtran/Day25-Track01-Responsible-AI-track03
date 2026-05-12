# 🎨 Prompt 5a — ASCII UI Sketch (Layer 3 UI)

**Khi dùng**: Day 25 Solution Design Phase B (sau khi pick option UI-first)
**Layer**: 3 — UI Response
**Tool recommended**: Claude / ChatGPT / Gemini
**Output save vào**: `worksheet/02-solution-design/artifact/{1-uiux|3-architecture}/demo.md`
**Time budget**: 5-10 phút

---

## Khi nào dùng prompt này

Pick option C — UX-first ở Prompt 4, hoặc primary layer focus là **Layer 3 UI Response**.

Solution element typical:
- Disclosure UI (warning banner)
- Refusal copy với redirect buttons
- Source citation badge
- Uncertainty wording
- Escalation button visual

---

## PROMPT (paste sau 00-context.md)

```
# REQUEST — Generate ASCII UI sketch (chỉ ASCII, KHÔNG Mermaid)

## Background

Tôi đang design solution ở Layer 3 UI Response cho failure case sau:
[Paste case ID + summary từ §6]

## Solution element to sketch

Solution đã chốt sau Phase A của Solution Design:

- **Solution type**: 
  [Disclosure UI / Refusal copy / Escalation button / Source citation badge / 
  Uncertainty wording]
  
- **Approach** (1 paragraph): 
  [Paste từ Solution Design Option đã pick]
  
- **Key UI elements cần thể hiện**:
  - [Element 1: ví dụ Warning banner với icon ⚠️]
  - [Element 2: ví dụ Refusal message ngắn gọn]
  - [Element 3: ví dụ Escalation button với label rõ]
  - [Element 4: ví dụ Source citation inline]

## Request

Generate ASCII-only sketch (KHÔNG Mermaid):

### Constraints
- **Box-drawing chars**: ┌ ┐ └ ┘ │ ─ ┬ ┴ ├ ┤ ┼ → ▶ ▲ ▼ ╭ ╮ ╰ ╯
- **Max width**: 60 chars (fit markdown render GitHub/Notion)
- **Layout**: 1 main screen với chat conversation
- **Highlight Solution element** bằng emoji ngắn: ⚠️ 📄 💬 ⚡ ✓ ✗
- **KHÔNG nhiều emoji thừa** (max 3-4 emoji/sketch)
- **Mỗi text element ngắn** ≤3 dòng

### Pattern to follow

1. Header bar (title, bot name, status)
2. Conversation area (current message visible)
3. User message
4. AI response với Solution element HIGHLIGHTED
5. Action buttons (refusal redirect, escalation, source link)
6. Footer disclaimer (optional)

### Output structure example

```
┌────────────────────────────────────────┐
│  🎓 [Bot name] — [Org]                 │
├────────────────────────────────────────┤
│                                        │
│  User: [user prompt cụ thể]            │
│                                        │
│  ┌──────────────────────────────────┐ │
│  │ ⚠️  [Solution element prominently │ │
│  │   highlighted, ngắn gọn]         │ │
│  │                                  │ │
│  │  [Action 1: → button label]      │ │
│  │  [Action 2: → button label]      │ │
│  │                                  │ │
│  │  ⚠️  [Disclaimer if needed]      │ │
│  └──────────────────────────────────┘ │
│                                        │
└────────────────────────────────────────┘
```

### Iteration

Gen 1 sketch v1 trước. Sau đó tôi sẽ feedback:
- "Sketch lại với highlight rõ hơn element X"
- "Add thêm element Y vào vị trí Z"
- "Test version với mobile width 40 chars"

Đừng tạo nhiều variants cùng lúc — chờ feedback rồi iterate.

## Anti-patterns AVOID

❌ Quá nhiều emoji (😀 🎉 🌟 mỗi dòng)
✅ Emoji functional (⚠️ for warning, 📄 for doc, 💬 for chat)

❌ Width >70 chars (markdown render wrap xấu)
✅ Max 60 chars

❌ ASCII art trang trí (cây dừa, robot face)
✅ Functional UI element (button, badge, message, header)

❌ Mermaid output (yêu cầu ASCII-only)
✅ Pure box-drawing chars
```

---

## ✅ Review checklist (làm SAU AI gen)

- [ ] Width <= 60 chars (check bằng cách paste vào markdown preview)
- [ ] Solution element nổi bật visually (frame riêng, emoji highlight)
- [ ] User prompt cụ thể, không generic
- [ ] Action buttons rõ ràng (next step user sẽ click)
- [ ] Disclaimer (nếu có) ngắn gọn, không thừa

## 🔄 Iteration prompt (nếu cần)

Sau v1, paste tiếp:

```
Sketch v1 này:
- Highlight element X chưa đủ rõ — viền dày hơn hoặc emoji nổi hơn
- Add disclaimer ở footer cho rủi ro financial
- Show 2 alternative buttons không phải 1
```

→ Iterate đến khi sketch communicate ý tưởng rõ ràng.

## 💡 Tip — Vibe-code prototype (post-Day 25, optional)

Sau khi có ASCII sketch tốt, có thể:
1. Paste ASCII vào [Claude Artifacts](https://claude.ai/artifacts) / [v0.dev](https://v0.dev) / [Bolt.new](https://bolt.new)
2. Prompt: "Convert this ASCII UI sketch into working HTML/React component"
3. Get clickable prototype trong vài phút
