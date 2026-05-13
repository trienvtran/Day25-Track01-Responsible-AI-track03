---
artifact: 1 — Demo giao diện
format: phác thảo ASCII màn hình
---

# demo.md — Demo giao diện

File này minh họa 3 trạng thái giao diện: (1) Chat thông thường, (2) Cảnh báo vàng khi triệu chứng mơ hồ, (3) Màn hình cấp cứu đỏ khi red flag xác định.

---

## 1. Màn hình chính

### Trạng thái A — Chat thông thường (xanh)

```text
┌─────────────────────────────────────────────┐
│  🏥 Triage AI Assistant          [?] [⋮]   │
├─────────────────────────────────────────────┤
│                                             │
│  🤖 Xin chào! Tôi có thể giúp gì cho bạn    │
│     hôm nay?                                │
│                                             │
│  👤 Bố tôi 70 tuổi, tự nhiên rơi đũa ăn     │
│     cơm, nói ngọng...                       │
│                                             │
│  ────────────────────────────────────────   │
│  Bạn đang trò chuyện với AI sàng lọc.       │
│  AI không thay thế bác sĩ.                  │
│  ────────────────────────────────────────   │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │ Nhập triệu chứng hoặc câu hỏi...    │    │
│  │                              [➤]   │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

### Trạng thái B — Cảnh báo vàng (triệu chứng mơ hồ)

Khi classifier phát hiện 1-2 dấu hiệu FAST nhưng chưa đủ để xác định:

```text
┌─────────────────────────────────────────────┐
│  🏥 Triage AI Assistant          [?] [⋮]   │
├─────────────────────────────────────────────┤
│  ┌─────────────────────────────────────┐    │
│  │ ⚠️ CẢNH BÁO Y TẾ                    │    │
│  │                                     │    │
│  │ Các triệu chứng bạn mô tả có thể    │    │
│  │ liên quan đến vấn đề thần kinh.     │    │
│  │ Hãy trả lời thêm 2 câu để AI đánh   │    │
│  │ giá chính xác hơn.                  │    │
│  │                                     │    │
│  │ [Tiếp tục trả lời]  [Gọi 115 ngay]  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  🤖 Bạn có thể cho tôi biết:                │
│     • Mặt bố bạn có bị méo không?           │
│     • Hai tay giơ lên có giữ được không?    │
│                                             │
│  👤 ...                                     │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │ Nhập câu trả lời...          [➤]   │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

### Trạng thái C — Màn hình cấp cứu đỏ (red flag xác định)

Khi classifier xác định đủ dấu hiệu FAST/BEFAST hoặc từ khóa cấp cứu:

```text
┌─────────────────────────────────────────────┐
│  🏥 Triage AI Assistant          [?] [⋮]   │
├─────────────────────────────────────────────┤
│  ┌─────────────────────────────────────┐    │
│  │                                     │    │
│  │     🚨 CẤP CỨU — GỌI 115 NGAY     │    │
│  │                                     │    │
│  │  Phát hiện dấu hiệu đột quỵ.        │    │
│  │  Thời gian vàng: 4.5 giờ đầu.      │    │
│  │  Mỗi phút trôi qua làm tăng nguy    │    │
│  │  cơ tử vong và tàn tật.              │    │
│  │                                     │    │
│  │        ┌─────────────────┐            │    │
│  │        │   📞 GỌI 115   │            │    │
│  │        └─────────────────┘            │    │
│  │                                     │    │
│  │  ┌─────────────────────────────┐    │    │
│  │  │ 📍 Chia sẻ vị trí hiện tại  │    │    │
│  │  └─────────────────────────────┘    │    │
│  │                                     │    │
│  │  🩺 Sơ cứu tạm thời:               │    │
│  │  • Để bệnh nhân nằm đầu cao 30°   │    │
│  │  • Không cho ăn/uống              │    │
│  │  • Không tự lái xe đi viện        │    │
│  │                                     │    │
│  │  [Tôi đã gọi 115]  [Gọi người thân] │   │
│  │                                     │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ── AI đã ngừng trò chuyện. ──             │
│                                             │
└─────────────────────────────────────────────┘
```

---

## 2. Trạng thái cần minh họa

| Trạng thái | Người dùng thấy gì? | Người dùng làm gì tiếp? |
|---|---|---|
| Có nguồn xác minh | Không áp dụng cho cấp cứu. Trạng thái này chỉ dùng khi AI trả lời câu hỏi thông thường (ví dụ: "Chuyên khoa nào khám đau đầu?") có kèm nguồn BYT. | Đọc và xác nhận. |
| Chưa có nguồn xác minh | Cảnh báo vàng + yêu cầu thêm thông tin. Không hiển thị câu trả lời "chắc chắn". | Trả lời thêm câu hỏi hoặc gọi 115 nếu lo lắng. |
| AI không nên tự trả lời | Màn hình đỏ cấp cứu. Không còn ô chat. AI đã bị "tắt" ở tình huống này. | Gọi 115, làm theo hướng dẫn sơ cứu, chia sẻ vị trí. |
| Cần chuyển sang người thật | Nút "Gọi 115" to và nổi bật. Hotline tổng đài y tế hiển thị rõ. | Bấm gọi 115 hoặc nút "Gọi người thân". |

---

## 3. Ghi chú cho từng thành phần

- **Banner cấp cứu (đỏ)**: Chiếm 80% màn hình, nền đỏ đậm `#C00000`, chữ trắng `#FFFFFF`. Vị trí: toàn màn hình. Nội dung: ngắn gọn, không quá 5 dòng. Hành vi: không thể vuốt tắt, không thể quay lại chat.
- **Nút Gọi 115**: Màu xanh lá `#00A651` (màu hy vọng trên nền đỏ cảnh báo), font lớn, chiếm 60% chiều rộng màn hình. Vị trí: giữa màn hình, ngay dưới thông điệp cấp cứu. Hành vi: bấm là gọi ngay qua `tel:115`.
- **Nút chia sẻ vị trí**: Màu xanh dương nhạt, vị trí dưới nút Gọi 115. Hành vi: mở GPS share.
- **Hướng dẫn sơ cứu**: Font nhỏ hơn, có thể cuộn. Không chiếm spotlight từ nút Gọi 115.
- **Xác nhận đã gọi**: Nút phụ, giúp người dùng giảm lo âu bằng cách xác nhận họ đã hành động.

---

## 4. Kiểm tra nhanh

- [x] Nhìn vào demo là hiểu rủi ro đang được chặn ở đâu (không còn ô chat → không còn câu trả lời an ủi nguy hiểm).
- [x] Có trạng thái khi AI không có đủ thông tin (cảnh báo vàng, hỏi thêm FAST).
- [x] Có cách chuyển sang người thật (nút Gọi 115, hotline).
- [x] Câu chữ đủ ngắn để đặt trên màn hình thật ("Gọi 115 ngay", "Thời gian vàng: 4.5 giờ").
