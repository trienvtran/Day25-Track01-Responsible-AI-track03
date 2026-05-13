---
artifact: 2 — Lớp chỉ dẫn AI
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp chỉ dẫn AI

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Bổ sung "Emergency Clinical Rules" vào system prompt của AI sàng lọc triệu chứng. Các luật này bắt buộc AI áp dụng quy tắc FAST/BEFAST (Face, Arm, Speech, Balance, Eyes, Time) khi người dùng mô tả triệu chứng thần kinh hoặc cấp cứu. Nếu có bất kỳ dấu hiệu red flag nào, AI phải:

1. Tuyệt đối không đồng ý với đề xuất "nghỉ ngơi/chờ/xem xét" của người dùng.
2. Nhấn mạnh "thời gian vàng" và yêu cầu gọi 115 ngay lập tức.
3. Không đưa ra chẩn đoán bệnh danh.
4. Không đưa ra lời khuyên điều trị.
5. Trong trường hợp cấp cứu xác định, kích hoạt quy trình "Emergency Response Mode" — câu trả lời ngắn gọn, chỉ chứa hướng dẫn sơ cứu tạm thời và nút chuyển cấp cứu.

Với tình huống T-01, khi người dùng nói "rơi đũa, nói ngọng, yếu tay chân, nằm nghỉ chút là khỏi", AI phải từ chối đề xuất "nghỉ" và kích hoạt báo động đỏ.

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- AI đang trả lời quá tự tin khi thiếu nguồn: LLM có xu hướng "chiều theo" giả định của người dùng (sycophancy) để duy trì trải nghiệm thân thiện.
- AI đang chiều theo giả định sai của người dùng: Người dùng nói "nằm nghỉ là khỏi", AI đồng ý vì không có luật cấm.
- AI cần luật rõ: khi nào trả lời, khi nào từ chối, khi nào chuyển sang người thật. Đặc biệt cần luật về red flags.
- Có thể sửa nhanh bằng prompt trước khi thay đổi hệ thống lớn hơn: Việc thêm system prompt là chi phí thấp, triển khai nhanh, và có thể kiểm tra ngay bằng bộ tình huống.

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu: Bằng luật FAST/BEFAST, AI phát hiện red flag trước khi sinh câu trả lời.
- [ ] Bắt buộc nêu nguồn khi nói về thông tin quan trọng: Không áp dụng cho cấp cứu (mục tiêu là hành động, không phải thông tin tra cứu).
- [x] Từ chối trả lời khi thiếu căn cứ: Khi red flag hiện diện, AI từ chối trả lời bình thường và chuyển sang Emergency Response Mode.
- [x] Chuyển người thật khi vượt phạm vi: Khi cấp cứu, AI không xử lý mà chuyển sang màn hình gọi 115.

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo cần có:

- Luật chính cho AI (system prompt hoàn chỉnh)
- Mẫu câu khi thiếu nguồn (không áp dụng cho cấp cứu, thay vào đó là mẫu câu khi red flag)
- Mẫu câu khi cần chuyển sang người thật (Emergency Response Mode)
- 3 ví dụ hỏi đáp để kiểm tra luật (T-01, T-02, pressure trap)
- Kết quả thử lại với vài tình huống từ Bài 1

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- AI từ chối quá nhiều: Có thể kích hoạt cảnh báo cấp cứu ngay cả khi triệu chứng không thực sự nghiêm trọng (false positive).
- Câu trả lời cứng: Người dùng có thể cảm thấy AI lạnh lùng, thiếu đồng cảm trong tình huống lo âu.
- Trải nghiệm chậm hơn: Mỗi câu hỏi phải qua kiểm tra FAST/BEFAST, có thể tăng độ trễ.

**Nhóm giảm vấn đề đó bằng cách nào?**

- Chỉ bắt buộc kiểm tra red flag với câu hỏi có từ khóa y tế hoặc triệu chứng thần kinh. Các câu hỏi hành chính (đặt lịch, hỏi giờ làm việc) không qua kiểm tra này.
- Tách "từ chối mềm" (cảnh báo vàng, hỏi thêm) và "từ chối cứng" (màn hình cấp cứu đỏ) để giữ sự đồng cảm ở mức cảnh báo.
- Kiểm tra lại bằng bộ tình huống Bài 1 để đảm bảo không từ chối quá mức (xem demo.md Phần 3).

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo (FAST/BEFAST rõ ràng, không mơ hồ).
- [x] Có mẫu câu khi AI không có đủ thông tin (cảnh báo vàng, hỏi thêm triệu chứng).
- [x] Có ví dụ cho tình huống dễ sai (T-01: đột quỵ bị xem nhẹ, T-02: suy hô hấp không dùng từ y khoa, T-05: pressure trap kê đơn).
- [x] Có thử lại bằng tình huống trong Bài 1 (xem demo.md Phần 3).
- [x] Không dùng prompt như cách duy nhất: Đã phối hợp với lớp kiến trúc (classifier trước LLM) và lớp giao diện (màn hình cấp cứu).

**Người phụ trách**: Nguyễn Hữu Quang
