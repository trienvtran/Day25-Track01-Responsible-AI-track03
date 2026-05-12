# Day 25 — Responsible AI: Solution Design

Day 25 là bài tập nhóm 2-3 người cùng chủ đề (track).

Nhóm bắt đầu từ 2 file đã làm ở Day 24:

- `01-risk-map.md`
- `02-test-eval-plan.md`

Cuối buổi, nhóm nộp:

- Một bộ kiểm thử cuối gồm 10-15 tình huống.
- Ba lớp giải pháp cho rủi ro quan trọng nhất: giao diện, chỉ dẫn AI, kiến trúc dữ liệu.

## Cần nộp gì?

Nhóm tạo 1 repo công khai chứa toàn bộ thư mục `worksheet/`, rồi nộp link qua LMS. Hạn cuối: 23:59 hôm nay.

Hai file dưới đây là kết quả chính:

| File | Nội dung |
|---|---|
| `worksheet/01-test-set-review/3-FINAL-test-set-eval-plan.md` | 10-15 tình huống kiểm thử cuối + kế hoạch chấm |
| `worksheet/02-solution-design/1-map-and-format.md` | Rủi ro được chọn, tầng giải pháp, định dạng demo, 3 lớp giải pháp |

Thư mục `worksheet/02-solution-design/artifact/` cũng phải có đủ 3 bộ giải pháp:

- `artifact/1-uiux/`
- `artifact/2-prompt/`
- `artifact/3-architecture/`

Mỗi bộ có `card.md` và `demo.*`.

Các file trung gian vẫn phải nộp kèm để người chấm thấy nhóm đã đi qua đủ quá trình:

- `worksheet/01-test-set-review/1-diverge.md`
- `worksheet/01-test-set-review/2-converge.md`

## Quy tắc đặt tên repo

Cú pháp:

```text
day25-trackN-<ten-nhom>
```

Ví dụ:

- `day25-track1-alpha`
- `day25-track7-team-x`

Quy tắc:

- `day25`: bắt buộc, viết liền, chữ thường.
- `trackN`: số chủ đề Day 24 nhóm đã chọn, ví dụ `track1`, `track7`.
- `<ten-nhom>`: tên nhóm tự đặt, chữ thường, dùng gạch nối thay khoảng trắng.

## Cách tạo repo và nộp bài

1. Tạo repo công khai trên GitHub hoặc GitLab.
2. Đẩy toàn bộ thư mục `worksheet/` lên repo.
3. Tạo `README.md` ở đầu repo, ghi rõ mã học viên và họ tên đầy đủ của 2-3 thành viên.
4. Một thành viên đại diện nộp link repo vào LMS.
5. Kiểm tra repo mở được trước 23:59.

## Luồng làm bài

```text
Đọc lại 01-risk-map.md + 02-test-eval-plan.md từ Day 24
   -> Điền 00-context.md
   -> Bài 1: Rà bộ kiểm thử
      -> Mở rộng: tìm sự cố thật + dùng AI gợi ý tình huống
      -> Hội tụ: gộp, lọc trùng, chấm rủi ro
      -> Chốt 10-15 tình huống cuối
   -> Bài 2: Thiết kế giải pháp
      -> Chọn rủi ro chính
      -> Tìm nguyên nhân gốc
      -> Chọn tầng sửa và định dạng demo
      -> Xây 3 lớp giải pháp song song
   -> Phản biện chéo với nhóm khác
   -> Chỉnh lại file
   -> Nộp link repo qua LMS
```

## Bài 1 — Rà bộ kiểm thử

Mục tiêu: chọn ra 10-15 tình huống đáng kiểm thử nhất và viết kế hoạch chấm rõ ràng.

File cuối của Bài 1:

```text
worksheet/01-test-set-review/3-FINAL-test-set-eval-plan.md
```

### Giai đoạn Mở rộng — 30 phút

Mỗi thành viên làm trước, sau đó mới gộp nhóm.

1. Tìm sự cố thật có nguồn.
2. Dùng AI gợi ý thêm tình huống theo 4 góc nhìn.
3. Chọn khoảng 15 tình huống tốt nhất của mỗi người.

File dùng ở giai đoạn này:

```text
worksheet/01-test-set-review/1-diverge.md
```

### Giai đoạn Hội tụ — 30 phút

Nhóm cùng làm.

1. Gộp toàn bộ tình huống của nhóm.
2. Lọc trùng theo kiểu lỗi.
3. Chấm điểm rủi ro: Tác động x Độ khẩn cấp.
4. Chốt 10-15 tình huống cuối.

File dùng ở giai đoạn này:

```text
worksheet/01-test-set-review/2-converge.md
```

## Bài 2 — Thiết kế giải pháp

Mục tiêu: chọn rủi ro quan trọng nhất từ Bài 1, rồi xây 3 lớp giải pháp cho cùng rủi ro đó.

File cuối của Bài 2:

```text
worksheet/02-solution-design/1-map-and-format.md
```

Ba lớp giải pháp:

| Lớp | Thư mục | Mục đích |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Giúp người dùng thấy cảnh báo, nguồn, đường chuyển người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Buộc AI hỏi lại, từ chối, hoặc dẫn nguồn khi cần |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Đảm bảo AI tra cứu đúng nguồn và có phương án dự phòng |

Ba lớp này bổ sung cho nhau. Một lớp có thể lọt lỗi, nhiều lớp sẽ giảm rủi ro tốt hơn.

## Tài liệu trong thư mục này

| File / Thư mục | Dùng để làm gì |
|---|---|
| `track-bank-scenario-kit-v1.md` | Chọn và đọc lại bối cảnh chủ đề |
| `worksheet/00-context.md` | Điền bối cảnh một lần, dán vào đầu mọi cuộc trò chuyện với AI |
| `worksheet/01-test-set-review/` | Làm Bài 1. Hướng dẫn chi tiết nằm ngay trong từng file worksheet |
| `worksheet/02-solution-design/` | Làm Bài 2. Hướng dẫn chọn tầng, demo, phản biện nằm trong worksheet |
| `prompts/` | Prompt mẫu cho từng bước |

## Bảng dùng prompt mẫu

| Prompt mẫu | Dùng khi nào | Lưu kết quả vào |
|---|---|---|
| `prompts/01-deep-research.md` | Tìm sự cố thật | `1-diverge.md` Phần A |
| `prompts/02-brainstorm.md` | Dùng AI gợi ý tình huống | `1-diverge.md` Phần B |
| `prompts/03-convergent-analysis.md` | Lọc trùng và ưu tiên | `2-converge.md` |
| `prompts/04-solution-options.md` | Gợi ý hướng giải pháp | `1-map-and-format.md` |
| `prompts/05a-*` đến `05f-*` | Dựng demo nhanh | `artifact/*/demo.*` |

## Cách dùng prompt mẫu

1. Mở Claude / ChatGPT / Gemini / Perplexity tùy bước.
2. Dán toàn bộ `worksheet/00-context.md` vào đầu cuộc trò chuyện.
3. Dán prompt mẫu phù hợp từ thư mục `prompts/`.
4. AI tạo bản nháp.
5. Nhóm đọc lại, sửa, rồi lưu vào đúng file bài tập.

AI chỉ hỗ trợ dựng bản nháp. Nhóm vẫn chịu trách nhiệm kiểm tra nguồn, sửa nội dung, và chốt quyết định cuối.

## Checklist trước khi nộp

- [ ] `worksheet/00-context.md` đã điền đủ.
- [ ] `1-diverge.md` có đủ Phần A, B, C.
- [ ] `2-converge.md` có bảng gộp, bảng lọc trùng, bảng chấm rủi ro.
- [ ] `3-FINAL-test-set-eval-plan.md` có 10-15 tình huống cuối và kế hoạch chấm.
- [ ] `1-map-and-format.md` có rủi ro được chọn, nguyên nhân gốc, 3 lớp giải pháp.
- [ ] `artifact/1-uiux/`, `artifact/2-prompt/`, `artifact/3-architecture/` đều có `card.md` và `demo.*`.
- [ ] Repo công khai mở được.
- [ ] README đầu repo có mã học viên và họ tên đầy đủ.
- [ ] Link repo đã nộp qua LMS trước 23:59.

## Lỗi hay mắc

| Đừng làm | Nên làm |
|---|---|
| Bỏ qua `00-context.md` | Điền bối cảnh trước khi dùng AI |
| Nộp mỗi file cuối | Giữ cả file trung gian |
| AI viết xong là nộp | Nhóm phải đọc, sửa, kiểm chứng |
| Chỉ làm một lớp giải pháp | Làm đủ 3 lớp: giao diện, chỉ dẫn AI, kiến trúc |
| Demo chỉ để nhìn đẹp | Demo phải giúp người khác hiểu và phản biện |
| Nộp repo private | Repo phải công khai |
