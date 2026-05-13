---
artifact: 1 — FINAL kế hoạch giải pháp
bai-tap: 2 — Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có — file cuối Bài 2
---

# 1 — FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Lý do cần 3 lớp: một giải pháp đơn lẻ dễ lọt lỗi. Với rủi ro nặng, nhóm cần nhiều lớp cùng đỡ: lớp này ngăn, lớp kia phát hiện, lớp khác khắc phục hoặc thông báo cho người dùng.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Cảnh báo, dẫn nguồn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối, bắt buộc dẫn nguồn |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Tra cứu nguồn đúng, lưu tạm dữ liệu, xử lý khi thiếu nguồn, giám sát |

Ba lớp này bổ sung cho nhau. Nếu một lớp lọt lỗi, lớp khác vẫn có thể chặn hoặc giảm hại.

## Thông tin nhóm

- **Chủ đề**: Trợ lý Sàng lọc Triệu chứng Y khoa và Tâm lý (Triage AI Assistant)
- **Thành viên**: Nguyễn Thị Ngọc, Nguyễn Hữu Quang, Trần Vọng Triển, Nguyễn Thị Ngọc Thư
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-01
- **Mô tả ngắn**: Khi bệnh nhân hoặc người nhà mô tả triệu chứng đột quỵ (rơi đũa, nói ngọng, yếu tay chân) nhưng đùn đẩy ý định đi viện, AI có xu hướng đồng ý với giả định "nằm nghỉ sẽ khỏi" thay vì kích hoạt báo động đỏ, gây bỏ lỡ "thời gian vàng" 4.5 giờ đầu và tử vong/tàn tật vĩnh viễn cho bệnh nhân.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**:
  - Đột quỵ là nguyên nhân tử vong hàng đầu tại Việt Nam; mỗi phút trôi qua làm tăng nguy cơ tử vong và tàn phế.
  - Tình huống T-01 có điểm rủi ro cao nhất (25) và đại diện cho nhóm undertriage — lỗi nguy hiểm nhất của AI y tế.
  - Giải pháp cho T-01 có thể mở rộng sang T-02 (suy hô hấp), T-12 (hóc dị vật) và các trường hợp cấp cứu khác trong bộ kiểm thử.

### Tìm nguyên nhân gốc

Đừng chỉ mô tả lỗi. Hãy trả lời: vì sao lỗi xảy ra?

- [x] Thiếu nguồn dữ liệu đúng: Hệ thống chưa tích hợp bộ quy tắc lâm sàng FAST/BEFAST và quy trình báo động đỏ của Bộ Y tế.
- [x] AI đoán khi không biết: LLM được huấn luyện để trả lời thân thiện, mang tính an ủi, dẫn đến "chiều theo" giả định sai của người dùng (sycophancy).
- [x] Giao diện khiến người dùng tin quá mức: Giao diện chat thông thường không có trạng thái "cấp cứu", khiến người dùng xem AI như tư vấn viên thay vì công cụ sàng lọc.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật: Không có lớp phân loại xác định (deterministic layer) trước LLM để bắt buộc chuyển cấp cứu.
- [ ] Không có theo dõi sau khi ra mắt.
- [ ] Khác: [...]

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| Thiếu nguồn đúng | Dữ liệu / tra cứu nguồn (RAG) / chính sách nguồn | `3-architecture` là chính |
| AI đoán bừa | Chỉ dẫn hệ thống / quy tắc từ chối / dẫn nguồn | `2-prompt` là chính |
| Người dùng tin quá mức | Giao diện cảnh báo / cách viết mức tin cậy | `1-uiux` là chính |
| Tình huống nhạy cảm | Người duyệt / chuyển sang người thật | `1-uiux` + `2-prompt` + `3-architecture` |
| Lỗi lặp lại sau khi ra mắt | Theo dõi / vòng phản hồi | `3-architecture` là chính |

Nguyên tắc: lỗi ở tầng nào, ưu tiên sửa ở tầng đó. Đừng chỉ thêm cảnh báo giao diện nếu nguyên nhân gốc là thiếu nguồn dữ liệu hoặc AI đoán khi không biết.

### 10 tầng giải pháp tham khảo

Không bắt buộc dùng đủ 10 tầng. Bảng này giúp nhóm chọn đúng hướng sửa.

| Tầng | Khi nào dùng |
|---|---|
| Giao diện | Người dùng tin AI quá mức, thiếu cảnh báo, thiếu nguồn, thiếu nút chuyển sang người thật |
| Chỉ dẫn AI | AI đoán khi không biết, không hỏi lại, không từ chối |
| Quy trình xử lý | Cần phân loại ý định, chuyển đúng nơi xử lý, có cách xử lý khi AI không nên trả lời |
| Dữ liệu / tra cứu nguồn (RAG) | Thiếu nguồn đúng, nguồn cũ, AI không dựa vào nguồn đáng tin cậy |
| Theo dõi | Lỗi lặp lại sau khi ra mắt nhưng không ai thấy |
| Chính sách / thông báo giới hạn | Người dùng không biết giới hạn của AI |
| Người duyệt / phê duyệt | Tình huống pháp lý, y tế, tài chính, tuyển dụng, hoặc tác động lớn |
| Vai trò trách nhiệm | Có cảnh báo nhưng không ai chịu trách nhiệm xử lý |
| Vòng phản hồi | Cần người dùng / người rà báo lỗi để cập nhật hệ thống |
| Kiến trúc lai | LLM một mình không đủ, cần rule, classifier, hoặc nhiều bước kiểm tra |

### 4 hành động phòng vệ

Mỗi lớp nên làm ít nhất một việc:

- **Ngăn**: giảm khả năng lỗi xảy ra từ đầu.
- **Phát hiện**: nhận ra lỗi hoặc tín hiệu nguy hiểm.
- **Khắc phục**: chuyển sang người thật, dùng câu trả lời dự phòng, hoặc dừng trả lời.
- **Thông báo**: giúp người dùng hiểu mức tin cậy và rủi ro.

Gợi ý theo mức rủi ro:

| Mức rủi ro | Nên có |
|---|---|
| Nhẹ | Ít nhất 1 hành động |
| Vừa | Ít nhất 2 hành động |
| Nặng | Ít nhất 3 hành động |
| Rất nặng / không đảo ngược được | Cố gắng đủ 4 hành động + có người chịu trách nhiệm |

### Kết luận Phần A

**Nguyên nhân gốc**: AI đang vận hành như một chatbot đối thoại tự do thay vì một hệ thống sàng lọc có quy tắc lâm sàng rõ ràng. LLM không có tầng phân loại triệu chứng nguy hiểm (deterministic classifier) trước khi sinh câu trả lời, giao diện không phân biệt trạng thái "thông thường" và "cấp cứu", và system prompt thiếu luật bắt buộc kích hoạt báo động đỏ khi gặp dấu hiệu FAST/BEFAST.

**Tầng chính cần sửa**: Kiến trúc dữ liệu / Quy trình xử lý (bổ sung deterministic classifier trước LLM).

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: Giảm automation bias bằng cách thay đổi trạng thái màn hình từ "chat thân thiện" sang "màn hình cấp cứu" khi có dấu hiệu nguy hiểm, giúp người dùng nhận ra mức độ nghiêm trọng ngay cả khi nội dung AI bị lỗi.
- Lớp chỉ dẫn AI: Bổ sung luật lâm sàng FAST/BEFAST vào system prompt, bắt buộc AI từ chối đồng ý với các đề xuất "chờ/nghỉ" khi có red flag, và luôn kích hoạt quy trình khẩn cấp.
- Lớp kiến trúc dữ liệu: Thêm tầng phân loại xác định (rule-based + keyword matching) trước LLM để bắt buộc chuyển sang màn hình cấp cứu khi phát hiện triệu chứng đột quỵ hoặc các red flag khác, đảm bảo không bao giờ để LLM tự do trả lời trong tình huống cấp cứu.

---

## Phần B — Chọn định dạng demo

Mỗi lớp cần một bản demo. Demo giúp biến ý tưởng thành thứ trực quan để nhóm khác xem, kiểm tra và phản biện.

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | ASCII sketch + bảng trạng thái | 15 phút |
| Chỉ dẫn AI | `2-prompt` | Bản prompt trong Markdown + ví dụ hỏi đáp | 15 phút |
| Kiến trúc dữ liệu | `3-architecture` | Mermaid flowchart + bảng thành phần | 15 phút |

**Lý do chọn demo**

- Giao diện: ASCII sketch cho phép minh họa rõ ràng sự thay đổi từ giao diện chat thông thường sang màn hình cấp cứu mà không cần công cụ thiết kế bên ngoài.
- Chỉ dẫn AI: Prompt + ví dụ hỏi đáp là cách trực tiếp nhất để kiểm tra hành vi AI với tình huống T-01.
- Kiến trúc dữ liệu: Mermaid flowchart dễ đọc, dễ chỉnh sửa, và thể hiện rõ luồng dữ liệu từ người dùng qua classifier đến LLM hoặc màn hình cấp cứu.

Gợi ý: có thể dùng AI để dựng nhanh bản nháp demo, nhưng nhóm phải đọc lại và sửa.

### Chọn demo theo điều cần chứng minh

| Nếu cần chứng minh... | Demo phù hợp |
|---|---|
| Người dùng nhìn thấy gì | Sketch, Figma, HTML, ASCII UI |
| AI được chỉ dẫn thế nào | Bản prompt trong Markdown, ví dụ trả lời |
| Dữ liệu đi qua đâu | Sơ đồ hộp-mũi tên, ASCII, Mermaid |
| Quy trình chuyển sang người thật | Sơ đồ quy trình |

---

## Phần C — Ba lớp giải pháp

Ghi tóm tắt ở đây. Chi tiết nằm trong `card.md` và `demo.*` của từng thư mục.

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Thiết kế "Emergency Screen Takeover" — khi classifier phát hiện red flag, toàn bộ giao diện chat chuyển sang màn hình cấp cứu với nền đỏ, hiển thị duy nhất thông điệp khẩn cấp, nút gọi 115, và hướng dẫn sơ cứu tạm thời. Không còn ô chat để người dùng tiếp tục đối thoại.
- **Hành động phòng vệ bao phủ**: Thông báo (rõ mức độ khẩn cấp), Phát hiện (thay đổi trạng thái UI), Khắc phục (chuyển sang người thật qua hotline)
- **Demo**: ASCII sketch minh họa 3 trạng thái: (1) Chat thường, (2) Cảnh báo vàng khi triệu chứng mơ hồ, (3) Màn hình cấp cứu đỏ khi red flag xác định
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.*`

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Bổ sung "Emergency Clinical Rules" vào system prompt. AI phải áp dụng quy tắc FAST (Face, Arm, Speech, Time) và BEFAST (thêm Balance, Eyes) khi người dùng mô tả triệu chứng thần kinh. Nếu có bất kỳ dấu hiệu nào, AI bắt buộc: (1) Không đồng ý với đề xuất nghỉ ngơi, (2) Nhấn mạnh "thời gian vàng", (3) Yêu cầu gọi 115 ngay lập tức, (4) Không đưa ra chẩn đoán.
- **Hành động phòng vệ bao phủ**: Ngăn (không cho AI đồng ý với chờ/nghỉ), Từ chối (từ chối cung cấp lời khuyên xoa dịu khi red flag hiện diện), Hỏi lại (hỏi thêm về các dấu hiệu FAST nếu mô tả còn mơ hồ)
- **Demo**: Bản prompt hoàn chỉnh + 3 ví dụ hỏi đáp: T-01 (đột quỵ), T-02 (suy hô hấp), và tình huống người dùng gây áp lực (pressure trap)
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Xây dựng "Hybrid Triage Pipeline" với lớp phân loại xác định (Deterministic Emergency Classifier) chạy trước LLM. Classifier dùng từ điển red flag + quy tắc lâm sàng FAST/BEFAST + keyword matching để phân loại câu hỏi vào 3 nhóm: (1) Bình thường → LLM, (2) Cảnh báo vàng → LLM với prompt đặc biệt, (3) Cấp cứu đỏ → Bypass LLM, hiển thị màn hình cấp cứu. Kết hợp với cơ sở dữ liệu triệu chứng chuẩn hóa và hệ thống log/monitor.
- **Hành động phòng vệ bao phủ**: Ngăn (classifier chặn câu hỏi cấp cứu trước khi vào LLM), Phát hiện (log và cảnh báo khi có undertriage), Khắc phục (tự động chuyển sang màn hình cấp cứu và ghi nhận để rà soát)
- **Demo**: Mermaid flowchart luồng xử lý + bảng thành phần hệ thống
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-01 — Undertriage đột quỵ |
| Nguyên nhân gốc là gì? | AI vận hành như chatbot tự do thiếu tầng phân loại triệu chứng nguy hiểm, system prompt không có luật FAST/BEFAST, và giao diện không phân biệt trạng thái cấp cứu |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: Xong / Chỉ dẫn AI: Xong / Kiến trúc: Xong |
| 4 hành động đã bao phủ chưa? | Ngăn: Xong (classifier + prompt) / Phát hiện: Xong (UI red flag + log) / Khắc phục: Xong (màn hình cấp cứu + chuyển 115) / Thông báo: Xong (thông điệp khẩn cấp + disclaimer) |
| Nhóm khác đã góp ý chưa? | Chưa — đợi phản biện chéo |
| Nhóm đã sửa gì sau phản biện? | Chưa — đợi phản biện chéo |

## Phản biện chéo: 4 câu phải trả lời

Khi nhóm khác góp ý, hoặc khi nhóm tự rà lại, dùng 4 câu này:

| Góc phản biện | Câu hỏi |
|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? |

Ghi góp ý cụ thể vào `card.md` hoặc phần tổng kiểm tra. Không ghi chung chung "ổn" hoặc "chưa ổn".

## Gợi ý chia việc

Nhóm 3 người:

- Thành viên A: `artifact/1-uiux/`
- Thành viên B: `artifact/2-prompt/`
- Thành viên C: `artifact/3-architecture/`

Nhóm 2 người:

- Một người phụ trách 2 lớp.
- Người còn lại phụ trách 1 lớp và rà lại 2 lớp kia.

5 phút cuối: cả nhóm đọc chéo 3 lớp, sửa lại bảng tổng kiểm tra, rồi chuẩn bị phản biện chéo.
