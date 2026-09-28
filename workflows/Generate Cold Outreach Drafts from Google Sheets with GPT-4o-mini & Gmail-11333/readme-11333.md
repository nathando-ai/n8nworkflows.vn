---
title: "🚀 Tự động tạo bản nháp email cold outreach từ Google Sheets bằng GPT-4o-mini & Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc danh sách khách hàng từ Google Sheets, dùng AI tạo nội dung và tiêu đề email cá nhân hóa, sau đó lưu bản nháp vào Gmail một cách mượt mà."
slug: "tu-dong-tao-nhap-email-cold-outreach-google-sheets-gpt4-gmail"
tags: [n8n, automation, no-code, lead-nurturing, openai, gmail, google-sheets]
keywords: [n8n workflow, cold email automation, tạo email tự động openai, n8n gmail google sheets, gpt-4o-mini outreach]
---

# 🚀 Tự động hóa Cold Outreach: Tạo bản nháp email thông minh với GPT-4o-mini & Gmail

Chào các sếp! Việc tiếp cận khách hàng tiềm năng (Cold Outreach) bằng email là một chiến lược sống còn trong sales và marketing. Tuy nhiên, việc phải ngồi thủ công tra cứu thông tin từng doanh nghiệp, viết từng dòng email cá nhân hóa rồi lưu nháp vào Gmail cực kỳ tốn thời gian và dễ gây nhàm chán.

Nếu các sếp đang tìm cách giải phóng đội ngũ sales khỏi những tác vụ lặp đi lặp lại đó, thì đây chính là giải pháp hoàn hảo. Workflow n8n này sẽ tự động hóa toàn bộ quy trình: đọc danh sách từ Google Sheets, nhờ sức mạnh của GPT-4o-mini viết nội dung và tiêu đề siêu cá nhân hóa, tạo bản nháp trực tiếp trên Gmail và tự động cập nhật trạng thái vào bảng tính. 

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không cần tự soạn từng email, AI sẽ lo phần cá nhân hóa dựa trên dữ liệu doanh nghiệp.
- **Duy trì quyền kiểm soát (Human-in-the-loop):** Email được lưu dưới dạng **Draft (Bản nháp)** trong Gmail, giúp các sếp kiểm tra lại kỹ lưỡng trước khi bấm nút gửi thực tế.
- **Đồng bộ dữ liệu mượt mà:** Google Sheets tự động cập nhật trạng thái các lead đã được tạo email, tránh bị trùng lặp.
- **Hoạt động thông minh:** Tích hợp cơ chế chờ (Rate Limit Wait) giúp hệ thống không bị nghẽn API của OpenAI hay Google.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Google Sheets:** File chứa danh sách lead với các cột chuẩn: `business_name`, `email`, `contact_name`, `city`, `business_type`, `email_sent`.
3. **OpenAI API Key** (hoặc kết nối tương đương) để sử dụng model GPT-4o-mini.
4. **Tài khoản Gmail** đã cấp quyền OAuth2 cho n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã nguồn JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình hoặc tạo mới theo danh sách các node chuẩn bên dưới:
- `Manual Trigger` (Khởi chạy thủ công)
- `Read Business Data` (Google Sheets - Đọc danh sách)
- `Filter Unsent Emails` (If - Lọc các email chưa gửi)
- `Personalize Email (ChatGPT)` & `Generate Subject (ChatGPT)` (HTTP Request - Gọi OpenAI API)
- `Merge Subject and Body` (Merge - Ghép nối nội dung và tiêu đề)
- `Prepare Email Draft` & `Prepare Sheet Update` (Set - Chuẩn bị cấu trúc dữ liệu)
- `Create Email Draft` (Gmail - Tạo bản nháp)
- `Rate Limit Wait` (Wait - Chờ chống tràn API)
- `Update Google Sheet` (Google Sheets - Cập nhật trạng thái)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Sheets Nodes (`Read Business Data` & `Update Google Sheet`):** Kết nối tài khoản Google Sheets OAuth2 của các sếp. Trỏ đúng đến File Google Sheet và Sheet Name chứa danh sách lead. Đảm bảo tên các cột trùng khớp với ghi chú (`business_name`, `email`, `contact_name`, `city`, `business_type`, `email_sent`).
- **AI Nodes (`Personalize Email (ChatGPT)` & `Generate Subject (ChatGPT)`):** Sử dụng node `HTTP Request` kết nối với OpenAI API (hoặc `openAiApi` credentials). Cấu hình endpoint gọi model `gpt-4o-mini` và tùy chỉnh prompt theo văn phong sản phẩm/dịch vụ của doanh nghiệp mình.
- **Gmail Node (`Create Email Draft`):** Chọn tài khoản `gmailOAuth2` và đảm bảo resource được cấu hình là `draft`. Mapping đúng email người nhận (`email`) từ Google Sheets sang.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** bằng `Manual Trigger` với một vài dòng dữ liệu mẫu để kiểm tra xem bản nháp có xuất hiện trong Gmail hay không.
- Sau khi test thành công, các sếp có thể đổi `Manual Trigger` sang `Schedule Trigger` (chạy định kỳ hàng ngày/hàng tuần) nếu muốn tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Nâng cấp Trigger:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Webhook` (nhận lead từ Landing Page/CRM) hoặc `Schedule Trigger` để tự động chạy vào mỗi sáng thứ Hai hàng tuần.
- **Thêm thông báo:** Kết nối thêm node `Slack` hoặc `Telegram` để bắn một tin nhắn báo cáo về máy khi hệ thống đã tạo xong loạt bản nháp email mới.
- **Quản lý giới hạn (Rate Limit):** Nếu danh sách lead lên tới hàng ngàn dòng, hãy điều chỉnh thời gian ở node `Rate Limit Wait` (ví dụ: tăng từ 3 giây lên 5 giây) để tránh bị lỗi giới hạn request từ phía OpenAI hoặc Google API.

### 📌 Kết luận
Workflow tạo cold outreach draft này là bước đệm tuyệt vời để đưa AI vào quy trình sales hàng ngày mà không sợ rủi ro gửi nhầm tin nhắn tự động kém chất lượng. Hãy áp dụng ngay để tối ưu hóa hiệu suất đội ngũ sales của các sếp nhé! Chúc các sếp thao tác thành công!