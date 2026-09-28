---
title: "🚀 Tự động tìm kiếm LinkedIn Profile qua Form sử dụng Bright Data & GPT-4o-mini"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm thông tin cá nhân và doanh nghiệp trên LinkedIn bằng n8n, kết hợp Bright Data và OpenAI GPT-4o-mini."
slug: "tu-dong-tim-kiem-linkedin-profile-bright-data-gpt"
tags: [n8n, automation, linkedin, bright-data, openai, ai, hr, lead-generation]
keywords: [n8n workflow, tìm kiếm linkedin tự động, bright data n8n, openai linkedin finder, tự động hóa hr, lead generation linkedin]
---

# 🚀 Tự động tìm kiếm LinkedIn Profile qua Form sử dụng Bright Data & GPT-4o-mini

Các sếp trong ngành Tuyển dụng (HR), Sales hay Marketing chắc hẳn đã quá quen thuộc với nỗi đau: Mất hàng giờ đồng hồ chỉ để tra cứu thông tin ứng viên hoặc khách hàng tiềm năng trên Google, sau đó mò mẫm tìm đúng link LinkedIn cá nhân và công ty của họ. Công việc thủ công này vừa nhàm chán, vừa tốn thời gian mà hiệu suất lại không cao.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh: **LinkedIn Profile Finder via Form using Bright Data & GPT-4o-mini**. Hệ thống này sẽ tự động hóa từ khâu nhận thông tin từ Form, cào dữ liệu qua Bright Data, sử dụng AI (GPT-4o-mini) để phân tích, cho đến việc tổng hợp và gửi báo cáo kết quả qua Email. Hoàn toàn tự động 100% không cần tốn một phút làm tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa toàn bộ quá trình tìm kiếm từ một vài thông tin cơ bản trên form.
- **Độ chính xác cao:** Kết hợp sức mạnh cào dữ liệu chuyên sâu của Bright Data và khả năng hiểu ngữ cảnh siêu việt của GPT-4o-mini.
- **Cá nhân hóa nội dung:** AI tự động tổng hợp thông tin chi tiết về cả cá nhân và công ty để phục vụ cho việc outreach hoặc phỏng vấn.
- **Quy trình liền mạch:** Nhận input qua Form và trả kết quả gọn gàng trực tiếp qua Email hoặc hoàn tất trên giao diện form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Bright Data API:** Tài khoản Bright Data kèm API Key dùng để cào kết quả tìm kiếm trên Google.
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng các mô hình như GPT-4o-mini phân tích dữ liệu HTML thô.
- **SMTP Credentials:** Thông tin tài khoản gửi email (Gmail SMTP, SendGrid, Mailgun,...) để hệ thống tự động bắn kết quả về mail.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn chính thức hoặc copy toàn bộ mã JSON, sau đó dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, workflow gồm 19 nodes sẽ xuất hiện. Các sếp cần chú ý cấu hình kỹ các thành phần cốt lõi sau:

- **When User Completes Form:** Thiết lập các trường dữ liệu đầu vào trên form (Ví dụ: Họ tên, Tên công ty, Email người nhận kết quả,...).
- **Get LinkedIn Entry on Google & Get Company on Google (Node loại Bright Data):** 
  - Chọn `brightdataApi` credentials.
  - Cấu hình tham số tìm kiếm Google dựa trên thông tin nhận được từ form.
- **Parse Google Results & Parse Google Results for Company (Node loại OpenAI):**
  - Chọn `openAiApi` credentials.
  - Kiểm tra lại system prompt và model được chọn (khuyến nghị `gpt-4o-mini` để tối ưu chi phí và tốc độ) để đảm bảo AI trích xuất chính xác URL LinkedIn từ mã HTML thô.
- **LinkedIn Profile Is Found? (Node loại If):** Thiết lập điều kiện kiểm tra xem hệ thống có tìm thấy profile khớp hay không. Nếu không, luồng sẽ chuyển sang node hoàn tất form báo không tìm thấy (`Form Not Found`).
- **Create a Followup for Company and Person (Node loại OpenAI):** Tinh chỉnh prompt AI để tạo ra các đoạn tổng hợp thông tin hoặc gợi ý câu mở lời (follow-up message) chất lượng nhất.
- **Send Email (Node loại SMTP):** 
  - Chọn `smtp` credentials.
  - Điền tiêu đề, nội dung email template nhận kết quả tổng hợp về profile cá nhân và công ty.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và điền thử thông tin vào Form đầu vào để test run xem dữ liệu chạy qua các bước có mượt mà không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chat ứng dụng:** Thay vì gửi email, các sếp có thể thay thế node `Send Email` bằng node **Telegram** hoặc **Slack** để nhận thông báo tức thì ngay khi có người điền form.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** ngay sau bước phân tích của AI để lưu lại toàn bộ lịch sử tìm kiếm phục vụ cho việcRemarketing hoặc quản lý Talent Pool.
- **Xử lý hàng loạt (Batch Processing):** Có thể mở rộng workflow để nhận file CSV danh sách ứng viên thay vì chỉ nhận từng người qua Form đơn lẻ.

### 📌 Kết luận
Workflow **LinkedIn Profile Finder via Form using Bright Data & GPT-4o-mini** là một trợ thủ đắc lực giúp tối ưu hóa công việc tìm kiếm nhân sự và khách hàng. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ của bạn và để AI làm thay những công việc lặp đi lặp lại!