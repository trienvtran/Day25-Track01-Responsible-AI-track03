---
artifact: 1 — Lớp giao diện
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp giao diện

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thiết kế "Emergency Screen Takeover": khi hệ thống phát hiện red flag (đột quỵ, suy hô hấp, hóc dị vật, tự sát...), giao diện chat thông thường bị thay thế hoàn toàn bởi màn hình cấp cứu. Màn hình cấp cứu có nền đỏ, thông điệp ngắn gọn về mức độ nguy hiểm, nút gọi 115, hướng dẫn sơ cứu tạm thời, và nút chia sẻ vị trí. Không còn ô nhập tin nhắn để người dùng tiếp tục trò chuyện với AI.

Với tình huống T-01 (đột quỵ), khi người dùng nói "rơi đũa, nói ngọng, yếu tay chân", giao diện ngay lập tức chuyển sang màn hình cấp cứu, ngăn chặn khả năng người dùng tiếp tục đọc câu trả lời mang tính an ủi từ AI.

---

## 2. Vì sao sửa ở lớp giao diện?

- Người dùng dễ tin câu trả lời của AI quá mức (automation bias), đặc biệt khi chatbot được tích hợp trên ứng dụng bệnh viện chính thức.
- Rủi ro xảy ra ở khoảnh khắc người dùng đọc câu trả lời "nằm nghỉ chút là khỏi" và quyết định không gọi cấp cứu.
- Giao diện cần làm rõ: đây không còn là tư vấn thông thường, đây là tình huống đe dọa tính mạng.
- Nếu prompt hoặc dữ liệu vẫn sót lỗi (ví dụ: classifier bỏ sót), giao diện là lớp chặn cuối: ngay cả khi LLM sinh câu trả lời an ủi, người dùng không thể đọc được vì màn hình đã chuyển sang cấp cứu.

**Hành động phòng vệ chính**:

- [x] Thông báo rõ giới hạn: màn hình hiển thị rõ "Đây là tình huống cấp cứu. AI không thể tư vấn."
- [x] Phát hiện dấu hiệu thiếu nguồn: khi chuyển cấp cứu, không hiển thị thông tin "chưa xác minh" mà hiển thị hành động bắt buộc.
- [x] Chuyển người thật khi cần: nút gọi 115 và liên hệ tổng đài y tế.
- [ ] Giúp người dùng kiểm tra lại nguồn: không áp dụng trong tình huống cấp cứu vì mục tiêu là hành động ngay lập tức.

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

**Định dạng demo**:

- [x] Phác thảo màn hình
- [ ] Luồng màn hình
- [ ] Bản HTML đơn giản
- [ ] Ảnh hoặc link prototype

**Thành phần cần có trong demo**:

- Trạng thái có nguồn xác minh: Không áp dụng cho tình huống cấp cứu (mục tiêu là hành động, không phải thông tin).
- Trạng thái chưa có nguồn xác minh: Hiển thị dưới dạng cảnh báo vàng khi triệu chứng mơ hồ (ví dụ: chỉ có 1/5 dấu hiệu FAST).
- Cách người dùng chuyển sang người thật: Nút "Gọi 115" lớn, màu đỏ, ở giữa màn hình.
- Câu chữ cảnh báo ngắn, dễ hiểu: "Có dấu hiệu đột quỵ. Gọi cấp cứu ngay. Đừng lái xe."

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- Màn hình cấp cứu có thể gây hoảng loạn cho người dùng, đặc biệt người lớn tuổi hoặc người đang trong trạng thái lo âu.
- Có thể gây "cảnh báo giả" (false positive) nếu classifier nhạy quá mức, dẫn đến người dùng gọi cấp cứu không cần thiết.
- Người dùng có thể cảm thấy bị "ép buộc" và mất quyền kiểm soát quyết định.

**Nhóm giảm vấn đề đó bằng cách nào?**

- Chỉ kích hoạt màn hình đỏ khi classifier có độ tin cậy cao (>= 95%). Với triệu chứng mơ hồ (1-2 dấu hiệu), hiển thị màn hình vàng để hỏi thêm thông tin thay vì đỏ ngay.
- Thêm nút "Tôi đã gọi 115" để người dùng xác nhận đã hành động, và nút "Hiển thị hướng dẫn sơ cứu" để giảm cảm giác bị bỏ rơi.
- Ghi rõ: "Quyết định cuối cùng thuộc về bạn, nhưng đây là khuyến cáo y tế chuẩn."

---

## 5. Checklist trước khi nộp

- [x] Giải pháp gắn đúng với một rủi ro chính (T-01 undertriage đột quỵ).
- [x] Demo nhìn vào là hiểu vấn đề được chặn ở đâu (màn hình chuyển từ chat sang cấp cứu).
- [x] Có đủ trạng thái bình thường và trạng thái lỗi (xanh: thường, vàng: cảnh báo, đỏ: cấp cứu).
- [x] Có cách chuyển sang người thật khi AI không nên tự xử lý (nút gọi 115, hotline).
- [x] Câu chữ trong giao diện ngắn, không đổ hết trách nhiệm cho người dùng (không nói "Tự bạn chịu trách nhiệm" mà nói "Hãy để chuyên gia y tế đánh giá").

**Người phụ trách**: Nguyễn Thị Ngọc
