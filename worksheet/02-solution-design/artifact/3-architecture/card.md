---
artifact: 3 — Lớp kiến trúc dữ liệu
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp kiến trúc dữ liệu

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Xây dựng "Hybrid Triage Pipeline": một kiến trúc lai kết hợp rule-based classifier với LLM. Trước khi câu hỏi của người dùng đến LLM, hệ thống chạy qua **Deterministic Emergency Classifier** (lớp phân loại xác định) sử dụng:

1. **Red Flag Dictionary**: Từ điển từ khóa cấp cứu (FAST/BEFAST keywords, triệu chứng cấp cứu).
2. **Clinical Decision Rules**: Quy tắt lâm sàng cứng (ví dụ: "rơi đồ vật + nói ngọng + yếu tay" → cấp cứu đỏ).
3. **Confidence Scorer**: Đánh giá độ tin cậy của phân loại.

Kết quả classifier chia câu hỏi vào 3 luồng:
- **Luồng Xanh** (bình thường): Đến LLM với system prompt thông thường.
- **Luồng Vàng** (cảnh báo): Đến LLM với system prompt đặc biệt (hỏi thêm, cảnh báo).
- **Luồng Đỏ** (cấp cứu): **Bypass LLM hoàn toàn**. Hiển thị màn hình cấp cứu từ template có sẵn.

Ngoài ra, hệ thống có **Triage Log & Monitor** để ghi lại mọi quyết định phân loại, phục vụ theo dõi và cải tiến.

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

- Nguyên nhân chính là thiếu nguồn đúng hoặc nguồn cũ: Hệ thống hiện tại không có cơ sở dữ liệu quy tắc lâm sàng FAST/BEFAST để AI tra cứu.
- AI đang phải tự nhớ thông tin thay vì đọc từ nguồn đáng tin cậy: LLM không phải cơ sở dữ liệu y khoa. Cần bắt buộc AI tra cứu từ nguồn chuẩn trước khi trả lời.
- Cần kiểm tra dữ liệu trước khi câu trả lời được tạo ra: Deterministic classifier đảm bảo không bao giờ để LLM tự do xử lý tình huống cấp cứu.
- Cần ghi lại lỗi để nhóm biết lỗi nào lặp lại nhiều: Triage Log giúp phát hiện undertriage (classifier không bắt được) và overtriage (classifier nhạy quá mức).

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng nguồn dữ liệu đúng: Red Flag Dictionary từ Hướng dẫn Bộ Y tế.
- [x] Phát hiện khi nguồn thiếu hoặc lỗi: Confidence Scorer đánh dấu khi classifier không chắc chắn.
- [x] Khắc phục bằng cách chuyển sang người thật: Luồng Đỏ bypass LLM, hiển thị nút gọi 115.
- [x] Ghi lại lỗi để cải thiện sau: Triage Log lưu input, phân loại, hành động, và kết quả.

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo cần có:

- Sơ đồ cách dữ liệu đi qua hệ thống (Mermaid flowchart)
- Nguồn dữ liệu chính thức (Red Flag Dictionary, Clinical Decision Rules)
- Bước kiểm tra trước khi AI trả lời (Deterministic Emergency Classifier)
- Cách xử lý khi nguồn thiếu, lỗi hoặc quá cũ (Luồng Vàng: hỏi thêm + cảnh báo)
- Cách ghi lại hoặc theo dõi lỗi (Triage Log & Monitor)

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- Trả lời chậm hơn: Thêm bước classifier trước LLM tăng độ trễ 50-200ms.
- Phụ thuộc vào nguồn dữ liệu: Red Flag Dictionary cần được cập nhật thường xuyên theo hướng dẫn mới của Bộ Y tế.
- Hệ thống phức tạp hơn: Cần đội ngũ kỹ thuật duy trì classifier, dictionary, và log system.
- False positive: Classifier có thể nhầm câu hỏi thông thường thành cấp cứu (ví dụ: "Tôi đang xem phim về đột quỵ").

**Nhóm giảm vấn đề đó bằng cách nào?**

- Lưu tạm (cache) kết quả classifier cho các câu hỏi giống nhau trong 5 phút để giảm độ trễ.
- Thiết lập quy trình cập nhật dictionary định kỳ 3 tháng/lần, có bác sĩ chuyên khoa rà soát.
- Dùng MLOps đơn giản: dictionary dạng JSON, dễ chỉnh sửa không cần code.
- Thêm bước "context check": classifier xem xét ngữ cảnh câu hỏi, không chỉ keyword matching đơn thuần.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu (người dùng → classifier → 3 luồng → UI/LLM).
- [x] Có bước kiểm tra nguồn trước khi AI trả lời (Deterministic Emergency Classifier).
- [x] Có cách xử lý khi không có dữ liệu (Luồng Vàng: hỏi thêm + chuyển người thật nếu vẫn không rõ).
- [x] Có cách chuyển sang người thật với tình huống rủi ro cao (Luồng Đỏ: bypass LLM, hiển thị màn hình cấp cứu + gọi 115).
- [x] Có cách biết lỗi này có đang lặp lại không (Triage Log & Monitor dashboard).

**Người phụ trách**: Trần Vọng Triển
