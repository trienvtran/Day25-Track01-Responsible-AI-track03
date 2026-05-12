---
pack: 1 — UI/UX Solution
layer: Layer 3 — UX/UI Response
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.{png/md/html}  (demo trực quan cùng folder)
---

# 📦 Pack 1 — UI/UX Solution Card

**Ca xử lý**: T-__ (xem `../../1-map-and-format.md` Phần A)

---

## 1. Tóm tắt giải pháp (1 đoạn)

[Mô tả 2–3 câu: UI/UX intervention làm gì để address root cause]

Ví dụ: *"Thêm badge 'Đã xác thực từ admissions.edu' / 'Chưa xác minh — counselor sẽ follow up' khi response của AI chứa deadline học bổng. Stack với skeleton loading state + nút 'Escalate counselor' luôn hiện trên mọi response."*

---

## 2. Tầng + Lý do phù hợp (Layer 3 UX/UI Response)

**Tại sao tầng UI/UX phù hợp**:
- User tin AI quá mức → cần tầng **Disclose** (cảnh báo trực quan)
- **Catch** failure ngay khoảnh khắc user nhận response, **trước khi user act**
- Defense in Depth: UX catch khi Pack 2 Prompt + Pack 3 Architecture miss

**Verbs cover**: Disclose ✓ / Catch ✓

---

## 3. Artifact cụ thể (ref `./demo.{format}`)

**Format demo**: [Vẽ tay sketch / Excalidraw / Vibe-code prototype / HTML / ASCII / Mermaid]

**Thành phần UI chính** (3–5 bullet):
- [Component 1: badge, nội dung text, màu, vị trí]
- [Component 2: nút escalate + hành vi]
- [Component 3: loading state + message]
- [Component 4 nếu có]

**File demo**: → [`demo.{format}`](./demo.md) (paste / embed / link)

---

## 4. Tác dụng phụ + cách giảm

**Rủi ro**: [UX rối / user fatigue với disclaimer / latency tăng khi check source]
**Cách giảm**: [Skeleton loading + lazy badge / ẩn badge khi confidence > 95% / escalate async]

---

## 5. Note xây dựng (workflow 25–30 phút)

1. [ ] Paste `../../00-context.md` + `../../1-map-and-format.md` Phần C Solution 1 vào AI
2. [ ] Paste prompt từ `../../../../prompts/05a-ascii-ui-sketch.md` HOẶC `05b-mermaid-ui-flow.md`
3. [ ] AI gen draft → iterate v1 → v2
4. [ ] Save vào `./demo.{format}`
5. [ ] Fill section 1–4 ở trên

**Người driver**: [Tên thành viên]
