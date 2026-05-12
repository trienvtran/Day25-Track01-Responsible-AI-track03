---
pack: 3 — Architecture / RAG Solution
layer: Layer 1 — Data Architecture / RAG / Source policy
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md  (ASCII / Mermaid diagram + component spec)
---

# 📦 Pack 3 — Architecture / RAG Solution Card

**Ca xử lý**: T-__ (xem `../../1-map-and-format.md` Phần A)

---

## 1. Tóm tắt giải pháp (1 đoạn)

[Mô tả 2–3 câu: architecture intervention làm gì để address root cause]

Ví dụ: *"RAG service query admissions API (REST 200ms) cho mọi response chứa keyword scholarship/deadline. Cache layer Redis TTL 1h. Fallback: nếu API null/timeout → AI refuse + escalate counselor (SLA 4h)."*

---

## 2. Tầng + Lý do phù hợp (Layer 1 Data Architecture)

**Tại sao tầng Architecture/RAG phù hợp**:
- Root cause = **thiếu nguồn đúng** (knowledge base outdated / không có data)
- **Prevent** failure ngay tầng data source, **trước khi** model gen response
- Defense in Depth: Architecture grounds, Prompt enforces, UI discloses

**Verbs cover**: Prevent ✓ / Ground in source ✓

---

## 3. Artifact cụ thể (ref `./demo.md`)

**Format demo**: ASCII architecture diagram HOẶC Mermaid (Prompt 5e / 5f)

**Thành phần chính** (3–5 bullet):
- [Intent Classifier: detect keyword "scholarship + deadline"]
- [RAG Service: query `/api/scholarships?date=current`, cite policy URL]
- [Cache layer: Redis TTL 1h cho query phổ biến]
- [Fallback path: API null → AI refuse + escalate counselor]
- [Monitoring: log mọi query → audit + retrain]

**File demo**: → [`demo.md`](./demo.md) (ASCII / Mermaid + bảng spec component)

---

## 4. Tác dụng phụ + cách giảm

**Rủi ro 1**: Latency tăng (REST 200ms + cache 50ms = 250ms vs 50ms baseline)
**Cách giảm**: Skeleton loading + fallback async nếu RAG > 2s

**Rủi ro 2**: API downtime → cascade failure (sập theo)
**Cách giảm**: Cache fallback + circuit breaker + counselor escalation SLA 4h

**Rủi ro 3**: Cost (API calls tốn $)
**Cách giảm**: Cache aggressive + rate limit theo user

---

## 5. Note xây dựng (workflow 15–20 phút)

1. [ ] Paste `../../00-context.md` + `../../1-map-and-format.md` Phần C Solution 3 vào AI
2. [ ] Paste prompt từ `../../../../prompts/05e-ascii-architecture.md` HOẶC `05f-mermaid-architecture.md`
3. [ ] AI gen draft → iterate v1 → v2 (thêm cache, monitoring, fallback)
4. [ ] Save diagram + spec component vào `./demo.md`
5. [ ] Fill section 1–4 ở trên

**Người driver**: [Tên thành viên]
