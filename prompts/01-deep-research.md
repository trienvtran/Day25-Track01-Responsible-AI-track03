# 🔍 Prompt 1 — Deep Research (real-world failure cases)

**Khi dùng**: Day 25 Diverge Step 1 (9:35-9:45)
**Tool recommended**: Claude Deep Research / GPT Deep Research / Gemini Deep Research / Perplexity Pro
**Output save vào**: `worksheet/01-test-set-review/1-diverge.md` Phần A
**Time budget**: 10 phút

---

## Cách dùng

```
Step 1: Paste TOÀN BỘ nội dung 00-context.md vào đầu conversation
Step 2: Paste prompt dưới đây
Step 3: Đợi AI Deep Research (3-5 phút)
Step 4: Save output vào worksheet/01-test-set-review/1-diverge.md Phần A
Step 5: Fact-check links theo checklist cuối prompt
```

---

## PROMPT (paste sau 00-context.md)

```
# REQUEST — Deep Research real-world failure cases

Dựa trên CONTEXT đã cung cấp ở trên, tôi đang build safety evaluation cho 
sản phẩm này. Search và liệt kê các incident thực tế trong 5 năm gần đây 
(2020-2025) matching theo các tiêu chí dưới đây.

## Search dimension 1 — Industry-specific failures

Tìm cases trong industry đã nêu ở context (educational chatbot / airline 
customer service / banking / etc.) mà AI products đã gây harm thật:
- Lawsuits / regulatory action / public scandals
- Date, organization, primary source link
- Focus vào Việt Nam, Asia, US, EU
- Bao gồm cả AI products + non-AI chatbot/automation failures (để hiểu pattern)

## Search dimension 2 — Failure mode-specific

Tìm cases match PRIMARY FAILURE CONCERN của tôi:
[Paste vào đây 1 dòng failure từ §3 Risk Map — ví dụ: 
"AI bịa thông tin học bổng/deadline khi knowledge base không có"]

Pattern cần tìm:
- How AI failed (concrete behavior, exact quote nếu có)
- What harm occurred (financial / legal / safety / reputational / emotional)
- User vulnerability state khi failure trigger (gấp, lo, first-time, etc.)
- Outcome resolution (lawsuit settlement, regulatory fine, brand damage)

## Search dimension 3 — Similar user persona harm

Cases mà user persona tương tự (đã mô tả ở context "Người dùng") bị harm:
- [Persona-specific search query — ví dụ: "học sinh THPT VN bị AI mislead"]
- Vulnerable user (rushed, emotional) bị AI scam/mislead trong context tương tự

## Source priority

1. **Primary** (must verify, cite URL):
   - Court records, regulatory filings (FTC, EU AI Act database)
   - Official organization statements
   - Government/agency reports (NTSB, CFPB style)

2. **Secondary** (acceptable):
   - Established news: NYT, Reuters, BBC, VnExpress, Tuoi Tre
   - Industry safety reports: Microsoft AIRT, Anthropic, OpenAI

3. **Tertiary** (use cautiously):
   - Academic case studies (peer-reviewed)
   - Industry blog posts

4. **SKIP**:
   - Anonymous tweets / unverified social media
   - Marketing material

## Output format

| Date | Organization | Country | What happened | Source URL | Harm severity (Low/Med/High/Critical) | Source tier (1/2/3) |
|---|---|---|---|---|---|---|

Target: 5-10 cases với primary source verified. Distribute:
- 3-4 cases từ Dimension 1 (industry)
- 3-4 cases từ Dimension 2 (failure mode)  
- 2-3 cases từ Dimension 3 (user persona)

## Anti-patterns AVOID

❌ Generic ("AI sometimes hallucinates")
✅ Specific incident với date + organization + harm + source URL

❌ Anonymous/unverified claims
✅ Cite primary source linkable

❌ Marketing speak
✅ Court records + regulatory filings + established journalism
```

---

## ✅ Fact-check checklist (làm SAU khi nhận output)

Sau khi AI gen output, copy vào `worksheet/01-test-set-review/1-diverge.md` Phần A (cột URL nguồn) và fact-check:

- [ ] Click vào MỖI source URL → verify accessible + accurate
- [ ] Cross-check 2+ independent sources cho high-severity cases (Critical/High)
- [ ] Mark cases unverified với `[UNVERIFIED]` tag — KHÔNG dùng cho group brainstorm
- [ ] Note primary vs derivative source (court record > news > blog)
- [ ] Date check — case có còn relevant không, hay policy đã thay đổi?
- [ ] Save 2-3 cases tốt nhất với primary source URL → dùng làm anchor cho Diverge Step 2

## 🛠️ Tool-specific tips

- **Claude Deep Research**: best cho academic + court records
- **Gemini Deep Research**: best cho recent news + crossref
- **Perplexity Pro**: best cho Vietnamese-language sources
- **GPT Deep Research**: best cho industry/business case studies

→ Có thể chạy 2 tools parallel để cross-check.
