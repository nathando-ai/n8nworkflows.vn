---
title: "🚀 Tự động tạo bản đề xuất khách hàng từ nội dung cuộc gọi với AI, Google Slides và Airtable"
description: "Biến bản ghi âm cuộc gọi thành slide đề xuất chuyên nghiệp tự động bằng AI, Google Slides và lưu trữ trên Airtable mà không cần tốn hàng giờ soạn thảo thủ công."
slug: "tao-de-xuat-khach-hang-tu-dong-ai-google-slides-airtable"
tags: [n8n, automation, no-code, openai, google-slides, airtable]
keywords: [n8n workflow, tự động hóa đề xuất khách hàng, ai google slides, airtable n8n, tạo proposal tự động]
---

# 🚀 Tự động tạo bản đề xuất khách hàng từ nội dung cuộc gọi với AI, Google Slides và Airtable

Các sếp có bao giờ cảm thấy mệt mỏi sau mỗi cuộc gọi tư vấn khách hàng (Sales Call) lại phải lọ mọ ngồi nghe lại bản ghi âm, tổng hợp nhu cầu, rồi lại copy-paste thủ công vào file Google Slides để làm bản đề xuất (Proposal)? Công việc này vừa tốn thời gian, dễ bỏ sót ý, lại làm giảm tốc độ phản hồi khách hàng – yếu tố quyết định chốt đơn thành công!

Giải pháp ở đây chính là workflow n8n tự động hóa 100%. Chỉ với một câu lệnh qua chat hoặc kích hoạt sự kiện, hệ thống sẽ tự động phân tích bản ghi cuộc gọi bằng AI thông minh, điền trực tiếp thông tin vào template Google Slides được thiết kế sẵn, chia sẻ quyền truy cập và cập nhật trạng thái ngay lập tức lên Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Bỏ hoàn toàn khâu soạn thảo proposal thủ công, rút ngắn thời gian từ vài tiếng xuống chỉ còn vài giây.
- **Tăng tỷ lệ chốt đơn:** Gửi bản đề xuất chuyên nghiệp, bám sát 100% pain-point của khách hàng ngay sau cuộc gọi.
- **Cá nhân hóa thông minh:** AI tự động phân tích ngữ cảnh cuộc gọi để đưa ra giải pháp, mức giá và lộ trình phù hợp cho từng khách hàng cụ thể.
- **Quản lý tập trung:** Tự động đồng bộ file và cập nhật trạng thái lead chuyên nghiệp trên Airtable.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Dùng cho node *Message a model* để phân tích nội dung).
- **Google Cloud Console Project** (Cấu hình OAuth2 cho Google Drive và Google Slides để copy template, thay thế text và share file).
- **Airtable Account & Personal Access Token** (Lưu trữ thông tin khách hàng và cập nhật trạng thái Lead).
- **Template Google Slides chuẩn** có sẵn các thẻ (tags) để AI thay thế nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file JSON từ n8n.io/workflows/7558), sau đó vào giao diện n8n, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các credentials và tham số cho từng node sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu để nhập nội dung cuộc gọi hoặc kích hoạt quy trình. Các sếp có thể thay đổi node này thành Webhook hoặc Airtable Trigger nếu muốn hệ thống tự động chạy ngầm.
- **Message a model (`openAi`):** 
  - Chọn `openAiApi` credentials.
  - Viết Prompt hướng dẫn AI đọc hiểu bản ghi cuộc gọi (Call Transcript) và trích xuất các trường dữ liệu cần thiết (Tên khách hàng, vấn đề, giải pháp, báo giá...).
- **Copy file (`googleDrive`):** 
  - Chọn `googleDriveOAuth2Api` credentials.
  - Chọn file Template Google Slides mẫu gốc để hệ thống tự động tạo một bản copy mới cho từng khách hàng.
- **Replace text in a presentation (`googleSlides`):**
  - Chọn `googleSlidesOAuth2Api` credentials.
  - Map dữ liệu từ AI output vào các placeholder tương ứng trong slide (ví dụ: thay thế `{{ClientName}}`, `{{Solution}}`...).
- **Share file (`googleDrive`):**
  - Cấu hình chia sẻ file Google Slides vừa tạo cho email của khách hàng hoặc nội bộ team sales.
- **Update record (`airtable`):**
  - Chọn `airtableTokenApi` credentials.
  - Chọn Base và Table tương ứng, nhớ đảm bảo bảng của các sếp có trường dữ liệu **Lead Status** để hệ thống tự động chuyển trạng thái (ví dụ: từ *Called* sang *Proposal Sent*).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** với một đoạn transcript mẫu để kiểm tra xem Slide có được tạo và Airtable có được update đúng không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram / Slack:** Thêm một node gửi thông báo về group chat của team sales kèm link file Google Slides ngay khi proposal được tạo xong.
- **Gửi Email tự động:** Kết hợp thêm node Gmail để gửi thẳng file proposal (hoặc PDF) đến email khách hàng mà không cần click tay.
- **Lưu trữ file PDF:** Thêm bước convert Google Slides sang định dạng PDF trước khi gửi cho khách để tăng tính chuyên nghiệp.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp các đội ngũ Sales tối ưu hóa quy trình chăm sóc khách hàng sau meeting. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ và tăng tốc độ chốt deal với khách hàng!