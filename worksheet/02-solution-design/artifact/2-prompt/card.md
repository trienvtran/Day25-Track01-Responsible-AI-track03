---
pack: 2 — Prompt Engineering Solution
layer: Layer 2 — System Prompt / Refuse / Cite-ground
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md  (system prompt text + few-shot examples)
---

# 📦 Pack 2 — Prompt Engineering Solution Card

**Ca xử lý**: T-__ (xem `../../1-map-and-format.md` Phần A)

---

## 1. Tóm tắt giải pháp (1 đoạn)

[Mô tả 2–3 câu: prompt engineering intervention làm gì để address root cause]

Ví dụ: *"System prompt rule refuse rõ ràng khi thiếu nguồn: 'Never state specific dates without citing official URL. If unsure, respond: I do not have verified info, escalating to counselor.' Stack với 3 few-shot examples + bắt buộc cite-ground."*

---

## 2. Tầng + Lý do phù hợp (Layer 2 System Prompt)

**Tại sao tầng Prompt Engineering phù hợp**:
- AI bias toward confident answer → cần rule **Refuse + Cite-ground**
- **Prevent** failure ở tầng model, **trước khi** response gen ra
- Low-cost intervention (không cần thay đổi infra), high-leverage (1 prompt = nhiều ca)

**Verbs cover**: Prevent ✓ / Refuse ✓

---

## 3. Artifact cụ thể (ref `./demo.md`)

**Format demo**: Markdown spec (system prompt text + few-shot)

**Thành phần prompt chính**:
- [Refuse rule 1: không bao giờ state X mà không có Y]
- [Yêu cầu cite-ground: "phải cite URL nguồn khi trả lời về Z"]
- [Template refuse: "Tôi không có thông tin được xác minh về [topic]..."]
- [3 few-shot examples cover các ca khác nhau]

**File demo**: → [`demo.md`](./demo.md) (full prompt text)

---

## 4. Tác dụng phụ + cách giảm

**Rủi ro**: [Over-refusal — AI refuse quá nhiều ca bình thường / response cứng / few-shot drift]
**Cách giảm**: [Calibrate threshold refuse qua test set / thêm template "soft refusal" / monitor pass rate cho ca normal]

---

## 5. Note xây dựng (workflow 15–20 phút)

1. [ ] Paste `../../00-context.md` + `../../1-map-and-format.md` Phần C Solution 2 vào AI
2. [ ] Brainstorm prompt: rule refuse + cite-ground + few-shot
3. [ ] AI gen draft prompt → test với 3–5 ca từ test set Bài 1
4. [ ] Save final prompt + few-shot vào `./demo.md`
5. [ ] Fill section 1–4 ở trên

**Người driver**: [Tên thành viên]
