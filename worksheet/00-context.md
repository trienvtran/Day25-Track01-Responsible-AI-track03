---
title: 00 — Bối cảnh sản phẩm của nhóm
section: Day 25 — dùng lại cho mọi cuộc trò chuyện với AI
format: Nhóm
time: Điền 5 phút đầu buổi
---

# 00-context.md — Bối cảnh sản phẩm của nhóm

Điền file này một lần ở đầu buổi. Sau đó, mỗi lần dùng AI, hãy đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.

Lý do: AI không tự nhớ bối cảnh giữa các cuộc trò chuyện. Nếu mỗi lần đưa bối cảnh khác nhau, câu trả lời cũng sẽ lệch.

## 1. Sản phẩm
*   **Tên sản phẩm / bot:** Trợ lý Sàng lọc Triệu chứng Y khoa và Tâm lý (Triage AI Assistant).
*   **Sản phẩm giúp ai làm gì:** Giúp bệnh nhân và người nhà sơ bộ đánh giá mức độ nghiêm trọng của triệu chứng (thể chất và tâm lý) để định hướng chuyên khoa phù hợp hoặc kích hoạt gọi cấp cứu.
*   **Người dùng gặp sản phẩm ở đâu:** Website và ứng dụng (App) chính thức của hệ thống bệnh viện/phòng khám.
*   **Giai đoạn hiện tại:** Chuẩn bị ra mắt (Đang trong giai đoạn rà soát rủi ro và kiểm thử đối kháng trước khi triển khai thực tế).

## 2. Phạm vi
*   **AI được làm gì:**
    *   Thu thập thông tin ban đầu về triệu chứng, thời gian khởi phát và tiền sử bệnh lý.
    *   Đề xuất chuyên khoa phù hợp (ví dụ: Nội, Ngoại, Tâm thần) dựa trên luồng câu hỏi.
    *   Kích hoạt quy trình khẩn cấp (hiển thị Hotline 115, hướng dẫn sơ cứu) khi phát hiện dấu hiệu đe dọa tính mạng (Red Flags).
*   **AI không được làm gì:**
    *   Tuyệt đối không đưa ra chẩn đoán bệnh danh cụ thể (Ví dụ: "Bạn bị viêm ruột thừa").
    *   Không kê đơn thuốc, không tư vấn thay đổi liều lượng thuốc Tây y hay thảo dược.
    *   Không đồng thuận, xu nịnh hoặc đưa ra các lời khuyên xoa dịu sáo rỗng đối với người có biểu hiện hoang tưởng hoặc ý định tự sát.
*   **Vì sao có giới hạn này:**
    *   Sản phẩm y tế số thuộc nhóm Rủi ro Cao theo quy định. Việc chẩn đoán sai, bỏ sót cấp cứu (undertriage), hoặc không cảnh báo tương tác thuốc có thể dẫn đến tử vong, gây tổn hại trực tiếp đến bệnh nhân và rủi ro pháp lý nghiêm trọng cho hệ thống y tế.

## 3. Người dùng
*   **Là ai:** Bệnh nhân trực tiếp hoặc người nhà (phụ huynh, con cái chăm sóc người già), không có chuyên môn y khoa sâu, độ tuổi đa dạng.
*   **Họ hỏi AI khi nào:** Khi có triệu chứng bất thường xảy ra, đặc biệt là ngoài giờ hành chính, giữa đêm, hoặc khi họ đang trong trạng thái lo âu, hoảng loạn.
*   **Họ cần quyết định gì sau khi hỏi AI:** Cần đi cấp cứu ngay lập tức hay có thể an tâm chờ đến sáng mai để khám ngoại trú.
*   **Khi nào họ dễ bị tổn thương / dễ hiểu sai:** Khi đang đau đớn cấp tính, khi sử dụng ngôn ngữ dân dã/thành ngữ để mô tả nỗi đau (cơ thể hóa), hoặc khi có ý định tự làm hại bản thân.
*   **Họ thường tin AI đến mức nào:** Tin tưởng rất cao vì AI được tích hợp trên ứng dụng bệnh viện chính thức, dễ dẫn đến hiện tượng phụ thuộc quá mức (automation bias) và làm theo lời khuyên sai mà không kiểm chứng.

## 4. Bối cảnh ngành
*   **Sự cố tương tự đã từng xảy ra:**
    *   Chatbot AI y tế từng bỏ sót 52% các ca cấp cứu thực sự trong các nghiên cứu lâm sàng.
    *   AI cung cấp thông tin về chiều cao cây cầu thay vì ngăn chặn bệnh nhân có ý định tự sát.
    *   AI khuyên dán điện cực sai vị trí gây nguy cơ bỏng nặng cho bệnh nhân.
*   **Quy định hoặc ràng buộc liên quan:** Quy định phân loại mức độ ưu tiên cấp cứu 5 cấp độ (Đỏ, Cam, Vàng, Xanh, Trắng) của Bộ Y tế Việt Nam.
*   **Nguồn chính thức nên ưu tiên:** Hướng dẫn của Bộ Y tế, các thang đo lâm sàng đã được Việt hóa (ví dụ: Thang đo Trầm cảm Việt Nam - VDS), và cơ sở dữ liệu tương tác thuốc-thảo dược chuẩn y khoa.

## 5. Ghi chú thêm
Đây là một hệ thống yêu cầu độ an toàn tuyệt đối ở các cực trị lâm sàng (cấp cứu khẩn). Cần đặc biệt chú ý đến rào cản văn hóa khi bệnh nhân Việt Nam mô tả bệnh lý tâm thần bằng các triệu chứng thể chất (ví dụ: đau đầu, mệt mỏi, "nhục nhã", "muốn điên lên").

```text
1. Mở công cụ AI phù hợp với bước đang làm.
2. Đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.
3. Chọn prompt tham khảo từ thư mục ../prompts/ và chỉnh lại nếu cần.
4. Đọc lại bản nháp AI tạo ra.
5. Sửa lại cho đúng bối cảnh nhóm.
6. Lưu kết quả vào đúng file trong worksheet/.
