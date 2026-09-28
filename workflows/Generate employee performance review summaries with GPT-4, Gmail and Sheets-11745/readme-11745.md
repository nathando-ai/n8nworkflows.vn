---
title: "🚀 Tự Động Hóa Đánh Giá Nhân Sự Với GPT-4: Gửi Email & Báo Cáo Hình Ảnh"
description: "Workflow n8n sử dụng AI để phân tích hiệu suất nhân viên, tạo bản tóm tắt chuyên nghiệp, chuyển đổi thành hình ảnh đẹp mắt và gửi email tự động, đồng thời thông báo cho HR qua Slack."
slug: "tu-dong-hoa-danh-gia-nhan-su-gpt-4"
tags: [n8n, automation, no-code, hr-automation, ai-summarization, openai]
keywords: [n8n workflow, tự động hóa nhân sự, đánh giá hiệu suất, gpt-4, gmail automation]
---

# 🚀 Tự Động Hóa Đánh Giá Nhân Sự Với GPT-4: Gửi Email & Báo Cáo Hình Ảnh

Việc đánh giá hiệu suất nhân viên (Performance Review) thường là một quy trình tốn nhiều thời gian và dễ gây áp lực cho cả HR lẫn quản lý. Bạn phải tổng hợp điểm số, viết nhận xét cá nhân hóa, định dạng báo cáo cho đẹp mắt và gửi đi. Làm thủ công cho hàng chục hay hàng trăm nhân viên? Đó là một cơn ác mộng về mặt thời gian và sự nhất quán.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình từ A-Z. Chỉ cần gửi dữ liệu thô (điểm số, phản hồi) qua Webhook, hệ thống sẽ sử dụng **GPT-4** để viết ra những bản tóm tắt chuyên nghiệp, chuyển đổi chúng thành **hình ảnh báo cáo trực quan**, gửi email cho nhân viên, lưu log vào Google Sheets và thông báo ngay cho team HR qua Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý lượng lớn dữ liệu nhân sự, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian HR:** Không cần soạn thảo từng email hay chỉnh sửa file Word/Excel.
- **Trình bày chuyên nghiệp:** Báo cáo được render thành hình ảnh (Image) đẹp mắt, dễ đọc trên mọi thiết bị, thay vì văn bản khô khan.
- **Cá nhân hóa bằng AI:** GPT-4 phân tích điểm số và phản hồi để tạo ra nhận xét phù hợp với từng nhân viên, tránh cảm giác "cào bằng".
- **Minh bạch & Theo dõi:** Tự động lưu lịch sử đánh giá vào Google Sheets và thông báo tức thì cho HR qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các credentials (thông tin xác thực) sau:
1. **OpenAI API Key:** Dùng cho node `AI Summary Generator` để tạo nội dung.
2. **Gmail OAuth2:** Dùng cho node `Send Review to Employee` để gửi email.
3. **Google Sheets OAuth2:** Dùng cho node `Log to Google Sheets` để lưu dữ liệu.
4. **Slack API:** Dùng cho node `Notify HR Team` để gửi thông báo.
5. **HTMLCSS to Image API:** Dùng cho node `Convert HTML to Image` để render HTML thành ảnh. (Có thể dùng dịch vụ như ScreenshotOne, Puppeteer, hoặc API tương tự).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor của bạn.
3. Chọn **Import from URL** hoặc **Import from Clipboard**.
4. Dán code JSON vào và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node quan trọng sau để khớp với hạ tầng của mình:

*   **Node: `Receive Review Data` (Webhook)**
    *   Đây là điểm đầu vào. Hãy chú ý đến **Webhook URL** (Production URL).
    *   Dữ liệu đầu vào (JSON) cần bao gồm các trường như: `employee_name`, `employee_email`, `scores` (điểm số), `feedback` (phản hồi), `review_period`.
    *   *Mẹo:* Bạn có thể test bằng Postman hoặc curl với method POST.

*   **Node: `AI Summary Generator` (OpenAI)**
    *   Chọn credentials OpenAI đã tạo.
    *   **Quan trọng:** Kiểm tra phần **System Prompt** và **User Prompt**. Các sếp có thể chỉnh sửa prompt để thay đổi giọng văn (ví dụ: từ trang trọng sang thân thiện, hoặc tập trung vào kỹ năng mềm thay vì chỉ số KPI).
    *   Đảm bảo model được chọn là `gpt-4` hoặc `gpt-3.5-turbo` (tùy ngân sách).

*   **Node: `Generate Review Card HTML` (Code)**
    *   Node này chứa template HTML/CSS để tạo giao diện báo cáo.
    *   Các sếp có thể chỉnh sửa màu sắc, font chữ, layout trong code để phù hợp với thương hiệu công ty.
    *   Đảm bảo các biến từ bước trước (tên nhân viên, điểm số, nhận xét AI) được map đúng vào template.

*   **Node: `Convert HTML to Image` (HTMLCSS to Image)**
    *   Chọn credentials API render ảnh.
    *   Đảm bảo URL hoặc nội dung HTML được truyền đúng vào input của API này. Kết quả sẽ là một URL ảnh hoặc Base64.

*   **Node: `Send Review to Employee` (Gmail)**
    *   Chọn credentials Gmail.
    *   Cấu hình **To:** (lấy từ dữ liệu đầu vào `employee_email`).
    *   Cấu hình **Subject:** (ví dụ: "Báo cáo hiệu suất quý [Quarter] - [Name]").
    *   **Attachment:** Map URL ảnh hoặc Base64 từ node `Download Image` vào phần đính kèm.

*   **Node: `Log to Google Sheets` (Google Sheets)**
    *   Chọn credentials Google Sheets.
    *   Chọn **Spreadsheet ID** và **Sheet Name** (ví dụ: "Performance_Logs").
    *   Đảm bảo các cột trong Sheet khớp với các trường dữ liệu được append (Tên, Email, Điểm, Ngày, Link Báo cáo...).

*   **Node: `Notify HR Team` (Slack)**
    *   Chọn credentials Slack.
    *   Chọn **Channel** (ví dụ: `#hr-notifications`).
    *   Tùy chỉnh nội dung thông báo (Message) để bao gồm tên nhân viên và trạng thái gửi email thành công/thất bại.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với dữ liệu mẫu (Test Data) để kiểm tra toàn bộ quy trình.
2. Kiểm tra hộp thư Gmail xem email có đến đúng không, hình ảnh có hiển thị rõ ràng không.
3. Kiểm tra Google Sheets xem dòng dữ liệu mới có được thêm vào không.
4. Kiểm tra Slack xem HR có nhận được thông báo không.
5. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì nhận dữ liệu qua Webhook thủ công, các sếp có thể kết nối trực tiếp từ HubSpot, Zoho CRM hoặc Salesforce để tự động lấy dữ liệu nhân viên khi có thay đổi trạng thái.
- **Đa ngôn ngữ:** Chỉnh sửa prompt trong node `AI Summary Generator` để yêu cầu GPT-4 viết báo cáo bằng tiếng Việt, tiếng Anh hoặc bất kỳ ngôn ngữ nào khác tùy theo quốc gia làm việc.
- **Gửi qua Telegram/WhatsApp:** Thay vì chỉ gửi email, các sếp có thể thêm node Telegram hoặc WhatsApp Business API để gửi báo cáo trực tiếp vào chat cá nhân của nhân viên, tăng tỷ lệ mở đọc.
- **Phân tích xu hướng:** Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể dùng thêm một workflow khác để đọc Sheet này và tạo dashboard PowerBI/Looker Studio để phân tích hiệu suất toàn công ty theo thời gian thực.

### 📌 Kết luận
Việc đánh giá nhân sự không nhất thiết phải là một gánh nặng hành chính. Với workflow n8n này, các sếp có thể biến quy trình khô khan thành một trải nghiệm chuyên nghiệp, cá nhân hóa và tự động hoàn toàn. Hãy thử áp dụng ngay để giải phóng thời gian cho team HR, tập trung vào những công việc chiến lược hơn. Chúc các sếp triển khai thành công!