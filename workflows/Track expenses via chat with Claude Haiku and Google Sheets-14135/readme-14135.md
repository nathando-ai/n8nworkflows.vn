---
title: "💰 Theo dõi chi tiêu thông minh bằng AI và Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi chi tiêu cá nhân bằng cách chat với AI Claude Haiku và Google Sheets - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "theo-doi-chi-tieu-voi-ai-va-google-sheets"
tags: [n8n, automation, no-code, google-sheets, ai-chatbot]
keywords: [theo dõi chi tiêu, tự động hóa tài chính, n8n workflow, ai chatbot, google sheets]
---

# 💰 Theo dõi chi tiêu thông minh bằng AI và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải theo dõi chi tiêu hàng ngày một cách thủ công, đặc biệt là khi phải xử lý nhiều giao dịch khác nhau. Việc nhập liệu vào bảng tính Google Sheets thủ công không chỉ tốn thời gian mà còn dễ gây lỗi và không nhất quán. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình theo dõi chi tiêu chỉ bằng cách chat với AI Claude Haiku, đồng thời lưu trữ và phân tích dữ liệu trên Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình theo dõi chi tiêu chỉ bằng cách chat với AI
- Dữ liệu được lưu trữ và quản lý trên Google Sheets một cách chuyên nghiệp
- Nhận báo cáo chi tiêu hàng tháng một cách tự động
- Tiết kiệm thời gian đáng kể so với phương pháp thủ công
- Dữ liệu được xử lý và phân tích một cách chính xác và nhất quán
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được kích hoạt
- API key của Anthropic để sử dụng Claude Haiku
- Bảng tính Google Sheets đã được tạo với cấu trúc như sau:
  - Cột A: Date
  - Cột B: Amount
  - Cột C: Category
  - Cột D: Description
  - Cột E: Currency
  - Cột F: Month
  - Cột G: Raw Message
  - Cột H: Total
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When chat message received**: Node này sẽ nhận tin nhắn từ người dùng và truyền dữ liệu đến các node tiếp theo.
- **Detect Intent**: Node này sẽ phân tích nội dung tin nhắn để xác định ý định của người dùng (chi tiêu, báo cáo, trợ giúp).
- **Intent Switch**: Node này sẽ chuyển hướng dữ liệu đến các luồng xử lý tương ứng dựa trên ý định được phát hiện.
- **Read All Expenses**: Node này sẽ đọc toàn bộ dữ liệu từ Google Sheets để lấy thông tin chi tiêu hiện tại.
- **Prepare Data**: Node này sẽ chuẩn bị dữ liệu để tính toán tổng chi tiêu hàng tháng.
- **AI Parse Expense**: Node này sẽ sử dụng AI Claude Haiku để phân tích và trích xuất thông tin chi tiêu từ tin nhắn.
- **Claude Haiku**: Node này sẽ cấu hình model AI Claude Haiku để xử lý và trả về kết quả dưới dạng JSON.
- **Parse & Total**: Node này sẽ phân tích kết quả từ AI và tính toán tổng chi tiêu hàng tháng.
- **Is Valid Expense?**: Node này sẽ kiểm tra xem thông tin chi tiêu có hợp lệ hay không.
- **Save Expense to Sheet**: Node này sẽ lưu thông tin chi tiêu hợp lệ vào Google Sheets.
- **Reply Saved**: Node này sẽ gửi phản hồi xác nhận khi thông tin chi tiêu đã được lưu.
- **Reply Invalid**: Node này sẽ gửi phản hồi yêu cầu người dùng cung cấp thêm thông tin khi thông tin chi tiêu không hợp lệ.
- **Read for Summary**: Node này sẽ đọc dữ liệu từ Google Sheets để chuẩn bị báo cáo chi tiêu.
- **Build Summary**: Node này sẽ xây dựng báo cáo chi tiêu hàng tháng.
- **Send Help**: Node này sẽ gửi hướng dẫn sử dụng khi người dùng yêu cầu trợ giúp.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo chi tiêu và báo cáo hàng tháng.
- Lưu log các giao dịch để theo dõi lịch sử chi tiêu.
- Gửi báo cáo chi tiêu hàng tháng tự động đến email của người dùng.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa toàn diện cho việc theo dõi chi tiêu cá nhân, giúp các sếp tiết kiệm thời gian và quản lý tài chính một cách hiệu quả. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!